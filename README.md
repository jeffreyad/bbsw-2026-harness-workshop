# BBSW 2026 — Harness Engineering Slides

Trimmed, prompt-based slide deck for the BBSW 2026 Day 0 hands-on workshop,
*Agentic AI for Biometrics: From Vibe Coding to Practical Workflows*
(Nov 4, 2026). Covers the harness engineering block (specs, checks, agent
skills) and the integration sprint.

Every exercise slide is a copy-paste prompt for the AI agent.

## Contents

- `index.qmd` — the slide deck
- `prompts.md` — all workshop prompts (1–7) for copy-paste into Posit
  Assistant or Claude Code; core vs. stretch prompts are marked
- `fallback/SPEC.md` — a ready-made ADVS spec for attendees whose spec
  interview goes sideways
- `assets/` — slide images (QR codes for the slides and the repo, Navitas
  logo, Vibe Coding Ken)

## Render

```
quarto render index.qmd
quarto preview index.qmd
```

Requires [Quarto](https://quarto.org). Output is a reveal.js deck
(`index.html`); speaker notes are in each slide's `notes` block (press `S`).

## Publish

Every push to `main` re-renders the deck and publishes it to GitHub Pages
(<https://jeffreyad.github.io/bbsw-2026-harness-workshop/>) via
`.github/workflows/publish.yml`. To publish by hand instead:

```
quarto publish gh-pages index.qmd
```

Adapted from [rpharma-2026-workshop](https://github.com/jeffreyad/rpharma-2026-workshop).
