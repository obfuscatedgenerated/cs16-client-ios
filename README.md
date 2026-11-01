# CS16Client [![Build Status](https://github.com/Velaron/cs16-client/actions/workflows/build.yml/badge.svg)](https://github.com/Velaron/cs16-client/actions) <img align="right" width="128" height="128" src="https://github.com/Velaron/cs16-client/raw/main/android/app/src/main/ic_launcher-playstore.png" alt="CS16Client" />
Reverse-engineered Counter Strike 1.6 client, designed for mobile platforms and other officially non-supported platforms.

## Donate
[![Boosty.to](https://img.shields.io/badge/Boosty-F15F2C?logo=boosty&logoColor=fff&style=for-the-badge)](https://boosty.to/velaron)

[Support me](https://boosty.to/velaron) on Boosty.to, if you like my work and would like to support further development goals, like reverse-engineering other great mods.

Important contributors:
* [a1batross](https://github.com/a1batross), initial project creator and maintainer.
* [jeefo](https://github.com/jeefo), the creator of [YaPB](https://github.com/yapb/yapb).
* The people behind [ReGameDLL_CS](https://github.com/rehlds/ReGameDLL_CS) project.
* [Vladislav4KZ](https://github.com/Vladislav4KZ), bug-tester and maintainer.
* [SNMetamorph](https://github.com/SNMetamorph), author of the PSVita port.
* [Alprnn357](https://github.com/Alprnn357), touch menus maintainer.
* [wh1tesh1t](https://github.com/wh1tesh1t), [pwd491](https://github.com/pwd491), [Elinsrc](https://github.com/Elinsrc), [xiaodo1337](https://github.com/xiaodo1337), [nekonomicon](https://github.com/nekonomicon), [lewa-j](https://github.com/lewa-j) and others for minor contributions.

## Download
You can download a build at the `Releases` section, or use these links for common platforms:
* [Android](https://github.com/Velaron/cs16-client/releases/download/continuous/CS16Client-Android.apk)
* [Linux](https://github.com/Velaron/cs16-client/releases/download/continuous/CS16Client-Linux-i386.tar.gz)
* [Windows](https://github.com/Velaron/cs16-client/releases/download/continuous/CS16Client-Windows-X86.zip)
* [PS Vita](https://github.com/Velaron/cs16-client/releases/download/continuous/CS16Client-PSVita.zip)
* [macOS (arm64)](https://github.com/Velaron/cs16-client/releases/download/continuous/CS16Client-macOS-arm64.zip) - not tested
* [macOS (x86_64)](https://github.com/Velaron/cs16-client/releases/download/continuous/CS16Client-macOS-x86_64.zip) - not tested

[Other platforms...](https://github.com/Velaron/cs16-client/releases/tag/continuous)

## Installation
To run CS16Client you need the [latest developer build of Xash3D FWGS](https://github.com/FWGS/xash3d-fwgs/releases/tag/continuous).
You have to own the [game on Steam](https://store.steampowered.com/app/10/CounterStrike//) and copy `valve` and `cstrike` folders into your Xash3D FWGS directory.
After that, just install the APK and run.

## Configuration (CVars)
| CVar                     | Default       | Min | Max | Description                                                                                 |
|--------------------------|---------------|-----|-----|---------------------------------------------------------------------------------------------|
| hud_color                | "255 160 0"   | -   | -   | HUD color in RGB.                                                                           |
| cl_quakeguns             | 0             | 0   | 1   | Draw centered weapons.                                                                      |
| cl_weaponlag             | 0             | 0.0 | -   | Enable weapon lag/sway.                                                                     |
| xhair_additive           | 0             | 0   | 1   | Makes the crosshair additive.                                                               |
| xhair_color              | "0 255 0 255" | -   | -   | Crosshair's color (RGBA).                                                                   |
| xhair_dot                | 0             | 0   | 1   | Enables crosshair dot.                                                                      |
| xhair_dynamic_move       | 1             | 0   | 1   | Jumping, crouching and moving will affect the dynamic crosshair (like cl_dynamiccrosshair). |
| xhair_dynamic_scale      | 0             | 0   | -   | Scale of the dynamic crosshair movement.                                                    |
| xhair_gap_useweaponvalue | 0             | 0   | 1   | Makes the crosshair gap scale depend on the active weapon.                                  |
| xhair_enable             | 0             | 0   | 1   | Enables enhanced crosshair.                                                                 |
| xhair_gap                | 0             | 0   | 15  | Space between crosshair's lines.                                                            |
| xhair_pad                | 0             | 0   | -   | Border around crosshair.                                                                    |
| xhair_size               | 4             | 0   | -   | Crosshair size.                                                                             |
| xhair_t                  | 0             | 0   | 1   | Enables T-shaped crosshair.                                                                 |
| xhair_thick              | 0             | 0   | -   | Crosshair thickness.                                                                        |

## Building
Clone the source code:
```shell
git clone https://github.com/Velaron/cs16-client --recursive
```

### Using CMakePresets.json
```shell
cmake --preset <preset-name>
cmake --build build
cmake --install build --prefix <path-to-your-installation>
```

### Windows
```shell
cmake -A Win32 -S . -B build
cmake --build build --config Release
cmake --install build --prefix <path-to-your-installation>
```
### Linux and macOS
```shell
cmake -S . -B build
cmake --build build --config Release
cmake --install build --prefix <path-to-your-installation>
```
### Android
```shell
cd android
./gradlew assembleRelease
```

### iOS
The iOS build produces an arm64 `client_ios_arm64.dylib` and a matching
`client_ios_arm64.dylib.dSYM` for use by Xash3D FWGS. The dylib is
intentionally not signed by this project; the dSYM is only for symbolication
and must not be copied into the app.

The dSYM is included in the generated package under `dSYMs/`. Use the exact
dSYM from the same build as the dylib when symbolizing a crash.

If you use SideStore, add the unsigned dylib to the Xash app bundle at the
relative path configured by your Xash fork (normally
`cstrike/cl_dlls/client_ios_arm64.dylib`), then let SideStore sign the complete
IPA. SideStore's final signing pass can then sign the app and its nested dylib
with the same provisioning identity.

The standalone plugin build cannot replace signing the host app. A dylib
downloaded independently may still be distributed as a separate file, but it
must be inserted into the app before SideStore signs it; signing it afterward
does not update the app's signed bundle. Remove stale copies from writable
storage while testing so you know which signed bundle dylib is being loaded.

This project only provides symbols for the client dylib. The Xash executable
and any other bundled dylibs need matching dSYMs from the Xash build itself.

The `Crash: signal ...` text shown by Xash is not a full iOS crash dump, and
Xash does not load dSYMs at runtime. For the actual exception type, thread
stacks, and loaded-image UUIDs, collect the device crash report from Xcode's
Devices and Simulators window (or macOS Console), then symbolicate it with
the matching Xash and client dSYMs. The crash report must contain the client
dylib's UUID before its addresses can be resolved.
