# Roundtrip Radar

> Per-workflow code audit tracing data through complete user flows for bugs, data safety, performance, and round-trip completeness.

## Moved to Radar Suite

This skill is now maintained as part of **[Radar Suite](https://github.com/Terryc21/radar-suite)** — all 5 audit skills in one install.

```bash
git clone https://github.com/Terryc21/radar-suite.git
cd radar-suite
./install.sh
```

The 5 skills are deeply interdependent — they update each other's findings, share a deferred-items tracker, and feed into a unified grade. Installing them together is the intended experience.

### Audit methodology

The skill follows three scanning principles to minimize false negatives:

1. **Enumerate-then-verify** — For domains where violations can lack searchable code signatures, the skill lists all candidate files and verifies each one rather than relying on grep alone. This addresses the 57% miss rate observed in grep-only audits.
2. **File-scoped skip lists** — A resolved finding applies to that file only. Callers and dependents of a fixed file need independent verification.
3. **Negative pattern matching** — The skill searches for subjects, then verifies the correct pattern exists around them. Findings from absent patterns are ranked into three confidence tiers (Almost certain / Probable / Possible) and presented separately from verified findings.

See [FIDELITY.md](https://github.com/Terryc21/radar-suite/blob/main/FIDELITY.md) for the design philosophy behind the audit approach.
