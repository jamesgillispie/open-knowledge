# Log

Change history for this knowledge base, newest entry first. Add a dated entry (`## YYYY-MM-DD: <summary>`) whenever you create, edit, or restructure content — one entry per working session, not per file.

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
