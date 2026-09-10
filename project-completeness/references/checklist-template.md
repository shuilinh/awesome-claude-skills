# Confirmed Feature Specification Checklist Template (Full Lifecycle + Collaboration-Reinforced)

```
【Confirmed Feature Specification Checklist】
Project/Feature: [Name]
Domain: [identified domain]
Version scope: v1 MVP includes... / later iterations...

Visual design direction:
- Confirmed style: ...
- Primary / secondary colors: ...
- Typography & overall feel: ...
- Final project name: ...

Technical architecture summary:
- Core module responsibilities: ...
- Data ownership matrix: ...
- Key interface contracts: ...
- State management & invariants: ...
- Key event / notification flows: ...
- Tech stack choices: ...

Cross-feature collaboration design summary:
- Main interaction relationships & sequences: ...
- Key multi-feature user journeys (at least 3): ...
- Collaboration risks & constraints: ...

Risks & constraints:
- ... (each with mitigation direction or explicit acceptance; integration/collaboration risks flagged in particular)

Universal foundation: execute the three project-skeleton layers
- Engineering framework
- Interface & interaction skeleton
- Basic function sets

Professional features:
1. [Behavior that must genuinely work] — Acceptance: [observable criterion] — Depends on: ... — Effects: ...
2. [Behavior that must genuinely work] — Acceptance: [observable criterion] — Depends on: ... — Effects: ...
3. ...

Documentation & delivery requirements:
- How to run / start
- User usage notes
- Developer documentation (architecture, module contracts, data ownership, cross-feature collaboration notes)
- Known limitations
- Changelog

Deployment / packaging requirements: (name concrete artifacts per platform)
- Desktop / Web / Mobile / CLI: ...

Known limitations / open items:
- [if any]
```

Usage notes:
- Visual design direction, version scope, technical architecture (incl. interface contracts & data ownership), cross-feature collaboration design, and the risk list must be written in after their early gates are confirmed
- Every professional feature must be a verifiable real behavior, annotated with dependencies and effects
- Documentation (incl. contracts and collaboration notes in developer docs) and deployment/packaging requirements are part of the professional delivery — cannot be omitted
- Once locked, it becomes the execution contract; any deviation requires re-confirmation
- After each major feature point is completed during implementation, run Stage 4.5 evidence-based verification, including at least one cross-feature integration scenario
- Final acceptance must use the Stage 6 strict acceptance report format and cover the multi-feature journeys defined in the collaboration design
- "A single feature passes standalone testing" is forbidden as a completion criterion
