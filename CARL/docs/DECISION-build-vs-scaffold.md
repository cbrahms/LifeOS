# LifeOS (danielmiessler/LifeOS) — Reverse Spec and Fit Assessment for Carl's Life OS

**Analyzed:** 2026-10-18 · **Source:** repo HEAD `5e2f2e8` (release v7.40.4, last commit 2026-09-03), ourlifeos.ai/install, docs.ourlifeos.ai
**Method:** clone + file inspection. LifeOS was not installed or run. Claims tagged FACT (seen in code/docs) or INFERENCE (reasoned from evidence).

---

## 1. Technology stack and architecture

| Layer | What it is | Evidence |
|---|---|---|
| Runtime | TypeScript on Bun, plus Bash | `install/package.json`, README badges |
| Host | Claude Code first; other harnesses get context files only, no hooks | `LifeOS/INSTALL.md` §6 |
| Install target | The harness config root, normally `~/.claude/` | `INSTALL.md` §2, `SystemUserBoundary.md` |
| Constitution | `LIFEOS/LIFEOS_SYSTEM_PROMPT.md` (209 lines), loaded only via a `lifeos` launcher alias | `INSTALL.md` §7 |
| Enforcement | 58 hook files merged into `settings.json` (routing, memory loop, gates, voice, spend audit) | `install/hooks/` |
| Skills | 57 bundled skills (Research, Telos, Interview, Art, RedTeam, Fabric, etc.) | `install/skills/` |
| Personal data | `USER/` tree (TELOS, WORK, DA identity) symlinked from `~/.config/LIFEOS/USER/`, meant to be its own private git repo | `SystemUserBoundary.md` |
| Dashboard | Pulse: local web app + launchd/systemd service on `localhost:31337`, macOS menu bar app | `INSTALL.md` §8, `LIFEOS/PULSE/` |
| Code volume | ~148K lines of TypeScript, ~274K lines total (ts/sh/md, excluding built output) | `wc -l` |

## 2. Module structure

```
LifeOS/install/
├── LIFEOS/      ALGORITHM, ATLAS, PULSE, HERMES, TOOLS (180 files), DOCUMENTATION (33 subsystems), RULES
├── USER/        TELOS/ (TELOS.md, GOALS, CURRENT_STATE/*, IDEAL_STATE/*), WORK/, DIGITAL_ASSISTANT/, CUSTOMIZATIONS/
├── hooks/       58 hooks + lib + handlers
├── skills/      57 skills
├── agents/, commands/
└── settings.system.json, settings.enhancements.json, CLAUDE.template.md
```

## 3. Observed requirements (EARS)

| ID | Requirement | Evidence |
|---|---|---|
| R1 | The installer shall add only missing files and shall not overwrite existing ones on first install. | `INSTALL.md` §4 |
| R2 | Install tools shall be dry-run unless passed `--apply`. | `INSTALL.md` §4–6 |
| R3 | When the harness is Claude Code, the installer shall merge the hook set into `settings.json` after backing it up. | `INSTALL.md` §6 |
| R4 | When the harness is not Claude Code, the system shall load context via AGENTS.md and shall not provide always-on hook behavior. | `INSTALL.md` §6 |
| R5 | While launched with plain `claude`, the system shall load CLAUDE.md but not the constitution. | `INSTALL.md` §7 |
| R6 | The system shall treat `TELOS.md` as the single source of truth for mission/goals and auto-generate `PRINCIPAL_TELOS.md` for session load. | `USER/TELOS/README.md` |
| R7 | The system shall keep USER data outside the public SYSTEM tree via symlink to `~/.config/LIFEOS/USER/`. | `SystemUserBoundary.md` |
| R8 | Where Pulse is enabled, the system shall serve a dashboard on `localhost:31337`. | `INSTALL.md` §8 |
| R9 | The Upgrades queue shall never auto-apply; acceptance requires the principal. | `Upgrades/UpgradesSystem.md` |
| R10 | The system shall model exactly one principal (one human) and one digital assistant. | `{{PRINCIPAL_NAME}}` placeholders throughout; no multi-user docs found |

## 4. Non-functional observations

| Area | Observation | Tag |
|---|---|---|
| Change velocity | v7.0.0 → v7.40.4 in roughly one quarter; Algorithm at v8.20.2; major restructures (PAI/ → LIFEOS/ rename, USER moved to XDG path 2026-05-22, ~16 hooks consolidated in v7.0) | FACT |
| Public vs private | Parts of the tooling (release skill, Arbol, some workflows) are excluded from the public payload; docs reference paths that do not exist on a public install | FACT (`UpgradesSystem.md`, `INSTALL.md` §7) |
| Blast radius | Hooks live in `~/.claude/settings.json`, so they would fire in every Claude Code session on the machine, not only LifeOS sessions | INFERENCE (Claude Code hook scoping) |
| Multi-user | No shared/household model; single principal | FACT (absence) + INFERENCE |
| Mobile/remote | "Remote Access" is a roadmap item; Pulse is localhost | FACT (README roadmap) |
| External deps assumed | codex CLI, Interceptor browser, Cloudflare/wrangler, ElevenLabs voice | FACT (`INSTALL.md` §8.5) |
| License | MIT | FACT |
| Security | Release gates, egress guards, write guards as hooks | FACT (`hooks/`) |

## 5. Fit against Carl's Life OS charter (2026-10-15)

| Charter requirement | LifeOS provides | Fit |
|---|---|---|
| Registry of ~18 projects across domains | `USER/WORK/` folders, per-work ISA files | Partial — no registry schema or status rollup comparable to `registry.json` |
| Single resumption point (`NOW.md`) | Cortex memory + session context injection | Different model — memory-driven, not one human-readable NOW file |
| Focus sequence / one primary build / WIP limit | Nothing equivalent; the Algorithm optimizes per task, not portfolio | Gap |
| Shared with Nicole, editable from a phone | Single principal; localhost dashboard; remote on roadmap | Gap (hard) |
| Household/private lane, never in a remote | USER zone in a private repo | Partial — private repo still means a remote by design |
| Domains keep their own repos (Resale OS, YT, book, consulting) | WORK/ assumes work lives under the LifeOS tree | Partial |
| Metric of record: shipped units/week | No such metric | Gap |
| Low maintenance for large future changes | You inherit upstream's change rate on top of your own overlay | Inverse of the goal |
| Goals / identity / "who I am" | TELOS.md + CURRENT_STATE/IDEAL_STATE + `/interview` | Strong |
| Clean system/user separation | Four-zone boundary contract | Strong (pattern worth copying) |

## 6. Inferred acceptance criteria for "use LifeOS as the foundation"

1. Nicole can read and update project status from her phone without a terminal. **Not met.**
2. Upstream upgrades do not alter Carl's registry, sequence, or NOW semantics. **Unverified; high change rate makes this unlikely without pinning.**
3. Installing does not change behavior of unrelated Claude Code work (CareerOps, Resale scripts). **Not met by default (global hooks).**
4. Portfolio-level focus rule is enforced. **Not provided.**

## 7. Uncertainties

- Whether `CLAUDE_CONFIG_DIR` (or DetectEnv's config root) can isolate LifeOS into its own root so hooks don't touch normal sessions. Not tested.
- Actual upgrade behavior on a populated install (merge vs overwrite of SYSTEM files you edited). Install page and docs do not say.
- Real-world breakage rate across 7.x minor releases. Shallow clone only; GitHub API access unavailable this session.
- Whether Carl's previously installed `pai-*` skills are this project's predecessor (LifeOS was formerly PAI). Name match only.

## 8. Recommendation

**Do not adopt LifeOS as the Life OS foundation. Harvest three parts from it.**

| Harvest | Into | Effort |
|---|---|---|
| TELOS schema (Mission, Goals, Problems, Strategies, CURRENT_STATE/IDEAL_STATE by life dimension) | `life-os/docs/TELOS.md` replacing the scattered Bio-File/goals | 1 session |
| Four-zone System/User/Interface boundary as a written contract | `life-os/docs/BOUNDARY.md` (codifies the existing `private/` rule) | 25 min |
| `/interview` question flow | One-time pass to fill TELOS; prompts copied, not installed | 1 session |

Optional, after Slot 1 (Resale OS) exits on 2026-10-29: trial LifeOS in an isolated config root on one non-household domain for one week, judged on whether it reduced or increased sessions spent configuring tools.
