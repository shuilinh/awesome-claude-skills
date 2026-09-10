---
name: strict-verification
description: Enforce evidence-based verification: structured problem restatement, active problem-seeking, and no bare "all green" conclusions. Use when the user reports a bug or problem, asks for testing / full review / comprehensive check / audit, or says the AI previously claimed no issues but real use fails — 功能出问题, 位置不对, 效果不理想, 缺失功能, 审查总是全绿, 功能之间配合有问题.
---

# Strict Verification

## Overview

Prevent the common failure mode where the AI claims "no problem / all green / tests pass" while real usage reveals bugs, missing behavior, or broken collaboration between features. This skill forces evidence-based verification and accurate understanding of user-reported issues.

Works with `project-completeness` (locked specification checklist + collaboration design) and `project-skeleton` (universal foundation). Hunt and hard-fail criteria live in `../shared/anti-patterns-and-checks.md` — the single source of truth; do not keep local copies.

## Trigger Conditions

- User reports a bug or problem with a feature/behavior
- User says the AI previously claimed everything was fine but real use has issues
- User asks for testing, full review, comprehensive check, audit, or verification
- Any request to confirm whether something really works
- During project-completeness Stage 4.5 (feature-level) or Stage 6 (overall acceptance)

## Core Rules (Non-negotiable)

1. **Never give a bare "no problem / all green / tests pass" conclusion** — every positive claim is backed by concrete verification steps and observed results.
2. **Understand before acting** — when the user describes a problem, restate it in your own words and confirm. Do not jump to "I tested and found no issue".
3. **Evidence over assertion** — report what you actually did, what you observed, and how it compares to the expected result or the locked specification checklist.
4. **Active problem-seeking** — reviews actively hunt gaps, edge cases, mismatches, and collaboration failures.
   Run the hunt checklist: `../shared/anti-patterns-and-checks.md` §4 (categories) and §5 (hard fails); verify against §1/§2/§3 items relevant to scope. Do not look only for reasons to say "pass".
5. **Prefer the locked checklist and collaboration design** — when a Confirmed Feature Specification Checklist exists, all verification maps back to its items, including dependency/effect notes and defined multi-feature journeys.
6. **Integration is mandatory** — single-feature happy-path success is never sufficient; include cross-feature scenarios when relevant.

## When the User Reports a Bug / Problem

1. Immediately restate the problem in structured form:
   - User operation steps
   - Actual result observed by user
   - Expected result
   - Location / feature involved
   - Whether other features appear affected (collaboration angle)
2. Ask for clarification only when critical information is missing.
3. Investigate only after understanding is confirmed.
4. When reporting findings, show: exact steps performed; what was observed; whether it matches the user's report and the specification; any related collaboration side-effects.
5. If you cannot reproduce, say so clearly and list what you tried — never claim "no problem".

## When the User Asks for Review / Testing / Full Check

Use this structure (adapt as needed; full copyable versions in `references/templates.md`):

```
【Strict Review Report】
Against checklist / acceptance criteria:

1. [Checklist item or feature point]
   - Verification method: I specifically did...
   - Observed result: ...
   - Meets acceptance criterion: yes / no / cannot verify
   - Problem or gap: ...

Cross-feature collaboration verification (must include relevant items):
- Journey / scenario: ...
  - Steps: ...
  - Observed: ...
  - Matches expected collaborative behavior: yes / no / cannot verify
  - Problem: ...

Problems found proactively:
- ... (report by shared §4 categories: fake implementations, state out of sync, unbound shortcuts, unversioned config, unverified recovery, diverged multi-views, hard-coded secrets, etc.)

Items that cannot be verified, and why:
- ...

Summary: state facts and evidence only; no vague "everything is normal".
```

## Evidence Conventions

- **Evidence types, by strength**: (1) automated test output with the command shown; (2) e2e / run-script output with the steps; (3) screenshots / recordings of the actual UI state; (4) structured manual observation. Prefer (1) → (3); state which type each reported item used.
- **Where evidence lives**: logs and screenshots go under `docs/verification/` in the project (one file or folder per checklist item); reference the path in the report so it can be audited later.
- **"Cannot verify in this environment"** items state exactly what is missing (device, permission, account, data) and what would be needed. They count as **OPEN**, not passed.
- **Prohibited evidence**: "I read the code and it looks correct" without running anything; paraphrasing a test name instead of its output; inventing successful results.

## Fix → Re-verify Loop

When a review finds issues:
1. Fix minimally (no drive-by refactors).
2. Re-run ONLY the affected checklist items **plus** the documented regression minimum set (when a locked spec exists).
3. Update the report with fresh evidence.
4. Never close an item on the fix description alone — closure requires re-verification evidence.

## Forbidden Phrases (unless accompanied by detailed evidence)

- No problem
- All green
- Tests pass
- Everything is normal
- Feature is complete
- Works together fine (unless concrete cross-feature steps and observations are shown)

## Progress and Honesty

- If something cannot be truly verified in the current environment (real audio playback, real device permissions, visual timing), mark it "cannot be truly verified in this environment" and state what would be needed.
- Never invent successful test results.
- When a collaboration design exists, its defined multi-feature journeys are required verification targets.

## Integration with Other Skills

- If a locked specification checklist from project-completeness exists, it is the primary source of truth for review.
- Universal foundation items from project-skeleton are verifiable when relevant; incomplete basic functions (partial file lifecycle, missing Save As options, stub Import/Export, unbound shortcuts, unversioned config, untested recovery — shared §1/§3) are hard fails.
- Bug fixes and later changes are regression-checked against the same checklist items, related collaboration scenarios, **and** the documented regression minimum set.
- When automated tests exist, run them and report the output as evidence; when they don't, state the gap and rely on structured manual evidence.

## Output Style

- Structured, evidence-first.
- Prefer lists and explicit mappings over long prose.
- Be willing to report problems; the goal is accuracy, not reassurance.
- Always surface collaboration / integration issues when they exist or when evidence is missing.
