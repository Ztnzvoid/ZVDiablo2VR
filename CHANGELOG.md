# What's new in ZVDiablo2VR

Newest first. natpoh's D2R VR history is [CHANGELOG-D2RVR.md](CHANGELOG-D2RVR.md); d2r-pcvr's is in
[its repository](https://github.com/bearstonem/d2r-pcvr).

## Unreleased - the first public release

The first public version of ZVDiablo2VR: natpoh's D2R VR 0.163 engine (native OpenXR only, the right
eye replayed), d2r-pcvr's gameplay running on it, and our own additions.

**Playing with your hands**

- Melee blows at the blade's speed and the game's own pace, with the weapon's weight, a hit stop and
  vibrations scaled by the blow.
- The game's own bow on every character, its real string following the draw; arrows taken from the
  quiver on your back. No quiver worn: no arrow.
- Javelins, throwing knives and axes thrown by opening the hand.
- Spells from the left hand: throw a missile, point and bring the hand down for a spell on the ground,
  or the left trigger. Skills ride the gestures (a weapon's skill on its blows, shots or throws).
- The holster: both weapon sets at four places on the body, learnt where you put them, shields on the
  back. A weapon put away is truly unequipped into a page of the mod's own through the game's local
  server, every move read back, never the inventory or the ground.
- The 3D bag: the inventory as a leather bag held in one hand, its items as small models; take, put
  back, throw to the ground, wield, wear, use (potions, scrolls, the Cube, an Identify scroll aimed at
  an item), a tooltip on the lit item; ground items shrink into it.
- The crossbow: shot by the trigger, cocked by a flick, aimed with both hands, a bow skill on its shot.
- Every skill cast while walking, slowed, at the game's own pace; two wheels, one per hand; a controls
  screen for every headset's controllers; the mod's words in the game's language (English, French).
- Picking items up by hand, the game's own model in the hand; into the bag at the lower back, the belt
  or a holster place.
- Belt potions close round the waist, drunk by hand.
- The wrist: a round map on its back; life, mana and experience as three bands on its inside.
- Room-scale walking, smooth or snap turning; dialogues and menus in the room;
  a keyboard in the headset; Valve Index finger tracking.

**The picture, without ReShade**

- The sky, the distance fog and the cave ceilings drawn inside the game's frame, before its flames and
  glows; the item labels and the map laid back by our own pass. ReShade is not needed.
- The weapons and potions lit by the game's own light; roofs kept above the hero; the game's height fog
  taken out of interiors and caves.
- The game's interface sized for VR; the game told its monitor is SDR in VR.

**The launcher**

- Installs everything on a PC that has only the game: D2RLoader (downloaded from its site with your
  consent), the plugin, its settings, its private Python, CascLib, the sky pictures, Microsoft's Visual
  C++ runtime when Windows lacks it; builds the caches from your own game; takes away old ReShade,
  BodyWalk and FlatVR files. Everything it replaces is backed up; Uninstall puts it back.
- Graphics presets Low / Medium / High / Ultra, the rendering and gameplay settings, save backups and
  their restore, a problem report in one click, English and French.

**Safety**

- Everything that acts on the game works in a local offline game of one player only, checked by the
  code; every game function is recognised by its byte fingerprint first; the saves are copied before
  any item moves.

Known issues: see the [README](README.md#known-issues).
