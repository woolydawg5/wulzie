# M-VAVE FM-1 — what we know, and how sure we are

This page is the hardware truth Wulzie builds on. Every line says **where it came from** and **how
confident** we are in it. Nothing here was measured on Wooly's unit yet. Phase 0 verifies what it
can and turns `REPORTED` into `VERIFIED` or `WRONG`.

| Legend | Meaning |
|---|---|
| **VERIFIED** | checked on Wooly's own FM-1 (date) |
| **DOCUMENTED** | stated in the README or docs of a working open-source firmware |
| **REPORTED** | secondhand: a write-up, a forum post or an AI digest; treat as a lead |
| **UNKNOWN** | nobody we read says |

## Chip and memory

| Fact | Status | Source |
|---|---|---|
| JieLi AC79-family SoC (WL82 / "AC791N"), **pi32v2** CPU | REPORTED (chip name) · DOCUMENTED (toolchain targets pi32v2, SDK path `cpu/wl82`) | AL-255/FM-1-RE via Zeli digest; SLOOP `BUILDING.md` |
| **Two cores**, both usable for audio | DOCUMENTED | SLOOP README ("the sound now runs on both of the FM-1's cores") |
| ~**96 KiB** main RAM region (98,304 B) | DOCUMENTED | SLOOP `RAM.md` |
| ~**344 KiB** audio/sample pool (344,064 B) | DOCUMENTED | SLOOP `RAM.md` |
| Flash size | UNKNOWN | — some units have a newer **UC25HQ80** flash chip that older firmwares failed to recognise (SLOOP README) |
| Stock FM engine is Dexed-derived (6-op) | REPORTED | Zeli digest; unverified |

## Controls

| Fact | Status | Source |
|---|---|---|
| **16 white keys** + black keys | DOCUMENTED | SLOOP, Felucca, Hortator |
| **KNOB 1–4** | DOCUMENTED | SLOOP |
| SELECT, ALGORITHM, PRESETS, MASTER volume knobs; whether they are endless encoders or pots | DOCUMENTED (names) · UNKNOWN (type) | Hortator |
| Buttons: HOME, EDIT, SEQ, FX, ARP, LFO, GLO, SAVE, SCL/SEL, OCT−, OCT+, PLAY, REC | DOCUMENTED | Felucca / Hortator |
| Button backlight, 3 levels; per-track colours in SLOOP (blue/green/yellow/orange) | DOCUMENTED (levels) · UNKNOWN (whether LEDs are RGB) | SLOOP |

## Screen

| Fact | Status | Source |
|---|---|---|
| **Colour screen** | VERIFIED (2026-11-10, Wooly looking at his own unit) | an earlier draft called it monochrome, misreading Hortator's "true white-on-black LCD", which appears to describe a display theme |
| Resolution and colour depth | UNKNOWN | — Phase 0 finds these in the SLOOP/Felucca display code |

The neon theme can live **on the device itself**. The limit is memory, not colour: a full colour
frame may not fit comfortably in ~96 KiB of RAM (for example, 320×240 at 16 bits per pixel would
be 150 KiB). So the screen may have to be drawn in strips. Phase 0 settles this.

## Audio

| Fact | Status | Source |
|---|---|---|
| Built-in speaker | DOCUMENTED | Hortator |
| Headphone output | DOCUMENTED | Hortator, SLOOP |
| **No audio input** (no mic, no line-in) | DOCUMENTED by absence | none of SLOOP / Felucca / Hortator mention one |
| USB Audio *to* the computer (44.1 kHz stereo; the computer records the FM-1) | DOCUMENTED | SLOOP, Felucca |
| USB Audio *from* the computer (the FM-1 as a USB "speaker") | UNKNOWN | the chip's SDK appears to support the class; nobody has shipped it on the FM-1 that we found. A Wulzie experiment (see ROADMAP). |

## Connectivity and storage

| Fact | Status | Source |
|---|---|---|
| USB-C, class-compliant MIDI in/out | DOCUMENTED | all three |
| TRS MIDI **in** (3.5 mm, needs TRS-to-DIN adapter) | DOCUMENTED | SLOOP, Felucca |
| MIDI out on TRS | UNKNOWN (none mentioned) | — |
| The FM-1 is a USB **device** only: a USB keyboard or the DDJ-FLX4 can't plug straight in | DOCUMENTED | SLOOP |
| Bluetooth/Wi-Fi radio on the chip | DOCUMENTED (Hortator BT build) | Hortator |
| Internal flash storage; **no SD card** | DOCUMENTED | Hortator, SLOOP |
| Internal battery ~2,000 mAh | REPORTED | Elektronauts forum |

## Flashing and recovery

See [SAFETY.md](SAFETY.md).

## Sources

- SLOOP — <https://github.com/isod89/sloop-fm1> (GPL-3.0)
- Felucca — <https://github.com/hugelton/Felucca> (GPL-3.0-only)
- Hortator — <https://codeberg.org/armin/hortator> (GPL-3.0-only)
- FM-1 reverse engineering — <https://github.com/AL-255/FM-1-RE> (not yet read directly; summarised at <https://zeli.app/story/49994065>)
- FM-1 Transporter (recovery) — <https://github.com/kurogedelic/FM-1-transporter> (not yet read)
- JieLi AC79 SDK — <https://gitee.com/Jieli-Tech/fw-AC79_AIoT_SDK> (Apache-2.0)
