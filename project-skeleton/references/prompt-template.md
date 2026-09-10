# Reusable Prompt Template (Three-Layer Foundation)

Copy and adapt this when starting a new project with any AI:

```
Please fully design and implement [project name].

【Platform】Desktop / Web / Mobile / CLI / Other: [fill in]

【Must include the complete three-layer universal foundation — no omissions】

1. Foundation framework (engineering & architecture)
- Clean directory structure
- Unified configuration management
- Logging system
- Global error handling
- State management approach
- Theme / design tokens
- i18n readiness (string extraction)
- Baseline accessibility support
- Versioning + update-check entry

2. Interface & interaction skeleton
- Startup flow (splash/loading → main UI)
- Platform-appropriate complete navigation (menu bar + toolbar / top nav + sidebar / bottom tabs, etc.)
- Sensible division of the main content area
- Right-click context menus
- Complete keyboard shortcut system
- Empty-state guidance
- Unified feedback, loading, and error messaging
- Multi-document / multi-tab support (where applicable)

3. Basic function sets
File: New, Open, Recent, Save, Save As, Close, Exit (with unsaved checks), Autosave
Edit: Undo/Redo, Cut/Copy/Paste, Delete, Select All, Find/Replace
View: Zoom, Fullscreen, Show/Hide panels, Theme switch
Windows: New window/tab, Close tab, etc.
Settings & Help: Preferences, Shortcut list, Help, Check for updates, About

【Concrete business goal】
Project goal: [one sentence]
Core features (by priority):
1. ...
2. ...
3. ...

【Frontend / backend integration】
- Define frontend/backend responsibilities and interfaces
- The foundation layer must remain usable while the backend is not ready

【Output requirements】
1. First output the complete architecture + interface layout sketch + three-layer foundation checklist, and wait for my confirmation
2. Only start writing code after confirmation
3. Overall completeness must be maintained — do not implement just a single feature point
4. Business features must collaborate with the foundation layer (shared undo, unified feedback, settings reactivity, unsaved state, etc.); isolated implementations are forbidden
5. End with run & test instructions
```

## Short Version

```
Implement [project name] as a complete project skeleton (three-layer universal foundation).
Must include:
1. Engineering framework (directory, config, logging, error handling, theme, etc.)
2. Interface skeleton (startup, navigation, layout, shortcuts, empty states, feedback)
3. Basic functions (New/Open/Save, Undo/Redo, Copy/Paste, Find, theme, Settings, About, etc.)
First output the architecture and checklist for my confirmation — do not write code directly.
```
