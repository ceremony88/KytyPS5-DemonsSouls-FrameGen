# KytyPS5 – Demon's Souls Frame Generation Build

A tuned Windows build of the **KytyPS5** PS5 emulator (by chenxiao07 and the KytyPS5 developers) for
**Demon's Souls (PPSA01341)**, based on the upstream release **v20261012**. It adds working DLSS Frame
Generation, ultrawide, a render-resolution option and a themed launcher.

Upstream project: https://github.com/chenxiao07/KytyPS5


> **Disclaimer:** an unofficial, personal build. Not affiliated with or endorsed by Sony Interactive Entertainment,
> Bluepoint Games, FromSoftware, NVIDIA or the KytyPS5 developers. **No game files are included**: use your own
> legally dumped copy of Demon's Souls. Provided as is, without warranty.

**Download:** the zip under [Releases](../../releases/latest). Extract it and follow the Quick start below.
---

## Quick start

1. Extract this folder anywhere (an SSD is best). Keep the files together.
2. Double-click **`launcher.cmd`**.
3. **Game folder** → **Browse...** → choose your unpacked game folder: the one that directly contains
   `eboot.bin` and `sce_sys` (usually `PPSA01341-app0`).
4. Pick your options and press **PLAY**.
5. **Before you play, run Precompile shaders** (the first launch offers it; also a launcher button). It
   builds this PC's shader cache and takes a while, but it resumes if interrupted. Without it the first
   session loads slowly, stutters, and shows **black squares** on the screen until each shader has compiled
   in the background (they go away as you play; nothing is broken).

If Windows SmartScreen warns about the files (they are not signed): **More info → Run anyway**.

**In-game hotkeys:** **F1** = FPS counter · **F2** = DLSS Frame Generation on/off

---

## Precompile shaders (do this once, for a smooth game)

The emulator turns the game's PS5 shaders into shaders for your graphics card. Done while you play, every
new area, effect and enemy stutters the first time it appears (pauses of 0.1–0.4 s). **Precompile shaders**
does all of that ahead of time, for the whole game:

- **When:** once after installing, and again after a new GPU driver or a new version of this build. The
  first launch offers it; afterwards use the launcher's **Precompile shaders** button.
- **How long:** a long job: up to a few hours, depending on the CPU. Run it overnight or while you do
  something else. It resumes where it stopped if you close it.
- **Tip:** tick **Precompile on efficiency cores** (Intel 12th gen and newer) to keep the PC usable meanwhile.
- **Result:** several GB in `_PipelineCache\static\`, made for your GPU and driver. Afterwards the game boots
  in seconds and areas load without compile stutter. Shaders it still meets for the first time are cached
  as you play, so the second visit is smooth anyway.

---

## Requirements

| | |
|---|---|
| OS | Windows 10 (1803+) or 11, 64-bit |
| CPU | AVX2 (Intel Core 4th gen / AMD Ryzen or newer), 8+ cores recommended |
| RAM | 32 GB recommended, 16 GB works (keep the page file "system managed") |
| GPU | NVIDIA RTX, 12 GB VRAM recommended. **Frame Generation needs an RTX 40-series or newer** and hardware-accelerated GPU scheduling on; other GPUs run without it |
| Driver | The latest NVIDIA driver |
| Game | Your own dump of Demon's Souls PPSA01341. The ultrawide and render-resolution patches are for version **01.007.000** |
| Disk | ~83 GB for the game; the shader caches grow to a few GB |

---

## Performance

Measured on **RTX 4080 · Core i7-13700K · 32 GB RAM · NVMe SSD**, 3440x1440 ultrawide:

| Situation | Result |
|---|---|
| Frame Generation on | **~117 fps output** (game ~58), lows ~112 |
| Heavy areas, native 2560x1440 render | 40–49 fps |
| Heavy areas, **1080p render** (4K output) | mostly 50s to high 50s, rare dips to 48–49 |

---

## Features

**DLSS Frame Generation (NVIDIA Streamline DLSS-G + Reflex)**
- Reflex paces every frame (without it DLSS-G held the game at 30 fps).
- Presenting runs on its own thread, so the game's 60 Hz timing never waits on the driver.
- **Camera learning:** frame generation needs the game's camera each frame. The build learns where each
  shader keeps it and saves that to `_PipelineCache\framegen-camera-layouts.txt`. This package already
  includes 300 learned layouts, so it covers the whole game from the start, and keeps learning.
- Brief gaps in camera data no longer make frame generation flicker on and off.
- It pauses while the window is minimized or not in focus, and resumes when you return.

**Render resolution:** lowers the PS5 performance mode's internal 3D resolution and keeps the 3840x2160
output, so the HUD stays sharp and correctly sized; the game's own temporal upscaler rebuilds the image.
Native (2560x1440) · 1260p · **1080p** (recommended for heavy areas) · 900p. Applied in memory at launch;
the game files are never modified.

**Ultrawide 3440x1440:** a 43:18 aspect patch for the 3D view, full screen with no black bars (the HUD
and menus stretch sideways).

**Shader caches:** the pipeline cache survives emulator updates and holds up to 2 GiB; a warm-up at boot
plus the precompiled shaders remove compile stutter.

---

## Launcher options

| Option | What it does |
|---|---|
| Game folder | The game dump (folder with `eboot.bin` and `sce_sys`) or a `.zar` archive |
| Display mode | Ultrawide 3440x1440 · Fullscreen 16:9 with black bars · Fullscreen stretched · Windowed |
| Window size | The window's size in windowed mode |
| Render resolution | Native / 1260p / 1080p / 900p internal render, always 4K output |
| FPS counter | On-screen fps (F1 in game) |
| Console language | The game's language |
| Graphics effects | Volumetric fog (~+4.6% off) · Torch/spot shadows · Contact shadows (~+3% off) · Sun shadows (~+8.5% off) · Depth of field · Bloom · Film grain |
| DLSS Frame Generation | Starts with FG on (F2 in game) |
| Red-zone protection | Stability protection for the game's code (keep on) |
| Precompile on efficiency cores | Precompile on the E-cores only, so the PC stays usable |
| Buttons | Play · Precompile shaders · Logs folder · README |

**Always on: the game's GPU culling pass is skipped.** Before drawing each object the game runs a small GPU
program that throws away its hidden triangles (about 2,800 extra GPU jobs a frame in Boletaria). On a PS5
that saves work; in the emulator each job costs CPU time, the bottleneck, so the build skips the pass and
simply draws every triangle: ~6% faster, the picture identical (only triangles you could not see were removed).

**Recommended (RTX 40-series):** Ultrawide or Fullscreen 16:9 · Render resolution 1080p · Frame
Generation on.

---

## Files

- `launcher.cmd` – the launcher; `run.cmd` – start without the launcher.
- `logs\` – a log per session (the launcher's **Logs folder** button). Include the latest one when
  reporting a problem.
- `_SaveData\` – your saves. `_PipelineCache\` – shader caches and the camera layouts. Back up
  `_SaveData` before deleting the folder.

---

*Based on KytyPS5 v20261012 by chenxiao07 and the KytyPS5 developers (MIT, see `LICENSE` and
`LICENSES\`). Frame generation uses NVIDIA Streamline, DLSS Frame Generation and Reflex; their license
files are in `streamline\bin\x64`. A personal build, not an official release. No game files are
included.*
