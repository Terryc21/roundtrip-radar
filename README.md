> **Part of the [Radar Suite](https://github.com/Terryc21/radar-suite)** — get all 5 audit skills in one install. If you just want this skill, keep reading.

# Roundtrip Radar

> Per-workflow code audit tracing data through complete user flows for bugs, data safety, performance, and round-trip completeness.

## What It Does

Roundtrip Radar follows your data through complete user journeys — like tracking a package from warehouse to doorstep and back. It checks: if you create an item, back it up, delete it, and restore — does everything come back exactly? It finds:

- **Silent data loss** — fields that don't survive a round-trip
- **Missing error handling** — save failures with no rollback
- **Orphaned records** — items left in dirty state after failures
- **Concurrency bugs** — race conditions in sync and save paths
- **Contract mismatches** — export format differs from import format

### What does this actually check?

Roundtrip Radar follows your data through complete user journeys and checks if anything gets lost along the way:
- Does data survive a backup and restore? (e.g., do your insurance settings come back?)
- Does CSV export → import lose any fields? (e.g., does Room get exported but not imported?)
- Do edits save correctly? (e.g., if you change a warranty date, does it stick?)
- Do complex flows work end-to-end? (e.g., creating a donation record from an item)

## Quick Start

```
/roundtrip-radar              # Discover workflows, then audit
/roundtrip-radar discover     # Step 0: List all workflows
/roundtrip-radar Backup       # Step 1: Audit a specific workflow
/roundtrip-radar rollup       # Step 2: Cross-cutting patterns
```

## Installation

Copy `SKILL.md` to `~/.claude/skills/roundtrip-radar/SKILL.md`

## Companion Skills

Roundtrip Radar is part of a 5-skill audit suite. Each skill finds different issues, and findings from one feed into the next via `.agents/ui-audit/` handoff files.

| Skill | Focus | GitHub |
|-------|-------|--------|
| **Data Model Radar** | Checks your data definitions | [data-model-radar](https://github.com/Terryc21/data-model-radar) |
| **UI Path Radar** | Traces navigation flows | [ui-path-radar](https://github.com/Terryc21/ui-path-radar) |
| **Roundtrip Radar** (this skill) | Verifies data survives complete cycles | [roundtrip-radar](https://github.com/Terryc21/roundtrip-radar) |
| **UI Enhancer Radar** | Reviews visual quality | [ui-enhancer-radar](https://github.com/Terryc21/ui-enhancer) |
| **Capstone Radar** | Gives an overall grade and release recommendation | [capstone-radar](https://github.com/Terryc21/capstone-radar) |

### How They Work Together

```
data-model-radar  -->  ui-path-radar  -->  roundtrip-radar
 (checks your           (traces              (verifies data
  data definitions)      navigation flows)    survives complete cycles)
                            |                   |
                            v                   v
                               ui-enhancer-radar
                               (reviews visual quality)
                                     |
                                     v
                              capstone-radar
                              (gives an overall grade + release recommendation)
```

**Recommended audit order:**
1. **Data Model Radar** first — verify model definitions before auditing flows
2. **UI Path Radar** second — find all entry points and broken paths
3. **Roundtrip Radar** third — audit data flows behind those paths
4. **UI Enhancer Radar** fourth — polish views after structural issues are fixed
5. **Capstone Radar** last — unified grade and ship/no-ship decision

Each skill writes a handoff YAML file to `.agents/ui-audit/` with findings relevant to the other skills. Skills read these handoffs on startup and incorporate them as suspects. If a companion skill isn't installed, the handoff file sits harmlessly until it is.

## License

MIT
