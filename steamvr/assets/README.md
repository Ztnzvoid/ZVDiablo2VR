# Wrist vitals artwork

`wrist-vitals.png` is new artwork generated with the built-in OpenAI image tool
on 2026-10-09. The style reference was the life/mana HUD in a local D2R gameplay
capture (`build-frame/dlss-artifacts-20261009-162519/dlss-off.png`). That screenshot
is development-only and is not distributed. The exact generation prompt is in
[`wrist-vitals-prompt.txt`](wrist-vitals-prompt.txt).

The source is a 1774 × 887 RGBA PNG with transparent surroundings. It is embedded
in the plugin and preview executable by `interaction_assets.rc`, then decoded
once with WIC at 512 × 256. No loose asset installation is required.

Both source orbs are full. `interaction_ui.cpp` darkens the drained portion of
each glass well from authoritative live life/mana values, retaining its glass
highlight and leaving the stone figures intact. Runtime text is drawn into the
empty nameplates. Unknown/stale vitals use empty wells and `-- / --`, never a
misleading full orb. The final atlas preserves the source alpha.

At the 512 × 256 runtime size the glass centers are `(147.8,125)` and `(364,125)`;
their radii are approximately `(57.5,56.5)`. If replacing the artwork, update
these masks and the nameplate rectangles in `interaction_ui.cpp` together.

Run `interaction-preview.exe <output.png> --wrist-check` to render full, partial,
empty and unavailable states and check fill/alpha/other-atlas-tile isolation.
The preview uses synthetic values and never opens game data.

## Wheel

The wheel has no artwork (HoradrimVR, 2026-10-13). The generated carved-stone
frame (`wheel-frame.png`, removed) was too ornate: filigree, eight spiked stars
and a heavy bronze ring around content that already has its own frames, two
footer buttons painted under three runtime buttons, and labels small enough to
cross the dividers. `interaction_ui.cpp` now paints the wheel itself: dark stone
with a faint grain, thin bronze rims and dividers, the game's icons as the only
colour; the slot pointed at gains a gold edge and a lighter face, the skill in
use a deep red mark on its rim (the centre's ring in weapon mode). Each half
says its held buttons once (Hold LT / Hold LT + Left Grip) and each slot its
key. Text is at least 22 atlas pixels (the wheel is 0.45 m: about 14 pixels a
degree at arm's length), system fonts only (Palatino Linotype, Segoe UI; the
game's Exocet for titles only if the player installed it in Windows).

`[wheel] style` in `horadrim.ini` picks the look: `tiles` (eight separate tiles,
the default, the player's choice on 2026-10-13), `plain` (one disc) or `panel`
(a square panel, as the game's). An unknown value is `tiles`. (An older file's
`[roue] style = tuiles | sobre | panneau` reads the same.)
The still part of each look is computed once and cached; a refresh repaints
only the cells pointed at or in use.

At 768 square, the interactive center is `(384,345.6)`. Segments start at the
top divider; their centers run clockwise from 22.5 degrees (upper right).
`WheelCell` is shared by highlights and ray selection, so a painted edge is a
hit-test edge. `interaction-preview.exe <output.png> --wheel-check <cache-dir>
[tiles|plain|panel]` renders both pages with synthetic assignments and
locally extracted icons (`--editor-check` the skill editor's two pages).

Native spell/item icons are **not** in this folder or in the release. Run
`steamvr/prepare_icons.py` against a legitimate local Steam installation to
create `d2rloader/plugins/d2r_vr_icons`. See INSTALL.md for the command.
