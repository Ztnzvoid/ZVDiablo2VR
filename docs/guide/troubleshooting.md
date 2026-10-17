# Troubleshooting

First, the log: `<game folder>\d2rloader\logs\d2r-vr-frame.log`. Every feature of the mod writes there what
it did and why it refused something.

## Send a report

The launcher's **Report a problem** (Play page, or About) gathers the logs, the last crash report, your
settings files, the game's video options and a description of your PC into one zip. Your Windows user name
is replaced by `%USERNAME%`; your characters, stash, keys and memory dumps are never included, and the list
of files is shown first.

1. Write in a few words what you were doing and what happened.
2. Press **Create the report and open GitHub**: the project's crash form opens in your browser with a
   summary, and Explorer shows the zip.
3. Add your headset and runtime, **drag the zip into the form**, and press **Submit**.

When the game the launcher started crashes or hangs, the launcher offers a report by itself.

![Report a problem](../../tools/launcher/screenshots/launcher-report-en.png)

Without the launcher, open the [bug form](https://github.com/Ztnzvoid/ZVDiablo2VR/issues/new?template=bug.yml)
and attach `d2r-vr-frame.log`. Never post saves, game files or account details. A security problem:
[SECURITY.md](../../SECURITY.md).

## Starting

| What you see | What to do |
|---|---|
| "D2R.exe found, but no D2RLoader.exe: install ZVDiablo2VR first" | Press **INSTALL** on the Play page ([Installing](install.md)) |
| The launcher does not find the game | Type your game folder's path under **Game folder**, or press **Detect** |
| "Nothing to install from yet" | No release reachable: put `ZVDiablo2VR-mod-<version>.zip` beside the launcher, or choose it under **Install details** |
| The D2RLoader download is blocked | An antivirus may flag mod loaders. Get D2RLoader from [d2rloader.net](https://d2rloader.net/) yourself, then **INSTALL** again |
| "Windows lacks the Microsoft Visual C++ runtime..." | **INSTALL** again and accept Windows' prompt, or **Download it from Microsoft…**. Restart Windows if asked |
| **PLAY** is greyed, or "The game is already running" | Close the game first |
| "Not started: ... is beside the game" | natpoh's plugin or ReShade came back (his installer or settings window). Press **Set them aside** on the Play page |
| A setting on the Rendering page is not saved | Close the game: those settings are saved only with the game closed |
| The game starts on the monitor, nothing in the headset | Start your headset's software before **PLAY** (Virtual Desktop: connect the headset first). Check **Headset runtime** on the Play page; pick another installed runtime if the default is wrong |
| The game was started from Battle.net or Steam and is flat | Start it from the launcher or its desktop shortcut |

## The picture

| What you see | What to do |
|---|---|
| The world wobbles or smears when you turn your head | The card does not hold the headset's rate. Pick a lower graphics preset ([Performance](performance.md)) |
| The two eyes do not match, or shimmer | In the game's video options (Rendering page): DLSS off, anti-aliasing FXAA (not TAA), VSync off |
| Black squares around some lights in one eye | A known issue with the square window. Setting `replay_right = 0` under `[stereo]` in `d2r_vr.ini` makes them go, at a cost in frame rate. Check that `[render] light_culling_fix`, `ui_over_sky` and `clamp_submit` are `yes` |
| Halos round smoke and some see-through effects | A known issue |
| No sky or fog, or flames look see-through | `[render] reshade = off` and `world_fog = engine` (the defaults). If the in-frame pass cannot be drawn, the log says why once a minute; send a report |
| The title or character screens look squeezed | `[render] wide_menus = yes` (the default) |
| The stash and the inventory overlap | `[render] vr_interface_size = auto` (the default) or a number below 100. Read at start: restart the game |
| A tab or a row of a panel is cut | Raise `[render] panels_margin` (60 by default) |
| A panel shows on the flat screen instead of in the room | `[render] panels_in_room = yes`; if the panels cannot be shown in the room, the mod falls back to the flat picture and the log says why |
| The menus look dark in the headset, Windows HDR on | `[render] force_sdr = yes` (the default), read at start |
| The picture changes or costs more than it should, with an OpenXR add-on installed for another game | Such add-ons load into every OpenXR game. Each one's `.json` names a variable that keeps it out: list those in `[render] xr_layers_off`, comma separated |
| No weapon, quiver or potion in your hands or on your body | The caches are missing. In the launcher, **Install details**, tick **Build the item and potion caches** and install again, game closed |
| The wrist's map is empty | Turn the game's minimap on: the wrist shows it |
| The wrist's bands sink into your arm or float beside it | `[wrist] stats_radius_cm` and `stats_offset_cm`, read while you play; `stats_debug = yes` shows the wrist's axes |
| The world's scale or your arms feel wrong | Calibrate again: `version = 0` under `[calibration]` in `d2r_vr.ini`, then start the game. Left grip + left stick click resets your height |

## Gestures

| What you see | What to do |
|---|---|
| Swings do not hit | A blow needs a deliberate stroke through the monster, the tip at 2 m/s. Lower `[melee] min_speed` if it is too hard. Swings pause while a menu is open, while you cast and while you hold a potion |
| The same monster is not hit twice | Each monster is hit once a stroke: swing back the other way, or pull the blade out |
| A weapon does not go back on your body | Keep the hand open about half a second, slowly. A fast hand strikes or throws. All four places taken: it stays in your hand |
| A dull pulse when you draw or put away a weapon | The game would not take that move (a two-handed weapon with something in the other hand, a shield with no free back place...). Nothing moved; the log says why. Try again |
| The holster stopped working for the session | Two items it lost track of switch it off until the next start: both hands vibrate and the log says where the items are (`Horadrim safety: real_holster failed`). Open a wheel's Holster page, or `horadrim holster status` |
| No arrow comes from the quiver | No quiver of arrows is worn; it is put on by itself when the other hand is empty and one is in the holster or the inventory (`[bow] auto_quiver`) |
| The arrow does not leave, a long weak buzz in both hands | The game refused the shot: in town, dead, or no arrows (the log says which) |
| The crossbow only gives a dull pulse | It is not cocked: flick it down and straight back up after each shot |
| A spell does not leave the left hand | The hand must be empty (grip open). A missile needs a fast throw (`[spells] throw_speed`); or use the left trigger |
| An item does not come into your hand | Lower your hand closer to it (within `[pickup] reach`, under `height`), then grip |
| An item let go falls back on the ground | Only the lower back (the bag), the belt (a potion with a column for it), a free holster place (a weapon) or the open 3D bag take it. Anywhere else it stays on the ground |
| A doesn't pick items up any more | Grip them instead. `[pickup] button_picks_up = yes` brings the button back |
| Valve Index: the hand takes things by itself, or never lets go | Raise `[index] squeeze` (a firmer squeeze needed), or lower `[index] release` |
| The keyboard types nothing in the game | `[keyboard] send = keys` |
| The wheel opens when you wanted the game's menu | Hold the stick click longer (`[controls] stick_long_press_ms`, 500 by default) |
| A feature stopped working after a game update | Its game code was not recognised: it switched itself off, and the log says which. Wait for an update of the mod |

## The 3D bag

| What you see | What to do |
|---|---|
| The bag does not open | Reach behind your middle or lower back with an **empty** hand. Or use the bag icon in a wheel. It does not open while a menu or the game's inventory is open |
| An item comes back into the bag with a dull vibration | The game refused it (no room, its requirements, a menu open, an item on the cursor); the log says why (`Horadrim bag: ... - not done: ...`) |
| The trigger on a potion or an Identify scroll is refused | The first time, the game's own requests must be confirmed. Set `[packet_log] enabled = yes`, then in the game's inventory right-click one potion, and right-click an Identify scroll then click an unidentified item. Once is enough: they are kept for the next sessions. Set `enabled = no` again |
| A potion let go at the belt comes back | Not possible yet (the game's request is not known); the log says so |
| The bag shakes, a long vibration | The inventory is full |

## Characters and saves

| What you see | What to do |
|---|---|
| A character does not load after uninstalling ("invalid inventory") | Its holster page still holds an item. Install the mod again, load the character offline, empty the holster ([The holster](holster.md#emptying-the-holster)), leave the game, then uninstall |
| An item is missing or doubled | Close the game. Your saves are copied at every start and after every save into `<game folder>\d2rloader\plugins\horadrim\backups\`; the launcher's **Backups** page restores everything, one character or the stash |
| Your hero died with weapons in the holster | The holster's page is kept through a death; the log says for each item where it is. Worn items are on the corpse, as in the game |
| Your interface size changed outside VR | The mod puts your size back when the game quits. If the game crashed, start it once and quit, or set it again in the game's options |
