# Game of Life, pimped

*Flavor: algorithmic / visual. Suggested stacks: any — Python, JS/TS, Rust, Go.*

**Premise:** Build Conway's Game of Life, then make it unmistakably your own.

---

## What the Game of Life is

The Game of Life is a *cellular automaton* invented by John Conway. It is not a game you play;
it is a simulation that evolves on its own from a starting pattern. The world is a grid of
**cells**, each either **alive** or **dead**. Time advances in discrete steps called
**generations**. Each generation, every cell is born, survives, or dies based on how many of
its neighbours are alive. Simple rules produce surprisingly lifelike behaviour: gliders that
crawl across the grid, oscillators that blink forever, and still lifes that never change.

## How the world works

- **Grid:** a rectangular field of cells, some width by some height.
- **Coordinates** (only so the examples below are unambiguous): `(row, col)`, with `row 0` at
  the top and `col 0` at the left, so `(0, 0)` is the top-left cell.
- **Neighbours:** each cell has eight neighbours — the cells touching it horizontally,
  vertically, and diagonally.
- **Wrapping (required from the start):** the grid wraps around like a torus. Going off the
  right edge brings you back on the left; going off the top brings you back on the bottom.
  Because of this, *every* cell has eight neighbours, even cells on an edge — the missing ones
  come from the opposite side.

## The rules

Each generation, every cell counts its live neighbours (0–8) and then:

1. A **live** cell with **2 or 3** live neighbours stays alive. With fewer than 2 it dies (as
   if from loneliness); with more than 3 it dies (as if from overcrowding).
2. A **dead** cell with **exactly 3** live neighbours becomes alive.
3. Otherwise the cell is dead next generation.

All cells change **together**, based on the state at the start of the generation — a cell being
born or dying does not affect its neighbours until the next generation.

---

## T0 — the core

A running Conway's Game of Life on a wrapping grid.

**It works when:**
- The grid has a configurable width and height, and a starting pattern can be loaded.
- It runs continuously, advancing generation after generation, applying the rules above with
  every cell changing together.
- Edges wrap, so patterns that run off one side reappear on the other.
- The user can watch it evolve (a simple text view of the grid is enough).

**Golden examples** (`.` = dead, `#` = live; rows top-to-bottom). These sit away from the edges,
so wrapping doesn't affect them — use them to check your rules:

Blinker (oscillator, period 2) on a 5×5 grid:

```
generation 0       generation 1       generation 2
.....              .....              .....
.....              ..#..              .....
.###.      →       ..#..      →       .###.
.....              ..#..              .....
.....              .....              .....
```

Block (still life) — never changes:

```
....
.##.
.##.
....
```

Glider — after 4 generations the same shape reappears, shifted by one row down and one column
right:

```
generation 0       generation 4
.#....             ......
..#...             ..#...
###...      →      ...#..
......             .###..
......             ......
......             ......
```

Wrapping check: a vertical blinker straddling the top/bottom edge of a 5×5 grid — live cells at
`(4,2)`, `(0,2)`, `(1,2)` — becomes a horizontal blinker along row 0 after one generation:
`(0,1)`, `(0,2)`, `(0,3)`.

## Starting patterns (live cells; everything else dead)

- **Blinker:** `(2,1) (2,2) (2,3)`
- **Block:** `(1,1) (1,2) (2,1) (2,2)`
- **Glider:** `(0,1) (1,2) (2,0) (2,1) (2,2)`

---

## Expansions

Self-contained packages to add on top of the core, in any order and combination.

- **Controls** — pause and resume, single-step one generation at a time, and adjust the speed.
  *Done when:* the user can pause, step, and speed the simulation up or down.
- **Pattern editor** — draw your own starting pattern by toggling cells on and off. *Done when:*
  a hand-drawn pattern can be set running.
- **Save & load** — store patterns and reload them later, using **RLE** (Run Length Encoded),
  the standard Game of Life pattern format (so patterns are shareable with other Life tools).
  RLE works like this:
  - Lines starting with `#` are comments (e.g. `#N name`, `#C a remark`) and may be ignored.
  - A header line gives the pattern's bounding box and rule: `x = 3, y = 3, rule = B3/S23`.
  - The pattern is a run of items. Each item is an optional number (a repeat count, default 1)
    followed by a tag: `b` = dead cell, `o` = live cell, `$` = end of row. A `!` ends the
    pattern. Trailing dead cells in a row may be omitted, and `$` may carry a count for several
    empty rows. Whitespace and line breaks in the data are ignored.

  For example, a glider:
  ```
  x = 3, y = 3, rule = B3/S23
  bob$2bo$3o!
  ```
  *Done when:* a pattern survives being saved to RLE and reloaded and runs identically. *Golden
  example: load the glider RLE above, run it 20 generations, and it has moved 5 cells down and 5
  cells right, intact.*
- **Pattern library** — a built-in catalogue of famous patterns (glider gun, pulsar, spaceship,
  …) to drop in. *Done when:* the user can pick a pattern from a library.
- **Alternative rule sets** — let the user switch between rule sets live. (Conway, the default,
  is: a dead cell is born on exactly **3** live neighbours; a live cell survives on **2 or 3**.)
  - *HighLife* — born on **3 or 6**; survive on **2 or 3**. *Golden example: a dead cell with
    exactly 6 live neighbours stays dead under Conway but is born under HighLife.*
  - *Day & Night* — born on **3, 6, 7, or 8**; survive on **3, 4, 6, 7, or 8**. *Golden example:
    a dead cell with 7 live neighbours is born under Day & Night but not under Conway; a live
    cell with 4 live neighbours survives under Day & Night but dies under Conway.*
  *Done when:* the user can switch rule sets while it runs.
- **Endless world** — remove the edges entirely: an unbounded world a glider can cross forever,
  with a view the user can pan and zoom. *Done when:* patterns can travel arbitrarily far and
  the user can pan and zoom. *Golden example: a glider runs for 40 generations and ends up
  intact, 10 cells down and 10 cells right of where it started, never clipped by an edge.*
- **Hexagonal grid** — run on a hex grid, where the cells tile so each one shares an edge with
  exactly **six** neighbours (no diagonals), using a rule suited to hexes — for example: born on
  **2**, survive on **3 or 4**. *Done when:* the simulation can run on a hex grid. *Golden
  example: under that rule, an empty cell with exactly 2 live neighbours is born next
  generation, and a live cell with 5 live neighbours dies.*
- **Front-ends** — a nicer interface with smooth animation and cells coloured by how long
  they've been alive, in one or more of:
  - *TUI* — a polished terminal interface with colour and in-app controls.
  - *Web* — runs in a browser.
  - *Standalone* — a native desktop window.
  *Done when:* the simulation is shown through one of these front-ends, not as plain text.
- **Statistics** — a live population graph, a generation counter, and detection of when the
  world has stabilised or died out. *Done when:* the user can see the population change over
  time. *Golden example: a block reports a constant population of 4; a blinker is detected as
  oscillating; a pattern that empties the grid is flagged extinct.*
- **Ship it** — package and distribute what you've built so others can install and run it: an
  installer, a deployed website, or an app-store build. *Done when:* someone else can install
  and run it without your help.
