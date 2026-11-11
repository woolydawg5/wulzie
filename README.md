# Wulzie

**Custom firmware for the M-VAVE FM-1** that turns it into a bass-heavy, space-bending groovebox
for dubstep, riddim, psychedelic glitch-bass, spacey synthwave and drones. It's built from the
ground up, open source under GPL-3.0, and it runs identically on the device and in a browser
simulator.

> **Status: v0.1 in planning. No firmware to install yet.** Don't flash anything from this repo
> until a release says it's ready. See [docs/SAFETY.md](docs/SAFETY.md).

## What it will do

- **Deep bass:** reese stacks, FM growls, talking formant wobbles, tempo-synced modulation.
- **Time:** polyrhythmic sequencing, looping, reversing, slowing, scratching.
- **Space:** reverb, delays and binaural 3D movement for headphones.
- **Drones:** long, evolving, meditative textures.
- **A guided tutorial** built into the device that teaches every function by having you make
  something.
- **Standalone first,** with a web companion that expands it when it's plugged into a computer.

## How it's built

One portable C core holds the synth, the interface and the screen drawing. It talks to the world
only through a small hardware layer, and it's compiled three ways:

| Build | Purpose |
|---|---|
| `platform/host` | the test harness: unit, scenario, fuzz and golden-audio tests on a PC |
| `platform/wasm` | the browser simulator (and later the WulWorks lab instrument) |
| `platform/fm1` | the real firmware, via the JieLi AC79 SDK |

Full plan: [docs/ROADMAP.md](docs/ROADMAP.md) · current spec: [docs/SPEC-v0.1.md](docs/SPEC-v0.1.md)
· what we know about the hardware: [docs/HARDWARE.md](docs/HARDWARE.md).

## Why it's built this way

- **From scratch, and GPL-3.0 anyway.** Wulzie is written fresh so that we understand every line
  of it. It's GPL-3.0 because the firmwares we learn from (SLOOP, Felucca, Hortator) are GPL-3.0
  and Wulzie is published openly. That way no borrowed idea or fragment is ever a legal question,
  and permissively licensed DSP (MIT, Apache) can be reused with credit.
- **One core, three builds.** The simulator isn't a re-creation of the firmware: it *is* the
  firmware. Every bug can be reproduced on a PC, every test runs without risking the device, and
  the lab simulator can never drift from the real thing.
- **Proven flashing, not our own.** The device keeps a single copy of its firmware. Wulzie uses
  the update path the community has already proven and never writes its own bootloader in v0.x.
  See [docs/SAFETY.md](docs/SAFETY.md).
- **Diagnostics on the screen.** CPU, memory and audio health are shown on the device and in the
  simulator. Nobody should need a developer console to find out what's wrong.
- **Standalone first.** The FM-1 has very little memory (about 96 KB of working RAM and a ~340 KB
  sample pool) and no audio input. Everything core works on the device alone; the computer
  companion only adds.

## Style

Wulzie is a WulWorks project. Its look comes from the WulWorks house style guides (`STYLE.md`,
`MATERIALS.md`): deep-space black, neon purple for interactive chrome, cyan for data, magenta for
focus, terminal green for confirmed states, and hardware that reads as a real object you could
pick up.

**How Wulzie modifies that style:** the FM-1's screen is reported to be a **monochrome**
white-on-black LCD. On the device, the cyber-vaporwave theme is expressed through 1-bit pixel art
(space and alien icons) and motion, not colour. The full neon palette lives in the simulator and
the companion app.

## Credits and learning sources

Learned from, not copied: [SLOOP](https://github.com/isod89/sloop-fm1),
[Felucca](https://github.com/hugelton/Felucca), [Hortator](https://codeberg.org/armin/hortator),
[FM-1-RE](https://github.com/AL-255/FM-1-RE), [FM-1 Transporter](https://github.com/kurogedelic/FM-1-transporter).
Not affiliated with M-VAVE.

## Origin

Wulzie's intent is preserved in the creator's own words in [docs/PROMPTS.md](docs/PROMPTS.md).

## License

GPL-3.0. See [LICENSE](LICENSE).
