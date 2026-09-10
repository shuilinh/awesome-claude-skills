---
name: project-skeleton
description: Enforce the three-layer universal foundation (engineering / interface skeleton / basic functions) before any business feature. Use when the user builds, creates, develops, or scaffolds an app, system, tool, website, desktop/mobile app, full-stack project, or UI scaffolding — 做应用, 开发项目, 做一个项目, 搭建项目骨架.
---

# Project Skeleton

## Overview

When creating any application or multi-feature project, always build a complete, usable foundation first. Never deliver only isolated features. This skill enforces a three-layer universal foundation before any domain-specific functionality.

## Core Principle

Every project has two major parts:

1. **Universal Foundation** (mandatory, never skip) — three layers
2. **Domain-Specific Layer** (business goals and unique features)

Always complete and confirm the foundation before implementing domain features.

## The Three-Layer Universal Foundation

### Layer 1 — Engineering Framework

Invisible to end users, critical for maintainability:

- Clean, conventional directory structure (src, assets, config, tests, docs...)
- Unified configuration system (defaults + user overrides + environment separation)
  - **Config schema versioning**: every persisted config carries a version field
  - **Migration path**: on schema change, explicit migrate(old → new); never silently drop user settings
- Logging system (error / warn / info / debug, console + optional file)
- Global error handling and graceful degradation
  - Recoverable vs fatal errors distinguished
  - **Unified retry / degradation strategy** for network and IO: retry with backoff where safe, clear offline / degraded messaging, no silent swallow
  - Permission / sandbox denials surface a user-actionable explanation and a fallback path
- State management with a single source of truth
- Theme / design tokens (colors, fonts, spacing)
- Internationalization: **all user-visible strings extracted** + at least one working language switch or locale demo proving the pipeline
- Accessibility baseline: logical focus order, keyboard-reachable interactive elements, no unescapable focus traps
- Version info + update-check entry
- Single-instance control (desktop), command-line arguments where relevant
- Build / packaging readiness
- **Secrets policy**: no hard-coded keys in source; secrets from environment / secure store; example configs use placeholders
- **Privacy baseline**: if personal data is stored, provide export + delete paths
- **Performance baseline awareness**: critical paths (open, save, main list render) usable under a documented typical data volume; extreme scale may be deferred but must be named

### Layer 2 — Interface & Interaction Skeleton

- Startup / loading entry → main window or main page
- Platform-appropriate primary navigation (desktop: menu bar + toolbar + status bar; web: top nav + sidebar/tabs; mobile: bottom tabs / stack + drawers)
- Clear content area division; context menus (right-click)
- **Complete keyboard shortcut system (hard)**: shortcuts actually bound and trigger the correct actions; duplicate bindings resolved or reported at design time; user-visible reference in Help/Settings; customization where the platform supports it
- Responsive / resizable layout that does not break
- Multi-document / multi-tab when applicable:
  - **Multi-view policy**: if the same document can open in more than one place, define and implement conflict / dirty-state / lock behavior; never leave two views silently diverging
- **First-run onboarding** (required for non-trivial products): guided entry or sample content; never drop the new user into a blank wall
- **Empty states with clear next actions** (not decoration only)
- Unified feedback system (toast, dialog, confirmation, error); loading states for long operations
- **Common input methods**: drag-and-drop open/reorder/import, paste of domain-relevant content, multi-select + bulk actions when lists are central

### Layer 3 — Basic Functions

Real, fully usable standard actions. **A function is not implemented if it is only a menu entry, a stub, or a happy path missing the options a real product exposes.**

- **File lifecycle (complete sets, not single verbs)**: New / Open (picker + filters + recent) / Save (untitled falls through to Save As) / Save As (location + name + format + overwrite confirm) / Close & Exit (unsaved checks + cleanup) / Import (format/options dialog) / Export (format/options dialog) / recent files / drag-and-drop open / autosave + crash recovery when claimed (must be verified: recovery restores content + metadata consistently)
- **Edit core**: Undo/Redo (multi-level, **shared stack**; which business actions push to it is listed, exemptions documented), Cut/Copy/Paste (clipboard integration incl. domain content types), Delete, Select All, Find/Replace (+ case / whole-word / regex where relevant)
- **View control**: zoom (in/out/actual/fit), fullscreen, panel show/hide, theme switch that actually applies and persists
- **Window & tabs**: new window/tab, close tab / others / to the right, tab switching, always-on-top (desktop)
- **Settings & Help**: preferences (real categories, persistence + schema version + migration, live effect where expected), shortcut list (viewable and bound), Help, check-for-updates, About (version/author/license)
- **Cross-cutting**: unsaved-state indication, context-aware enable/disable (Save disabled when clean), consistent success/failure/progress feedback, dangerous operations reversible or confirmed, permission-denial explanations

**Hard-fail list**: the full reject-criteria (stubs, single-verb file lifecycle, unbound shortcuts, unversioned config, hard-coded secrets, silent divergence, ...) live in `../shared/anti-patterns-and-checks.md` §1 (required sets), §4 (active hunt), §5 (hard fails). Verify against it — do not maintain a local copy.

## Mandatory Process

### Stage 1 — Clarify and Confirm Scope
- Restate the goal in one sentence; list core business features with priority.
- State that the full three-layer foundation is included.
- Confirm the target platform (desktop / web / mobile / CLI) before writing code.

### Stage 2 — Design the Universal Foundation (present, then confirm)
Present a complete foundation design covering:
1. Engineering structure and key technical decisions
2. Interface layout and navigation sketch
3. Basic-function list adapted to the platform

**IN/OUT confirmation rule (no silent trimming)**: the design must list every optional foundation item as IN or OUT for this project — e.g. autosave/crash recovery, multi-window, i18n beyond string extraction, system tray, offline support — each with a one-line rationale. Only an item the user confirmed in (or explicitly declined) may be dropped. If the user gives no input, mark it **default-in** and say so.

Wait for user confirmation before implementation.

### Stage 3 — Domain-Specific Layer
- Design and implement the requested features on top of the confirmed foundation.
- Map them onto foundation services: shared undo, unified feedback, settings reactivity, unsaved-state indication. Isolated implementations that bypass foundation services are incomplete.
- Never remove or bypass foundation navigation, settings, feedback, or file/edit capabilities.

### Stage 4 — Frontend / Backend Integration (when applicable)
- Separate presentation from business logic and data; define API contracts early.
- The foundation stays usable with a mocked/delayed backend.
- Provide a simple way to run and test the full stack.

### Stage 5 — Delivery Checklist
Verify and explicitly state (check each line, cite shared §1/§2/§3 for the details):

**Engineering**: directory structure, config system (+schema version/migration), logging + global error handling, theme tokens, version info, secrets policy, privacy export/delete if applicable, performance baseline documented
**Interface**: startup entry works, full navigation skeleton, layout regions, context menus, shortcuts bound + conflict-checked + viewable, empty states actionable, first-run guidance, unified feedback, multi-view policy if multi-tab
**Basic Functions**: complete file lifecycle sets, edit core on shared undo stack, view controls, settings + about, no stubs / no hard-coded secrets / strings extracted
**Overall**: all requested business features integrated (not isolated), how to run/test documented

## Platform Adaptations

Keep the same completeness, adapt the patterns:

- **Desktop**: full menu bar / toolbar / status bar, multi-window, **single-instance handling** (second launch focuses existing window or warns), **file associations**, system tray (optional, mark default-in/out), and a decision recorded for **native menus vs in-app menus** (per-OS expectations differ).
- **Web**: routing, responsive top + side navigation, download-based save, browser theme integration. Add PWA / offline-availability criteria and extension expectations **only when the user's goal implies them** — never as default bloat.
- **Mobile**: splash, bottom tabs / stack navigation, safe areas, share sheet, limited undo, settings screen, **lifecycle handling** (background/foreground state persistence), **permission flows** (explain + fallback on denial).
- **CLI / Service**: entry point, subcommands, config file, logging, `--help` / `--version`, graceful signal handling, **exit-code conventions** (0 ok, 1 general error, 2 usage error), and **idempotency expectations** (re-running a completed operation is safe or explicitly destructive).

## Output Style

- Structured: Architecture → Layout → Module & Function list → Implementation plan → Code.
- Separate foundation code from domain code (folder structure or clear markers).
- If the user asks only for "one feature", still present the foundation and offer to include it.
- Never silently omit any part of the confirmed three-layer foundation.

## Quick Trigger Reminder

Activate on: "create an app / build a tool / develop a system / scaffold a complete project / full-stack application".

## Additional Resources

- Reusable prompt templates: see `references/prompt-template.md`
- Hard-fail / hunt criteria: see `../shared/anti-patterns-and-checks.md`
