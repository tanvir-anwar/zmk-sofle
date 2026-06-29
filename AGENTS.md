# AGENTS.md

## Project Overview

ZMK firmware configuration for the **Eyelash Peripherals Sofle** — a split ergonomic keyboard. This is **not** compatible with the standard Sofle and requires its own shield definition.

Built on [ZMK Firmware](https://zmk.dev/) (v0.3.0+dya) / Zephyr RTOS. The repo contains no traditional source code — it's devicetree overlays, Kconfig, and keymap definitions.

## Repository Structure

```
config/
  west.yml                  # West manifest — pulls ZMK and modules from GitHub
  eyelash_sofle.keymap      # User keymap — layers, bindings, combos (primary edit target)
  eyelash_sofle.conf        # Keyboard feature config (Bluetooth, sleep, RGB, backlight, etc.)
  eyelash_sofle.json        # ZMK Studio layout metadata
boards/shields/eyelash_sofle/  # Shield definition
  eyelash_sofle.dtsi        # Main devicetree include — pin mappings, peripherals
  eyelash_sofle-layouts.dtsi # Physical layout definitions
  eyelash_sofle_left.overlay   # Left half devicetree overlay
  eyelash_sofle_right.overlay  # Right half devicetree overlay
  eyelash_sofle_left.conf      # Left half Kconfig defaults
  eyelash_sofle_right.conf     # Right half Kconfig defaults
  Kconfig.shield             # Shield Kconfig options
  Kconfig.defconfig          # Shield Kconfig defaults
build.yaml                  # GitHub Actions build matrix (which shields to compile)
keymap-drawer/              # Auto-generated keymap SVG diagrams
.github/workflows/
  build.yml                 # Firmware build workflow (produces .uf2 artifacts)
zephyr/module.yml           # Zephyr module registration
```

## Key Entry Points

- **Keymap customization**: `config/eyelash_sofle.keymap` — where layers, key bindings, and combos are defined
- **Feature toggles**: `config/eyelash_sofle.conf` — enable/disable Bluetooth, RGB, backlight, deep sleep, etc.
- **Build targets**: `build.yaml` — defines which board/shield combos to compile (left, right, studio, settings_reset)
- **Shield hardware**: `boards/shields/eyelash_sofle/eyelash_sofle.dtsi` — pin mappings and hardware peripherals

## Build System

Firmware is built via **GitHub Actions** (`.github/workflows/build.yml`). The `build.yaml` matrix currently compiles:
- `eyelash_sofle_left` + `nice_view` + ZMK Studio support
- `eyelash_sofle_right` + `nice_view`
- `nice_nano_v2` + `settings_reset` (for resetting bond info)

Output: `.uf2` firmware files flashed via USB mass storage mode.

## Keymap Change Workflow

Keymap changes use a **markdown-first staging workflow**:

1. **Stage changes in `config/KEYMAP.md`** — edit the human-readable markdown tables to describe the desired layout. This is the design document; it's easier to review and reason about than raw devicetree syntax.
2. **Review the diff** — use `git diff config/KEYMAP.md` to verify the proposed changes make sense before touching firmware code.
3. **Update `config/eyelash_sofle.keymap`** — translate the markdown tables into ZMK devicetree bindings. New behaviors (tap-dance, mod-morph, hold-tap) must be defined in the `behaviors {}` block before referencing them in layer bindings.
4. **Parse and generate the diagram** — validates the keymap syntax and catches errors faster than a full firmware build:
   ```bash
   source .venv/bin/activate
   keymap parse -z config/eyelash_sofle.keymap > keymap-drawer/eyelash_sofle.yaml
   keymap -c keymap_drawer.config.yaml draw keymap-drawer/eyelash_sofle.yaml > keymap-drawer/eyelash_sofle.svg
   ```
5. **Build and flash** — push to GitHub, download `.uf2` artifacts from the Actions workflow, and flash both halves.

The KEYMAP.md legend documents notation conventions (`hold/tap`, `SHIFT/Caps_Word`, `&mo_tog L1`, etc.) that map to specific ZMK behaviors. When adding new behavior types, update the legend first.

## Coding Guidelines
1. ALWAYS use conventional commits syntax to write commit messages.
2. NEVER update keymap config unless KEYMAP.md changes are manually reviewed and confirmed.
3. ALWAYS ask the user to manually review and validate the rendered keymap diagram, before the final commit.

## Conventions

- This is a shield-based build (not a board), unlike the Corne variant which has its own board definition.
- Devicetree syntax (`.dtsi`, `.overlay`) — not C code. Use ZMK docs as reference, not general Zephyr docs.
- Keymap uses ZMK behavior bindings (e.g., `&kp`, `&mo`, `&lt`, `&bt`). See [ZMK keycodes docs](https://zmk.dev/docs/keymaps).
- Soft-off combo: Q + S + Z held for 2 seconds enters deep sleep. Wake via hardware reset button only.
- The right half has no encoder. Encoder is left-half only.
- The keyboard includes a joystick (pointing device) — see CONFIG_ZMK_POINTING in config.
