# Shared Anti-Pattern & Acceptance-Check Library (Single Source of Truth)

> This file is the single source of truth shared by the three general skills:
> - `project-skeleton`: design/implementation phase cross-checks **§1 Basic functions** + **§2 Interaction** + **§3 Resilience & security**
> - `project-completeness`: gate and spec-locking phases reference this file; **do not** copy checklists into SKILL.md
> - `strict-verification`: review phase follows §4 Active hunt + §5 Hard-fail criteria
>
> Rule: the three SKILL.md files only state "which section of this file to reference when"; checklist content is edited here only.

---

## §1 Basic-Function Completeness (missing any item = incomplete)

### File lifecycle (must be complete sets, single verbs forbidden)
- [ ] New: blank document/project; handles unsaved state; updates title and dirty flag
- [ ] Open: file picker + format filters + recent files + corrupted/unsupported error handling
- [ ] Save: has a path → overwrite; no path → automatically falls through to Save As; updates dirty flag/title
- [ ] Save As: full location picker + filename + multi-format options + overwrite confirmation
- [ ] Close / Close All / Exit: unsaved confirmation (save/don't save/cancel) + resource cleanup
- [ ] Import: format/encoding/mapping options dialog + progress + error reporting
- [ ] Export: format/quality/scope/location options dialog + progress + success/failure feedback
- [ ] Recent-files list, drag-and-drop open (where the platform allows)
- [ ] Autosave + crash recovery (when claimed, recovery consistency must be genuinely verified, including metadata)

### Edit core
- [ ] Undo/Redo: multi-level + **shared stack**; the list of business actions participating in undo is written out, exemptions documented
- [ ] Cut/Copy/Paste (including domain-relevant clipboard content types)
- [ ] Delete, Select All
- [ ] Find/Replace + options (case sensitivity, whole word, regex — where domain-relevant)

### View
- [ ] Zoom (in/out/actual/fit)
- [ ] Fullscreen toggle
- [ ] Panel show/hide (toolbar/sidebar/status bar)
- [ ] Theme switch **genuinely applies and persists**

### Windows/tabs
- [ ] New window/tab, close tab, close others
- [ ] Conflict/dirty-state policy for the same document opened in multiple places is defined and implemented (silent divergence forbidden)

### Settings & Help
- [ ] Preferences: real categories + persistence + schema version + migration + live reaction of already-open views
- [ ] Shortcut list (viewable, actually bound, no unresolved duplicate bindings)
- [ ] Help entry, check for updates, About (version/author/license)

---

## §2 Interaction & UX

- [ ] All shortcuts actually bound; duplicate bindings found and resolved at design time
- [ ] Empty states have a **clear next action** (pure decoration forbidden)
- [ ] Non-trivial products have first-run onboarding or sample content (new users never face a blank wall)
- [ ] Domain-relevant drag-and-drop/paste/multi-select (if the UI implies it exists, it must be implemented)
- [ ] Dangerous operations are reversible or require confirmation
- [ ] Contextual enable/disable of actions (e.g. Save greyed out when there are no changes)

---

## §3 Resilience, Data & Security

### Persistence & recovery
- [ ] All persisted configuration carries a schema version; structural changes have explicit migration, silently dropping user settings forbidden
- [ ] Autosave/crash-recovery paths verified, content and metadata consistent

### Errors & degradation
- [ ] Network/IO failure: recoverable errors have retry/backoff strategy; user-facing degraded messaging; console-only forbidden
- [ ] Permission/sandbox denial: explain the reason to the user and give a workable path
- [ ] Errors bubble through the unified feedback system (toast/dialog); "error silos" forbidden (a feature catching and staying silent)

### Security & privacy
- [ ] No hard-coded secrets in source or sample configs (placeholders excepted)
- [ ] Personal data stored → export path + delete path provided
- [ ] All user-visible strings extracted; i18n pipeline proven by at least one working language switch

### Performance baseline
- [ ] Critical paths (open/save/main list render) usable at the **declared typical data volume**
- [ ] Deferrable extreme-scale support is explicitly named, not silently dropped

---

## §4 Active Hunt Checklist (executed item by item during review/acceptance; "only hunting for pass reasons" forbidden)

| Category | Hunt targets |
|---|---|
| Fake implementation | Menu/button exists but handler is empty, TODO, console.log, "not implemented" toast |
| Half-finished | File lifecycle implements only one verb; Save doesn't fall through to Save As; Import/Export without options dialog |
| State inconsistency | After a basic action, dirty flag/title/recent list/feedback are out of sync |
| Collaboration failure | Feature A passes alone but A+B interaction unverified; settings change doesn't reach open views; undo stack corrupted by business actions |
| Shortcuts | Listed in help but never bound; duplicate bindings unresolved |
| Resilience | Errors only in local console; config unversioned; recovery path unverified; multi-view silent divergence |
| Security | Hard-coded secrets; personal data without export/delete path; i18n never proven |
| Process | Acceptance without evidence structure; changes not impact-checked against the spec checklist; regression minimum set not run |

## §5 Hard-Fail Criteria (any trigger = incomplete; must be fixed or explicitly parked with rationale)

1. Any §1 complete-set item missing without explicit statement
2. Menu item / button handler empty or fake
3. Cross-feature journey never designed or verified ("A works on its own" treated as done)
4. Configuration without schema version while the structure has changed
5. Autosave/crash recovery claimed but the recovery path never executed and verified
6. Shortcuts claimed supported but no real binding
7. Acceptance conclusion is evidence-free "all green / no problem"
