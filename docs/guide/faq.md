# Questions

**Is this a game I can download?**
No. It is a mod for Diablo II: Resurrected; you need your own copy of the game for PC (Battle.net or Steam).
Nothing of the game is in the mod: what you see in your hands is read from your own installation.

**What is the idea behind it?**
Immersion, with as few menus as possible. Your body is the interface: your weapons hang on you, your
inventory is a bag you hold, your potions are on your belt, your life and map are on your wrist, and your
skills ride your gestures. The game's menus stay for what has no gesture yet.

**Can I play online, on Battle.net?**
No. The mod is for offline single player. Everything that acts on the game works only in a local game of
one player, checked by the code; and loading third-party code into an online game can get an account
banned.

**Does it run on a standalone Quest?**
No. The game runs on your PC; the Quest shows it through Virtual Desktop, Meta Link or Air Link, or Steam
Link with SteamVR. Quest 3 with Virtual Desktop is what it is played with most.

**Which headsets?**
Any PC VR headset with an OpenXR runtime: Quest through Virtual Desktop or Meta Link, Valve Index, Steam
Frame and others through SteamVR, Pimax, Windows Mixed Reality. The controls screen at the start shows
your own controllers. Valve Index controllers have their own grip handling (`[index]`).

**Do I need natpoh's D2R VR, BodyWalk, FlatVR or ReShade?**
No. The mod carries natpoh's D2R VR engine inside its own plugin, talks to the headset through native
OpenXR, and draws the sky, the fog and the cave ceilings itself. If you have natpoh's D2R VR installed, the
launcher keeps it aside and lets you switch between the two.

**Do I need Python?**
No. The mod brings its own private Python for building the caches at install.

**Do I need Steam?**
Only if your runtime is SteamVR. The launcher starts the game itself; no Steam library entry is needed.

**Should I use my main character?**
Start a new offline character for your first sessions. The mod moves items with your hands through the
game's own functions; with a fresh hero nothing precious is at stake while you learn. Your saves are copied
at every start and after every save anyway, and the launcher's Backups page puts a copy back.

**Will it damage my characters?**
It is built not to: items move only offline, after your saves are copied, through the game's own
functions, each move read back. But no mod is free of bugs, and nothing can stop the game from saving a
mistake. Learn on a new character, and keep the backups.

**Can I play seated?**
Mostly. Room-scale only walks the hero when your head moves 15 cm or more, so leaning in a chair is safe,
and the left stick walks. The wheels' **EQUIPMENT** page draws and stows weapons, and the bag icon opens the
bag, without reaching behind you. Picking things off the floor is easier standing.

**Can I play left-handed?**
Not really yet. The layout assumes a right-handed player: the weapon and the bow string in the right hand,
spells in the left. The bag opens in whichever hand grabs it, and either hand draws from any holster place.

**What language is it in?**
The mod's own words in the headset follow the game's language: French when the game is in French, English
otherwise (`[interface] language`). The launcher has its own switch, English or French. This guide is in
English.

**The game updated and something stopped working.**
Each game function the mod uses is recognised by its bytes. If an update changed one, that feature turns
itself off and the log says which; the rest keeps working until the mod is updated.

**Can I go back to plain D2R VR, or to the flat game?**
Yes. Empty the holster of every character that used it, then switch the launcher to **D2R VR (natpoh)**, or
press **Uninstall**: the game folder goes back to what it was. See [Installing](install.md#uninstalling).

**Is it free?**
Yes, under the MIT licence, like the two projects it is built on. If you enjoy it, support natpoh, whose
engine it runs on, on [Patreon](https://www.patreon.com/c/d2vr).

**Who made it?**
ZVDiablo2VR is built on natpoh's [D2R VR](https://github.com/natpoh/diablo2-vr-port) (the engine) and on
bearstonem's [d2r-pcvr](https://github.com/bearstonem/d2r-pcvr) (the motion gameplay it started from). See
[CREDITS.md](../../CREDITS.md).
