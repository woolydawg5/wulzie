# Flashing safety — how we don't brick the FM-1

The FM-1 keeps **one copy** of its firmware. Reverse-engineering notes say that no safe recovery
from an interrupted write has been established. So these rules are hard rules.

## The rules

1. **Recovery comes before risk.** No Wulzie build touches the device until the FM-1 Transporter
   recovery path has been read, the parts are on the bench, and we know the exact steps.
2. **Prove the pipeline with someone else's firmware first.** Install an unmodified SLOOP release.
   Then return to the official firmware with M-VAVE's M-UPGRADE. Then install SLOOP again. If any
   step fails on this unit, we stop and find out why.
3. **We don't write our own bootloader or update loader in v0.x.** The loader is the code that
   rewrites the flash, and it's the one piece that can brick the device. Wulzie uses the **proven
   update path** that SLOOP, Felucca and Hortator use, the JieLi SDK's package format. Wulzie only
   replaces the *application*.
4. **Every build passes the host tests and runs in the simulator before it's flashed.** If the
   simulator can't run it, the FM-1 doesn't get it.
5. **Back up before every install.** Export any SLOOP projects and samples first. Projects saved
   by one firmware may not open in another.
6. **Data cable, no USB hub, laptop on mains power** during installs.
7. **Never unplug during an install.** If it's interrupted, the device usually stays in update
   mode. Run the install again.

## The ladder back (try in order)

| Rung | When | How |
|---|---|---|
| 1 | Wulzie boots but misbehaves | Its own menu item: return to official firmware (to build in v0.1). |
| 2 | Wulzie won't start but the installer still sees the FM-1 | Run the install again, or M-UPGRADE with the official `FM-1.fwsc`. |
| 3 | Neither tool sees it, but the chip's boot mode still answers | Boot-mode recovery (Hortator documents one; to be read and rehearsed). |
| 4 | It never reaches boot mode | **FM-1 Transporter** with a Seeed XIAO RP2040, which writes the flash directly. |

⬜ **Before the first Wulzie flash:** read the Transporter's instructions in full. Find out whether
it needs soldering or opening the case, then write the exact steps into this file.
