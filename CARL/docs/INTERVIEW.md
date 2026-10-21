# INTERVIEW — the check-in flow (copied as prompts, not installed)

Harvested from upstream LifeOS `skills/Interview` (ContextCheckin). The rules worth keeping:

1. **Read what is on file before asking.** A blank "what is your mission?" is forbidden when `TELOS.md` is populated.
2. **Staleness is information, not failure.** A 95-day-old goal may still be right; the prompt is "still right?", never "you are behind."
3. **Open with the sharpest claim-vs-evidence contradiction.** Evidence here is the activity log and the registry, not a wearable.
4. **Stop signals are sacred.** "Enough", "stop", "later" ends the session. State persists in the file.
5. **IDs are stable.** G3 stays G3 when edited or dropped; a new goal gets the next number.
6. **Bump the marker on every approved edit** (`<!-- updated: YYYY-MM-DD by:carl -->`).

## Paste into a Claude session (Sunday, 20 minutes)

```
Read CARL/docs/TELOS.md and the Control Room store (meta/now, meta/log, projects).
For each ## section, compute age from its updated marker. Sort stalest first.
For each section, one question only, in this form: "<ID or section> is <n> days old and says <claim>. The log shows <evidence>. Still right?"
Accept "yes", "edit: …", "drop", "stop". On edit or drop, draft the replacement line, show the diff, wait for a yes, then bump the marker.
End with: shipped units this week (count from the log), one Keep/Kill on open loops, one line to add to the Bio-File, and the next action for tomorrow written into meta/now.
Never propose a new tool, agent or framework. If one comes up, write it to the parking lot and move on.
```

## First-time fill (already done 2026-10-21 from the operating record and charter)

If TELOS.md is ever empty again, the order is: Mission → Goals (with slot windows) → Problems (mechanism, not moral) → Strategies (one per problem) → Current State (facts with dates) → Ideal State (by a date) → Narratives → Wisdom. One section per message. Stop on "enough".
