# Credits

ZVDiablo2VR stands on other people's work. This page says whose, under which license, and what we
use. The license texts themselves are in [LICENSE](LICENSE), [THIRD_PARTY.md](THIRD_PARTY.md),
`steamvr/licenses/`, `third_party/minhook/`, `external/reshade/` and `tools/launcher/assets/`.

Diablo II: Resurrected is Blizzard Entertainment's. This project is not affiliated with or endorsed by
Blizzard Entertainment, nor by the authors listed below. It ships none of the game's files.

## The projects we build on

| Project | Author | License | What we use |
|---|---|---|---|
| [D2R VR](https://github.com/natpoh/diablo2-vr-port) ([BodyWalkVR page](https://bodywalkvr.com/mods/d2r-vr)) | natpoh / BodyWalkVR | MIT, Copyright (c) 2026 BodyWalkVR | **The engine.** The D2RLoader plugin `d2rl-vrcam.dll`: the stereo camera, first person, native OpenXR (0.163), the replayed right eye, the painted skies, the fog and cave ceilings, the HUD panels, the weapon-weight (heft) model, the settings program. Most of `vr/`, `cleanroom/`, `shared/`, `reshade/`, `tools/settings/`, `d2r_vr.ini`. |
| [d2r-pcvr](https://github.com/bearstonem/d2r-pcvr) | bearstonem and contributors | MIT (the same LICENSE, kept unchanged) | **The gameplay base.** Motion melee, the physical bow, javelin throws, belt potions, the wrist display, the skill wheel, VR menus and laser, native panel controls, body calibration, foveated rendering, the potion renderer, the Windows tool-chain scripts, the cache scripts. Most of `steamvr/`. |
| [D2RLoader](https://d2rloader.net/) and its [Plugin SDK](https://github.com/D2RLoader/PluginSDK) | D2RLoader contributors | SDK: MIT. Loader: its own terms | The plugin host and its services. The loader is downloaded by the launcher from its official site, with the player's consent; it is never bundled. |
| [MinHook](https://github.com/TsudaKageyu/minhook) | Tsuda Kageyu | BSD 2-clause | Hooks of Windows functions, compiled into the plugin (`third_party/minhook`). |
| [OpenXR SDK](https://github.com/KhronosGroup/OpenXR-SDK) | The Khronos Group and contributors | Apache 2.0 (JsonCpp inside: MIT / public domain) | The OpenXR headers and loader, linked into the plugin. Fetched at build time. |
| [ReShade](https://reshade.me/) SDK headers | Patrick Mours (crosire) | BSD 3-clause | Compiled into the plugin (D2R VR's add-on interface, `external/reshade`). ReShade itself is not used by this mod. |
| [CascLib](https://github.com/ladislav-zezula/CascLib) | Ladislav Zezula | MIT | Reads a Battle.net game's own archives at install time, for the caches. Built from one pinned commit. |
| [D2RExtractor](https://github.com/levinium/D2RExtractor) | D2RExtractor contributors (levinium; Steam reader credits rustydemon) | MIT | The read-only Steam archive reader in `steamvr/steam_assets.py`, adapted by d2r-pcvr. |
| [blendergranny](https://github.com/Rasetsuu/blendergranny) | ciupix and contributors | MIT | The BitKnit decoder `steamvr/vendor/bitknit.py`, used at install to read potion models from the player's game. |
| [pybg3](https://github.com/eiz/pybg3) | Mackenzie Straight | MIT | Its `rans.h` BitKnit2 decoder, ported to C++ in `steamvr/item_bitknit.cpp` for the weapon and quiver models. |
| [LLVM-MinGW](https://github.com/mstorsjo/llvm-mingw) | Martin Storsjö and the LLVM project | Apache 2.0 with LLVM exceptions; runtime notices in `steamvr/licenses/` | The Windows compiler and its static runtime. Fetched at build time. |
| [CPython](https://www.python.org/) embeddable package | Python Software Foundation | PSF License | The private Python the install-time cache scripts run with; bundled in the mod package, checksum pinned. |
| Microsoft Visual C++ 2015-2022 Redistributable (x64) | Microsoft Corporation | Microsoft's terms | Bundled unmodified in the mod package; the launcher runs it only when Windows lacks the runtime D2RLoader needs. |
| [Cinzel](https://github.com/NDISCOVER/Cinzel), [Noto Sans](https://github.com/notofonts/latin-greek-cyrillic) | The Cinzel Project Authors; The Noto Project Authors | SIL Open Font License 1.1 | The launcher's title and text fonts (`tools/launcher/assets`, with their OFL texts). |
| [egui / eframe](https://github.com/emilk/egui) and the Rust crates in `tools/launcher/Cargo.lock` | Emil Ernerfeldt and contributors; each crate's authors | MIT or Apache 2.0 (each crate) | The launcher's window, HTTPS, zip and SHA-256. Their notices ship with the launcher (`tools/release/rust_licenses.py`). |

Thank you to natpoh for releasing D2R VR as open source and keeping it free, and to bearstonem for
d2r-pcvr's gameplay on top of it. To thank natpoh, see D2R VR's [Patreon](https://www.patreon.com/c/d2vr).
The name "D2R VR" is natpoh's and is not covered by the MIT license.

## Projects we learnt from (no code copied)

| Project | What we learnt |
|---|---|
| [RuffnecKk's D2RLoader plugins](https://github.com/RuffDood/RuffnecKk-D2RLoader-Suite) (MIT) | Where some of the game client's functions are, their prototypes and threads. We re-checked each one by its own byte fingerprint on our game build. |
| [MapAssist](https://github.com/OneXDeveloper/MapAssist) | Unit and room layouts in the game's memory, checked again on our build. |
| [emmericp/D2R-3D](https://github.com/emmericp/D2R-3D) | The idea of a free 3D camera in D2R, credited by D2R VR; neither project contains its code. |
| [D2R-Reimagined's TextureReader](https://github.com/D2R-Reimagined/reimagined-level-editor) | The game's texture header and formats, checked by d2r-pcvr. |
| [Microsoft DirectX-Headers](https://github.com/microsoft/DirectX-Headers) | D3D12 variable-rate-shading declarations follow its API definitions. |

## Built on the player's PC, never shared

The game's own art - item icons, weapon, quiver and potion models - is read at install time from the
player's own installation into local caches (`d2r_vr_icons`, `d2r_vr_items`, `d2r_vr_potions`). These
caches must never be shared.

## Art

- The skies (`reshade/sky/`) are D2R VR's, drawn with an image model from text prompts
  (`tools/gen_sky.py`, `tools/gen_night_sky.py`).
- The wrist frame (`steamvr/assets/wrist-vitals.png`) is d2r-pcvr's, generated; its prompt is kept
  beside it.
- The launcher's art (`tools/launcher/assets/art.jpg`) and its icon are the project owner's, made with
  an image model.
