# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for the **REC GenAI Rapid Build Hackathon** — a TCS-organized event where teams tackle Tamil Nadu-focused challenges using GenAI. The site has three pages: a landing page, 24 challenge cards across 4 themes, and a 5-step prompt library that guides teams from discovery to a platform-ready build prompt.

## Architecture

- **Pure static site** — no build step, no framework, no bundler. HTML + CSS + vanilla JS.
- **Deployed on Vercel** with `cleanUrls: true` (configured in `vercel.json`), so links between pages omit `.html` extensions in production but use them in source.
- **Three pages**: `index.html` (landing), `challenges.html` (24 challenge cards), `prompts.html` (prompt library with copy-to-clipboard).
- **Single stylesheet**: `styles.css` — editorial design system with CSS custom properties for colors, typography, and spacing. Tamil Nadu-inspired palette (emerald, saffron, indigo, violet) applied via `data-accent` attributes on theme sections.
- **Fonts**: Fraunces (display), DM Sans (body), JetBrains Mono (code/labels) — loaded via Google Fonts.
- **No JS framework**: `prompts.html` has a `<script>` block handling challenge selection via `?t=` query param, platform selector for the Build prompt, and clipboard copy buttons.

## Key Patterns

- Challenge cards use `<details>` elements for expand/collapse — no JS needed.
- Challenge selection flows from `challenges.html` to `prompts.html` via query string (`?t=Challenge%20Name`), which auto-populates `[selected challenge]` tokens in prompt text.
- The Build prompt's `[platform]` token is replaced client-side when users click platform selector buttons (Google AI Studio, Lovable, v0).
- Theme accent colors are driven by `data-accent` attributes (`emerald`, `saffron`, `indigo`, `violet`) on section elements, mapped to CSS custom properties.
- Entry animations use the `.rise` class with delay variants `.d1`–`.d4`.

## Development

To preview locally, serve the directory with any static file server:
```
npx serve .
# or
python3 -m http.server 8000
```

There is no build, lint, or test pipeline.

## Assets

- `logos/tcs-logo.png` and `logos/tata-logo.png` — used in the site footer.
- `REC_GenAI_Challenge_Cards 2.pptx` and `REC_GenAI_Challenges.xlsx` — source materials (not served by the site).
