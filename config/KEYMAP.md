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
- Colemak-DH is a persistent alternate base layer, toggled with the left-thumb
  sticky Shift key plus the right-thumb Space key.
- Joystick = arrow keys on the base layer; mouse cursor on the Function layer.
- Three layers: QWERTY (0) + Colemak-DH (1) + FUNCTION (2, hold Enter).
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
| L2/Enter | Hold for Layer 2 (Function), tap for Enter |
| CMD/TAB | Hold for Cmd, tap for Tab |
| ⌘+key | Modified keycode — sends Cmd+key (not a macro) |
| ⌘⇧4 | Screenshot macro — sends Cmd+Shift+4 |
| &sk | Sticky keys. Use modifiers with the next keypress, or hold for active modifier |

### ZMK Reference
1. Keycodes: https://zmk.dev/docs/keymaps/list-of-keycodes
2. Mod Morph: https://zmk.dev/docs/keymaps/behaviors/mod-morph
3. Hold Tap: https://zmk.dev/docs/keymaps/behaviors/hold-tap

## Layer 0: QWERTY (default)

| L        | L1 | L2 | L3 | L4 | L5 | L6  | R6 | R5 | R4 | R3 | R2 | R1 | R       |
|----------|----|----|----|----|----|-----|----|----|----|----|----|----|---------|
| `        | 1  | 2  | 3  | 4  | 5  |     |    | 6  | 7  | 8  | 9  | 0  | EQUAL   |
| TAB      | Q  | W  | E  | R  | T  |     |    | Y  | U  | I  | O  | P  | MINUS   |
| Caps Lock | A  | S  | D  | F  | G  |     |    | H  | J  | K  | L  | ;  | '       |
| ALT      | Z  | X  | C  | V  | B  |     |    | N  | M  | ,  | .  | /  | SHIFT   |
| Mute (enc) | Caps_Word | BSLH | CMD/TAB | Bksp | &sk Shift |    |    | Space | L2/Enter | CTRL/ESC | [  | ]  |  |

Encoder: Volume Up / Down (push = Mute)
Joystick (center column): Arrow Keys

> **Notes:**
> - **10 thumb keys** (5 left + 5 right) + the encoder. The joystick center-press is
>   omitted from this row for clarity (like the Corne 5-way switch).
>   - Left:  `Caps_Word`, `BSLH`, `CMD/TAB`, `Bksp`, `&sk Shift`
>   - Right: `Space`, `L2/Enter`, `CTRL/ESC`, `[`, `]`
> - `Mute (enc)` (leftmost cell) is the rotary encoder push-button (`&kp C_MUTE`) —
>   shown only because the firmware row forces a binding there.
> - The three alpha-row outer keys match Corne on both sides:
>   `TAB` / `Caps Lock` / `ALT` on the left and `MINUS` / `'` / `SHIFT` on the right.
> - `CMD/TAB` holds Cmd or taps Tab. It sits inboard of Backspace so the two primary
>   left-thumb editing keys are adjacent.
> - Sticky `Shift` (L5) lives on the thumb, mirroring the Corne thumb-cluster hand
>   position.
> - **No sticky Function layer.** Function is reached by **holding Enter**
>   (`&lt 2 ENTER`) only — the old layer lock was dropped because an accidental
>   tap on the outermost thumb key silently trapped you in the Function layer.
> - **Thumb-cluster mods** (matches Corne): `Ctrl/Esc` on the **right thumb** for
>   unix/terminal chords; `Cmd/Tab` on the **left thumb** (Mac position); `Bksp`
>   immediately inboard of it; and sticky Shift on the innermost left thumb.
> - `Caps_Word` (`&caps_word`) lives on the **outermost** left thumb key — the easiest
>   spot to mis-hit, but a stray tap self-cancels at the next word-break, so it's
>   harmless there. This also frees the right pinky to be a plain `SHIFT` (`&kp RSHFT`)
>   instead of the `&caps LSHFT 0` hold-tap — simpler, and a true cross-hand Shift.

## Layer 1: Colemak-DH

From QWERTY, press left-thumb sticky Shift and right-thumb Space
(`&sk Shift` + `Space`) together to switch to Colemak-DH. Press the same
physical chord again to return to QWERTY.

The number row and thumb row remain transparent to fall back to the QWERTY layer.
The two outer columns explicitly match QWERTY and Corne.

| L        | L1 | L2 | L3 | L4 | L5 | R5 | R4 | R3 | R2 | R1 | R  |
|----------|----|----|----|----|----|----|----|----|----|----|----|
|          |    |    |    |    |    |    |    |    |    |    |    |
| TAB      | Q  | W  | F  | P  | B  | J  | L  | U  | Y  | ;  | MINUS |
| Caps Lock | A  | R  | S  | T  | G  | M  | N  | E  | I  | O  | ' |
| ALT      | Z  | X  | C  | D  | V  | K  | H  | ,  | .  | FSLH | SHIFT |
|          |    |    |    |    |    |    |    |    |    |    |    |

## Layer 2: FUNCTION (hold Enter)

The three alpha rows mirror Corne's Function layer as closely as possible.
Sofle's number row becomes **F11, F1–F10, F12**. Center column = joystick → mouse cursor.

| L | L1         | L2     | L3      | L4    | L5       | R5  | R4     | R3     | R2  | R1 | R          |
|---|------------|--------|---------|-------|----------|-----|--------|--------|-----|----|------------|
| F11 | F1       | F2     | F3      | F4    | F5       | F6  | F7     | F8     | F9  | F10 | F12      |
| Reset | TAB    | Mute   | F3      | ⌘⇧4   | USB      |     | LClick | RClick |     |    | Bootloader |
| BT Clr All | Caps Lock | &sk CTRL | &sk ALT | &sk CMD | Caps Word | ← | ↓ | ↑ | → | | |
| Soft Off | RGB Off | RGB On | BT 0 | BT 1 | BT 2 | PgDn | PgUp | | | | |
|   |            |        |         |       |          |     |        |        |     |    |            |

Encoder: Brightness Up / Down
Joystick (center column): Mouse cursor (`&mmv MOVE_*`); center-press = Left Click

> **Notes:**
> - **F11, F1–F10, F12** fill the number row. These send
>   *true* function keys (HID F-codes); macOS does **not** remap them to media on a
>   non-Apple keyboard. Mute remains available on the encoder and the Corne-matching
>   Function position.
> - **Bluetooth** matches Corne: `BT Clr All` sits on the left outer home-row key,
>   a deliberate stretch — it wipes *all* pairings, so it must be hard to hit by
>   accident. `BT 0` / `BT 1` / `BT 2` sit on `C` / `V` / `B`.
> - `USB` occupies Corne's Symbol-toggle position because Sofle has no Symbol layer.
> - **No function-layer `~`** (unlike Corne): Sofle's base layer already has a physical
>   `` ` ``/`~` in its top-left corner (real number row), so the tilde family is already
>   home — no function-layer slot needed. This divergence from Corne is intentional.
> - **Right hand mirrors Corne Layer 3**: Q-row has left/right mouse clicks,
>   A-row has arrows, and Z-row has Page Down / Page Up.
> - **Bootloader** on the Q-row right `R` column (MINUS position, right of P) —
>   rare maintenance key pushed high and out of the way. Bottom-right (RSHFT position)
>   is now transparent so `Func + Shift + navigation` chords work.
> - `⌘⇧4` screenshot macro sits on the **R key** (Q-row, L4) — physically the same
>   key as on the Corne, for cognitive parity.
> - The physical `MINUS` and `'` positions remain transparent on Function because
>   those keys are already directly available on Sofle's base layers.

## Combos

| Keys                 | Action                |
|----------------------|-----------------------|
| Q + S + Z (hold 2s)  | Soft off (deep sleep) |
| Left `&sk Shift` + right `Space` | Toggle Colemak-DH |
