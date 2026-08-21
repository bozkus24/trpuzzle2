# HANDOFF — KESME

> Read `CLAUDE.md` first for how the project is built and the dev/delivery workflow. This file is the current-state snapshot.

## State
Fully functional and shipped. Everything is in `index.html` (single file). Latest work is on `main` and mirrored to branch `claude/cutle-turkey-adaptation-7r3qxp`; the live Artifact is republished and current: https://claude.ai/code/artifact/7f915701-93cf-4297-8a1e-636c639eed29 . No pending edits, working tree clean.

## Completed (highlights)
- Core game: deterministic daily shape, drag-to-cut, Sutherland-Hodgman split, 6 win tiers (50:50…55:45), half-up rounding, scissors cut + separation animation, fluid blob shapes + ~19 extra shapes (gear/heart/crescent/etc.).
- Three modes in one segment: **Günlük / Antrenman / Arşiv**. Archive = monthly calendar from **2026-08-01**, each past day shows its shape thumbnail + result dot; ‹ › day nav flanking the "Arşiv #N · date" line above the circle. Daily result also recorded to archive.
- Result restore: daily, practice (`kesme2-practice-last`, needs `si` shape index), and archive days restore solved state + score instead of restarting.
- Stats modal: day result on top, general stats, distribution; stats icon always opens Günlük view; **share** shares the *displayed* record via `shareRecord` (correct per mode).
- Settings (⚙): **Tema** (Aydınlık/Karanlık segment), **Vurgu Rengi** (14-color 7×2 grid, drives shape color), **Renk Körü Modu** (green/red → blue/orange, key `kesme-cvd`).
- First-visit auto how-to-play popup with "Bir daha gösterme" + "Anladım" (only in the intro popup, not the ? icon view); `kesme-help-seen`.
- Separated daily/practice stats & streaks. Countdown reserved only in daily mode. Header enlarged; nav arrows are sharp SVG chevrons.
- `CLAUDE.md` added.

## Important decisions
- **Never rename localStorage keys** (listed in CLAUDE.md) — breaks user history/streaks.
- `DAILY_UNLIMITED` test flag is ON (daily is replayable; each replay counts in daily stats). Turn off for a "real" one-play-per-day daily.
- Archive numbering epoch = 2026-08-01 (#1); `puzzleNo`/`fmtDate` depend on it. Dates are UTC.
- `shade()` returns `rgb(...)`; `hex2rgb` parses both hex and rgb so nested `shade()` works (this fixed a black-border-on-restore bug — keep it).
- Cut colors: larger piece slightly darker, borders derived from fill (never black), intentionally low-contrast/soft.

## Known issues / watch-outs
- Colors/spacing were tuned by repeated user feedback — change cautiously and screenshot mobile + desktop before shipping.
- `DAILY_UNLIMITED` inflates daily stats; expected for testing, revisit before "launch".
- Artifact packaging depends on an embedded-fonts CSS (Space Mono woff2 subsets as data URIs) that lived in the session scratchpad (ephemeral). To republish from a fresh session you must regenerate it (embed Space Mono @font-face data URIs) + base64 `logo.png`, and strip the doctype/html/head/body wrapper.

## Possible next steps (none requested/blocking)
- Optionally disable `DAILY_UNLIMITED` for production behavior.
- Persist the embedded-fonts snippet into the repo (e.g. a build note/script) so artifact rebuilds don't depend on scratchpad.
