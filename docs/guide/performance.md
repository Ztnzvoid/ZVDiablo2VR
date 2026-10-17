# Performance

VR needs two pictures a frame at the headset's rate (72 to 120 a second). Below that rate the runtime fills
in with guessed frames (Virtual Desktop's SSW, Meta's ASW), which wobble when you move your head. This page
is how to hold the rate.

## What costs the most

The **graphics card** does nearly all the work. The game draws each frame once, for the left eye, and the
right eye is replayed on the card from the same work (D2R VR's performance mode), so the processor is
rarely the limit. The card's cost follows **the size of each eye's picture**: roughly 1 ms a frame for every
million pixels of one eye, plus about 2 ms.

| Each eye | Pixels an eye | Seen on an RTX 4090 |
|---|---|---|
| about 1400 (the desktop window's own size) | 1.9 million | 90 pairs a second |
| 2000 x 2000 | 4 million | about 100 |
| 3000 x 3000 | 9 million | 50 |
| 4000 x 4000 | 16 million | about 30 |

A Quest 3's screen is 2064 x 2208 an eye: **2000 is about its own resolution**; 3000 and 4000 are
supersampling, sharper and much slower. On a 100 Hz headset even an RTX 4090 needs about 2000 a side to
hold the rate. A new install starts with a square picture of 2880 a side (what Virtual Desktop streams to a
Quest 3 at its "1.0"); pick a preset below to match your card.

## The launcher's graphics presets

The **Rendering** page's **Graphics presets** card sets in one click everything that costs the most: the
picture each eye gets, the mod's own load (`[performance] preset`) and the game's graphics options, with
what VR needs on top - no DLSS, no dynamic resolution, VSync off, no frame cap, resolution scale 100 %.

| Preset | Each eye | The game's options | Anti-aliasing | The mod's tier |
|---|---|---|---|---|
| Low | 1600 | Low, ambient occlusion off | FXAA | `low` |
| Medium | 2000 | Medium | FXAA | `medium` |
| High | 2600 | High | FXAA | `high` |
| Ultra | 4000 | Very High | SMAA | `ultra` |

The card shows each preset's cost in pixels, and **Custom** once you change a setting after it. Nothing is
written until you press **Save**, with the game closed.

## The mod's tier: `[performance] preset`

`preset = auto` (the default) reads your graphics card at the start and picks a tier; the log says which
(`Horadrim performance: ...`). A setting of its own in `horadrim.ini` always wins over the tier.

| Card | Tier |
|---|---|
| RTX 4080, 4090, 5080, 5090, 3090; RX 7900 | ultra |
| RTX 4070, 3080, 5070; RX 6800, 6900, 7800, 9070 | high |
| RTX 4060 Ti, 3070, 3060 Ti, 2070, 2080; RX 6700, 7700; Arc A770, B580 | medium |
| RTX 4060, 3060, 3050, 2060, 5060; GTX; RX 6600, 7600, 5700; Intel | low |
| A card not in the list | by its memory: 16 GB high, 10 GB medium, less low |

| | low | medium | high | ultra |
|---|---|---|---|---|
| Largest side of each eye | 1600 | 2000 | 2600 | as the window size asks (up to 4000) |
| Far grass | off | off | as set | as set |
| A character's speech | on the flat picture | in the room | in the room | in the room |
| Wrist map refresh | 5 a second | 10 a second | 25 a second | 25 a second |
| Ground read for picking up | 2 a second | 4 a second | 4 a second | 4 a second |

## On a smaller card, in this order

1. **A smaller picture**: a lower preset, or **Headset resolution per eye** on the Rendering page. 1600
   instead of 2000 draws a third fewer pixels.
2. **The game's own options**: shadows, ambient occlusion, light quality (the Rendering page).
3. **Fixed foveated rendering** (restart needed): the edges of the picture shaded at a lower rate. Off is
   the safe choice with Virtual Desktop.
4. **The draw distance**: past the full fog nothing is seen, so drawing beyond it is wasted.
5. Set your headset software's frame rate to a rate you can hold (90 rather than 100 or 120).

## The game's own video options

These are on the launcher's Rendering page (and in the game's Options > Video):

| Option | Set to | Why |
|---|---|---|
| VSync | **Off** | The headset paces the frames; VSync halves what each eye gets |
| NVIDIA DLSS | **Off** | Untested in VR: each eye would need its own history; the two pictures can shimmer apart |
| Anti-aliasing | FXAA (or SMAA), **not TAA** | TAA builds each frame from the ones before, which belong to the other eye: everything moving leaves a ghost |
| Frame rate cap | Off (0) | The headset paces the game |
| Resolution scale | 100 % | More multiplies the picture size above |
| Shadows, ambient occlusion, light quality | low to high by your card | Drawn for each eye: a cheap way to gain frames |

## Checking

The log, `<game folder>\d2rloader\logs\d2r-vr-frame.log`, writes one health line a minute
(`Horadrim health:` the pairs a second, the graphics card's and the processor's milliseconds a pair), and
says when the card falls under 30 pictures a second for 6 seconds. `[debug] diagnostics = on` adds the
detailed measuring lines; leave it off to play. A problem report carries these lines.

The technical breakdown of each part's cost is in
[docs/horadrim/PERFORMANCE.md](../horadrim/PERFORMANCE.md).
