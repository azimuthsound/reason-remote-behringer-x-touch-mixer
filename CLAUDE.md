# Behringer X-Touch (Mixer) — Reason Remote Codec

> **Status: no longer in development.** This codec is kept as an archive and is not being updated. Don't make changes here unless the user explicitly asks for this codec.

Reason Remote (Lua) codec and mixer-focused remote map for the Behringer X-Touch. **Origins:** the codec is based on the Jaexx X-Touch codec, modified by the project owner. The remote map is entirely the project owner's own work. (Some source comments are tagged `[Propellerhead Comment]`; that's just a comment label carried over in the code, not a sign of a separate Propellerhead codec.)

- **Codec / map version:** 1.6.9 (`.luacodec` `version={1,6,9}`, remotemap `Map Version 1.6.9`)
- **Surface name in Reason:** Manufacturer `Behringer`, Model `X-Touch`
- **File dates:** codec Nov 2023, map Dec 2023, map guide Feb 2024
- **Repo:** public on GitHub (`reason-remote-behringer-x-touch-mixer`). Keep it public, and don't add anything personal or private.

---

## Files

| File | What it is |
|------|-----------|
| `Behringer X-Touch.luacodec` | Stub: declares the `X-Touch` surface, points to the `.lua` and `.png`. |
| `Behringer X-Touch.lua` | The codec (~1,550 lines). |
| `Behringer X-Touch.png` | Surface picture for Reason's Control Surfaces preferences. |
| `X-Touch.remotemap` | Remote map (~2,600 lines). Only two scopes, **Reason Document** and **Reason Master Section**, i.e. a mixer controller rather than a per-device map. |
| `X-Touch Map Guide v1.pdf` | 7-page guide to the map's layout: General, Track, Pan, EQ, Send, Plug-In pages. |

---

## Codec notes (`Behringer X-Touch.lua`)

- Structure: `remote_init` defines the items, `remote_set_state` buffers state, `remote_deliver_midi` sends only what changed (`g_new_*` / `g_sent_*`), and `remote_probe` sends an identity SysEx (`F0 00 00 66 14 00 F7`).
- **Items:** 8 faders + master, 8 rotaries, rotary buttons, Record/Solo/Mute/Select per channel, the named Mackie buttons (`28`–`65`), Jog Wheel, rear panel switches/controller, peak meters, 2 LCD rows (per channel and per row), and 7-segment time displays.
- **Rotary modes:** Single Dot, Single Dot Bipolar, Wrap, Boost/Cut, Spread, On/Off, Off, MJ Meter.
- **Model constants** for Control (56), Extender (57), Combo (58/59), C4 (60) and dual extender (61) are still present from the Jaexx base codec's multi-model support. The `.luacodec` only exposes the single `X-Touch` model; `remote_probe` also contains an "MJ X-Touch Trinity LR" branch (control + 2 extenders) that this stub doesn't register.
- Modifications in the source include the "MJ Meter" rotary mode, an "MJ Edit" fix for peak meters crashing the X-Touch / X-Touch Extender, and `rfx_enable_timefix = true` (blanks leading zeros on the time display).
- `k_max_peak_value = 26` (vertical meters).

---

## Install

On this Mac, Reason loads:
- **Codec** (`.luacodec`, `.lua`, `.png`) from `~/Library/Application Support/Propellerhead Software/Remote/Codecs/Lua Codecs/Behringer/`
- **Map** (`.remotemap`) from `~/Library/Application Support/Propellerhead Software/Remote/Maps/Behringer/`

A 2023 `Behringer X-Touch.lua` is already in Reason's codec folder. **Don't modify anything in Reason's Remote folder without asking the user.**
