# Wulzie v0.1 "First Contact" — specification

**Goal:** prove the whole loop end-to-end with the smallest useful firmware. Wulzie boots on the
FM-1, sees every control, makes one good sound, shows its own health on screen, can always get
back to the official firmware, and runs identically in the simulator and the test harness.

Status: **draft, 2026-11-10.** Items marked ⚠️ depend on Phase 0 facts we don't have yet.

## 1. Architecture — one core, three builds

```
            ┌──────────────────────────────────────────┐
            │  core/   portable C (C99)                 │
            │  synth · ui state machine · screen draw   │
            │  no hardware calls, no malloc, no clock   │
            └──────────────┬───────────────────────────┘
                           │  hal.h  (the only door in or out)
        ┌──────────────────┼──────────────────────┐
  platform/host      platform/wasm          platform/fm1
  tests, WAV render  simulator in browser   JieLi SDK, real device
```

- **The core is deterministic.** Given the same events and the same number of audio blocks, it
  produces the same samples and the same screen, on every platform. That's what makes testing
  real.
- **Core entry points:** `wz_init()`, `wz_event(ev)` (key/button/knob/MIDI), `wz_audio(block)`
  (fills N stereo frames), `wz_draw(fb)` (draws the colour screen using a small neon palette), `wz_tick(ms)`.
  ⚠️ Screen size, colour depth and whether it draws whole frames or strips come from Phase 0.
- **All memory is static.** Sizes are fixed at compile time, and a build fails if they exceed the
  FM-1 budget.
- ⚠️ **Number format:** float or fixed-point depends on whether the pi32v2 has a usable FPU. Phase 0
  answers this by reading SLOOP's DSP code and timing a test on the device. The core uses a
  `wz_sample` type, so the choice is one switch.

## 2. Features

| # | Feature | Detail |
|---|---|---|
| F1 | **Boot** | Neon splash screen: a small alien in purple, blue and green, "WULZIE v0.1", then the Play screen. |
| F2 | **Input test page** | Every key, button and knob drawn on screen, lighting up live. Also the first thing to check when a control seems dead. |
| F3 | **One voice** | Mono: saw + square sub oscillator, 2-pole low-pass filter, ADSR amp envelope, glide. Keys play notes; OCT−/OCT+ shift octaves. Knobs: **1** cutoff · **2** resonance · **3** detune (a second saw: the reese seed) · **4** glide. |
| F4 | **Diagnostics overlay** | On screen, never in a console: CPU load %, peak CPU, RAM used/free, audio underrun count, firmware version. Toggled by a button combo. |
| F5 | **Hearing safety** | Starts at a low output level. DC blocker and soft limiter on the master. A filter at high resonance can never produce a full-scale scream. |
| F6 | **Way home** | A menu item to put the FM-1 into update mode for M-UPGRADE. ⚠️ The exact mechanism depends on the proven loader. |
| F7 | **Tutorial lessons 1–3** | 1 "First Contact" (keys and octaves) · 2 "Shape the Signal" (the four knobs) · 3 "Two Saws Make a Reese" (detune). Each lesson shows a step, waits for you to do it, then confirms. |

The control layout is drafted after Wooly has played SLOOP. The *ideas* of a good layout ("hold a
function button and the keys change job") are free to reuse; only code is licensed.

## 3. Testing — every function, every order of operations

| Layer | What | Example |
|---|---|---|
| Unit | each DSP block and UI function alone | the filter's measured cutoff matches the requested one; the envelope reaches sustain at the right time |
| Scenario | scripted event sequences, checking screen and sound | "hold note, turn knob 3, change octave mid-note, release" → no stuck note, correct pitch |
| Fuzz | millions of random events (button mashing at machine speed) | never hangs, never outputs NaN or above full scale, no stuck notes after all-release |
| Golden audio | rendered WAVs compared against approved references | a change that alters the sound is noticed, not accidental |
| Budget | CPU per audio block measured on the device, shown in the diagnostics | the voice stays under its budget with headroom |

Tests run on the host with one command. The simulator runs the same core, so every scenario can
also be watched.

## 4. Simulator shell (v0.1 scope)

A browser page with the FM-1 drawn as hardware, running the same core compiled to WebAssembly.
You play it with mouse and keyboard, with sound through Web Audio. v0.1 is a working shell; the
polished lab instrument is Phase 8.

## 5. Acceptance — v0.1 is done when

- [ ] Host tests (unit, scenario, fuzz, golden) pass with one command.
- [ ] The simulator plays the voice, and the input test page responds to mouse and keyboard.
- [ ] On the FM-1: boots, every control shows on the input test page, the voice plays on
      headphones, diagnostics show real numbers, "way home" returns to official firmware.
- [ ] A round trip Wulzie → official → Wulzie succeeds on Wooly's unit.
- [ ] Tutorial lessons 1–3 can be completed on the device and in the simulator.
- [ ] README, CHANGELOG and PROMPTS updated.

## 6. Not in v0.1

Sequencer, effects, sampling, saving, MIDI beyond notes in, the companion app, the lab placement.
