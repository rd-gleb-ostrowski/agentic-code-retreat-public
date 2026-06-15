# Retro Arcade

*Flavor: a TUI game collection. Suggested stacks: any language that can draw and read keys in a
terminal.*

**Premise:** A retro arcade that lives in your terminal — a menu that launches a growing
collection of tiny classic games.

---

## T0 — the core

A terminal arcade with a launcher and one playable game (Snake).

**The launcher**
- On start, it shows a menu listing the available games (just Snake at first).
- The user moves a highlight through the list with the keyboard and presses a key to launch the
  selected game.
- When a game ends or the player leaves it, control returns to the menu.
- From the menu, a key quits the whole arcade and restores the terminal to normal.

**Snake (the first game)**
- A rectangular playfield is drawn in the terminal and refreshes on a steady tick.
- The snake starts at length 3 and moves one cell per tick in its current direction, continuing
  on its own.
- Arrow keys (or WASD) change direction; the snake cannot reverse directly back into itself.
- One piece of food sits on a random empty cell. Eating it grows the snake by one segment and
  increases the score.
- The game ends when the snake hits a wall or its own body; the final score is shown, then
  control returns to the launcher.

**Visual flair & sound (part of the core — make it feel like an arcade)**
- A colourful playfield: distinct colours for the snake's head, its body, the food, and the
  walls.
- A retro-styled title on the menu (ASCII-art header, highlighted selection).
- A satisfying *eat* effect — a brief flash or pop when food is eaten.
- A *game over* effect — a visible flourish (the snake flashes, a screen shake, or an animated
  "GAME OVER") before returning to the menu.
- Sound: audio cues (terminal beeps or real audio) for eating, scoring, and dying.
- Smooth, flicker-free redraws.

**It works when:**
- From the menu you can launch Snake, play it, die or quit, and land back in the menu.
- The snake moves continuously, steers, eats, grows, scores, and dies on wall or self collision.
- Eating and dying are visibly punctuated by effects and sound, and the whole thing is colourful
  rather than monochrome.
- Quitting from the menu leaves the terminal usable (no garbled state).

**Golden checks:**
- The snake starts at length 3 with score 0.
- After eating exactly one food: length 4 and a higher score.
- Driving into a wall ends the game and returns to the menu.

---

## Expansions

Self-contained packages to add on top of the core, in any order and combination.

### More games (each playable from the same launcher)

Every game here automatically includes the same bling and sound as the core — colour, effects,
and audio cues are expected, not optional.

- **Breakout** — a paddle at the bottom moves left and right; a ball bounces around the screen;
  a wall of bricks sits at the top. The ball bounces off the walls, the paddle, and bricks;
  hitting a brick destroys it and scores. Where the ball strikes the paddle changes its bounce
  angle. Clear all bricks to win the level; if the ball falls past the paddle you lose a life,
  and losing all lives ends the game. *Done when:* it's playable from the launcher. *Golden
  check: a brick disappears and the score rises when the ball hits it; letting the ball fall
  past the paddle costs a life.*
- **Tetris** — the seven tetromino shapes (I, O, T, S, Z, J, L) fall one at a time into a well
  10 wide by 20 tall. The player moves them left/right, rotates them, and drops them faster. A
  piece locks when it can't fall further; any completely filled rows clear and the rows above
  shift down. Clearing 1/2/3/4 rows at once scores 100/300/500/800. Pieces fall faster as the
  score climbs; the game ends when a new piece can't enter. *Done when:* it's playable from the
  launcher. *Golden check: filling a complete horizontal row clears it, shifts everything above
  down by one, and adds to the score.*
- **Space Invaders** — rows of alien invaders march side to side, dropping a step and reversing
  when they reach an edge, advancing toward the bottom. The player's cannon moves left/right and
  fires upward; hitting an invader destroys it and scores. Invaders occasionally fire back; a
  hit costs a life. Clear all invaders to win; if invaders reach the bottom or you lose all
  lives, the game ends. *Done when:* it's playable from the launcher. *Golden check: shooting an
  invader removes it and scores; the invaders speed up as fewer remain.*
- **Hunt the Wumpus** — a cave of 20 **numbered** rooms (1–20), each joined by tunnels to
  exactly 3 others (the classic dodecahedron map). The game always shows the player which room
  they're in and the numbers of the three rooms its tunnels lead to — e.g. *"You are in room 5.
  Tunnels lead to 4, 6 and 14."* The player roams the cave hunting a sleeping **Wumpus**. Two
  rooms hide bottomless pits (enter one and you fall to your death); two hold super-bats (enter
  either and they whisk you to a random room). When the player is in a room next to a hazard
  they get a warning before moving: *"I smell a Wumpus"* (Wumpus in an adjacent room), *"I feel
  a draft"* (pit adjacent), *"I hear bats"* (bats adjacent).
  **Moving:** enter the number of one of the three connected rooms to walk there.
  **Shooting:** the player starts with **5 crooked arrows**. To shoot, the player steers an
  arrow through the tunnels — select how many rooms it should travel, choose a connected room
  for it to enter, then from that room choose the next connected room, and so on, up to the
  chosen number of rooms deep (you pick room numbers, each must connect to the previous).
  If the arrow passes through the Wumpus's room, the player **wins**.
  If the player enters a cave number that is not connected to where the arrow is,
  the game picks a valid option at random. If the arrow hits the player while it is travelling,
  the player loses.
  **Startling the Wumpus:** the noise of a shot may wake it. After any shot that doesn't kill
  it, the Wumpus has a 3-in-4 chance to shamble into one of its adjacent rooms; if it moves into
  the player's room, it eats them.
  If the player enters the Wumpus room, the Wumpus will either move to another room or remain
  and kill the player. Unlike the player, the Wumpus is not affected by super bats or pits.
  The player **loses** by entering a pit, being eaten by the Wumpus, or running out of arrows.
  *Done when:* it's playable from the launcher. *Golden check: standing adjacent to the Wumpus
  prints the smell warning; an arrow steered into the Wumpus's room wins; entering a pit room
  ends the game.*

### Going deeper: Space Invaders

- **Boss battle** — after the regular waves are cleared, a large boss appears with its own
  health bar and attack patterns; defeating it clears the stage. *Done when:* a boss with a
  health bar can be fought and beaten. *Golden check: the boss takes multiple hits before dying,
  and the stage ends only when its health reaches zero.*
- **Ship variety** — several enemy types with different movement and fire behaviour, plus
  selectable player ships with different speeds and weapons. *Done when:* the player can choose
  among distinct ships and faces more than one enemy type.

### Arcade features

- **High scores** — persistent per-game leaderboards. *Done when:* a new best is recorded and
  survives a restart. *Golden check: beat the stored best and it updates; relaunch and it's
  still there.*
- **Pause** — pause and resume any game mid-play. *Done when:* a paused game freezes and resumes
  cleanly.
- **Difficulty & speed** — per-game settings that change the challenge. *Done when:* changing the
  setting visibly changes the game.
- **Achievements & profile** — a player profile that tracks achievements spanning all the games.
  Example achievements: *First Blood* (lose your first game), *Centurion* (score 100 in any
  game), *Gourmand* (eat 50 food across Snake runs), *Tetris!* (clear four rows at once),
  *Wumpus Slayer* (kill the Wumpus with your first arrow), *Arcade Rat* (play every game in one
  session). *Done when:* an achievement unlocks from in-game events and is shown in the profile.
- **Replays** — record a game and play it back. *Done when:* a recorded game replays identically.
  *Golden check: a replay reproduces the same run that was recorded.*
- **Two-player** — head-to-head or co-op modes. None of the games ship with one, so **inventing
  a two-player design for a single-player game is the whole point**: a second snake racing for
  food, split-well Tetris that sends garbage rows across, co-op invaders, or a duel in the
  Wumpus cave. *Done when:* at least one game has a working two-player mode.
