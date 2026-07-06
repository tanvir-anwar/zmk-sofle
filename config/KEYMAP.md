# Eyelash Sofle Keymap Reference

This is a human-readable reference of the keymap defined in `eyelash_sofle.keymap`.
Edit this file to describe desired changes, then update the keymap to match.

The encoder (left thumb cluster) and joystick (center column) are shown where relevant.

## Design Philosophy

- SHOULD be as close to the [Corne Design Philosophy](https://github.com/tanvir-anwar/zmk-new-corne/blob/mainline/config/KEYMAP.md)
  as possible, ONLY differing when the extra keys in Sofle provide clear benefit.

Sofle-specific differences (justified by the extra keys/hardware):

- Number row + brackets live on the base layer, so **no symbol layer is needed**
  (Corne's SYMBOL layer existed only because it lacked a number row).
- Left Home (a spare bottom-row key) → `&mo_tog 1 1`: hold for momentary Function,
  tap to lock it on. Corne had no spare key for this — it lives on the left thumb there.
- Joystick = arrow keys on the base layer; mouse cursor on the Function layer.
- Two layers only: QWERTY (0) + FUNCTION (1, hold Enter).
- **The joystick center-press is omitted from the layout tables below for clarity**
  (like the Corne 5-way switch). It still occupies a slot in the `.keymap` thumb row
  — don't be fooled into thinking the bottom row has an extra physical key. There are
  exactly **10 thumb keys (5 left + 5 right)** plus the encoder push-button.

## Legend

| Notation | Meaning |
|----------|---------|
| _(blank)_ | Transparent — falls through to the layer below |
| _(none)_ | No action |
| hold/tap | Hold for first action, tap for second |
| SHIFT/Caps_Word | Hold-tap — hold for Shift, tap for Caps Word |
| &mo_tog L1 | Hold-tap — hold for momentary Layer 1, tap to toggle Layer 1 on/off (sticky) |
| FUNC/BSLH | Hold for macOS Fn/Globe key, tap for Backslash |
| L1/Enter | Hold for Layer 1 (Function), tap for Enter |
| ⌘+key | Modified keycode — sends Cmd+key (not a macro) |
| ⌘⇧4 | Screenshot macro — sends Cmd+Shift+4 |
| ⌘+Click | Macro — holds Cmd while left-clicking (open link in new tab, multi-select) |

### ZMK Reference
1. Keycodes: https://zmk.dev/docs/keymaps/list-of-keycodes
2. Mod Morph: https://zmk.dev/docs/keymaps/behaviors/mod-morph
3. Hold Tap: https://zmk.dev/docs/keymaps/behaviors/hold-tap

## Layer 0: QWERTY (default)

| L        | L1 | L2 | L3 | L4 | L5 | L6  | R6 | R5 | R4 | R3 | R2 | R1 | R       |
|----------|----|----|----|----|----|-----|----|----|----|----|----|----|---------|
| `        | 1  | 2  | 3  | 4  | 5  |     |    | 6  | 7  | 8  | 9  | 0  | EQUAL   |
| TAB      | Q  | W  | E  | R  | T  |     |    | Y  | U  | I  | O  | P  | MINUS   |
| FUNC/BSLH | A  | S  | D  | F  | G  |     |    | H  | J  | K  | L  | ;  | '       |
| ALT      | Z  | X  | C  | V  | B  |     |    | N  | M  | ,  | .  | /  | SHIFT   |
| Mute (enc) | &mo_tog L1 | Caps_Word | Bksp | Cmd | Shift |    |    | Space | L1/Enter | CTRL/ESC | [  | ]  |  |

Encoder: Volume Up / Down (push = Mute)
Joystick (center column): Arrow Keys

> **Notes:**
> - **10 thumb keys** (5 left + 5 right) + the encoder. The joystick center-press is
>   omitted from this row for clarity (like the Corne 5-way switch).
>   - Left:  `&mo_tog L1`, `Caps_Word`, `DEL`, `Cmd`, `Shift`
>   - Right: `Space`, `L1/Enter`, `CTRL/ESC`, `[`, `]`
> - `Mute (enc)` (leftmost cell) is the rotary encoder push-button (`&kp C_MUTE`) —
>   shown only because the firmware row forces a binding there.
> - `ALT` (left pinky, Z-row) matches Corne's `Alt/=` position (Sofle keeps plain Alt —
>   `=` already lives on the number row, so no tap action is needed here).
> - The thumb `Shift` (L5) replaces the old `&mo 1` — Shift now lives on the thumb,
>   mirroring the Corne thumb-cluster hand position.
> - `&mo_tog L1` (leftmost thumb key) = `&mo_tog 1 1`: hold = momentary Function,
>   tap = lock Function on (tap again to unlock).
> - **Thumb-cluster mods** (matches Corne): `Ctrl/Esc` on the **right thumb** for
>   unix/terminal chords; `Cmd` on the **left thumb** (Mac position); `DEL` on the
>   **left thumb, outboard of Cmd** — logical reverse of Enter on the opposite hand,
>   so a mishit lands on `Cmd` rather than `Enter`. `Alt` drops to the left-of-Z pinky;
>   the rare `FUNC/BSLH` (hold macOS Globe, tap Backslash) sits on the left-of-A pinky.
> - `Caps_Word` has its **own dedicated thumb key** (`&caps_word`). This frees the
>   right pinky to be a plain `SHIFT` (`&kp RSHFT`) instead of the `&caps LSHFT 0`
>   hold-tap — simpler, and a true cross-hand Shift.

## Layer 1: FUNCTION (hold Enter, or lock via &mo_tog L1)

Parity with Corne: **Bluetooth on row A**, **RGB on row Z**, vim nav on the right hand.
Sofle's number row becomes **F1–F10**. Center column = joystick → mouse cursor.

| L | L1         | L2     | L3      | L4    | L5       | R5  | R4   | R3   | R2  | R1     | R          |
|---|------------|--------|---------|-------|----------|-----|------|------|-----|--------|------------|
|   | F1         | F2     | F3      | F4    | F5       | F6  | F7   | F8   | F9  | F10    | RGB Bri+   |
|   |            |        |         | ⌘⇧4   |          |     |      |      |     |        | RGB Bri−   |
|   | BT Clr All | BT 0   |         |       | USB      | ←   | ↓    | ↑    | →   | LClick | RClick     |
|   | RGB Off    | RGB On | RGB Eff | Reset | Soft Off | ⌘+← | PgDn | PgUp | ⌘+→ | ⌘+Click | Bootloader |
|   |            |        |         |       |          |     |      |      |     |        |            |

Encoder: Brightness Up / Down
Joystick (center column): Mouse cursor (`&mmv MOVE_*`); center-press = Left Click

> **Notes:**
> - **F1–F10** on the number row (no F11/F12 — the encoder owns volume). These send
>   *true* function keys (HID F-codes); macOS does **not** remap them to media on a
>   non-Apple keyboard, so e.g. F10 is F10, not Mute. (Mute lives on the encoder.)
>   F-key usefulness is a TODO — revisit how to better leverage this row.
> - **RGB brightness** on the right `R` column: `RGB Bri+` on the EQUAL position,
>   `RGB Bri−` on the MINUS position — mnemonic mirror of ⌘+ zoom-in / ⌘- zoom-out.
> - **RGB Off / On / Eff** on the Z-row left (Corne's three), then Reset, Soft Off.
> - **BT 0 only** (+ Clr All), matching Corne. USB output toggle on L5.
> - **Right hand mirrors Corne Layer 2**: A-row = vim arrows `← ↓ ↑ →` then
>   `LClick`/`RClick`; Z-row = `⌘+← PgDn PgUp ⌘+→` then `Bootloader`.
> - `⌘⇧4` screenshot macro sits on the **R key** (Q-row, L4) — physically the same
>   key as on the Corne, for cognitive parity. Mute is **not** here (encoder covers it).
> - Top-right corner (GRAVE position) stays **transparent**.
> - Home/End **dropped** — redundant with vim `0/$/gg/G` and macOS `⌘+←/→`.

> ⚠️ The Function-layer thumb under `&mo_tog L1` must stay **transparent**. When
> Function is locked on, the unlock tap falls through this transparent key to Layer 0's
> `&mo_tog` to toggle it back off. Do **not** assign a real binding there, or you will
> lose the ability to exit the locked Function layer.

## Combos

| Keys                 | Action                |
|----------------------|-----------------------|
| Q + S + Z (hold 2s)  | Soft off (deep sleep) |
