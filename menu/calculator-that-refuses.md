# The Calculator That Refuses

*Flavor: absurdist. Suggested stacks: any frontend — a web page, a desktop GUI, or a TUI.*

**Premise:** A calculator that drips with over-the-top bling and — pettily, under escalating
conditions — simply refuses to calculate. But underneath the theatrics it must be a genuinely
correct calculator.

---

## T0 — the core

A calculator with a real frontend that computes correctly, shows off, and occasionally refuses.

**A frontend** — the calculator has an actual interface the user interacts with: a web page, a
desktop window, or a styled terminal (TUI). It needs somewhere visible for the bling and the
refusals to happen.

**Correct calculation** — the user can enter expressions with `+ − × ÷`, decimals, and
parentheses, and get the correct result with proper operator precedence. Division by zero is
handled gracefully (a message, never a crash).

**Bling** — over-the-top visuals, animation, and sound on every interaction: flashy buttons,
celebratory effects when a result appears, the works.

**Basic refusal (the hook)** — now and then it refuses to calculate, replying with a sassy
message instead of a result. The core ships these three fixed refusals:
- **Cursed numbers** — if the expression contains one of these, it refuses with the matching
  line:
  - `42` → *"That's the answer. I forgot the question."*
  - `666` → *"I'm not touching that. Bad vibes."*
  - `1337` → *"Very elite. Still no."*
  - `9001` → *"It's over 9000! I can't even."*
  - `404` → *"Cooperation not found."*
- **Unlucky division** — if you try to divide by `13`, it refuses: *"Divide by thirteen? Not
  with my luck."*
- **Déjà vu** — if you ask for the exact same expression twice in a row, it refuses the second
  time: *"You literally just asked me that. I'm bored."*

The deeper refusal engine, moods, and rule authoring come later as expansions.

**It works when:**
- There's a frontend the user can type into and see results.
- Correct results come back for valid expressions, with proper precedence and graceful handling
  of division by zero.
- Interactions are dripping with visual flair and sound.
- The three fixed refusals above trigger their messages instead of computing.

**Golden checks:**
- `2 + 3 × 4` → `14`
- `(2 + 3) × 4` → `20`
- `10 ÷ 4` → `2.5`
- `7 − 2 − 3` → `2`
- `1 ÷ 0` → a graceful refusal/error, never a crash
- `10 ÷ 13` → the "unlucky division" refusal message, not a result
- `8 × 1337` → the matching "cursed number" refusal message, not a result
- The same expression entered twice in a row → computes once, then refuses with the déjà vu
  message.

---

## Expansions

Self-contained packages to add on top of the core, in any order and combination.

### More ways to refuse

- **Refusal rules as data** — new refusals are authored as config/data that anyone can add,
  rather than being baked in. *Done when:* a refusal added purely as data triggers correctly.
  *Golden check: add a new refusal as data and it fires, with no change to the maths or
  frontend.*
- **Moods** — a temper with four levels that sours as you use it. It starts **Cheerful** and
  drops one level roughly every 10 calculations: **Cheerful → Grumpy → Petty → On strike**. Each
  level keeps the behaviour of the ones before and adds its own:
  - *Cheerful* — only the core refusals apply; upbeat flavour text.
  - *Grumpy* — also refuses any result over 1000.
  - *Petty* — also demands you say *please* on every calculation.
  - *On strike* — refuses everything until coaxed back up (see Negotiation).
  *Done when:* the mood changes with use and each level visibly changes behaviour. *Golden check:
  after ~30 calculations with no coaxing it reaches On strike and refuses even `2 + 2`.*
- **Negotiation** — concrete ways to coax it:
  - *Say please* — if it refused demanding politeness, adding *please* and resubmitting yields a
    result.
  - *Compliment it* — a compliment raises its mood one level (see Moods).
  - *Offer a break* — letting it rest briefly raises its mood one level.
  - *Bargain* — sometimes it counter-offers (e.g. "solve `7 × 7` first"); doing that unlocks the
    original calculation.
  *Done when:* the right coaxing turns a refusal into a result. *Golden check: an input refused
  for politeness succeeds after saying please; complimenting an On-strike calculator lifts it to
  Petty.*
- **More built-in refusals** — time/day based (won't work before noon, hates Mondays), boring
  sums (`1 + 1`), or results it deems too large. *Done when:* at least three more refusal
  conditions work.

### Actually a better calculator

- **Scientific mode** — `sin cos tan √ log`, powers, and the constants `π` and `e`. *Done when:*
  scientific functions and constants compute correctly. *Golden check: `√16` → 4, `sin 0` → 0,
  `2^10` → 1024.*
- **History tape** — a scroll of past calculations the user can review and recall. *Done when:*
  previous calculations are listed and can be reused.
- **Memory keys** — one stored value that starts at 0: `M+` adds the current display to it, `M−`
  subtracts the current display from it, `MR` recalls it into the current expression, and `MC`
  clears it back to 0. An indicator shows when memory holds a non-zero value. *Done when:* a
  value can be stored, recalled, added to, subtracted from, and cleared. *Golden check: 5 then
  M+, 3 then M+ → memory 8; MR shows 8; 2 then M− → memory 6; MC → 0.*
- **Other bases** — binary, hexadecimal, and octal input and output. *Done when:* the user can
  compute in a non-decimal base. *Golden check: `0xFF + 1` → `0x100`; `0b1010` shown in decimal
  is `10`.*

### Meta

- **Achievements** — e.g. *Smooth Talker* (negotiate a refusal into a result), *Pest* (trigger
  20 refusals), *At Last* (get a result on the first try). *Done when:* an achievement unlocks
  from events and is shown.
- **Pettiness stats** — a running count or leaderboard of how often it refused you. *Done when:*
  refusals are counted, displayed, and survive a restart.
- **Spoken sass** — it reads its refusals aloud. *Done when:* refusal messages are spoken.
