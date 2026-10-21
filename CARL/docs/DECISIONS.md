# DECISIONS — durable choices with a revisit trigger

Format: date · decision · why · revisit when.

| Date | Decision | Why | Revisit when |
|---|---|---|---|
| 2026-10-18 | Build Life OS ourselves; do not scaffold on Miessler's LifeOS | Single-principal, localhost dashboard, fast-moving upstream, global hooks; harvested TELOS, boundary, interview only (`DECISION-build-vs-scaffold.md`) | A one-week isolated trial after Slot 1 proves it reduces sessions spent configuring tools |
| 2026-10-21 | The Control Room artifact store is the live state; `registry/registry.json` and `NOW.md` are mirrors | Nicole on a phone was the hard requirement; a localhost Postgres fails it | The Tracker Sheet breaks, or a third person needs access, or the store exceeds a few thousand documents |
| 2026-10-21 | Do not build the Fable "Life + Business OS" platform (Postgres, Next.js, n8n, MCP server, six agents) | 17 object types and five phases before a shipped unit is the system-building loop the operating record names as the primary avoidance behavior; the doc's own closing advice is a two-week vertical slice, which exists now | Same trigger as above: Tracker Sheet breaks or a third person needs access. Also: when two scheduled tasks exist, add an Agent Ops view |
| 2026-10-21 | Health (`on-track / at-risk / off-track`) and `needs_decision` are separate from workflow status | Workflow state alone could not distinguish "active and fine" from "active and waiting on Nicole" | Never; this is cheap |
| 2026-10-21 | Log and parking lot are one document per entry | A single array document is last-writer-wins and loses entries once two people write | Never |
| 2026-10-21 | Morning push is a cloud scheduled task (08:18 America/Chicago) that reads the capsule and sends one iMessage; no model reasoning beyond formatting | Externally delivered single actions are the only pattern that has worked; session-scoped recurring tasks expire in 7 days | If the Mac is not awake at 08:18 three mornings in a row, move the send to a cloud channel |
| 2026-10-21 | AI writes to the store carry `by: "claude"`; no approval queue | Two-person registry; an approval gate is overhead. The Sunday review reads the `by` field | A write by Claude is reversed twice |
