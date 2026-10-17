# Provenance and third-party notices

ZVDiablo2VR is an independently developed mod that adds VR support and motion interactions to the
original Diablo II: Resurrected. It is not a standalone game: you must own and install your own
legitimate copy of the game.

No Blizzard game executables, models, textures, audio or other game assets are distributed in this
repository or in its release packages. Native artwork, weapon, quiver and potion models are read from
the player's own installation into local caches, which must not be redistributed. The mod includes
licensed open-source components and retains their notices below. [CREDITS.md](CREDITS.md) lists every
project we build on or learnt from.

## Lineage

ZVDiablo2VR starts from [bearstonem/d2r-pcvr](https://github.com/bearstonem/d2r-pcvr) (at
`0aeb66ce8fefb7337b4e7b073a4d201133402ea1`), itself an adaptation of
[natpoh/diablo2-vr-port](https://github.com/natpoh/diablo2-vr-port) (from
`10cfb0a2a9080184101794d3ac8c238c35717967`), moved onto natpoh's D2R VR 0.163 (`4b6284c`, native
OpenXR). All three are under the retained [MIT license](LICENSE), copyright 2026 BodyWalkVR; our own
additions are under the same license, copyright 2026 Ztnzvoid. The original sky art and every
attribution remain. BodyWalk and FlatVR are natpoh's separate products: this mod does not distribute
them or use them at run time. `external/bodywalk/` and `external/flatvr/` hold only the interface
headers natpoh's code is written against, as natpoh's public tree ships them (`game_link.h`: MIT,
Copyright (c) 2026 BodyWalkVR).

## Compiled into the plugin, or built with it

| Component | Source / version | Notice |
|---|---|---|
| MinHook | Vendored `third_party/minhook` | `third_party/minhook/LICENSE.txt`, BSD 2-clause |
| ReShade SDK headers | Vendored `external/reshade` | `external/reshade/LICENSE.md`, BSD 3-clause (ReShade itself is not used) |
| D2RLoader Plugin SDK headers | [D2RLoader/PluginSDK](https://github.com/D2RLoader/PluginSDK), `717f727a0ec52912d1558764345f8fa3453a2bd6` | `steamvr/licenses/D2RLoader-PluginSDK-MIT.txt` |
| OpenXR headers and Windows loader | [KhronosGroup/OpenXR-SDK](https://github.com/KhronosGroup/OpenXR-SDK), 1.1.62, `57af7fc61f9f2d492580cb28aab6d0ea59d8d417` | `steamvr/licenses/OpenXR-Apache-2.0.txt`, `OpenXR-MIT.txt` |
| JsonCpp (compiled into the OpenXR loader) | OpenXR SDK's vendored JsonCpp | `steamvr/licenses/JsonCpp.txt`, public domain / MIT |
| Native Windows C++/compiler runtime | LLVM-MinGW 20260616, Clang 22.1.8, static libc++/compiler-rt and winpthreads | `steamvr/licenses/LLVM-Apache-2.0-with-exceptions.txt`, `LLVM-MinGW-runtime.txt`, `winpthreads-MIT.txt` |
| MinGW runtime and GCC runtime notices | kept from d2r-pcvr's earlier MinGW-w64 / GCC 13 builds | `steamvr/licenses/MinGW-copyright.txt`, `GCC-runtime-copyright.txt`, `GPL-3.0.txt`; GCC Runtime Library Exception |

OpenXR loader copyright holders include The Khronos Group Inc. (2017-2026), Valve Corporation
(2017-2019) and LunarG, Inc. (2017-2019), with additional per-file notices in the linked SDK. The
Windows build wrapper adjusts build flags for MinGW; the loader's source is otherwise unchanged. D3D12
VRS enum and interface compatibility declarations follow Microsoft's
[DirectX-Headers](https://github.com/microsoft/DirectX-Headers) API definitions.

## In the release packages

The **mod package** (`tools/release/make_release.py`) carries, besides the plugin and our files:

- **CascLib** (`CascLib.dll`), used only at install to read a Battle.net game's own archives:
  [CascLib 3.0](https://github.com/ladislav-zezula/CascLib/tree/4971d363e665551ac4142f541e5f2d71f1cda653),
  MIT, copyright 2014 Ladislav Zezula, built from the pinned revision
  `4971d363e665551ac4142f541e5f2d71f1cda653`, fetched by that hash (never a branch or master), by
  `steamvr/build_casclib.ps1` with the repository's native Windows toolchain. Online storage and
  downloads are not enabled. Notice: [`steamvr/licenses/CascLib-MIT.txt`](steamvr/licenses/CascLib-MIT.txt).
- **CPython 3.12.10 x64 embeddable package** from [python.org](https://www.python.org/downloads/release/python-31210/),
  checked against its pinned SHA-256, for the install-time cache scripts; its PSF license ships beside
  it. It does not replace a system Python.
- **Microsoft Visual C++ 2015-2022 Redistributable (x64)** (`redist/vc_redist.x64.exe`, Microsoft
  Corporation), unmodified and signed by Microsoft, redistributed as Microsoft's Visual Studio license
  terms allow for this installer. D2RLoader's `D2RCore.dll` needs its runtime. The launcher runs it
  (`/install /quiet /norestart`, Windows asking for permission) only when Windows has no runtime or an
  older one; it is never copied into the game. Its own terms are Microsoft's:
  [Visual Studio license terms](https://visualstudio.microsoft.com/license-terms/),
  [`steamvr/licenses/Microsoft-VC-Redist.txt`](steamvr/licenses/Microsoft-VC-Redist.txt). Our own
  binaries (the plugin, CascLib, the converter, the launcher) link their C runtime statically and need
  no redistributable.
- The notices above (`LICENSE`, this file, `steamvr/licenses/`, MinHook's, ReShade SDK's).

The **launcher package** carries the launcher, its fonts' licenses (Cinzel, Copyright 2020 The Cinzel
Project Authors; Noto Sans, The Noto Project Authors; both SIL Open Font License 1.1,
`tools/launcher/assets/OFL-*.txt`) and the notices of its Rust dependencies (eframe/egui, reqwest with
rustls, zip, sha2, serde, image, windows-sys, winresource and their own dependencies, pinned in
`Cargo.lock`; each MIT and/or Apache 2.0), generated by `tools/release/rust_licenses.py`.

## Downloaded with the player's consent, never bundled

The launcher downloads **D2RLoader 1.3.1-beta** from [d2rloader.net](https://d2rloader.net/) when the
game has none, after the player agrees, and checks it against its pinned SHA-256. D2RLoader's terms
govern it.

## Read from the player's own game, never distributed

- The read-only Steam static-container/TVFS adapter in `steamvr/steam_assets.py` is adapted from
  [levinium/D2RExtractor](https://github.com/levinium/D2RExtractor) (MIT; its Steam reader credits
  rustydemon). Notice: [`steamvr/licenses/D2RExtractor-MIT.txt`](steamvr/licenses/D2RExtractor-MIT.txt).
  The local SpA1 v31 RGBA decoder and PNG writer use Python's standard library. Spell and item artwork
  belongs to the game; it is generated only in the player's local icon cache.
- The installation-only BitKnit decoder in `steamvr/vendor/bitknit.py` is vendored from
  [Rasetsuu/blendergranny](https://github.com/Rasetsuu/blendergranny) commit
  `aec91bbd8e244d82277d1f5435dc20feff3086f9`, MIT, copyright 2026 ciupix and contributors. Only its
  imports were adapted to run standalone; notice:
  [`steamvr/licenses/blendergranny-MIT.txt`](steamvr/licenses/blendergranny-MIT.txt). The local bounded
  Granny mesh adapter exports static potion geometry only. The texture header/format mapping was
  checked against [D2R-Reimagined's TextureReader](https://github.com/D2R-Reimagined/reimagined-level-editor/blob/master/src/D2RLevel.Assets/TextureReader.cs).
  Potion models and textures belong to the game and go only into the local `d2r_vr_potions` cache. No
  Granny runtime is needed.
- The weapon and quiver models drawn on the body are copied unchanged (their largest texture levels
  left out) by `steamvr/prepare_items.py` into the local `d2r_vr_items` cache and decoded in the plugin
  by `steamvr/item_assets.cpp`. Its BitKnit2 decoder, `steamvr/item_bitknit.cpp`, is ported from
  [pybg3](https://github.com/eiz/pybg3)'s `src/rans.h`, MIT, copyright 2024 Mackenzie Straight; the
  notice is kept in the source and in [`steamvr/licenses/pybg3-MIT.txt`](steamvr/licenses/pybg3-MIT.txt).

## Art

The wrist frame (`steamvr/assets/wrist-vitals.png`) is separately generated artwork; its attribution
is in [`steamvr/assets/README.md`](steamvr/assets/README.md). The skies in `reshade/sky/` are D2R VR's
generated pictures.

Diablo II: Resurrected, its executable, archives and save data belong to Blizzard Entertainment and
are not distributed. This project is not affiliated with or endorsed by Blizzard Entertainment, Valve,
Meta, Virtual Desktop, or the upstream authors.
