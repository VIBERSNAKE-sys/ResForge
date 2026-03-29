# Contributing to ResForge

ResForge reached its current state through 50+ iterations, each traced to a specific documented failure. Contributions that continue that discipline are welcome.

## Reporting Failures

Open a GitHub Issue with:
- The job description (anonymized if needed)
- The Module output that failed
- What specifically went wrong
- Which gate should have caught it

## Proposing Fixes

Every proposed change must include a self-audit covering nine criteria:

1. **Root cause:** What specific failure does this fix?
2. **Location:** Which module, which section? Why there?
3. **Alternatives considered:** What else was considered and why rejected?
4. **Trade-offs:** What does this cost? (bloat, processing time, new failure modes)
5. **Verification criteria:** How do you test that the fix works?
6. **Failure modes:** What could go wrong? Rate LOW/MEDIUM/HIGH.
7. **Reversibility:** How easily can this be undone?
8. **Anti-drift check:** Does this expand the scope of any existing rule?
9. **Text audit:** Is every instruction unambiguous?

This is not bureaucracy. It is how the system went from producing fabricated certifications to producing resumes rated 9/10.

## What Makes a Good Pull Request

- Traces to a documented failure
- Proposes specific text with specific location
- Includes WRONG/RIGHT examples where applicable
- Does not add a new rule when an existing rule just needs better enforcement

## What Gets Rejected

- Fixes without root cause documentation
- New rules that address one-off failures (need pattern across 2+ occurrences)
- Changes that increase module size without clear quality improvement
- Personal evidence or identifying information in examples
