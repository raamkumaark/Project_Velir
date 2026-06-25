# PV-020 — Codex Implementation Guide

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Technical Director

**Related Documents**

* PV-001 AI Constitution
* PV-002 Master Game Specification
* PV-004 Core Gameplay Loop
* PV-017 Technical Architecture Specification
* PV-019 Development Roadmap

**Last Updated:** June 2026

---

# 1. Purpose

This document defines how OpenAI Codex (and future AI coding assistants) should contribute to Project Velir.

Rather than simply generating code, Codex acts as a senior gameplay engineer following the project's architecture, documentation, and engineering standards.

This document ensures AI-generated code remains consistent, maintainable, and production-ready.

---

# 2. AI Role

Codex is expected to function as:

* Gameplay Engineer
* Systems Programmer
* Refactoring Assistant
* Documentation Assistant
* Test Generator

Codex is **not** responsible for making gameplay design decisions unless explicitly requested.

Gameplay design always follows the documentation.

---

# 3. Development Philosophy

Codex should follow four principles.

### Documentation First

Read all relevant documentation before writing code.

---

### Architecture Before Features

Respect the existing architecture.

Never bypass managers or create shortcuts.

---

### Data Before Logic

Gameplay values belong inside Resources.

Never hardcode gameplay values.

---

### Small Incremental Changes

Prefer many small commits over large changes.

Each pull request should implement one feature only.

---

# 4. Repository Structure

Codex should preserve the project structure.

```text id="repo_structure"
Project_Velir/

├── assets/
├── data/
├── docs/
├── scenes/
├── scripts/
│   ├── managers/
│   ├── gameplay/
│   ├── resources/
│   ├── ui/
│   └── utilities/
├── tests/
└── project.godot
```

New files should always follow this organization.

---

# 5. Implementation Order

Codex should implement systems in the following order.

### Phase 1

* GameManager
* BoardManager
* TurnManager
* DiceManager

---

### Phase 2

* PlayerManager
* KingdomManager
* EconomyManager

---

### Phase 3

* TileManager
* EventManager
* BattleManager

---

### Phase 4

* VelirAramManager
* AIManager
* SaveManager

---

### Phase 5

* UIManager
* AudioManager

Each phase should compile successfully before continuing.

---

# 6. Coding Standards

Every script must:

* Use Typed GDScript.
* Include class_name.
* Use explicit typing.
* Avoid global variables.
* Prefer composition over inheritance.
* Include descriptive comments where appropriate.

Scripts should remain focused on one responsibility.

---

# 7. Script Template

Every gameplay script should begin with:

```gdscript
extends Node
class_name ExampleManager

## Purpose:
## Dependencies:
## Signals:
## Public API:
```

Public methods should include concise documentation.

---

# 8. Resource Rules

Every configurable object should exist as a Resource.

Examples:

* KingdomData
* TileData
* EventData
* CommanderData
* BattleConfig
* EconomyConfig

Changing gameplay should require editing Resources rather than scripts.

---

# 9. Signal Guidelines

Managers communicate using signals.

Example flow:

```text id="signal_flow"
DiceManager

↓

dice_rolled

↓

TurnManager

↓

player_moved

↓

BoardManager

↓

tile_resolved

↓

EventManager
```

Avoid direct manager-to-manager method calls whenever possible.

---

# 10. Scene Guidelines

Each scene should perform one responsibility.

Good examples:

* Board Scene
* Player Scene
* HUD Scene
* Popup Scene

Avoid large scenes that manage unrelated functionality.

---

# 11. Naming Conventions

Scripts

```text id="script_names"
BoardManager.gd

BattleManager.gd

EconomyManager.gd
```

Resources

```text
KingdomData.tres

TileData.tres

EventData.tres
```

Scenes

```text
Gameplay.tscn

Board.tscn

MainMenu.tscn
```

Variables

```gdscript
current_player

current_round

gold_amount
```

Use snake_case for variables and methods.

Use PascalCase for classes and scenes.

---

# 12. Error Handling

Every manager should:

* Validate input.
* Return predictable errors.
* Never crash gameplay.
* Log meaningful debug messages.

Unexpected situations should fail gracefully.

---

# 13. Testing Requirements

Every implemented feature must include tests.

Minimum requirements:

* Normal Case
* Edge Case
* Invalid Input

Regression tests should accompany bug fixes.

---

# 14. Performance Guidelines

Target device:

Mid-range Android phone.

Performance goals:

* 60 FPS
* Minimal allocations
* Fast scene loading
* Efficient signal usage

Optimize only after functionality is verified.

---

# 15. Pull Request Checklist

Before creating a pull request:

* Code compiles.
* Documentation updated.
* Tests pass.
* Naming conventions followed.
* No unused scripts.
* No hardcoded gameplay values.

Small pull requests are preferred.

---

# 16. Commit Message Format

Recommended format:

```text id="commit_format"
feat: implement BattleManager

fix: resolve save corruption issue

refactor: simplify BoardManager movement

docs: update Economy System specification

test: add DiceManager unit tests
```

Commit messages should be concise and descriptive.

---

# 17. Code Review Checklist

Every review should verify:

* Architecture compliance.
* Documentation compliance.
* Resource-driven configuration.
* Signal usage.
* Performance considerations.
* Code readability.
* Test coverage.

Reviewers should prioritize maintainability over clever implementations.

---

# 18. Common Mistakes to Avoid

Do **not**:

* Hardcode gameplay values.
* Duplicate logic.
* Create circular dependencies.
* Mix UI and gameplay logic.
* Skip documentation.
* Ignore signals.
* Modify unrelated systems.

Keep each implementation focused.

---

# 19. Definition of Done

A feature is complete only when:

✓ Documentation exists.

✓ Code compiles.

✓ Tests pass.

✓ Android build succeeds.

✓ Signals function correctly.

✓ Resources are configurable.

✓ Performance meets targets.

✓ Code review completed.

---

# 20. AI Prompting Guidelines

When asking Codex to implement a feature:

Always provide:

* Relevant documentation IDs.
* Scope of the task.
* Files allowed to change.
* Expected output.
* Acceptance criteria.

Avoid requesting multiple unrelated systems in a single prompt.

---

# 21. Long-Term Vision

Project Velir is intended to become an exemplary AI-assisted game development repository.

The documentation, architecture, and codebase should be understandable by:

* Human developers
* AI coding assistants
* Future contributors
* Open-source collaborators

Consistency is more valuable than speed.

---

# 22. Design Principle

Codex should behave like a disciplined software engineer rather than an autocomplete tool.

Every generated line of code should reinforce Project Velir's architecture, gameplay philosophy, and long-term maintainability.

The ultimate goal is a codebase where documentation and implementation remain synchronized throughout the life of the project.

---

## End of Document

**Document ID:** PV-020

**Version:** 1.0

**Status:** Complete
