# BOUNDARY — where things live

Adapted from upstream LifeOS `SystemUserBoundary.md` (four zones) and the 2026-10-12 handoff's five-tier trust model. One rule per zone. If a file does not fit a zone, it does not get written.

| Zone | Holds | Lives in | AI agent access | Nicole |
|---|---|---|---|---|
| **SYSTEM** | Dashboard page, content library, scripts, templates, this doc set | `cbrahms/LifeOS` → `CARL/` (private repo) | Read and write | Read |
| **SHARED STATE** | Registry, focus sequence, capsule (NOW), activity log, parking lot, P1 answers | Control Room artifact store (`meta/*`, `projects/*`) | Write through the page or `ArtifactData` | Contributor: read and write |
| **PRIVATE STATE** | Energy, reps, mood, values tracker, mastery ladder, evidence log, module settings | Artifact store `data/users/<id>/adhd` (per viewer, hidden from everyone else, the owner included) + browser mirror | Only the viewer's own | Her own only |
| **PROJECT-PRIVATE** | Resale item master, photos, comps, buyer records | Resale OS repo / Tracker Sheet / Drive, never this repo | Scope-limited grants per project | Co-owner |
| **HOUSEHOLD-PRIVATE** | Family records, finances, statements, medical | iCloud folders shared one by one; `private/` gitignored | None by default | Shared folder by folder |
| **VAULT** | Passwords, recovery codes, identity documents, private writing | 1Password + encrypted offline copy | Never | By agreed mechanism only (open question) |

## Interface rules

- SYSTEM reads SHARED STATE through the published page. It never embeds shared values in the page source.
- The dashboard may show that a lower tier *exists* and its health (e.g. "backup verified: date"). It never shows contents.
- `registry/registry.json` and the artifact store are reconciled weekly in the Sunday review. The store wins between reviews.
- Names in the repo: the home area and any address use a short non-descriptive label, never the street.
- Nothing in SYSTEM is a secret. `.env.example` holds names only.

## What this replaces

Upstream LifeOS puts everything under `~/.claude/` with hooks that fire in every session. Carl's version keeps the harness vanilla and puts state behind a page both people can open on a phone. The boundary is the only part of upstream that carries over unchanged in spirit.
