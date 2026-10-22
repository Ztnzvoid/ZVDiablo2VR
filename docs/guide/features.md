# What the mod does

Each feature, how it behaves and the setting that changes it. Settings are in
`<game folder>\d2rloader\plugins\horadrim.ini` (most of them on the launcher's **Gameplay** page) unless
said otherwise; the file is read again within 2 seconds of a save, game running or not. The gestures
themselves, with pictures, are in [Controls and gestures](controls.md).

**The goal is immersion with as few menus as possible.** Every feature below exists so that you do with
your body what the game would ask you to do in a menu. Each one ships on by default and has its own off
switch.

**Some mechanics break the original game's rhythm - on purpose.** Diablo II was made for a mouse: you click
and the hero acts at once, at the game's tempo. In VR that tempo fights what players expect from a VR game:
presence, things done by hand, objects with weight. So in places the mod trades the click's rhythm for
physical play: a blow lands when your blade actually goes through a monster, and a heavy weapon you are
barely strong enough for follows your hand late; a spell goes where your arm points, further the more you
stretch it; pots and barrels break when you strike them; potions are taken from your belt and drunk at your
mouth; weapons are grabbed anywhere, passed from hand to hand, and fall to the ground when you let go.
These moments can feel slower, or simply different, than the original. That is a deliberate choice, made to
meet the immersion standards of VR games - not a bug. The game's own rules stay in charge (its damage, its
attack speed, its drops), and every one of these mechanics has its own off switch if you prefer to stay
closer to the original pace.

## The world in the headset

natpoh's D2R VR engine draws the game in stereo, in first person, through native OpenXR: your head is the
hero's head, your hands are his hands, holding what he holds. No BodyWalk, no FlatVR, no ReShade.

- **Sky, fog and caves.** Each act has a painted sky that follows the game's day and night; fog grows
  with distance so the world has depth; caves get a ceiling. All three are drawn inside the game's own
  frame, before its flames, glows and quest marks (`[render] world_fog = engine`, `reshade = off`), so a
  torch's flame stays solid against the fog.
- **Roofs kept indoors.** The game takes a roof away while your hero stands under it (it was made for the
  view from above). In first person the roof stays, drawn from both sides so the sky does not show through
  (`[render] roofs = keep`, `roofs_two_sided = under`; `roofs = game` if something looks wrong).
- **Lighting fixes** for VR: torch shadows that stay on the same torches when you turn your head, sun
  shadows that reach further, no dark rectangles next to a torch, no hard band across the floor in houses
  and caves, monsters that fade in and out instead of popping (`[render]`).
- **Weapons and potions lit by the game's light** - dark in a cave, warm by a fire, the scenery reflected
  in steel and glass (`[lighting]`). They are the game's own models, read from your installation.
- **The game's interface sized for VR**, the title and character screens laid out wide as on a monitor
  (`[render] vr_interface_size`, `wide_menus`), and Windows HDR handled (`force_sdr`).

## Moving

- **Room-scale.** Walk in your room and your hero walks with you, through the game's own walk (its walls,
  doors and paths). Below 15 cm you only lean; bending down is never a step. Walk your head into a wall and
  the view darkens until you step back (`[roomscale]`).
- **The left stick** walks; it always wins over your feet. The game's own run is its *Always run* option.
- **Turning** with the right stick: snap turns of 30 degrees by default, or smooth turning (the launcher's
  Gameplay page, **Turning**: style, snap angle, speed, invert; `[turn]` in `horadrim.ini`).
- **Height**: left grip + left stick click resets it. The body calibration (height and arm span) is asked
  at the first start; to do it again, set `version = 0` under `[calibration]` in `d2r_vr.ini`.

## Fighting

- **Melee by the blade.** A blow lands when the weapon's tip passes through a monster fast enough (2 m/s,
  the tip over 25 cm, the hand over 6 cm). Holding your arm out, moving slowly or shaking the hand never
  hits. Each monster is hit once a stroke. Blows follow the game's own attack speed for your class, weapon
  and Increased Attack Speed, with the game's breakpoints: you cannot out-swing the game (`[melee]`). Thrusts
  work: daggers, claws and throwing weapons need three quarters of the speed.
- **Weight and hit stop.** The weapon in your hand has weight: a dagger stays in your fist, a heavy weapon
  lags; two hands on the grip hold it steadier. A blow that lands stops the blade up to 120 ms and pushes
  it back a little (`[weight]`). Only what you see moves: the game reads your real controllers.
- **Vibration.** A blow vibrates by its speed, a kill at full strength, a blow you take in both hands
  (`[haptics] strength`).
- **Two weapons.** The left hand closing on a one-handed weapon at a hip takes it into the left hand; the
  left trigger then attacks with it. The game's rules stand: two weapons only for a Barbarian, or an
  Assassin with two claws.
- **The bow.** The game's own bow in your hand, its real string following your draw. The arrow comes from
  the quiver behind your right shoulder (`[bow] quiver`). The quiver goes on by itself when a bow is in hand
  and the other hand is empty: the holster's quiver, else the first one of the right kind in your inventory
  (`[bow] auto_quiver`). A shot the game refuses (in town, no arrows) is felt as a long weak buzz.
- **The crossbow.** The trigger shoots one bolt, the game's own attack at the game's pace. After each shot
  it must be cocked again by a flick down and back up (`[crossbow] cocking = flick`; `string`: the left
  hand pulls the string back to the right hand; `off`: the trigger held shoots at the game's pace). The left
  hand on the front of the stock aims along both hands (`two_hands_aim`); each shot kicks a little
  (`recoil`). A bow skill given to the trigger (Multiple Shot, Strafe, the elemental arrows) is one shot a
  cock, along the same line.
- **Throwing.** Javelins, throwing knives and axes leave your hand when you open it mid-swing, along the
  weapon (`[throw] aim = weapon`; `swing`: along your arm's motion; `gesture = trigger`: hold and release
  the trigger instead). They fly with the game's own throw, ammunition and damage.

## Skills and spells on your gestures

- **Your skills ride your gestures** (`[skills]`). Pick a weapon skill in a wheel and it goes to that
  weapon's gesture: Poison Javelin on every throw, Magic Arrow on every shot, Bash or Zeal on every blow
  that lands. Each gesture keeps its own (the bow's Magic Arrow waits while the sword swings). The wheel's
  middle gives the normal attack back. Two refusals in a row (no mana): that gesture attacks normally until
  your mana comes back.
- **Spells from your left hand** (`[spells]`). A spell given to the left hand leaves your right hand its
  weapon. A missile is thrown with the hand; a spell on the ground or a corpse is pointed, the hand raised
  and brought down; any skill is cast by the left trigger along the hand. `[spells] aim_ray = yes` shows a
  thin ray from the casting hand.
- **Every button holds a skill.** Your left trigger, X and Y, your right trigger and B: up to five skills,
  plus the weapon's own gestures. Held, a button repeats its skill at the game's pace.
- **Casting while walking.** Every skill casts while the left stick walks you. The game stands the hero
  for each cast (its rule); with a button held you cast, walk a little, cast again, as one continuous
  slowed walk (`[spells] while_moving`, `move_speed_while_casting = 0.6`). Two experimental options are
  off by default: `walk_through_cast = view` (your view keeps gliding while the hero stands) and
  `walk_after_cast = yes` (the spell leaves at the start of its animation and the hero walks on).
- **No auto-aim.** Missiles and area spells go along the hand; curses and corpse spells to the unit on
  the hand's line, else the nearest to it; weapon skills on the monster touched or the nearest within
  reach, in place. Your hero never walks to a target. No setting turns auto-aim on.

## Your body as inventory

- **The holster.** Both weapon sets and your shield hang on your body at four places: both hips and both
  sides of the upper back. A weapon put away is truly unequipped into a page of the mod's own, never the
  inventory, never the ground; drawing it equips it again. Shields hang on your back. See
  [The holster](holster.md).
- **The belt.** Your potions hang close round your waist, all drawn at one size (`[belt] distance_cm`,
  `potion_size_cm`, `spacing_cm`). Take one with the grip, bring it to your mouth and tip it: the game
  drinks it. Let an unused one go and it returns to the belt. A hand going down past the belt to the
  ground takes nothing.
- **The wrist** (`[wrist]`). Look at your left wrist: the side turned to your eyes shows. Its **back**,
  like a watch: a round map, the game's minimap (north up, or `map_orientation = player`). Its **inside**:
  three bands round the wrist like bracelets - life (red) nearest the hand, mana (blue), experience (gold,
  thinner) - with their values; life beats softly when it is low (`stats_style = orbs` for the old flat
  picture).

### Picking up by hand

Bring a low hand to an item on the ground (`[pickup] reach = 0.55` m away at most, the hand under
`height = 0.95` m) - the controller ticks - and squeeze the grip: the game's own model of that item comes
into your hand; turn it, look at it. Nothing is asked of the game yet. Where you let it go decides:

- **at your lower back** (the bag, left or right, from beside the hips down to the seat): the game picks
  it up into your inventory. Full: the game refuses, a long vibration, it stays on the ground;
- **inside the open 3D bag**: picked up, it lands where you let go;
- **at the belt**, a potion: into a column that takes it;
- **at a holster place**, a weapon: it hangs there;
- **anywhere else**: it never left the ground.

A weapon you grip that a free holster place can take is yours to fight with at once: it comes straight
into that hand. Bent over to the floor, an item goes into the bag only once your hand has carried it there
(`bent_body`). Gold is taken as soon as you touch it (`gold_on_touch`). The game's A button no longer picks
items up (`button_picks_up = no`). *Gravity gloves* - point at an item up to 2 m ahead and flick it into
your hand - exist but are off by default (`[gravity] enabled`).

### The 3D bag

Your inventory as a real leather bag, held in one hand while the other rummages (`[bag]`).

- **Open it**: reach behind your middle or lower back with an **empty** hand and squeeze the grip - that
  hand holds the bag. Or press the bag icon in a wheel: the hand that pressed it holds the bag.
- **Inside**: each item of your inventory as its own small 3D model, lying where you last put it (kept for
  each character; the game's own grid does not change). The brass studs on the front are the gauge: one
  lit for every 4 of the inventory's 40 cells used.
- **Rummage**: bring your other hand near an item, or point into the bag (a short ray): the item lights,
  with a light tick, and a **tooltip** beside it - its name in its quality's colour, count, durability,
  sockets, and what your hands can do with it (`pointer`, `tooltip`).
- **Take** it with the grip: it grows to its own size as it leaves the bag.
- **Put it back** anywhere inside: it lies where you let it go.
- **Throw it to the ground**: let go outside the bag - it falls, or flies on its arc if you throw it - and
  it is **dropped for real**; the game puts it at your feet (`drop`, `throw_to_aim`).
- **Wield** a weapon: take it out and squeeze that hand's trigger - it goes to a free holster place and is
  drawn into that hand, ready to fight. Let a weapon or shield go at a holster place: it hangs there.
- **Wear** armour or a jewel: let it go at its place on your body - a helm on top of the head, an amulet
  at the throat, a body armour at the chest, a belt at the front of the waist, boots low near the floor,
  gloves or a ring at the wrist of the hand holding the bag. What you wore there comes into the bag
  (`equip`).
- **Use** with the trigger, on a lit item or the one in your hand: a potion is drunk, a Town Portal scroll
  or tome opens a portal, a book is read, the Horadric Cube opens the game's Cube panel. An **Identify**
  scroll or tome is read, then point at an unidentified item (or hold one) and pull the trigger:
  *Identified!* (`use`). A potion, scroll or tome let go at your mouth is used too.
- **A ground item** brought near the open bag shrinks to its size in the bag, and within 15 cm of it goes
  in when you let go (a light tick says it will).
- **Full**: the bag shakes and the hand gets a long vibration; with `make_room = yes` the game's grid is
  rearranged first when the free cells would hold the item.
- **Put it away**: let go of the grip of the hand holding it (`let_go_closes`), bring that hand behind your
  back a moment, or press the icon again. The game's inventory, a menu or the hero's death close it.

Anything the game refuses (no room, its requirements, a menu open) comes back into the bag with a dull
vibration, and the log says why. Two things are not possible yet: a potion from the bag into the belt,
and a belt potion into the bag - the potion comes back. **Using items and identifying** wait, the first
time, for the game's own requests to be confirmed; until then they are refused and the log says how to
confirm them once (see [Troubleshooting](troubleshooting.md#the-3d-bag)).

## The wheels

Two wheels, one per hand, opened by a stick click and picked in by the other hand's laser: what you pick
goes to the pointing hand. The wheel lists what the weapon in your hand can use, then the spells, then what
is cast at once; more than eight skills turn over in pages. The footer holds the Holster page, the bag,
EQUIPMENT (draw or stow the weapons, the belt's potions) and the chat bubble. Its look: `[wheel] style =
tiles`, `plain` or `panel`. See [the two wheels](controls.md#the-two-wheels).

## The controls screen

At each start of the game, before its title screen, the headset shows the controls on three pages: the
controllers you hold (as the runtime presents them: Quest Touch, Valve Index, Vive wands, Windows MR; a
Steam Frame or a Pimax controller shows as the one the runtime emulates) with what each input does in your
layout, the places on your body, and the wheel. Push a stick left or right for the pages; any button or
trigger closes it, and the game gets nothing until you let go. Both stick clicks held together for a second
show it again. `[welcome] enabled = no`: not at the start; `every_start = no`: once, then again only when
the screen changes.

## Menus, dialogue and text

- **Panels in the room.** A panel opened in a game (inventory, stash, trade, character, skills) hangs in
  front of you as one screen, exactly as the game draws it, while the world goes on round you in stereo
  (`[render] panels_in_room`, `panels_width_m`, `panels_distance_m`, `panels_margin`). Use the right hand's
  laser like a mouse, or the game's own buttons.
- **Dialogue.** What a character says to you is shown in the game's own box hung in the room where you
  looked when it began: you stay in first person and see the one you talk to (`[dialogue] style = box`;
  `text`: the letters alone; `game`: the flat picture).
- **The keyboard** in the headset comes by itself when the game wants a hero's name; for the chat, press
  the speech bubble in a wheel (`[keyboard]`, `layout = qwerty` or `azerty`; `send = keys` if the game
  types nothing).
- **Language.** The mod's own words - the controls screen, the wheels, the Holster page, the bag's
  tooltip, the keyboard, the body calibration - follow the game's language: French when the game is in
  French, English otherwise (`[interface] language = auto`; `en` or `fr` forces one). The names the game
  gives (items, potions, skills) are always the game's own, in its language.
- **Monster bars**: `[interface] ordinary_monster_bars = no` hides ordinary monsters' names and health
  bars so a pack reads more easily; bosses, champions and uniques keep theirs.

## Safety

- **Offline only.** Everything that acts on the game (the holster, the bag, picking up, skills on
  gestures) checks in its code that the game is a local game of one player, and does nothing otherwise.
- **Fingerprints.** Every game function the mod calls is recognised by its bytes first. If a game update
  changed one, that feature switches itself off, the log says why, and the game goes on without it.
- **Save backups** at every start and after every save the game writes (the 20 newest kept). Nothing moves
  an item if the start's copy failed.
- **Every item move is read back.** A move the game refuses is only refused: the item stays where the game
  says it is, and the next try is a new one. Nothing is ever left on the cursor or dropped by mistake.
