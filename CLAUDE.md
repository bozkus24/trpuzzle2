# KESME — project instructions

Single-file web game. **Everything lives in `index.html`** (HTML + CSS + one IIFE `<script>`). No build step, no framework, no dependencies. Don't scan the repo — the game is that one file; `logo.png` is the only other asset.

## What it is
"KESME" — a Turkish daily shape-cutting puzzle (adaptation of Cutle/pfiffel.com/cutle). All UI text is Turkish. Deterministic daily shape via `POOL[hashStr(dateStr) % POOL.length]`. Modes: **Günlük** (daily), **Antrenman** (practice), **Arşiv** (past days, calendar from 2026-08-01).

## Code landmarks (all in index.html)
- `POOL` — shape list `{n, p:[[x,y]…]}`, coords in ~[0,1]. Generators: `regular/starShape/gear/blob/smoothClosed`.
- Render: canvas 2D, `fitShape`, `fillShape`/`fillPiece`, `draw`, `animateCut`. `shade(hex,amt)` derives tones (`hex2rgb` also parses `rgb(...)`).
- Scoring: `scoreOf` (minority % → 6 win tiers 50:50…55:45), `finalize`.
- Flow: `play`/`startRound`/`showDone`/`restoreDaily`/`restorePractice`/`restoreArchive`/`playArchiveDay`.
- Stats/share: `renderStats`, `openStats`, `shareRecord`.
- Theme/accent/color-blind: `applyTheme`/`applyAccent`/`applyCvd`; help intro popup uses `#helpModal.intro`.

## localStorage keys — NEVER rename (preserves user data)
`kesme2-day-<date>`, `kesme2-arch-<date>`, `kesme2-practice`, `kesme2-practice-last`, `kesme2-stats`, `kesme-theme`, `kesme-accent`, `kesme-cvd`, `kesme-help-seen`. Dates are UTC `YYYY-MM-DD`.

## Conventions
- Default theme light; default accent = `PALETTE[0]`. Turkish, formal ("siz") copy.
- Keep it self-contained: no external requests except the Google-Fonts `<link>` (Space Mono) in `<head>`.
- Match the existing terse, comment-in-Turkish style. Validate JS after edits: extract the `<script>` and `node --check`.

## Testing (headless Chromium)
`export NODE_PATH=/opt/node22/lib/node_modules`, Playwright at `/opt/pw-browsers/chromium`. Load `file://…/index.html`; simulate a cut by dragging across `#cv` from above to below the shape. Check mobile (≤430px) and desktop.

## Git / delivery
- Work on branch `claude/cutle-turkey-adaptation-7r3qxp`; base/default is `main`.
- Per change: reset branch to `origin/main`, apply, commit, force-with-lease push, open PR, squash-merge, then re-sync branch to `origin/main`. Use `mcp__github__*` tools for PRs.
- Then republish the Artifact (self-contained: inline Space Mono @font-face data URIs + base64 `logo.png`, strip `<!doctype>/<html>/<head>/<body>`) to the **same** URL: https://claude.ai/code/artifact/7f915701-93cf-4297-8a1e-636c639eed29
