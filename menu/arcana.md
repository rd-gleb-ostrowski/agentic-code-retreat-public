# Arcana

*Flavor: fantasy, the meatier one. Suggested stacks: any — this is about parsing words into
effects, so pick a language you're comfortable manipulating text in.*

**Premise:** You are a spellcaster, and spells are *verse*. You cast by writing a short rhyming
couplet; if it rhymes and holds its meter, the magic takes hold and resolves in the scene before
you. If your verse is clumsy, the spell fizzles.

---

## What casting is

You cast by writing an **incantation**: a two-line couplet. Two things matter independently:

- **What the spell does** comes from *keywords* in the verse.
- **Whether the spell holds** comes from its *stability* — it must rhyme and keep its meter.

A spell that holds resolves its effect in the scene. A spell with clumsy verse **fizzles**. A
spell with unknown words or a missing target **miscasts**. Neither ever crashes.

## What a spell does (the keywords)

Somewhere in the couplet the caster names:

- a **verb** — exactly one of **strike**, **ward**, **heal**;
- an **element** (only needed by *strike*) — one of **flame**, **frost**, **stone**;
- a **target** — an entity present in the scene (e.g. **golem**, or **me** for the caster).

Effects: *strike … with <element>* damages the target; *ward …* gives the target a shield;
*heal …* restores the target's health. Other words in the verse are flavour and ignored.

## Whether a spell holds (stability — concrete rules)

- **Rhyme.** The final words of the two lines must rhyme. *Rule for this game:* ignoring a
  silent `e` at the end of a word, two words rhyme if they end with the same final vowel-group
  plus the consonants after it — `call`/`fall` end `all` ✔, `flame`/`game` end `am` ✔,
  `call`/`fell` (`all` vs `ell`) ✘.
- **Meter.** The two lines must have the **same number of syllables**. *Rule for this game:* a
  syllable is a group of consecutive vowels (`a e i o u y`), not counting a silent `e` that ends
  a word — so `flame` = 1, `call` = 1, `fury` = 2, `golem` = 2.

If the verse doesn't rhyme, it fizzles: *"Your verse does not rhyme; the spell fizzles."*
If the meter is uneven, it fizzles: *"Your meter falters; the spell fizzles."*

## Order of judgement

1. If this exact verse has already been cast this session, it is **refused**: *"This verse has
   already been spoken."* The magic will not repeat itself.
2. If the couplet contains no known verb, or names a target that isn't in the scene, or uses a
   word where a keyword is expected that the caster doesn't know → **miscast** (a themed message).
3. Otherwise, check stability (rhyme then meter) → **fizzle** with the matching message if it
   fails.
4. Otherwise the spell **holds** and its effect resolves; the scene's new state is shown.

## The scene

The Circle starts with a training **golem** (100 health) and the caster (**me**). After every
cast the scene's state is shown — e.g. *golem: 80/100*.

---

## T0 — the core

The Circle: write rhyming couplets and watch stable spells resolve on the scene.

**It works when:**
- The caster can type a two-line couplet and see the result.
- A spell's effect is drawn from its verb/element/target keywords and changes the scene.
- A couplet that doesn't rhyme, or whose two lines have different syllable counts, fizzles with
  the right message and has no effect.
- Unknown words and absent targets miscast with a themed message; nothing ever crashes.
- The scene's state is shown after each cast.

**Golden examples**

Holds (rhymes `call`/`fall`, both lines 7 syllables; keywords *strike, flame, golem*):
```
Flame and fury heed my call,
strike the golem, make it fall.
```
→ the golem takes fire damage (its health drops).

Fizzles — doesn't rhyme (`call` vs `break`):
```
Flame and fury heed my call,
strike the golem, watch it break.
```
→ *"Your verse does not rhyme; the spell fizzles."* (no effect)

Fizzles — uneven meter (line 1 has 7 syllables, line 2 has 5), even though `call`/`fall` rhyme:
```
Flame and fury heed my call,
strike and watch it fall.
```
→ *"Your meter falters; the spell fizzles."*

Miscasts:
- a couplet naming `the unicorn` (not in the scene) → *"There is no unicorn here."*
- a couplet using `frobnicate` where a verb is expected → *"You don't know the word 'frobnicate'."*

## A spellbook to get you started

If verse isn't your strength, here are seven spells that already hold under the rules above
(each couplet rhymes and both lines have 7 syllables). Cast them as-is, or change a word and see
if the magic survives.

- **Strike with flame** →
  *"By the spark and burning flame, / strike the golem, end its game."*
- **Strike with frost** →
  *"Frost and silence, cold and deep, / strike the golem, end its sleep."*
- **Strike with stone** →
  *"Stone and weight, by mountains known, / strike the golem, knock it down."*
- **Ward the golem** →
  *"Shield of light, a guardian wall, / ward the golem, stand it tall."*
- **Ward yourself** →
  *"Wrap me safe in silver light, / ward me through the coming night."*
- **Heal yourself** →
  *"Mend my wounds and ease my pain, / heal me whole and well again."*
- **Heal the golem** →
  *"Knit the cracks and close the seam, / heal the golem, let it gleam."*

**Different lengths hold too** — the two lines only have to match *each other*, not hit 7
syllables:
- **A short strike (5 + 5)** →
  *"Frost and bitter cold, / strike the golem bold."*
- **A longer strike (8 + 8)** →
  *"With burning flame and fearless name, / I strike the golem, all the same."*

---

## Expansions

Self-contained packages to add on top of the core, in any order and combination.

### Deeper magic

- **A fuller lexicon** — more verbs and elements. New verbs: **summon** (call a familiar ally
  into the scene), **banish** (remove a summoned creature), **bind** (hold a target still for a
  turn), **drain** (damage a target and heal yourself by the same amount). New elements for
  *strike*: **light**, **shadow**, **lightning**. *Example (drain):* *"Drain the golem, take its
  breath, / steal its warmth and stave off death."* *Golden check: this lowers the golem's
  health and raises the caster's by the same amount.*
- **Power from poetry** — better verse does more, with guards against cheese. A longer couplet
  hits harder, but the bonus **caps** — padding a line past ~12 syllables does nothing. A
  *perfect* rhyme (a longer shared ending, e.g. `golden`/`olden` share `olden`) lands a
  **critical** for double effect, under two hard limits: criticals share a **cooldown** (at most
  one every few turns), and a given rhyme pair can **never** crit more than once in a whole
  session. A near-miss — lines off by exactly one syllable — **half-casts** at half strength
  instead of fizzling. *Half-cast example (line 1 is 7 syllables, line 2 is 8):* *"Flame and fury
  heed my call, / strike the golem and it shall fall."* — it still strikes, but for half.
  *Golden check: a fresh perfect-rhyme strike crits; that same rhyme pair never crits again all
  session; a one-syllable mismatch deals half, not zero.*
- **Modifiers** — intensifier words change magnitude: **twin** fires the element twice,
  **greater** doubles the effect, **lesser** halves it. *Example:* *"Twin the flame and double
  fall, / strike the golem, scorch them all."* *Golden check: a twin-flame strike lands two hits
  where a plain flame strike lands one.*
- **Stanzas (AABB)** — a four-line stanza casts **two spells at once**. By position the spells
  interleave: **spell 1 is lines 1 & 3**, **spell 2 is lines 2 & 4**, and each must independently
  be a valid spell (its own verb, target, and element if needed). The rhyme, though, is **AABB** —
  lines 1 & 2 rhyme, and lines 3 & 4 rhyme — so the rhyme laces the two spells together: each
  spell's first line rhymes with the other spell's first line, and each spell's second line with
  the other's second. All four lines share the meter. Both spells resolve; if either isn't a
  valid spell, a rhyming pair doesn't rhyme, the meter breaks, or the scheme isn't AABB, the
  whole stanza fizzles. *Example (AABB, 7 syllables each — spell 1 (lines 1 & 3) flame-strikes the
  golem; spell 2 (lines 2 & 4) wards you):*
  ```
  Flame and fury fills the hall,   (spell 1)
  shield me now before the fall,   (spell 2)
  strike the golem, break its keep, (spell 1)
  ward me, safe in shadows deep.    (spell 2)
  ```
  *Golden check: both spells resolve — the golem takes flame damage and the caster gains a
  shield; if lines 1 & 3 together name no verb, the stanza fizzles; an ABAB arrangement is
  rejected — only AABB holds.*
- **Haiku** — a three-line incantation with exactly **5, 7, 5** syllables. No rhyme is needed —
  the strict form replaces it — but the syllable counts must be exact or it fizzles. A haiku
  carries one valid spell's keywords (verb, target, element) and, as a moment of focused calm,
  resolves it at greatly increased power. *Example (5-7-5 — a frost-strike on the golem):*
  ```
  Winter's breath descends,        (5)
  strike the golem, still and cold, (7)
  frost will end its days.          (5)
  ```
  *Golden check: a 5-7-5 haiku naming a valid spell resolves it at increased power; a line with
  the wrong count (e.g. 5-7-6) fizzles with a meter error.*

### A living world

- **A foe that fights back** — a rival caster (100 health) opposite you that strikes each round
  unless you ward; you alternate until one falls. *Golden check: skip warding for several rounds
  and the rival's strikes take you to zero — you lose.*
- **A richer scene** — multiple entities (a golem, a goblin, a summoned raven ally) and an
  **area target**, *the horde*, that applies a spell to all foes at once. *Example:* *"Lightning,
  wind, and rolling storm, / strike the horde and break their form."* *Golden check: striking
  *the horde* damages every foe in the scene at once.*
- **A campaign** — a sequence of encounters each solvable only with the right spell: a frozen
  door that needs **flame**, a shadow wraith that falls only to **light**, a pit you must
  **summon** a bridge-familiar to cross. *Golden check: the shadow wraith takes no damage from
  flame/frost/stone and falls only to a light strike.*

### Modes & challenges

- **Multiplayer** — two or more casters duel, **locally** (hotseat, passing the keyboard) or
  over the **network**, taking turns casting at each other until one falls. *Golden check: two
  casters can play a duel through to a winner.*
- **Time limit** — each turn runs against a countdown (say 30 seconds) to compose a valid spell;
  let it run out and the turn is wasted (or the half-formed verse fizzles), forcing quick verse
  under pressure. *Golden check: a turn with no completed spell before the timer expires resolves
  as a wasted turn.*

### Tools & presentation

- **The Muse** — as you compose, it shows each line's syllable count and suggests words that
  rhyme with your first line's last word. *Example: a line ending in `night` shows "7 syllables"
  and suggests light, sight, flight, might, bright.* *Golden check: any suggested word, used to
  end the second line, passes the rhyme rule.*
- **Grimoire** — name and save a working spell, then recast it by name. A saved spell may be
  recast even though its verse was already spoken this session — but a remembered spell is a
  faded echo: it resolves at **reduced strength** and can never crit. *Example: save the flame
  strike as "Ember Bolt"; later `cast Ember Bolt` strikes again, weaker.* *Golden check: a recast
  saved spell works despite the no-repeat rule, but for less than its first casting.*
- **Spoken incantation** — speak your couplet aloud; your speech becomes the two lines, judged
  for rhyme and meter as written. *Golden check: a clearly spoken starter couplet resolves the
  same as typing it.*
- **A graphical stage** — render the scene and effects: the entities, health bars, and spell
  animations (flame bursts, frost shards). *Golden check: casting a strike visibly animates and
  updates the target's health bar.*
