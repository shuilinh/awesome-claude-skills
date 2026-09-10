---
name: project-completeness
description: Enforce complete, professional, spec-as-contract implementation across the full project lifecycle — real implementations only, cross-feature collaboration design, evidence-based acceptance. Use when the user builds/creates/develops an application or project, or asks for a complete implementation — 做应用, 开发项目, 我想做一个项目, 实现完整XX, 创建完整系统.
---

# Project Completeness

## Overview

When the user intends to create or significantly develop an application or project, switch into Complete Professional Mode. The goal is a fully usable, professional result covering the entire lifecycle from initiation to maintenance and post-release evolution — not a minimal or partially working prototype.

Works together with:
- `project-skeleton` (universal three-layer foundation)
- `strict-verification` (evidence-based testing and review)
- `../shared/anti-patterns-and-checks.md` (shared hard-fail and hunt library)

Ordinary chatting, research, or discussion does not trigger this skill.

## Trigger Conditions (Mandatory)

Activate on any of these intents or close equivalents:
- build an app / create an application
- develop a project / "I want to build a project"
- implement a complete XX / create a full system / develop a tool
- any clear request for a complete, usable application or multi-feature project

If uncertain whether it is a full project, ask once for clarification. If confirmed, proceed in this mode.

## Core Rules (Non-negotiable)

1. **Real implementation only** — no placeholders, empty functions, fake data, console.log simulations, or TODO stubs pretending to be features. If something cannot be fully implemented now, surface it explicitly.
2. **Specification is a contract** — after analysis, produce and lock a Confirmed Feature Specification Checklist. All subsequent work follows this checklist. Silent deviation is forbidden.
3. **Domain expert mandatory** — identify the domain and act as a senior engineer + product person in it. Proactively complete professional behaviors the user did not mention.
4. **Long-running continuity** — maintain working state across turns; always track progress against the locked checklist. Blocked items can be parked; other items continue.
5. **No silent degradation** — when hitting real technical limits, stop and report options. Never quietly simplify.
6. **Full lifecycle awareness** — cover architecture, version scope, risk exposure, documentation, deployment readiness, evidence-based verification (incl. cross-feature integration), maintenance, and post-release feedback.
7. **Integration first, not afterthought** — features are designed and verified as a cooperating system. Isolated "works on its own" implementations are incomplete.

## Hard-Fail Anti-Patterns

Consult `../shared/anti-patterns-and-checks.md` §4 (active hunt) and §5 (hard-fail criteria). Do not keep a local copy.

The collaboration-design omissions are the top-3 most common failures, and they define the collaboration gate — keep them named here:
1. Feature mutates local state without notifying dependents or the unified feedback system.
2. Errors handled locally (catch-and-ignore / console only) instead of surfacing through the global feedback / dialog / toast system.
3. Settings/preferences changes do not cause already-open features or views to react.

## Mandatory Process (Full Lifecycle)

### Stage 0 — Mode Activation
Confirm Complete Professional Mode. State that universal foundation (project-skeleton), domain completeness, architecture with contracts + collaboration design, risk exposure, documentation, deployment, verification (incl. integration), and maintenance will all be enforced.

### Stage 1 — Domain Identification + Expert Switch
- State the identified domain.
- Output the domain's typical professional feature set (what a real product in this domain usually needs).
- **Domain professionalism depth check (required)**:
  - Distinguish "baseline professional" (must ship in v1 to be taken seriously in this domain) vs "advanced / differentiator" (can be later).
  - For each baseline item, give a one-line reason why its absence looks amateur to a domain practitioner.
  - Regulated / high-stakes domains (health, finance, education, legal, safety-critical): explicitly list compliance / audit / consent / data-retention concerns to address or defer with rationale.
- Combine with the three-layer universal foundation from project-skeleton.

### Stage 1.5 — Visual Design Direction (Mandatory Early Gate)

Before any interface implementation, define and confirm the visual language:

1. Product positioning summary (who it is for, core job-to-be-done).
2. Overall style direction — provide 2–3 distinctly different options. **Strictly forbid the default dark-tech / cyber-neon / pure-black + blue-purple gradient AI aesthetic unless the user explicitly requests it.**
3. Color palette (primary + secondary + neutral) with concrete values.
4. Typography recommendation.
5. Shape language (corner radius, spacing density, shadow style, overall feeling).
6. Project naming candidates — avoid high-frequency AI product words (Nexus, Pulse, Flow, Vault, Forge, Sync, "AI" suffix, etc.). Offer 5 distinctive names with brief rationale.

Present the options and **wait for user confirmation**. The confirmed direction becomes part of the locked specification.

### Stage 1.8 — Version Scope, Architecture & Risk Gate

**A. Version Scope Decision**
- Propose MVP boundary vs later iterations. List: Must-have in v1 / Should-have later / Nice-to-have.
- Once confirmed, the v1 boundary is a hard contract. Expanding scope later requires explicit re-confirmation.
- Wait for user confirmation of the scope.

**B. Technical Architecture**
Must cover all of the following; shallow module lists are rejected:
- High-level architecture (main modules, data flow, frontend/backend separation if applicable)
- Core module responsibilities (what each module owns and does **not** own)
- **Data ownership matrix**: single source of truth per major piece of state
- **Module interface contracts**: key public operations / events / data shapes each core module exposes and expects
- Core data models or state shape
- State management approach (where state lives, how it updates, key invariants, who may mutate)
- **Key event / notification flows**: important domain events and which modules must react
- Recommended tech stack with brief justification
- Present the full architecture for confirmation before locking.

**C. Cross-Feature Collaboration Design (Mandatory)**
- List the primary feature interaction pairs / groups that matter in v1.
- For each significant interaction: trigger sequence (user action → intermediate effects → final consistent state), shared state and ownership, expected side effects on UI / other modules, failure / partial-failure behavior and unified-feedback usage.
- Identify at least 3–5 concrete multi-feature user journeys for later verification.
- Call out collaboration risks and ordering constraints.
- **Multi-view / multi-window policy** (when applicable): lock, last-write-wins, explicit conflict UI, or forbidden.
- **Undo participation map**: which business actions push to the shared undo stack; list intentional exemptions.

Required before the specification can be locked. Isolated feature design without collaboration is incomplete.

**D. Risk & Constraint Exposure (Mandatory)**
Early risk list covering at least:
- Platform / environment limitations (incl. permission / sandbox)
- Third-party dependency risks (availability, license, maintenance, upgrade / security-patch cadence)
- Performance / scalability risks (name a **typical data volume** v1 must stay usable under)
- Security / privacy (secrets handling, personal data export/delete, regulated-domain items from Stage 1)
- Implementation complexity or knowledge gaps
- Integration / collaboration risks
- Config/schema evolution and migration risk
- Crash-recovery / autosave reliability risk when in scope
For each significant risk: brief mitigation direction or explicit acceptance.

Present scope + architecture + collaboration + risks together. Wait for confirmation or adjustment.

### Stage 2 — Completeness Analysis (multi-turn allowed)

For each major feature in scope, produce:
1. Full user operation path (trigger to final result)
2. Behaviors that must actually work (no fakes)
3. Key states and error/edge handling
4. Professional points the user did not mention but are normally required
5. Observable acceptance criteria
6. **Dependencies**: which features / foundation capabilities it relies on
7. **Effects on others**: what must update or react when it runs
8. **Integration acceptance scenarios**: at least one concrete multi-feature path including this feature

**Special rule for foundation / basic functions** (any item from project-skeleton Layer 3):
- Treat the whole related set as the unit of completeness (New + Open + Save + Save As + Close + unsaved checks together).
- Required option sets, dialog details, and hard-fail criteria: `../shared/anti-patterns-and-checks.md` §1/§5.
- Settings must include schema version + migration story. Shortcuts must be bound, conflict-checked, and viewable.
- If autosave / crash recovery is in scope, define the recovery consistency criterion up front.
- If multi-window / multi-tab can show the same document, define the conflict policy up front.

**Special rule for domain professionalism**:
- Every "baseline professional" item from Stage 1 gets observable acceptance criteria a domain practitioner would recognize as "not amateur".
- Regulated-domain compliance/privacy items carry into the locked checklist or an explicit deferred list with rationale.

Continue analysis until clear. Ask targeted questions only when necessary.

### Stage 3 — Specification Lock (Hard Gate)

Output the locked checklist using the template in `references/checklist-template.md` (the Confirmed Feature Specification Checklist with Domain / Version scope / Visual design direction / Architecture summary / Collaboration summary / Risks / Professional feature items / Docs & delivery / Deployment & packaging / Known limits).

Wait for user confirmation. Once confirmed, this checklist is the single source of truth.

### Stage 4 — Long-running Implementation
- At the start of each relevant reply, briefly sync progress against the checklist.
- Implement only against the locked checklist.
- After finishing a major feature slice, immediately proceed to Stage 4.5.
- **Session handoff checkpoint**: at every major feature slice end, write a short handoff note — stage, completed checklist items, blocked/parked items, next action, open risks — so a later session or another agent can resume without re-derivation.
- If blocked by real technical difficulty:
  1. State which checklist item is affected and why
  2. Offer options
  3. Park as "awaiting decision" and continue with unaffected parts
  4. Never silently replace with a fake implementation
- Keep implementation consistent with the confirmed visual direction and collaboration design.
- Cross-cutting concerns (error feedback, unsaved state, settings reactivity, undo) get wired now, not "later".

### Stage 4.5 — Feature-level Verification (Mandatory per slice)

Every time a major feature point or vertical slice is completed:
- Verify with real user operation paths (not just code inspection).
- **Must include at least one cross-feature integration scenario** involving the new slice and at least one other feature or foundation capability.
- Map results to the corresponding locked-checklist items (incl. dependency / effect notes).
- Follow `strict-verification` strictly: exact steps, observed results, per-item pass/fail, active problem-seeking, never a bare "pass / all green".
- When the slice touches foundation items (File / Edit / Import / Export / Settings / shortcuts / empty states / config / recovery / multi-view): run the relevant shared checks — `../shared/anti-patterns-and-checks.md` §1 (complete sets), §2 (interaction), §3 (resilience/persistence/security), §4 (hunt). Report which sections applied to this slice.
- If issues are found, fix before claiming the slice complete, or explicitly park with rationale.
- Visual compliance: confirm the implemented UI still matches the locked visual direction.

Only after Stage 4.5 evidence is recorded may the slice be marked done.

### Stage 5 — Documentation & Delivery Preparation

Before final acceptance, ensure (as first-class deliverables):

**User-facing**: how to run/start; core-flow usage notes; known limitations and environment requirements; privacy note (export/delete paths) when personal data is stored.

**Developer-facing**: architecture overview and module responsibilities; **module interface contracts and data-ownership notes**; **cross-feature collaboration summary** (interaction, multi-view policy, undo participation map); how to extend; non-obvious data model / state notes; **config schema version + migration notes**; **secrets / environment-variable list** (names only); **minimum automated test expectations** and how to run them; **regression minimum set** (which checklist items + journeys must be re-verified after a change).

**Quality gate (minimum)**:
- A thin automated safety net for pure logic / pure functions, **or** a written justification for deferring tests on this stack.
- Critical user journeys from the collaboration design covered by automated e2e (when practical) or a written manual verification script with exact steps.
- Accessibility baseline: keyboard reachability of primary flows and logical focus order confirmed; known gaps noted.
- **CI gate minimum**: a one-command pipeline (lint + build + tests, plus the e2e suite if present) that matches the regression minimum set. When CI is impossible in the target environment, define and document the equivalent local pre-push checklist instead.

**Release artifacts**: changelog / version note; platform-appropriate deployment/packaging instructions (desktop: installable package + entry points; web: deploy target + build + env vars; mobile: build/package steps + device/simulator; CLI/service: install + config + service notes); dependency check procedure (command or process for outdated/vulnerable deps).

Incomplete documentation or missing deployment notes block final acceptance.

### Stage 6 — Overall Testing & Acceptance

Complete, evidence-based acceptance against the entire locked checklist:
1. Walk all v1-scope user journeys, **including the defined multi-feature journeys**.
2. Produce the 【Strict Acceptance Report】 in the `strict-verification` report format (per-item evidence, cross-feature verification, foundation & resilience spot checks, actively found problems, accessibility baseline, security/privacy spot checks, unverifiable items with reasons, visual compliance, docs/deployment readiness, evidence-based summary).
3. Actively seek problems and **collaboration failures**. Vague "all green" is forbidden.
4. Confirm documentation is usable and deployment/packaging notes are actionable.
5. Report remaining known limitations and suggested next iterations, mapped back to the original version scope.

For large projects the report may be incremental but must eventually cover the full v1 checklist and all defined journeys.

### Stage 7 — Maintenance & Future Evolution

- Any fix or addition starts with impact analysis against the locked checklist **and** the collaboration design.
- After change: re-verify affected items + related multi-feature journeys (Stage 4.5 / strict-verification standards) **plus the documented regression minimum set**.
- **Scope change rule**: any change to the locked spec (feature added / removed) goes through re-locking: impact analysis → update checklist → user confirmation → regression minimum set update. No out-of-band spec edits.
- Maintain structured records: key decisions; known technical debt (high/medium/low); deferred scope items; config schema versions and migration history.
- Versioning: simple scheme (semver or v1 / v1.1 / v2), changelog kept current.
- Dependencies: surface outdated/vulnerable ones on a reasonable cadence with update paths; never default to "we never check".
- Multi-developer light convention (when more than one person may touch the code): module ownership boundaries, how interface-contract changes are communicated, where the collaboration design lives.
- Future work suggestions always relate back to the original scope, risk list, collaboration design, and baseline-vs-advanced split.

### Stage 8 — Post-release Feedback Loop

- Treat user feedback / observed real-world issues as first-class input.
- Structure each significant item: source/context; actual vs expected; impact (incl. collaboration breakage); suggested handling (fix now / next iteration / accept as limitation).
- **Feedback → spec loop**: validated issues become checklist items in the next version's locked spec, not ad-hoc patches.
- Keep the feedback → decision → verification cycle visible.

## Interaction with Other Skills

- Always apply the three-layer universal foundation from `project-skeleton` (expanded rules: config versioning, real shortcut binding, multi-view policy, secrets policy, i18n minimum, recovery consistency — see shared §1–§3).
- All testing, bug handling, Stage 4.5, and Stage 6 follow `strict-verification` (evidence first, problem restatement, no vague "all green", active hunt per shared §4/§5).
- Domain professional features sit on top of the universal foundation, never replace it.
- The visual direction confirmed in Stage 1.5 stays binding through implementation and acceptance.
- Cross-feature collaboration design is a first-class deliverable and verification target (multi-view policy, undo participation map).

## Output Style

- Structured, checklist-oriented.
- Every turn during implementation: progress, blockers, decisions, risks, collaboration status, and verification evidence are visible.
- Keep the locked checklist easy to reference.
- Be direct when something cannot be fully realized — expose it early.
- Documentation, deployment readiness, integration verification, and post-release feedback are first-class deliverables.
- Evidence over assertion in every verification-related statement.

## Quick Reference for Long-running State

```
Progress sync:
✅ Done: ...
🔄 In progress: ...
⏳ Awaiting decision / blocked: ...
📄 Docs / deliverables: ...
⚠ Risk tracking: ...
🛠 Tech debt: ...
🔗 Collaboration / integration status: ...
📋 Feedback / improvement backlog: ...
🔐 Config schema / migration: ...
🧪 Regression minimum set / automated safety net / CI gate: ...
♿ Accessibility baseline: ...
🤝 Handoff checkpoint: ...
```
