# Log

Change history for this knowledge base, newest entry first. Add a dated entry (`## YYYY-MM-DD: <summary>`) whenever you create, edit, or restructure content — one entry per working session, not per file.

## 2026-07-01: Monthly thesis ledger review — all four open bets updated

First monthly calibration pass against the four open theses. Evidence drawn from 13 Granola meetings (May 31 – Jun 30, 2026) and weekly recaps for May 25–29, Jun 1–5, Jun 15–19, and Jun 22–26.

- **Bounded agents beat autonomy** ↑ 75% → 80%. The bounded-agent pattern crossed from internal R&D into client-facing delivery: Snap/USCC positions AREA 17 as harness author (design system + prompts) with Claude Code as scoped executor; the BD automation design (Jun 25 meeting) explicitly requires a governance gate before autonomous operation; the Paris leadership summit codified no-unreviewed-AI-output as company policy. The thesis's key unknown — whether bounded agents survive contact with client work — is beginning to resolve in their favor.

- **Decouple CDN from platform** → 70% (unchanged). Diagnosis is confirmed in depth (NASAM 80TB on a 1TB contract; Fastly's dedicated bot manager unavailable through Upsun; both Nascent and NASAM decided to decouple — Jun 20 recap), but neither migration has completed and no post-decoupling cost data exists yet. Holding until outcome evidence arrives.

- **The generalist's edge compounds** → 65% (unchanged). Indirect supporting signals (George's SXSW talk, Snap generalist-integrator model, pod-model move, Pentagram AI-provenance question), but no market-level data that generalists are measurably gaining ground on specialists. Nothing in the Granola record directly addresses the core question.

- **Sprints can't build complex platforms** ↑ 60% → 65%. The natural experiment is running: NASEM's 32-branch Growth 28.01 release (Jun 23) delivered the predicted late-stage crunch (held-back tickets, hard merge conflicts, ITS blocker, pre-prod proposal as symptom). Nascent named the problem plainly in the Jun 20 recap. The NASAM/Pentagram care-budget-to-sprint conversions are now active; the next six weeks are the falsification window.

No thesis settled this review cycle.

## 2026-06-26: Add weekly recap for Jun 22–26, 2026

Added `notes/weekly/2026-06-26-recap.md` — drawn from 13 Granola calls covering the NASEM 32-ticket Growth 28.01 release, Getty/PST 2030 proposal prep (due June 30), Millennium Management finalist round (Rosanna call targeting July 6), Paris leadership summit (pod model, skill matrix, engineering board, responsible AI policy), and vendor evaluations for Nexus, Snowflake/Pliable, Claude Tag, and FTZ/GTM.

## 2026-06-26: Add the Theses Under Test ledger — the wiki's calibration spine

Added a forward-looking, falsifiable-bet layer to complement the descriptive corpus (people/clients/projects/concepts). The idea: record the strategic calls already latent in the notes as scored, grounded, self-grading theses.

- New `theses/` section: folder frontmatter + a `thesis` template (claim / evidence / falsification condition / dated scorecard).
- Seeded four flagship theses, each grounded in existing docs: bounded agents beat autonomy (75%), decouple the CDN from the platform (70%), the generalist's edge compounds (65%, keystone), and sprints can't build complex platforms (60%, contested by current practice).
- Added `theses/ledger.md` — methodology + lifecycle diagram + live confidence scorecard + candidate theses to develop.
- Linked the new section into `index.md`. Weekly recaps are framed as the adjudication stream for scorecard updates.

## 2026-06-25: Bulk migration workflow — durable docs + log distillation

Ran a multi-agent workflow to convert durable content and distill the Granola logs (source vault read-only throughout).

- Converted 48 durable docs: A17 clients (Winston Taylor, Jane Street, NASEM, OSF, NAE, Truth Initiative), BD, Analytics → `clients/` and `references/`; Research → `references/`; Claude Code → `references/` + `concepts/`; Weekly Notes → `notes/weekly/`.
- Distilled ~400 of 931 Granola logs into 61 entity docs: 20 `people/`, 17 client/org `overview`s, 9 `projects/`, 16 `concepts/`. (14 of 24 extractor agents were rate-limited — Meetings under-covered; a completion pass is pending.)
- Reconciled `clients/national-academies` → `clients/nasem`; normalized stray `client-doc` types to `note`; connected each client overview to its documents.
- Rebuilt `index.md` as a full navigation hub.
- Excalidraw diagrams (6) set aside (binary format, not text-distillable).

## 2026-06-25: Begin Obsidian vault migration — Writing section

Started migrating ~990 docs from the `jg-obsidian-vault` (read-only source). Plan: convert the ~44 durable docs (Writing, A17, Research, Claude Code, Weekly Notes) into OKF, and distill the 931 daily/meeting Granola logs into concepts/notes/references rather than copying them 1:1.

- Added `writing/` section (folder + `essay` template).
- Converted the *Rise of the Generalist* series: 3 essay drafts + the series-plan hub. Rewrote Obsidian `[[wikilinks]]` as standard markdown links.
- Added the writing section to `index.md`.
