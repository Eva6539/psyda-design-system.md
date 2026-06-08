# Changelog

All notable changes to the PSYDA Design System skill are documented in this file.

The format follows [Skills Package Specification v0.1.0](https://github.com/kuanntw/skills-spec).

## 1.0.0 — 2026-06-08

### Added

- Initial spec-compliant release.
- `SKILL.md` with YAML frontmatter (name, description).
- `skill.json` package manifest including capabilities, source, and update policy.
- Reference files in `references/`:
  - `tokens.md` — color, typography, spacing, radius
  - `components.md` — atomic components (button, card, input, modal, table, badge, alert, toast)
  - `patterns.md` — composite patterns (step modal, 5:7 picker, cascade dropdowns, batch ops, action menu, delete confirm)
  - `rules.md` — concrete do/don't rules with code examples
- `evals/evals.json` — evaluation suite for skill validation.
- Capability declarations: filesystem read-only, no network access, no command execution, no secret access.

### Changed

- Restructured from single-file `psyda-design-system.md` (v3) to spec-compliant folder layout.

## 0.3.0 — 2026-06-08 (pre-release, single-file)

### Changed

- Rewrote as engineer-focused reference. Removed philosophical content.
- Added Quick Reference index table.
- Concrete rules with side-by-side code examples instead of prose explanations.

## 0.2.0 — 2026-06-08 (pre-release, single-file)

### Added

- Tailwind CSS class templates for all atomic components.
- Composite patterns: step modal, 5:7 dual-pane picker, cascade dropdowns.

## 0.1.0 — 2026-05-26 (pre-release, single-file)

### Added

- Initial draft.
- 5 design principles (later removed in 0.3.0 as too philosophical).
- Color palette, typography, spacing tokens.
- Anti-patterns section.
