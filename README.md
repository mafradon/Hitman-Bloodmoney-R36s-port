# Hitman: Blood Money - Reprisal for Linux handhelds (PortMaster)

A native **aarch64** port of the Android release of *Hitman: Blood Money -
Reprisal*. It runs Feral's original game engine directly on Linux through a
custom Android-on-Linux loader: Vulkan on KMS, OpenSL ES over ALSA, controller
input, touch and rumble. No emulation, no Box64.

**You must own the game and supply its five original APK files.** No game
content from Feral Interactive or IO Interactive is included here.

> **Device support: this port needs a GPU with a working Vulkan driver.**
> It is developed and tested on the **Anbernic RG353V** (Mali-G52, dArkOS).
> The **R36S and other RK3326 / Mali-G31 devices are NOT supported**: their
> Mali driver has no Vulkan screen output, and they have 1 GB of RAM or less
> (the game alone uses about 850 MB). On such a device the port shows
> "could not take over the screen with Vulkan" and returns to the menu.

## Download

Get **`bmr.zip`** from the [latest release](../../releases/latest).

## Installation

1. Unzip `bmr.zip` into your `ports/` folder (for example `/roms/ports/`). You
   should end up with:
   ```
   ports/Hitman Blood Money Reprisal.sh
   ports/bmr/
   ```
2. From your own Android install of the game, copy these five files (for
   example with SAI, or `adb pull` of the split APKs):
   - `base.apk` (~36 MB)
   - `split_data_core.apk` (~1.0 GB)
   - `split_data_support1.apk` (~1.0 GB)
   - `split_data_support2.apk` (~1.0 GB)
   - `split_data_support3.apk` (~0.5 GB)

   A single SAI bundle (`.apk` / `.apks` / `.xapk` holding those five) also works.
3. Put them in `ports/bmr/Gamefiles/`.
4. Restart EmulationStation (or refresh the games list) and launch
   **Hitman Blood Money Reprisal** from Ports.

The first launch shows an install screen with a progress bar. It takes several
minutes, builds the game (5.8 GB) and deletes the APKs as it goes. Then a
language picker appears, and the game starts.

**Free space:** about **3 GB in addition to the APKs** with the five loose
files, or about **6 GB in addition** with a single SAI bundle. The installer
checks first and refuses rather than failing part-way. If it is interrupted
(battery, power), it resumes on the next launch. Keep the remaining APKs in
`Gamefiles/` until it finishes.

## Requirements

- aarch64 Linux handheld with glibc 2.17+ (ArkOS / dArkOS family tested).
- **A Vulkan GPU driver that can drive the screen directly** (`VK_KHR_display`).
- Enough RAM: the game uses about 850 MB (tested on a 2 GB device).
- A landscape screen. Any resolution is picked up from the panel.
- Not supported yet: compositor-based firmware such as ROCKNIX (sway), and
  portrait-mounted panels.

## Controls

The engine sees an Xbox 360 controller and uses Feral's gamepad layout. The
front-end menus are a touch UI, and the touch screen works. Rumble works on
devices with a vibration motor.

| Button | Action |
|--------|--------|
| **SELECT + START** | Quit back to the frontend |

Profile-name keyboard: d-pad/stick move, **A** type, **B** delete, **X** space,
**Y** shift, **START** done (touch also works).

## Language

Pick it on the first launch: English, French, German, Spanish, Italian, Polish,
Russian or Japanese. To choose again, delete `ports/bmr/language.txt`. Speech
exists only in English, German and Spanish. The other languages get translated
text with English voices.

## Options

Edit the top of `Hitman Blood Money Reprisal.sh`:

| Variable | Default | Effect |
|----------|---------|--------|
| `BMR_MSAA` | `2` | Anti-aliasing: `0`, `2`, `4` or `8` |
| `BMR_NO_RUMBLE` | unset | `1` disables vibration |
| `BMR_NO_HOTKEY` | unset | `1` disables SELECT+START quit |
| `BMR_UI_SCALE` | `0.5` | Menu/HUD scale: `0.25`, `0.5`, `1` or `2` |
| `BMR_VK_ICD` | unset | Path of a Vulkan driver `.json` to force |
| `BMR_LANGUAGE` | `language.txt` | Game language as a locale, e.g. `de_DE` |

## Troubleshooting

Logs are in `ports/bmr/`: `bmr.log` (the last 10 runs are kept in `logs/`),
`install.log` and `launch-trace.log`. Please attach them when reporting an
issue, together with your device and firmware.

- **"needs a Vulkan driver" / "could not take over the screen with Vulkan"**:
  your device or firmware has no usable Vulkan display driver (see Device
  support above).
- **Installer refuses**: not enough free space, or an APK is missing or from a
  different game version (see `install.log`).

## Notes

- Offline only. The online update and specification checks are disabled.
- Hitman: Blood Money - Reprisal is © IO Interactive, Android version by Feral
  Interactive. This project is not affiliated with either.
- Third-party licences are in `bmr/licenses/` inside the zip.
