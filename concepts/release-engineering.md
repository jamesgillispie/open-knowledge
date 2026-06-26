---
type: concept
title: "Release Engineering: Large Multi-Branch Merges"
description: The mechanics of monster multi-branch releases and the philosophy favoring smaller, frequent ones.
tags:
  - concept
  - theme
---
# Release Engineering: Large Multi-Branch Merges

A repeated delivery pattern on the [NASEM Site](/projects/nasem-site.md): "monster" releases assembling 30 to 38 feature branches at once off a dedicated release branch.

## The mechanics

- **Release branch assembly.** Branches are merged into a release branch using `--no-ff` to preserve a clear merge history of what went in.
- **AI-assisted conflict resolution.** With that many branches, conflicts are heavy; GitKraken's AI conflict tool is used to work through them.
- **Smoke testing.** The assembled release is smoke-tested before it goes out.
- **Deployment via [Upsun](/clients/upsun/overview.md).** Releases deploy through the Upsun platform.
- **Hot-fix suffixes.** Post-release patches are versioned with suffixes (`.01`, `.02`) for quick traceable fixes.
- **Documented process.** The release workflow is written up in Confluence so it is repeatable rather than tribal knowledge.

## The philosophy

The explicit lesson is that smaller, more frequent releases are better than monster merges. Batching 30-plus branches concentrates risk, makes conflict resolution painful, and turns every release into a high-stakes event. Smaller releases spread risk, shrink the conflict surface, and make regressions easier to isolate.

## Why it recurs

Large multi-branch releases are usually a downstream symptom of cadence: when work accumulates between infrequent release windows (see [Sprint vs. Retainer Model for Complex Platforms](/concepts/sprint-vs-retainer.md)), each release inevitably balloons. The release-engineering pain is real, but the root cause is often upstream sequencing.

## Through-line

Keep releases small and frequent; when monster merges are unavoidable, lean on `--no-ff` history, AI conflict tooling, smoke tests, and a documented process to keep them survivable.