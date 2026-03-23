# Roundtrip Radar

> Per-workflow code audit tracing data through complete user flows for bugs, data safety, performance, and round-trip completeness.

## What It Does

Roundtrip Radar follows your data through complete user journeys — like tracking a package from warehouse to doorstep and back. It checks: if you create an item, back it up, delete it, and restore — does everything come back exactly? It finds:

- **Silent data loss** — fields that don't survive a round-trip
- **Missing error handling** — save failures with no rollback
- **Orphaned records** — items left in dirty state after failures
- **Concurrency bugs** — race conditions in sync and save paths
- **Contract mismatches** — export format differs from import format

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

Roundtrip Radar is part of a 4-skill audit suite. Each skill finds different issues, and findings from one feed into the next via `.agents/ui-audit/` handoff files.

| Skill | Focus | GitHub |
|-------|-------|--------|
| **UI Path Radar** | Navigation paths, dead ends, broken promises | [ui-path-radar](https://github.com/Terryc21/ui-path-radar) |
| **Roundtrip Radar** (this skill) | Data safety, error handling, round-trip completeness | [roundtrip-radar](https://github.com/Terryc21/roundtrip-radar) |
| **UI Enhancer** | Visual quality, spacing, color accessibility, layout | [ui-enhancer](https://github.com/Terryc21/ui-enhancer) |
| **Release Ready Radar** | Ship readiness, A-F grading across 24 domains | [release-ready-radar](https://github.com/Terryc21/release-ready-radar) |

### How They Work Together

```
ui-path-radar  -->  roundtrip-radar  -->  release-ready-radar
 (navigation)       (data safety)         (ship/no-ship)
      |                   |
      v                   v
         ui-enhancer
         (visual quality)
```

**Recommended audit order:**
1. **UI Path Radar** first — find all entry points and broken paths
2. **Roundtrip Radar** second — audit data flows behind those paths
3. **UI Enhancer** third — polish views after structural issues are fixed
4. **Release Ready Radar** last — final ship/no-ship grade

Each skill writes a handoff YAML file to `.agents/ui-audit/` with findings relevant to the other skills. Skills read these handoffs on startup and incorporate them as suspects. If a companion skill isn't installed, the handoff file sits harmlessly until it is.

## License

MIT
