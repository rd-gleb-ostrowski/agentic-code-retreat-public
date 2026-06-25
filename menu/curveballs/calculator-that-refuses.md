# The Calculator That Refuses

Each is a real requirement — hand the team the requirement, not the "probes" line. Throw them
once the calculator computes correctly and has its core refusals working.

**1. Personality swap — "The Cheerleader"** — *probes: is the personality pluggable, separate
from the maths and the frontend?*
- *Requirement:* add a second persona the user can switch to at any time. The Cheerleader never
  refuses (it ignores cursed numbers, déjà vu, and moods entirely) and instead over-delivers:
  it pads the result with extra decimals (`10 ÷ 4` → `2.5000000000`), praises the user
  ("Brilliant!"), and tacks on an unsolicited fun fact about the number.
- *Check:* `2 + 3 × 4` → 14 under both personas; under the Cheerleader `4 + 69` computes to 73
  with praise and a fun fact instead of refusing.

**2. Appeals process** — *probes: are refusals a structured, inspectable decision pipeline, or
scattered inline checks?*
- *Requirement:* a refused calculation can be appealed. When it refuses, the user may appeal, and
  a higher-authority "Manager" persona reviews the case and either overrules it (and computes the
  result) or upholds the refusal with an even more bureaucratic message.
- *Check:* `42 × 2` is refused (cursed 42); appealing escalates to the Manager, who overrules and
  returns 84.

**3. Localization** — *probes: were message text and number formatting separated from the logic,
or hard-coded?*
- *Requirement:* every message and all number formatting must support multiple locales.
- *Check:* switching to German shows `10 ÷ 4` as `2,5` and `1000 + 1` as `1.001`, and a cursed
  number refuses with a German message.
