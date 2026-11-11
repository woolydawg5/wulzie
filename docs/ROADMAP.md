# Wulzie roadmap

The priority order is Wooly's (2026-11-10): **bass sound design → sequencing and looping → sampling
and chopping.** The tutorial grows with every phase; it's never a final phase. Each version ships
only when its tests pass on the host and in the simulator, and it has been run on the FM-1.

| Phase | Version | Name | Delivers |
|---|---|---|---|
| 0 | — | **Safety bench** | WSL and the JieLi toolchain installed. SLOOP built from source and flashed (proves the pipeline). Round trip to the official firmware and back. Transporter steps read and written into `SAFETY.md`. Facts in `HARDWARE.md` checked on Wooly's unit (screen resolution and colour depth, knob types, per-button light control, FPU or not). |
| 1 | **0.1** | **First Contact** | See [SPEC-v0.1.md](SPEC-v0.1.md): boot, live input test, one voice, on-screen diagnostics, a way back to official firmware, the simulator shell, the test harness, tutorial lessons 1–3. |
| 2 | 0.2 | **Reese Engine** | The bass voice: a 3–7 saw supersaw/reese stack with detune spread and phase drift, a sub, a 2-pole/4-pole filter with drive, waveshaper/fold distortion, an LFO with tempo-synced wobble rates (1/4 to 1/32, triplets, dotted), mono/legato glide, macro knobs. A starter bank aimed at the reference tracks. |
| 3 | 0.3 | **Growl Lab** | FM growls (2–4 operator), a formant/vowel filter ("talking" bass), comb filter, bit/rate crush, a modulation matrix with 2 LFOs and envelopes into anything. |
| 4 | 0.4 | **Time Machine** | Transport, a 4-track step sequencer, **independent track lengths** (polymeter/polyrhythm), parameter locks, swing, MIDI clock in, save/load with versioned projects. |
| 5 | 0.5 | **Loop Station** | Resampling the FM-1's own output into RAM, overdub loops, reverse, half-speed, tape stop and start. |
| 6 | 0.6 | **Space** | Reverb (small, RAM-aware), ping-pong delay, binaural 3D panning and orbiting sources for headphones, drone/texture mode. |
| 7 | 0.7 | **Chop Shop** | Sample slicing, a scratch mode (knob/jog as a record), granular time-stretch, the companion app loading samples over USB. **Experiment:** the FM-1 as a USB audio *input* from the computer. |
| 8 | 0.8 | **The Bench** | The simulator placed in the WulWorks lab room as an instrument, with the firmware download beside it. |
| — | later | **Radio** | Custom hardware: radio receiver to audio input. |

## Companion app (grows alongside, from Phase 4)

A web page (Chrome/Edge, Web MIDI) that lives in the lab next to the simulator:

- back up and restore projects
- load samples
- edit presets on a big screen
- install firmware
- later, bridge the **DDJ-FLX4** to the FM-1. The FLX4 is a USB device and can't plug into the
  FM-1 directly, so the computer relays its jog wheels for scratching and its faders for
  crossfades. A hardware USB-MIDI host box into the FM-1's TRS MIDI jack is the computer-free
  alternative.

## Sound targets (reference tracks)

Wooly's references, as listening targets for the presets:

- **Tipper — "Puzzle Dust"** (psychedelic glitch-bass, intricate sound design)
- **Mind G4me — "Stupid Boi"** (dubstep/riddim)
- **Birrd — "Void Loop"** (drones)

The presets aim at the *techniques* behind these tracks, never their samples. Claude can't listen
to audio. Each target is described by Wooly with timestamps, turned into a preset recipe, and
checked by ear.
