# Starship Bridge

*Flavor: sci-fi systems sim. Suggested stacks: any — the dashboard can be a TUI or a GUI,
your team's choice.*

**Premise:** You stand on the bridge of a starship in crisis. There's never enough power to run
everything, and the universe keeps trying to kill you. Keep her flying by routing power,
watching the horizon, and fighting the damage.

> **Balance note:** none of the numbers in this document (the reactor budget, ramp rate, damage
> values, decay rates, foresight depth, the 20-tick wave) have had a balance pass. Treat them as
> a rough starting point and expect to tweak them — possibly a lot — until a scenario feels
> tense but winnable.

---

## The ship

- **Subsystems.** Five — **Shields**, **Engines**, **Weapons**, **Sensors**, and **Life
  Support**. Each has an **integrity** (0–100, its health) and a **power level** (0–100). A
  subsystem at 0 power is **offline**; at 0 integrity it's **destroyed**.
- **The Hull.** The ship's overall integrity (0–100). Not powered — it's what you're protecting.
  Hull at 0 → the ship is lost.
- **The Reactor.** Each tick it produces a budget of **130** power units to split across the five
  subsystems (each 0–100). Running everything at full would need 500, so you're always short.
- **Power ramps, it doesn't snap.** Each tick a subsystem's power moves toward the level you set
  by at most **±25** — bringing a cold system up to full takes several ticks, so you must commit
  *early*, not at the last second.

## What power buys

- **Shields** — absorb up to **(their power)** points of incoming damage; any overflow hits the
  Hull. Offline shields absorb nothing.
- **Weapons** — at **60+ power** they repel a raider for no damage; below that the raider gets
  through.
- **Engines** — at **60+ power** the ship evades a drift hazard; below that it can't.
- **Sensors** — reveal the **threat queue** (below). Offline, you see only the **next 1 tick**;
  every **30** power buys **one more tick** of foresight (30 → 2 ticks ahead, 60 → 3 ticks).
- **Life Support** — at **50+ power** the crew is safe and integrity **regenerates +5/tick**
  (cap 100); below 50 (including offline) it **decays −10/tick**. *Roughly a third of your budget
  is always spoken for — or the clock starts ticking on the crew.*

## The threat queue & how you react

Incidents are generated in advance and sit in a **threat queue** with ETAs. You don't react to
surprises — you read the queue and **prepare**. But you only see as far ahead as your **Sensors**
reach: blind (Sensors offline) you get just one tick's warning, which — with the ±25 ramp — isn't
enough to bring a cold subsystem up in time. Powering Sensors buys the foresight to ramp the
right subsystem early.

So every tick is a triage: spend power on **foresight** (Sensors), on **air** (Life Support), or
on **defending the next threat** — and you can't fully afford all three. Threats rotate between
Shields, Weapons, and Engines, so the one you warmed up often isn't the one arriving next.

- **One at a time.** Only one incident is scheduled per impact tick in the core; juggling
  several at once is an expansion.
- **Duration.** Most incidents are a single impact. **Fire** is the exception — it lingers,
  burning every tick until you smother it.

## Incidents

- **Asteroid (Shields)** — 70 incoming damage. Powered shields absorb up to their power value;
  the remainder hits the Hull.
- **Raider (Weapons)** — a 50-damage attack. Weapons at 60+ repel it for no damage; otherwise it
  hits the Hull.
- **Drift hazard (Engines)** — 40 damage. Engines at 60+ steer clear; otherwise it hits the Hull.
- **Fire (power management)** — breaks out in a random subsystem, costing it 15 integrity per
  tick until you cut that subsystem's power to 0 for a tick to smother it.

## Each tick

1. **The threat queue** updates; you see upcoming incidents and ETAs as far as Sensors reveal.
2. **You set allocations** across the five subsystems (each 0–100, total ≤ 130). Power then ramps
   toward those targets by at most ±25.
3. **Resolve** (using current power levels):
   - Any active **fire** burns its subsystem for −15, unless that subsystem's power is 0 this
     tick.
   - The incident scheduled for **this** tick impacts (shields absorb, weapons repel, engines
     evade, or the Hull takes it).
   - **Life Support** updates: +5 at 50+ power, −10 below.
4. **Defeat** if Life Support or the Hull is at 0; **victory** when the wave's 20th tick is
   survived.
5. The dashboard updates.

---

## T0 — the core

The Bridge: a live dashboard, the 130-power reactor budget ramping across five subsystems, a
Sensors-driven threat queue, the four incident types, and a 20-tick wave to survive.

**It works when:**
- A dashboard shows every subsystem's integrity and power, the Hull, the reactor budget, the
  tick count, and the threat queue (as deep as Sensors allow), and updates every tick.
- The player sets allocations across the five subsystems; power ramps by ≤25/tick and the total
  never exceeds 130.
- The threat queue reveals upcoming incidents to a depth set by Sensors power, and incidents
  resolve on their ETA tick by the rules above.
- The scenario ends in victory after 20 ticks survived, or defeat the instant Life Support or the
  Hull hits 0.

**Golden checks:**
- Setting Shields to 100 from 0 takes them up by at most 25 per tick (so ~4 ticks to full).
- Sensors offline reveal only the next tick of the queue; Sensors at 60 reveal three ticks.
- Life Support under 50 power loses 10 integrity per tick; at 50+ it regains 5 — so neglecting it
  kills the crew in 10 ticks.
- An asteroid (70) with Shields at 70 leaves the Hull untouched; with Shields at 30 the Hull takes
  40.
- A raider with Weapons under 60 deals 50 to the Hull; at 60+ it's repelled for 0.
- A fire in Engines costs 15 integrity per tick until Engines' power is set to 0 for a tick.
- Life Support or Hull integrity reaching 0 ends the game in defeat.

---

## Expansions

Self-contained packages to add on top of the core, in any order and combination.

### Deeper systems

- **Repair & damage control** — assign a repair crew to a damaged subsystem so it regains
  integrity over time (say +10/tick while crewed); a destroyed subsystem needs a longer rebuild
  before it works again. *Golden check: a subsystem at 40 integrity with repair assigned climbs
  back toward 100 over several ticks.*
- **More incidents** — a **hull breach** (−40 Hull on impact), an **ion storm** (knocks a random
  subsystem offline for 3 ticks no matter its power), and **boarders** (drain a subsystem −10/tick
  until repelled by Weapons power or a crew). *Golden check: an ion storm forces a subsystem
  offline for exactly 3 ticks regardless of allocation.*
- **Simultaneous threats** — more than one incident can share an impact tick; the queue shows the
  stack, and you can't prepare for all of them. *Golden check: two incidents scheduled for the
  same tick both resolve that tick.*
- **Reactor management** — **overclock** for extra budget at the risk of reactor integrity, and
  let incidents damage the reactor so its output drops. *Golden check: overclocking adds power
  this tick but can cost reactor integrity; a damaged reactor produces less than 130.*

### Crew & stations

- **Named crew** — assign crew to a station to boost that subsystem (e.g. a gunner lets Weapons
  repel at 40 power instead of 60); crew hurt by fire or boarders lose their boost until healed.
  *Golden check: a crewed Weapons station repels a raider at a lower power threshold than an
  uncrewed one.*
- **Bridge co-op (multiplayer)** — split the stations among players (one on power, one on
  Sensors, one on Weapons), local or over the network. *Golden check: two players can run a wave
  together, each controlling their own station.*

### Campaign & content

- **Campaign** — a run of escalating waves with repair and upgrades between them, on a persistent
  ship that carries its damage forward. *Golden check: damage at the end of one wave is still
  present at the start of the next, minus repairs.*
- **Loadout & upgrades** — spend earned resources between waves on a bigger reactor budget, a
  tougher hull, better Sensors, and so on. *Golden check: buying a reactor upgrade raises the
  per-tick budget in the next wave.*
- **Scenario editor** — author your own waves by placing incidents on a timeline, and share them.
  *Golden check: an authored wave plays back the same incidents at the same ETAs every run.*
- **Endless mode** — incidents escalate forever; survive as long as you can, scored by ticks
  lasted. *Golden check: difficulty rises over time and the run ends with a tick-count score.*

### Command & automation

- **Power presets** — save named allocation profiles ("combat", "evasive", "silent running") and
  recall one in a single action. *Golden check: switching to a saved preset retargets all
  subsystems at once (still subject to the ±25 ramp).*
- **Automation rules** — program if-then rules that adjust allocation on their own ("if Hull < 30,
  set Shields target to 100"). *Golden check: when its condition holds, the rule changes the
  allocation with no manual input.*

### Presentation

- **Red-alert feel** — klaxons, a flashing dashboard, and sound on alerts and impacts.
- **Ship schematic view** — a visual ship layout where subsystems light up, dim when offline, and
  show fire and damage.
- **After-action report** — a captain's log after each wave: hits taken, damage absorbed, the
  closest call, and the final state of the ship.
