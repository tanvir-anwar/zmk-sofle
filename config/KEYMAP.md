# Eyelash Sofle Keymap Reference

This is a human-readable reference of the keymap defined in `eyelash_sofle.keymap`.
Edit this file to describe desired changes, then update the keymap to match.

## Legend

| Notation | Meaning |
|----------|---------|
| _(blank)_ | Transparent — falls through to the layer below |
| _(none)_ | No action |
| hold/tap | Hold for first action, tap for second |
| [Sh/Caps] | Tap-dance — tap for Shift, double-tap for Caps Word |
| L1/Enter | Hold for Layer 1 (Function), tap for Enter |
| ⌘+key | Modified keycode — sends Cmd+key (not a macro) |
| ⌘⇧4 | Screenshot macro — sends Cmd+Shift+4 |

### ZMK Reference
1. Keycodes: https://zmk.dev/docs/keymaps/list-of-keycodes
2. Mod Morph: https://zmk.dev/docs/keymaps/behaviors/mod-morph
3. Hold Tap: https://zmk.dev/docs/keymaps/behaviors/hold-tap

## Layer 0: QWERTY (default)

| L   | L1 | L2 |  L3 |  L4  | L5  |    L6     | R6    |  R5      |  R4  | R3 | R2 | R1 | R     |
|-----|----|----|-----|------|-----|-----------|-------|----------|------|----|----|----|-------|
| `   | 1  | 2  |  3  |  4   |  5  |           |       |  6       |  7   | 8  | 9  | 0  | EQUAL |
| TAB | Q  | W  |  E  |  R   |  T  |           |       |  Y       |  U   | I  | O  | P  | MINUS |
| ESC | A  | S  |  D  |  F   |  G  |           |       |  H       |  J   | K  | L  | ;  | '     |
| CMD | Z  | X  |  C  |  V   |  B  |           |       |  N       |  M   | ,  | .  | /  | SHIFT |
|     |    | \  | FN  | LALT | DEL | [Sh/Caps] | Space | L1/Enter | CTRL | [  |  ] |    |       |

Encoder: Volume Up / Down
Joystick: Pointing device (middle click disabled)

> **Note:** L6 = rotary encoder, R6 = joystick. L/L1 and R1/R thumb positions are empty (no physical keys).

## Layer 1: Function (hold L1)

```
opencode -s ses_0f3ce088affekhwEEhXABlm8j5
```

| L   | L1 | L2 |  L3 |  L4  | L5  |    L6     | R6    |  R5      |  R4  | R3 | R2 | R1 | R     |
|-----|----|----|-----|------|-----|-----------|-------|----------|------|----|----|----|-------|


Encoder: Scroll Down / Up
Joystick: Pointing device (middle click disabled)

## Layer 1: FUNCTION / From Corne (reference)

| L      | L1         | L2       | L3         | L4    | L5       | R6       | R5       | R4       | R3       | R2       | R1     | R          |
|--------|------------|----------|------------|-------|----------|----------|----------|----------|----------|----------|--------|------------|
|        | F3         | Mute     | ⌘⇧4       |       |          |          |          |          |          |          |        |            |
|        | BT Clr All | BT 0     | BT 1       | BT 2  | USB      | ←        | ↓        | ↑        | →        | LClick  | RClick     |
|        | RGB Off    | RGB On   | RGB Eff    | Reset | Soft Off | ⌘+←      | ⌘+↓      | ⌘+↑      | ⌘+→      |         | Bootloader |
|        |            |          |            |       |          |          |          |          |          |         |            |

Encoder: Brightness Up / Down

## Combos

| Keys                 | Action                |
|----------------------|-----------------------|
| Q + S + Z (hold 2s)  | Soft off (deep sleep) |
