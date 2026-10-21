# AGENTS.md — CARL/

Scope: everything under `CARL/`. The rest of this repository is an untouched fork of `danielmiessler/LifeOS`; do not install it, run its hooks, or edit it.

Read first: `README.md`, `docs/NOW.md`, `docs/BOUNDARY.md`. Read `docs/DECISION-build-vs-scaffold.md` before proposing to adopt upstream.

Rules
- The Control Room artifact store is the live state. `registry/registry.json` and `docs/NOW.md` are mirrors, reconciled at the Sunday review.
- Every reply to Carl ends with "Next action:" and one physical step under 5 minutes.
- Never propose a new tool, agent, prompt library or framework. If asked to build one, ask first: "What shipped unit does the current system lack, and what single variable would change that?"
- Never write household, vault, financial or medical content into this repo or the shared store. See `docs/BOUNDARY.md`.
- Status labels: Implemented / Proposed / Unverified / Blocked. A diagram is not a deployment.
- Update `docs/NOW.md` at the end of any session that changed state, even without progress.
