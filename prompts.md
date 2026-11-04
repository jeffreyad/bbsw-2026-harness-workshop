# Harness Engineering: Copy-Paste Prompts

BBSW 2026 Day 0 Workshop, Agentic AI for Biometrics

Paste each prompt into **Posit Assistant** (Claude Code works too; differences are noted). Read each response before moving on.

> Review any code the agent writes before you run it. Use public or synthetic data only.
> LLM output can be wrong or vary between runs. Verify results with your own QC process before any regulatory, clinical, safety, or GxP use.

**Core:** Prompts 1, 2, 3, 5. **Stretch (if you're ahead):** Prompts 4 and 6. Prompt 7 is for the integration sprint.

---

## Prompt 1: Spec (let the agent interview you)

```
I want to derive ADVS from the VS domain in data/sdtm and the ADSL in
data/adam/adsl.parquet. Work in a new subfolder called harness/.

Do not write any code yet. Interview me, one question at a time, about
anything ambiguous: baseline definition, parameters, visit windows, flags.
Ask at most 5 questions. When I say "done" (or after question 5), write
harness/SPEC.md with a table of variables:
name, label, derivation rule, source, and open questions.
```

Answer the questions, then **read** `harness/SPEC.md` and edit anything wrong.
If the interview goes sideways, copy `fallback/SPEC.md` into `harness/`.

## Prompt 2: Checks first

```
Read harness/SPEC.md. Before deriving anything, write harness/checks.R:
a set of stopifnot() assertions that encode every testable rule in the
spec (one row per record key, flags are "Y" or NA, baseline and change
rules, etc.). Do not write the derivation yet. Show me the checks and
tell me which spec rules you could NOT turn into a check.
```

## Prompt 3: Derive, then check

```
Now write harness/derive_advs.R from harness/SPEC.md. Run it, then run
harness/checks.R. If a check fails, fix the code first and tell me what
you changed. If you believe the check itself is wrong, stop and tell me
why instead of editing it.
```

## Prompt 4 (stretch): Review markers

```
Add a "# REVIEW:" comment at every line where the code encodes a
protocol-specific decision (baseline definition, population, windowing).
Then list all REVIEW markers with line numbers and the SPEC.md row each
one comes from.
```

## Prompt 5: Make your own skill

```
Look at harness/SPEC.md, harness/checks.R, and harness/derive_advs.R
we just built. Create a skill called advs-derivation that captures how
to do this task again, saved in .posit/assistant/skills/advs-derivation/
(SKILL.md inside it).

The skill should include:
- frontmatter with a name and a description that says when to use it
- the steps we followed (interview, spec, checks, derive, review markers)
- the conventions we settled on
- what to ask the user rather than assume

Keep it under 100 lines. Show it to me before saving.
```

Claude Code: save to `.claude/skills/advs-derivation/SKILL.md` instead.

Then start a **new** chat so the skill loads, and test it:

```
Derive ADLB from the LB domain in data/sdtm.
```

Did the agent load your skill without being told to?

## Prompt 6: Check the harness itself (stretch)

```
Review the advs-derivation SKILL.md as a skeptical biostatistician.
What would a new agent get wrong following it? What is ambiguous? What
is missing a check? Suggest edits; don't apply them.
```

## Prompt 7 (integration sprint): your own idea

```
I want to build: ______

Do not write code yet. Interview me one question at a time until you can
write SPEC.md. Then propose checks for it and wait for my approval.
Use only public or synthetic data. Mark every decision I need to make
with a "# REVIEW:" comment.
```

Be ready to show **one spec line, one check, and one output** in the showcase.
