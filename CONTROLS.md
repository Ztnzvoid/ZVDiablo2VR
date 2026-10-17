# D2R PCVR controls

Windows preview for **SteamVR and Virtual Desktop (VDXR)**. These controls
use two tracked VR controllers; an Xbox controller is not required.

*The player's guide, with pictures of the controllers, the body and the gestures:
[docs/guide/controls.md](docs/guide/controls.md).*

## Button names

| Hand / button | Quest 2 / 3 label | Steam Frame label | Valve Index label |
| --- | --- | --- | --- |
| Right primary / secondary | A / B | A / B | A / B |
| Left primary / secondary | X / Y | A / B | A / B |
| Trigger | Index trigger | Index trigger | Trigger |
| Grip | Grip button | Grip input | Squeeze the handle (see below) |
| Stick click | Press the thumbstick | Press the thumbstick | Press the thumbstick |
| Menu | Left menu button | Controller menu button | None: right stick click in gameplay |

**Left primary** below means **Quest Left X / Frame or Index Left A**.
**Left secondary** means **Quest Left Y / Frame or Index Left B**.

### Valve Index controllers

The Index handle senses your fingers, so a hand resting around it already
reads as closed. With Index controllers the mod uses the grip like this:

- **Grab:** squeeze the handle. This covers a belt potion, a weapon at the hip
  or back, an item on the ground, and the weapon swap over the shoulder.
- **Hold:** keep your fingers around the handle. You do not have to keep
  squeezing.
- **Let go:** open your fingers. This puts the weapon back, throws, returns
  an unused potion, or drops or bags an item.
- **Grip as a modifier:** for Grip + stick click,
  the alternate quick-cast slots (classic layout), and Left Grip + Right Trigger or Right Grip
  in panels, squeeze while you press the other button. A relaxed hand does not
  count as holding the grip.
- **Game menu:** Index has no menu button, so **hold the right stick click** during
  gameplay (a short click is the wheel on the right hand; classic layout: the click). The left
  stick held opens the tabbed menu. In inventory, stash and other game panels the right
  stick click keeps its own role (hold it to sort).
- The squeeze force and finger opening can be tuned in `horadrim.ini`
  (`[index] serrer`, `lacher`).

## Gameplay

The default layout since 16/10/2026 (`[controls] layout = buttons` in `horadrim.ini`). In the game's
menus nothing changes: the sticks and buttons keep the game's own navigation (see *Menus* below).
**X / Y** are the left controller's buttons (Quest Left X / Y; Index and Steam Frame Left A / B).

| Control | In the world |
| --- | --- |
| Left stick | Walk |
| Right stick left / right | Snap turn |
| **Right stick click** (short) | Open / close a wheel on the **right** hand: point at it with the **left** hand - its picks go to the **left hand** (its trigger, X, Y) |
| **Left stick click** (short) | Open / close a wheel on the **left** hand: point at it with the **right** hand - its picks go to the **right hand** (its trigger, B) |
| **Either stick click held** (0.5 s, `[controls] stick_long_press_ms`) | The game's tabbed menu (inventory, character, skills, journal). Valve Index: the left stick; its right stick held is the game's menu (Esc) |
| Menu button (Quest left menu, Steam Frame menu) | The game's menu (Esc) |
| **Left trigger** | Casts the left hand's trigger skill, along the left hand |
| **X** | Casts the skill given to X, along the left hand |
| **Y** | Casts the skill given to Y, along the left hand |
| **Right trigger** | Casts the right hand's trigger skill, along the right hand; a crossbow shoots once cocked (below); at a bow's string: nock, draw, release to shoot |
| **A crossbow flicked down and straight back up** (the right hand, ~0.2 s) | Cocks it again after a shot: a click (`[crossbow] cocking`) |
| **B** | Casts the skill given to B, along the right hand |
| Right A | Interact / pick up / talk, aiming at the target |
| Left Grip + left stick click | Reset height (hold the grip first, then click: no wheel opens) |
| Grip near the belt / a holster / an item on the ground | Grab it; open the hand to let go (there is no cancel button). Bent over to the floor, the item stays in the hand: it goes into the bag only once the hand has carried it behind the back (`[pickup] bent_body`) |
| **Gravity gloves**: the hand pointed at an item on the ground up to 2 m ahead (a tick, the item shown lit above it), grip, flick the hand back | It flies into the hand, held as if picked up. Only items the game picks up where the hero stands (`[gravity] in_place_m`): the hero never walks. Same on every controller (Index: squeeze) |
| Left hand opened over a shoulder, a shield on the arm | The shield goes on your back (taken off for real, into the holster's page); grip there with either hand: back on the left arm. Opened anywhere else, the shield stays |
| Grip over a shoulder | Swap weapon sets I / II (`dominant_hand` in `d2r_vr.ini` `[interactions]`) |
| **Empty hand's grip at the middle / lower back** | The **3D bag** (below), held in the hand that grabbed it |
| A weapon through an enemy | Free melee swing / thrust |
| Looking at the back of the left wrist / its inside | The map / life, mana, experience |
| **Both stick clicks** held together 1 s | The controls screen again (see below) |

**A wheel open** (a stick's click; it stays open until a pick or another click; the other stick's
click switches to the other wheel). The wheel sits on the clicked stick's hand; the other hand points
at it, and what it picks goes to **that pointing hand** (16/10/2026: "the right hand's wheel is
selected with the left hand, so the skill goes to the left hand"):

| In a wheel | What it does |
| --- | --- |
| Point with the other hand's laser, press a **trigger** (either) | The skill goes to **the pointing hand's trigger**: a spell, or a weapon skill (it also rides its weapon's gesture: the blow, the shot, the throw). An aura, a warcry or an armour is cast at once. The wheel closes |
| Point, press **X** or **Y** (pointing with the left hand: the right stick's wheel) / **B** (pointing with the right hand: the left stick's wheel) | **That button holds the skill** (auras, warcries and armours too: the button casts them). The same skill again, or the wheel's middle: the button holds nothing. The wheel closes |
| Each cell's tag | The pointing hand's buttons holding it: **TRIGGER**, **X**, **Y**, **B** (a French game: **GACHETTE**) |
| The line under the wheel | The pointing hand's buttons and what each holds: `TRIGGER: ...  X: ...  Y: ...` (left) / `TRIGGER: ...  B: ...` (right) |
| The middle | The weapon's normal way again (picks for the left hand) / the right trigger's (picks for the right hand) |
| **EQUIPMENT** (bottom, the skills page) | Stow or draw the weapons, belt potions |
| Sheathed-sword icon (bottom left, `[holster] enabled`) | The holster page |
| Sack icon (bottom left) | The 3D bag, held in the hand that pressed the icon (pressed again: put away) |
| Speech bubble (bottom right) | The game's chat line and the headset keyboard |

EDIT SKILLS is no longer in the wheel (16/10/2026): with the buttons layout the eight controller slots are
lent by the mod itself; a slot is still set by hand in the game's own skills menu.

The same layout on every controller the mod reads (OpenXR's primary / secondary buttons, by hand):

| Control | Quest Touch (and Pimax, others on the Touch layout) | Valve Index, Steam Frame | Vive wands, Windows MR |
| --- | --- | --- | --- |
| A wheel | A stick's click | A stick's click | A trackpad's click |
| The game's tabbed menu | A stick held | The left stick held (Index's right stick held: the game's menu) | A trackpad held |
| Picks for the left hand | Point with the left hand: left trigger, X, Y | Left trigger, left A, left B | The triggers only |
| Picks for the right hand | Point with the right hand: right trigger, B | Right trigger, right B | The triggers only |
| The icons (holster, bag, chat) | Pointed at, either trigger | Pointed at, either trigger | Pointed at, either trigger |

Where a cast goes (no auto-aim): missiles and area spells along the hand; curses and corpse spells on
the unit on the hand's line, else the nearest to it; weapon skills on the monster touched or the nearest
within reach, in place. The hero never walks to a target. Held, a button repeats its skill at the
game's pace. Offline only.

Casting on the move: every skill casts while the left stick walks you, and you never stop: the game stands
the hero for each cast (its rule), but your view keeps walking along the stick, slowed to about 60 % of your
speed, a little ahead of him (75 cm at most), and he catches up when he walks on. A trigger or button held while
walking casts, walks, casts again: one continuous slowed walk. Let go of the stick and nothing moves
(`[spells] while_moving`, `move_speed_while_casting`, `walk_through_cast = view | off`, `cast_glide_max_cm`).
Teleport and weapon skills stay as they are. Experimental, off by default (`[spells] walk_after_cast = yes`): while the
stick walks you, a spell leaves at the start of its cast animation (`walk_after_cast_frame = 1`; 0: the game's own
moment) and your hero walks on right after it, instead of standing for the rest of the animation; your casts keep the game's pace (a spell pressed sooner than that is cast at
its turn, never dropped). A blow with a skill on it (Zeal, Sacrifice...) stops the weapon on the monster it meets.

Direct cast (`[skills] direct_cast = yes`, the default): a missile skill leaves the moment you release, along your
hand, and your hero walks on - no animation to stand through, as your bow's normal arrow. The bow and crossbow skills
(Magic, Fire, Cold, Exploding, Ice, Immolation, Freezing Arrow, Multiple Shot, Guided Arrow), the javelin skills
(Poison and Plague Javelin, Lightning Bolt, Lightning Fury) and the bolts and missiles (Fire Bolt, Ice Bolt, Charged
Bolt, Ice Blast, Fire Ball, Glacial Spike, Frozen Orb, Teeth, Bone Spear, Bone Spirit, Holy Bolt, Molten Boulder),
by the shot, the throw, a trigger or a button. The game's rules stay: its mana cost, your real skill level, an arrow
or a javelin used, its delays (Frozen Orb), nothing in town, and never faster than the animation would have been
(your FCR or IAS); a refusal is a dull pulse. Strafe, Lightning, Chain Lightning, Inferno, Teleport, the ground
spells, curses, summons, auras, warcries and blows keep their button, as do all skills while you are chilled,
slowed or shapeshifted. `direct_cast = no`: every skill by its button.

The game casts a skill only from one of its eight controller slots (B, X, Y, RB, and LT with each).
With this layout there are no quick casts, so every slot is lent: a skill given to a button is put on
a free slot by the game's own assignment, read back - **RB, Y, X, B** first, then **LT + RB, LT + Y,
LT + X, LT + B**. Five buttons and a weapon's two gestures fit the eight slots. The player never presses
these: our buttons press them.

Each character keeps his picks between games: the triggers, X, Y and B, and the skill on each of the
weapon's gestures (the blow, the shot, the bolt, the throw) are saved at each change in
`d2rloader\plugins\horadrim\binds\<character>.ini` and given back when that character enters a game -
the slots lent again as for a fresh pick. A skill he no longer has (an item taken off) is dropped. The
file is ours alone: the game's save is never touched.

What is gone with this layout: sprint on the left stick click (the game's own run stays; set *Always
run* in the game's options), the map on the stick (it is on the wrist), Right B as a cancel, holding
Left Y / Right B for the wheels, LT + a face button for the quick casts.

**The crossbow** (16/10/2026, `[crossbow]`): held like a gun in the right hand, the left hand may take the
front of the stock (its grip). The right trigger shoots one bolt, the game's own attack (its bolts, its damage,
its pace - a pull waits for the hero's last attack to end), along the right hand, or along the line between
your hands when the left one holds the stock (steadier). After each shot it is **un-cocked**: flick it down and
straight back up, quickly, like working a lever - a click, and a bolt lies in its groove again. Un-cocked, the
trigger gives only a dull pulse. Each shot kicks it up and back a little in your hand (the aim stays yours). A
bow skill given to the right trigger (Multiple Shot, Guided Arrow, Strafe, the elemental arrows...) is one shot
a cock the same way, along the same line. Drawn from your back, in a new game or after a load it is cocked.
No sight, no laser. `cocking = string`: the left hand pulls the string back to the right one instead; `off`:
the trigger held shoots at the game's pace, as before. The log says `Horadrim crossbow: ...`.

Javelins use the game's normal basic throw, ammunition and damage: hold the right trigger, throw,
release (or open the grip mid-throw, `[throw]`). Free swings pause during casting, menus and potion
handling. The belt shows potions in the game's belt slots even without an equipped belt. The wrist map
uses the game's corner minimap; it opens while you check your wrist and goes back when you lower it.
Calibrate height / arm span: asked at the first start (again: `version = 0` under `[calibration]` in
`d2r_vr.ini`). Recenter: PC F11. Save stereo images: PC F8. Settings: the launcher, or `horadrim.ini` /
`d2r_vr.ini`.

### The controls screen (`[welcome]`)

At each start of the game, before its title screen, the headset shows the controls on three pages: the
controllers you hold (as the runtime presents them: Quest Touch, Valve Index, Vive wands, WMR; a Steam
Frame or a Pimax controller shows as the one the runtime emulates) with what each input does in your
`[controls]` layout, the places on your body (the hips, the back, the bag at the lower back, the belt, the
mouth, the wrist) and the wheel. Push a stick left or right for the pages; any button or trigger closes it
(the game gets nothing until it is let go). In the game, both stick clicks held together a second show it
again. `[welcome] enabled = no`: not at the start; `every_start = no`: once, then when the screen changes.

**Our words follow the game's language** (`[interface] language = auto`, the default): the controls screen,
the wheel, the Holster page, the bag's tooltip, the keyboard and the body calibration are in French when the
game is in French (D2RLoader's `text_locale`, else your Battle.net language), in English for any other
language; `en` or `fr` forces one. The names the game gives (items, potions, skills) are always the game's own,
in its language: the belt's potions in the wheel read "Healing Potion", "Potion de vie"...

### Classic layout (`[controls] layout = classic`)

The layout before 16/10/2026, kept for comparison:

| Action | VR control |
| --- | --- |
| Tabbed game menu | Left primary (Quest Left X) |
| Left hand's wheel | Hold left secondary (Quest Left Y), with or without Left Grip; select with right laser + trigger |
| Right hand's wheel | Hold Right B; select with the left hand + left trigger |
| Left trigger / right trigger | The left hand's spell / the right hand's skill, as in the buttons layout |
| Cancel a grab / bow draw / javelin throw | Right B |
| Sprint | Hold the left stick click (`[move] sprint`) |
| Map | Quick tap of the left stick click |
| Quick casts | Left Trigger + a face button (below) |
| Index: game menu | Right stick click in the world |

## The 3D bag

Your inventory as a shallow leather satchel in your hand (`[bag]` in `horadrim.ini`), its items in one
layer near the rim. Offline only.

| Control | What it does |
| --- | --- |
| An **empty** hand reaches behind the **middle or lower back**, grip | The bag comes round, open, **in that hand** (the one that grabbed it); the other hand rummages. `[bag] hand` only when that hand is busy |
| The **bag icon** in a wheel | Opens it in the hand that pressed the icon, or puts it away |
| The bag hand brought behind the back a moment | Puts it away (the game's inventory, a menu or the hero's death too) |
| The other hand's fingers near an item in the bag | It lights (a light tick) |
| The other hand **points into the open bag** | A short ray from it (the menus' laser); the item it meets lights, a light tick (`[bag] pointer`). The ray only exists while the bag is open |
| An item lit | A small panel beside it: its name in its quality's colour, its count, durability, sockets, and what your hands can do with it (`[bag] tooltip`) |
| Grip on it | It is in your hand, growing to its own size as it leaves the bag (pointed at: it flies into your hand first) |
| **Trigger** on a lit potion, Town Portal scroll or tome, or book - or the **trigger of the hand holding one** taken from the bag | Used as the game's right click: drunk, the portal opened, read (`[bag] use`). An item in the hand stays there while the game uses it (a tome keeps its place in your hand, a charge less) |
| **Trigger** on the Horadric Cube (lit or in the hand) | The game's Cube panel opens, as its right click does (the bag is put away to show it) |
| **Trigger** on an Identify scroll or tome (lit or in the hand) | Read: the next trigger identifies. It goes back into the bag, the hand is free; point at an unidentified item (or hold one) and **pull the trigger**: identified by the game (the tooltip says "Identified!", two short pulses). The scroll's trigger again puts it away (30 s at most; the bag put away too) |
| **Trigger held 1 s** on the Token of Absolution (lit or in the hand) | Used, as its right click does: every skill and stat point forgotten. Its tooltip says so in red; let go before 1 s (or move off it) and nothing happens |
| **Trigger** on anything else | A dull vibration, nothing happens (the log says why) |
| Let go **inside** the bag | It lies where you let it go - the game's grid does not change |
| Let go **outside** the bag | It falls, or flies on its arc if you throw it, and is **dropped on the ground for real** (`[bag] drop`). The game puts it at your feet: its own drop can place it nowhere else (the drawn throw lands where you aimed, then the game's item lies at your feet) |
| A weapon or a shield let go at a **holster place** | Hung there (a one-hander at a hip or the back; bows, two-handers, javelins and shields on the back) |
| A weapon held out of the bag, **squeeze that hand's trigger** | It goes to a free holster place and is drawn into that hand, ready to fight with (`[bag] equip`) |
| Armour or a jewel let go at **its place on your body** | Worn (`[bag] equip`): a helm on top of the head, an amulet at the throat, a body armour at the chest, a belt at the front of the waist, boots low near the floor, gloves or a ring at the hand holding the bag (anywhere from its wrist to its fingers; a ring goes on **that** hand: open the bag with the other hand for the other ring). What you wore there comes into the bag. The item's panel says where it is worn ("Worn: let go on your head"); held there, the item glows, a brass stud marks the place and a light tick says it |
| Your **empty** rummaging hand's **grip on your body** where something is worn, the bag open | Taken off into the bag, **in that hand** while you keep squeezing (`[bag] equip`): the top of the head, the throat, the chest, the front of the waist, your feet, the bag hand's fingers (a ring) or wrist (gloves). A light tick and a lit stud say a worn item is under the hand. Not the belt where its potions hang (that grip takes a potion). Weapons and shields: the holster's places, as before |
| An item let go **on the Horadric Cube** in the bag | Into the Cube, at its first free place (`[bag] cube`); no room there: it stays in the bag |
| The **Cube held** out of the bag and **turned over** (the controller's top down) a moment | Emptied into the bag: every item in it into the inventory, or none if they do not all fit (`[bag] cube`). Transmuting: the game's Cube panel (trigger on the Cube) |
| The **brass button** on the bag's front (right of the gauge): touch it, or point at it and pull the trigger | **Sort** (`[bag] sort_button`): the game's grid sorted - the biggest first, by kind (weapons and armour, charms, gems, runes and jewels, potions, scrolls, tomes and keys, quest items and the Cube), packed with no hole, one move (all or nothing, nothing leaves the inventory) - and every item laid flat at its cells' place in the bag. Not while an item is in a hand or on its way, on the game's cursor, or a menu is open |
| A potion let go at the **belt** | Into that column (`[bag] belt`) - not possible yet: the game's request is not known; it comes back into the bag and the log says so |
| A **weapon in your hand** let go inside the open bag | Into the inventory (through a free holster place) |
| A belt potion let go inside the open bag | Into the inventory - not possible yet (the same reason): it goes back to the belt |
| Let go at the lower back | It stays in the bag |
| Let go at the mouth | A potion, Town Portal scroll or tome, or book: used the same way (it hangs at your mouth while the game uses it); anything else comes back |
| An item from the ground let go **inside the open bag** | The game picks it up; it lies where you let it go |

Anything the game refuses (no room, its requirements, a menu open, an item on the cursor) comes back into
the bag with a dull vibration; the log says why (`Horadrim bag: ... - not done: ...`). The use (trigger,
mouth) and the identify send the game's own request, as its right click in the inventory does (offline
games only). The item passes
through the holster's page on its way (a free spot there is needed for a moment; nothing ever stays
there, nothing is ever left on the cursor). `[bag] drop = no`: a let-go outside the bag comes back as
before; `throw_to_aim = no`: it falls straight down.

Each inventory item is drawn as its own 3D model, shrunk to its cells, where you last put it - kept for
each character in `d2rloader\plugins\horadrim\bag\<character>.txt` (the game's save is never touched).
The brass studs on its front are the gauge: a lit one for every 4 of the inventory's 40 cells used.
Full (the game refuses a pick-up for room): with `[bag] make_room = yes` the game's grid is rearranged
first when the free cells would hold the item (one move, all or nothing, nothing leaves the inventory),
then the item asked again; else the bag shakes and the hand gets a long vibration. The log says
`Horadrim bag: ...` for each of these.

## Quick-cast shortcuts (classic layout)

Hold **Left Trigger**, aim the right hand, then press the assigned face button.
Add **Left Grip** for slots 5–8. Assign the eight slots in the game's own skills
menu (EDIT SKILLS is no longer in the wheel); with `[skills] enabled = no` the wheel
shows each slot's VR shortcut. Release the face button before changing
slots or the grip modifier.

| Wheel slot | Quest shortcut | Steam Frame shortcut |
| --- | --- | --- |
| 1 | Left Trigger + Right A | Left Trigger + Right A |
| 2 | Left Trigger + Right B | Left Trigger + Right B |
| 3 | Left Trigger + Left X | Left Trigger + Left A |
| 4 | Left Trigger + Left Y | Left Trigger + Left B |
| 5 | Left Trigger + Left Grip + Right A | Left Trigger + Left Grip + Right A |
| 6 | Left Trigger + Left Grip + Right B | Left Trigger + Left Grip + Right B |
| 7 | Left Trigger + Left Grip + Left X | Left Trigger + Left Grip + Left A |
| 8 | Left Trigger + Left Grip + Left Y | Left Trigger + Left Grip + Left B |

## Menus: laser and native buttons

Both methods work in the main menu and native game panels, including inventory,
stash and merchants. Keep the D2R window focused on the PC.

Use a **stick or face button** to start native button navigation and follow the
game's displayed prompts. The idle laser will not move your native selection.
To return to the laser, release the native controls and deliberately move your
aim across the panel. A small hand tremor will not change methods.

### Laser controls

| Action | VR control |
| --- | --- |
| Hover / point | Aim the right controller's laser |
| Select / drag an item | Right trigger; hold while moving the item and release to place it |
| Context / alternate click | Left Grip + Right Trigger (hold grip first) |
| Use an item (Town Portal or Identify scroll, tome, potion) | Point at it and quickly tap **Left Trigger**: the game's right click there (`[menus] use_button` in `horadrim.ini`) |
| Native Ctrl-click shortcut | Hold Left Trigger, then click with Right Trigger; the game chooses drop, sell or transfer for the current panel (a quick tap alone uses the item instead) |
| Native Shift modifier | Hold Right Grip while using the laser |
| Back / close | Right B, or point and click the panel's close/back button |
| Tabs / page controls | Point and click the native on-screen controls |

Dragging keeps the item held if the ray briefly leaves the panel. Releasing
the trigger ends the drag at the last valid pointer position. Tracking or
desktop focus loss releases the injected mouse button; release the trigger
before starting again. Pressing or releasing Left Grip during a drag will
not convert it into a context-click.

### Native menu prompts

| Game's displayed input | Quest control | Steam Frame control |
| --- | --- | --- |
| A | Right A | Right A |
| B / back | Right B | Right B |
| X | Left X | Left A |
| Y | Left Y | Left B |
| Left stick / right stick | Left stick / right stick | Left stick / right stick |
| LS / RS click | Left stick click / right stick click | Left stick click / right stick click |
| Inventory: X / drop selected item | Left X; hold if the native prompt requires it | Left A; hold if the native prompt requires it |
| Inventory: hold RS / sort | Press and hold right stick click | Press and hold right stick click |
| Inventory: hold A / use the selected item | Hold Right A | Hold Right A |
| LB / RB | Left Grip / Right Grip | Left Grip / Right Grip |
| LT / RT | Left Trigger / Right Trigger | Left Trigger / Right Trigger |
| Menu / Start, where available to the game | Controller menu button | Controller menu button (Index: none in panels; right stick click opens the game menu in gameplay) |

Native menu actions use the same buttons in the main menu, tabbed menu, stash,
inventory and merchant panels. **A stick click held opens the tabbed menu during
gameplay (classic layout: left primary); inside a native menu every button performs
the displayed action** (X: the displayed X action, B: back).
Right-stick click does not swap weapons during gameplay. Use the shoulder
gesture or the wheel's **EQUIPMENT** page for weapon configurations.

Quest controllers do not need a separate D-pad or Xbox controller: use sticks
for native navigation and the laser for the on-screen controls. When using
the laser, Right Trigger is a mouse click and the grips/triggers above provide
its modifiers; once native navigation is selected, they perform LB/RB/LT/RT.
Release buttons, triggers and sticks when opening or closing menus so a held
input cannot also act in the next screen or in gameplay.

The mod's body calibration panel uses its VR laser controls:
right laser + trigger to select, Right B to close/cancel. Native gamepad input
does not pass through that panel.
