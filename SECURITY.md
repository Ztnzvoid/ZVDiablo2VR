# Security

## What this mod is, and is not

ZVDiablo2VR runs inside the game, through D2RLoader, and calls some of the game's own functions. It is
made for **offline single player only**:

- everything that acts on the game (moving items, the real holster, picking up, skills on gestures)
  checks in code that the game is a local game of one player with its local server, and does nothing
  otherwise;
- it is **not** for Battle.net. Do not inject it, or D2RLoader, into online games: Blizzard's terms do
  not allow third-party code there, and your account is your responsibility;
- reports or pull requests that aim at online play, at other players, or at cheating will be closed.

## What we care about

Please report privately anything that could hurt a player:

- a way for the mod to act in an online game despite its checks;
- loss or corruption of saves, or of items, that the save backups do not cover;
- the launcher installing something that is not the published, checksummed package (it accepts HTTPS
  only, checks every file against the release's SHA-256 list, and runs nothing it downloaded other than
  its own executable and the checked packages' Visual C++ redistributable);
- the launcher or the install-time scripts writing outside the game folder, the launcher's own folder
  or its data folder, or deleting the player's files;
- personal data in logs or problem reports that should not be there.

## How to report

Use GitHub's **private vulnerability reporting** on this repository (Security tab, "Report a
vulnerability"), or open an issue asking for a private contact without the details. Please give us a
reasonable time to fix it before telling anyone else. We will say when it is fixed and credit you if
you wish.

Only the latest release is supported.
