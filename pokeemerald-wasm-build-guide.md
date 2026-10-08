# Building `pokeemerald.wasm` on Debian

Step-by-step guide to compile [tripplyons/pokeemerald-wasm](https://github.com/tripplyons/pokeemerald-wasm) into `build/wasm/pokeemerald.wasm` on a Debian (or Ubuntu) system.

Tested on **Debian 13** with 4 vCPUs. A single-vCPU VM can work but is more prone to process-limit issues during asset generation.

---

## 1. Install system packages

```bash
sudo apt update
sudo apt install \
  build-essential \
  binutils-arm-none-eabi \
  git \
  libpng-dev \
  pkg-config \
  zlib1g-dev \
  clang \
  lld \
  llvm
```

| Package group | Purpose |
|---|---|
| `build-essential`, `git`, `libpng-dev`, `pkg-config`, `zlib1g-dev` | Standard pret/pokeemerald toolchain + tools |
| `binutils-arm-none-eabi` | ARM binutils (shared build system) |
| `clang`, `lld`, `llvm` | WASM compiler (`clang --target=wasm32-unknown-unknown`) and linker (`wasm-ld`) |

### Install `uv` (Python package runner used by WASM asset scripts)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source "$HOME/.local/bin/env"   # or open a new shell
```

### Verify tools

```bash
clang --version
wasm-ld --version    # or: which wasm-ld
uv --version
pkg-config --version
```

If `wasm-ld` is not found:

```bash
export WASM_LD="$(which wasm-ld)"
# or set the full path explicitly before building
```

---

## 2. Clone the repository

```bash
git clone https://github.com/tripplyons/pokeemerald-wasm.git
cd pokeemerald-wasm
```

---

## 3. Build and install agbcc

Required by the shared pret build system (even for the WASM target).

```bash
# from the parent directory of pokeemerald-wasm
cd ..
git clone https://github.com/pret/agbcc
cd agbcc
./build.sh
./install.sh ../pokeemerald-wasm
cd ../pokeemerald-wasm
```

---

## 4. Patch `generate_wasm_assets.py` (required)

The upstream script forces `SETUP_PREREQS=1` on every recursive `make` call used to build missing graphics. That re-enters the tools/generated bootstrap in a nested `$(shell $(MAKE) ...)`, which quickly hits:

```text
bash: warning: shell level (1000) too high, resetting to 1
bash: fork: Resource temporarily unavailable
```

**Fix:** change only `ensure_make_target` so child makes use `SETUP_PREREQS=0`. Leave `run_gbagfx` unchanged (it must still invoke `gbagfx`).

Edit `tools/generate_wasm_assets.py` so these two functions look exactly like this:

```python
def run_gbagfx(input_path, output_path, options=()):
    output = pathlib.Path(output_path)
    output.parent.mkdir(parents=True, exist_ok=True)
    if output.exists():
        return
    subprocess.run([str(GFX), input_path, output_path, *options], check=True)


def ensure_make_target(target):
    if pathlib.Path(target).exists():
        return
    # A parent `make -j` advertises its jobserver pipe through MAKEFLAGS, but
    # Python closes those descriptors. The child must not try to use them.
    env = {name: value for name, value in os.environ.items() if name not in ('MAKEFLAGS', 'MFLAGS')}
    subprocess.run(['make', 'NODEP=1', 'SETUP_PREREQS=0', target], check=True, env=env)
```

One-shot patch from the repo root:

```bash
sed -i "s/SETUP_PREREQS=1/SETUP_PREREQS=0/" tools/generate_wasm_assets.py
```

Verify:

```bash
grep -n "SETUP_PREREQS" tools/generate_wasm_assets.py
# should show SETUP_PREREQS=0 inside ensure_make_target only
```

---

## 5. Build the WASM module

```bash
# recommended: modest parallelism (full -j$(nproc) can still stress small VMs)
make -j2 wasm

# or sequential if the VM is very limited
# make wasm
```

Expected output path:

```text
build/wasm/pokeemerald.wasm
```

Typical size: about **11–12 MiB**.

---

## 6. Verify the build

```bash
ls -lh build/wasm/pokeemerald.wasm
file build/wasm/pokeemerald.wasm
```

You should see a regular file of roughly 11–12 MiB, identified as WebAssembly (or a binary blob).

### Optional: run in the browser

```bash
make serve-wasm
```

Open the printed local URL. Controls:

| Input | Action |
|---|---|
| Arrow keys | D-pad |
| Z | A |
| X | B |
| Enter | Start |
| Shift | Select |

If the title screen / intro appears, the build is good.

---

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `pkg-config: No such file or directory` | Missing `pkg-config` | `sudo apt install pkg-config` |
| `shell level (1000) too high` / `fork: Resource temporarily unavailable` | Recursive `SETUP_PREREQS=1` in asset script | Apply the patch in step 4; use `make -j2` or `make wasm` |
| `wasm-ld not found` | LLVM linker not on PATH | Install `lld` / `llvm`, or `export WASM_LD=/path/to/wasm-ld` |
| `uv: command not found` | `uv` not installed or not on PATH | Re-run the `uv` installer and `source "$HOME/.local/bin/env"` |
| Partial/failed previous build | Stale objects | `make clean` then rebuild |

---

## Minimal command sequence (after packages + agbcc + patch)

```bash
cd pokeemerald-wasm
make -j2 wasm
ls -lh build/wasm/pokeemerald.wasm
```

---

## Notes

- This produces a **recompilation** of the pret decompilation to WebAssembly (assets included in the build). It is not an emulator that loads a separate `.gba` ROM.
- The public demo site that previously served this binary is no longer available; building from source is the supported path.
- The `SETUP_PREREQS=0` change is a local workaround for nested-make resource exhaustion. Re-apply it after any `git pull` that restores the original line.
