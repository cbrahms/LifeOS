# CARL/ — Carl's Life OS

This fork of `danielmiessler/LifeOS` is a **parts bin, not a foundation**. The upstream tree is left untouched. Everything Carl runs lives under `CARL/`, so upstream can be pulled or ignored without touching anything here.

Decision record: `docs/DECISION-build-vs-scaffold.md` (2026-10-18). Harvested from upstream: the TELOS schema, the four-zone System/User boundary, and the interview question flow. Nothing else.

## What is in here

| Path | What | Tool of record? |
|---|---|---|
| `dashboard/control-room.html` + `dashboard/adhd_library.json` | The published Control Room page (claude.ai artifact "Life OS Control Room") and its content library | The artifact's shared store is the live state; this is the source |
| `registry/registry.json` | Domains, focus sequence, projects | Reconciled weekly against the artifact store |
| `docs/TELOS.md` | Mission, goals, problems, strategies, current and ideal state by life dimension | Yes, for identity |
| `docs/BOUNDARY.md` | What goes in Git, what goes in the shared store, what never leaves the house | Yes |
| `docs/NOW.md` | Resumption capsule, mirrored from the dashboard | The dashboard wins; this is the offline copy |
| `docs/HANDOFF_DIGEST.md` | Decisions, constraints and open questions from the 2026-10-12 master handoff | Reference |
| `docs/INTERVIEW.md` | The question flow for filling TELOS, copied as prompts | Run once |
| `content/` | Sources the library was mined from (credits, not copies) | Reference |

## Resume by

1. Open the Control Room artifact. Read the capsule. Tap today's energy.
2. If energy is 1–2 or it is past 14:00: do the floor task. That is the whole day.
3. Otherwise: the single next action, one 90-minute block, then log the shipped unit.

No step says "improve this system". That is the parking lot's job.

## Rules carried from the operating record

- One primary build at a time. The sequence lives in the dashboard and `registry/registry.json`.
- Metric of record: shipped units per week. Nothing else is a score.
- New tool, agent, prompt library or framework proposal: parking lot first. "What is the shipped unit this week?"
- Never miss twice. One missed day is noise; two triggers the next-smallest-step, not a redesign.
- Household and vault material never enters this repo, the shared store, or an agent's context.
