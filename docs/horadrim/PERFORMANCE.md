# Performance in ZVDiablo2VR

*The player's version: [docs/guide/performance.md](../guide/performance.md).*

What each part costs, what to turn down on a smaller PC, and how to measure it. The floor: no build ships slower
than natpoh's D2R VR 0.163 in native OpenXR, measured with `tools/fakexr/bench.py` (same character, same place,
60 s).

## Where the frame goes

A pair of eyes is one game frame drawn once (the left eye), the right eye replayed on the GPU from the same
work (natpoh's `[stereo] replay_right=1`). With the replay the frame is the **graphics card's**: in the player's
sessions of 2026-10-13 (RTX 4090, 100 Hz, FP16 eyes) the game's thread waited ~10 ms a pair for the GPU
("replay steps: wait last pair (effects)") and our own CPU in natpoh's frame was 0.15 ms.

The GPU's cost follows the size the game draws each eye at - about **1 ms a pair for every million pixels of
one eye**, plus ~2 ms:

| size an eye ([openxr] window_size with `full_size_image`) | pixels an eye | pairs a second seen (RTX 4090) |
| --- | --- | --- |
| the window's own (natpoh alone, ~1350-1400) | 1.9 Mpx | 90 (the headset's rate) |
| 2000 x 2000 | 4.0 Mpx | ~100 expected (bench it) |
| 3000 x 3000 | 9.0 Mpx | 50 |
| 4000 x 4000 | 16 Mpx | ~30 |

A Quest 3's panel is 2064 x 2208 an eye: 2000 is about its own resolution; 3000 and 4000 are supersampling.

### Our per-frame costs

| what | thread | cost | scales with the size | can be cut |
| --- | --- | --- | --- | --- |
| the virtual client (`full_size_image`, `[performance] image_size`) | GPU | the table above | yes, squared | the preset caps it |
| the GPU guard | worker (4 Hz) | none | - | only reports unless `gpu_guard_cuts = yes` |
| the eyes' clamp (`clamp_submit`) | GPU, natpoh's eye copy | two full-screen blends an eye (`Frame GPU: clamp`) | yes | measured; keep (black squares) |
| the light probe, potions, items (`Frame GPU: ours`) | GPU | probe: one read of the eye at 128 x 128; models: a few draws | slightly | no |
| the effects (natpoh's D2R_DepthFog.fx + our flame, sky, far grass parts) (`Frame GPU: effects`) | GPU | one full-screen pass an eye | yes | far grass by the preset |
| `flame_near_fog`, `flame_over_sky`, `ui_over_sky` | GPU, in the effect | a few instructions a pixel | yes | keep (cheap) |
| `fog_before_transparents` (off) | GPU | two full-screen copies an eye when on | yes | off |
| `light_culling_fix` | GPU | a symmetric view draws a little more above | yes, a few % | keep (squares) |
| `light_bins_fix` | GPU | about 20 instructions a light a screen square in the game's light binning (640 squares); a light near the eye lit through more squares | no | keep (unlit rectangles near torches) |
| `vr_depth`, `particles_face_head` | render thread | a constant rewritten a pass | no | no |
| torch shadows, hero light, sun reach | game thread | slots chosen once a frame | no | no cost difference |
| monster fade | worker | none (the game's own fade lengthened) | no | - |
| grass edge fade (`grass_fade_band`) | GPU | a patched placement shader, same cost | no | - |
| grass window hook (`grass_follows_draw_distance`, off) | game thread | one hook call a frame | no | off |
| shadows survey, roofs survey, code dump | worker | memory reads every 10 s | no | **off** (measuring only) |
| roofs kept (`roofs = keep`) | client thread | one hook call a hero step (two atomics, the game's own call) | no | keep |
| roofs from below (`roofs_two_sided`) | GPU / game's pipeline creation | under or near a roof in first person: back faces of the world rasterised (the depth test drops most); each world pipeline made twice at the game's start (the log gives the ms) | no | `no`, or `under` rather than `always` |
| the replay pause (weapon change) | render thread | the right eye drawn by the game for 1.5 s | - | - |
| roomscale, haptics, the hands' weight | render thread | microseconds (`Horadrim feel: filter ~5 us a pose`) | no | - |
| pick-up: the ground read | game's UI thread | rooms walked 4 times a second | no | the preset (`pickup_scan_ms`) |
| holster | worker / UI thread | on a gesture only | no | - |
| wrist HUD and map | GPU | a 512 x 512 copy 25 times a second while shown | no | the preset (`map_refresh_ms`) |
| wheel, overlay, laser | GPU | quads in the runtime's layers | no | - |
| a dialogue in the room | GPU | the game's interface copied each frame while it speaks (a swapchain of the window's size) | yes | the preset (`dialogue_in_room`) |
| telemetry and logs | a buffered writer | `[debug] diagnostics = off` (default): a health line a minute, the measuring lines and hookbus's counters off (docs/horadrim/fps-audit.md) | no | `diagnostics = on` to measure |
| `horadrim.ini` getters | any | one atomic load (read again only when the file changes; the file is read outside the lock) | no | - |
| natpoh's ceiling torches (`[ceiling] torches=1`) | a scan thread | all the game's heap read after an area change and every 20 s, caves only | no | `torches=0` on weak PCs |

`Frame GPU: 10 s - effects L/R | ours L/R | clamp L/R | pair` in the log (`[performance] gpu_timers`) gives the GPU
milliseconds of each line marked GPU above, measured.

The FPS audit of 2026-10-14 (every change with no loss of quality, ranked, and what reaching 90 needs):
our frame-time audit.

## The 2026-10-13 lag

`full_size_image = yes` with `window_size = 4000` asked for 16 Mpx an eye, and the GPU guard then cut the
picture three times in a row (each cut rebuilds the game's picture: a 2.3 s frame, the sky and effects gone a
moment). The guard counted the presents during the rebuild itself (0 a second) as a slow GPU. Since 11f8806 it no
longer cuts by itself (`[render] gpu_guard_cuts = no`), and since this review it ignores 4 s after any size change
and any look under 8 presents a second (a load, a rebuild). The "present R 99.92 ms" of that session was one such
2.3 s rebuild averaged over 23 pairs.

## The black squares (headset only)

Two candidates, both tested by `tools/fakexr/bisect.py` (captures of both eyes with `--shots`):

1. **The replayed right eye and the game's tiled lights.** The replay folds the right eye's shift into its
   projection (`[stereo] replay_proj=3`, natpoh's default); the game's light culling rebuilds each 16-pixel tile's
   view rays from the projection's diagonal only and so bins the right eye's lights as if it stood at the left
   eye: near lights are missing at tile edges, in black squares, in the **right eye only** - which the desktop
   (the left eye) never shows. The shift is 0.24 world units: at 10 units from a torch that is 1.4 degrees, 3 tiles
   at 3000 x 3000, 1.5 bigger tiles at 1680. Test: close the left eye; bisect states `replay_proj 1` and `no replay`.
2. **Frame pacing.** At 25-50 pairs a second on a 100 Hz headset the runtime reprojects (Virtual Desktop's SSW):
   its motion blocks move fast with the head. Test: a size that holds the headset's rate (`size window`).

## Latency, from the gesture to what is seen

Every gesture is read once a frame (F: 20 ms at 50 pairs a second, 11 ms at 90), in natpoh's frame, inside the
game's draw. From there: the game's UI thread at its next update (at most F), its game thread at its next tick (at
most 40 ms, 25 a second), the game's own pad read at its next frame (F).

| feature | path | typical / worst at 90 | cut in this review |
| --- | --- | --- | --- |
| holster, drawn (visual) | the grip at the place, the model at once | 6 / 11 ms | - |
| holster, put away | a 0.45 s open-hand hold (deliberate) | 456 / 461 ms | - |
| holster, real | UI hop, game tick, UI hop, reply next frame | 48 / 96 ms | - |
| pick-up: in the hand | the same frame | 6 / 11 ms | - |
| pick-up: confirmed (haptic, next pick-up free) | the ground read again | was 178 / 357 ms | now about the server's tick + F |
| melee | 1 ms thread, game tick, haptic next frame | 37 / 74 ms | - |
| bow / throw | 1 ms thread, game tick; the arrow's model the next UI update | 26-38 / 52-75 ms | - |
| spells | the pad, the game's next read, its tick | 42 / 73 ms | - |
| wheel: select, haptic | the same frame | 6 / 11 ms | - |
| wheel: hover highlight | an atlas painted on a worker, 10 a second at most | was up to 100 ms + paint | at once when nothing is being painted |
| menu laser | the same frame; the game's click next frame | 17 / 22 ms | - |
| roomscale | a 250 ms delay outside the dead zone (deliberate), the stick a frame late | 292 / 323 ms | - |
| turn | the stick read by the game's pad poll, used at the next pair | 17 / 22 ms | - |
| haptics on our events | the same frame | 6 / 11 ms | - |
| haptics on damage | the game's health read every 200 ms | 111 / 222 ms | - |
| potion: drunk (bottle out of the hand) | confirmed by the 200 ms state read | was 398 / 534 ms | now about the server's tick + F |
| weapon set swap: confirmed | the same read | was 142 / 284 ms | idem |

Not done, for a session in the headset first (each touches natpoh's frame or changes what is seen):
- the turn from this frame's stick (TurnTick moved after natpoh's xrWaitFrame): one frame less;
- the room-scale stick given at the game's pad read instead of the next frame's pad: one frame less;
- the damage haptic from the health read each UI update: up to 200 ms less;
- the held arrow kept until its flight's model exists (40-80 ms with no arrow at release);
- a refused pick-up out of the hand before its 3 s window, once the game has had the target and two ticks passed.

## [performance] in horadrim.ini

`preset = auto | low | medium | high | ultra`. `auto` reads the graphics card once (the log says which tier it
took). Each key that says `preset` follows it; a value of its own wins.

| | low | medium | high | ultra |
| --- | --- | --- | --- | --- |
| `image_size` (most a side) | 1600 | 2000 | 2600 | as `window_size` asks (up to 4000) |
| far grass | off | off | as set | as set |
| far grass density | - | at most 0.6 | as set | as set |
| `dialogue_in_room` | no (flat picture) | yes | yes | yes |
| `map_refresh_ms` | 200 | 100 | 40 | 40 |
| `pickup_scan_ms` | 500 | 250 | 250 | 250 |
| flame and sky fixes, shadows, monster fade | as set | as set | as set | as set |

`auto`: RTX 4080/4090/5080/5090, 3090, RX 7900 -> ultra; RTX 4070/3080/5070, RX 6800/6900/7800/9070 -> high;
RTX 4060 Ti/3070/3060 Ti/2070/2080, RX 6700/7700, Arc A770/B580 -> medium; RTX 4060/3060/3050/2060/5060,
GTX, RX 6600/7600/5700, Intel -> low; a card the table does not know by its memory (16 GB high, 10 GB medium).

`ultra` changes nothing: every setting as written. On a 100 Hz headset even a 4090 needs about 2000 a side
(`image_size = 2000`) to hold the rate; bench it.

## natpoh's d2r_vr.ini for each tier (the launcher offers these; the plugin never writes d2r_vr.ini)

| d2r_vr.ini | low | medium | high | ultra | why |
| --- | --- | --- | --- | --- | --- |
| `[openxr] window_size` | 1600 | 2000 | 2600 | 3000-4000 | the GPU's cost, squared |
| `[stereo] replay_right` | 1 | 1 | 1 | 1 | one CPU pass for two eyes |
| `[stereo] afr` | 1 | 1 | 1 | 1 | |
| `[render] rings` | 2 | 3 | 4 | 4 | rooms built round the hero (CPU, draws) |
| `[render] model_radius` | fog end + 25 | fog end + 25 | fog end + 50 | fog end + 50 | past the full fog nothing is seen: 700 with a fog end of 250 draws for nothing |
| `[fog] start / end` | 30 / 150 | 30 / 200 | 30 / 250 | 30 / 250 | less drawn, less seen |
| `[fog] caves_end` | 150 | 200 | 200 | 200 | |
| `[render] fixed_foveation` (restart) | 1 | 1 | 0 | 0 | the periphery shaded at 2x2: fewer pixels shaded |
| `[ceiling] torches` / `monster_lights` | 0 / 0 | 0 / 0 | 1 / 0 | 1 / 1 | the torch scan reads the game's heap (caves) |

## D2R's own Settings.json (Options > Graphics)

| | low | medium | high / ultra |
| --- | --- | --- | --- |
| Resolution Scale | 100 | 100 | 100 (more multiplies the size above) |
| NVIDIA DLSS | Quality, once proven with the replay | idem | off or Quality |
| Shadow Quality | low | medium | high |
| Ambient Occlusion | off | low | as wanted |
| Light Quality / Vfx Lighting | low | medium | high |
| Atmospherics / Transparency | medium | high | high |
| Texture Quality | by the card's memory (6 GB: medium) | high | high |
| Dynamic Resolution Scaling | try it with Framerate Target = the headset's rate (untested in VR) | | off |
| VSync / Framerate Cap | off / 0 (the headset paces) | | |

## Measuring

```
python tools/fakexr/bench.py run natpoh-0163           # natpoh's d2rl-vrcam.dll in place, the game on FakeXR
python tools/fakexr/bench.py run ours                  # ours, same character, same place
python tools/fakexr/bench.py presets                   # low, medium, high, ultra back to back, live
python tools/fakexr/bench.py table
python tools/fakexr/bisect.py [--only size,no] [--shots DIR]   # each suspect switched live, 30 s each
```

Both scripts drive FakeXR only (the game must already run on it: `launch_test.ps1`, the HoradrimTest mod), put
`horadrim.ini` and `d2r_vr.ini` back as they were, and keep their results in `%TEMP%\horadrim-bench`.
