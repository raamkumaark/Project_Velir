# PV-017 — Technical Architecture Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Technical Director

**Related Documents**

* PV-001 AI Constitution
* PV-004 Core Gameplay Loop
* PV-006 Board System Specification
* PV-012 AI System Specification
* PV-015 Save & Persistence System Specification

**Last Updated:** June 2026

---

# 1. Purpose

This document defines the software architecture of Project Velir.

Its purpose is to ensure the project remains modular, maintainable, AI-friendly, and scalable throughout development.

Every gameplay system should be independent, reusable, and easy to extend.

---

# 2. Architectural Principles

Project Velir follows the following engineering principles.

### Single Responsibility

Each manager performs exactly one responsibility.

Examples:

* TurnManager manages turns.
* BattleManager manages battles.
* EconomyManager manages resources.

No manager should perform unrelated work.

---

### Data-Driven Design

Gameplay values should never be hardcoded.

Instead, configurable Resources define:

* Kingdoms
* Tiles
* Events
* Commanders
* Battles
* Ancient Sites

Changing gameplay should rarely require changing code.

---

### Event-Driven Communication

Systems communicate using Signals.

Managers should not directly modify each other's internal state.

Example:

```text id="signal_flow"
DiceManager

↓

dice_rolled

↓

TurnManager

↓

PlayerManager

↓

BoardManager
```

---

### Loose Coupling

Gameplay systems should know as little as possible about one another.

Dependencies should remain minimal.

---

### High Cohesion

Every script should solve one well-defined problem.

Avoid creating "God Objects."

---

# 3. Project Folder Structure

Recommended structure:

```text id="folder_structure"
project/

├── assets/
│   ├── audio/
│   ├── fonts/
│   ├── icons/
│   ├── sprites/
│   └── themes/
│
├── data/
│   ├── kingdoms/
│   ├── events/
│   ├── tiles/
│   ├── relics/
│   └── configs/
│
├── scenes/
│   ├── board/
│   ├── gameplay/
│   ├── ui/
│   ├── menus/
│   └── common/
│
├── scripts/
│   ├── managers/
│   ├── gameplay/
│   ├── resources/
│   ├── ui/
│   └── utilities/
│
└── saves/
```

---

# 4. Manager Architecture

Version 1 contains the following core managers.

| Manager          | Responsibility    |
| ---------------- | ----------------- |
| GameManager      | Global game state |
| TurnManager      | Turn order        |
| BoardManager     | Board and tiles   |
| PlayerManager    | Player data       |
| DiceManager      | Dice logic        |
| EconomyManager   | Resources         |
| BattleManager    | Combat            |
| EventManager     | Events            |
| VelirAramManager | Ancient ruins     |
| AIManager        | AI decisions      |
| SaveManager      | Save/Load         |
| AudioManager     | Audio             |
| UIManager        | Interface         |

Managers communicate through signals rather than direct references.

---

# 5. Scene Hierarchy

Gameplay Scene

```text id="scene_tree"
Gameplay

├── Managers
├── Board
├── Players
├── UI
├── Audio
└── Camera
```

Each child scene remains independently testable.

---

# 6. Resource Architecture

Every configurable object exists as a Godot Resource.

Examples:

* KingdomData
* TileData
* BoardData
* EventData
* CommanderData
* BattleConfig
* EconomyConfig
* AIPersonalityData

Resources contain configuration only.

Runtime state is stored elsewhere.

---

# 7. Runtime Data Flow

```text id="runtime_flow"
Resources

↓

Managers

↓

Gameplay State

↓

UI

↓

Save System
```

Static data should never be modified during gameplay.

---

# 8. Signal Architecture

Example gameplay sequence.

```text id="signal_example"
Roll Dice

↓

dice_rolled

↓

player_moved

↓

tile_resolved

↓

resource_changed

↓

hud_updated
```

Signals should replace unnecessary direct method calls.

---

# 9. State Management

Primary game states:

* Boot
* Main Menu
* Loading
* Gameplay
* Pause
* Victory
* Statistics

Only one global state may be active at a time.

---

# 10. Performance Targets

| Metric           | Target   |
| ---------------- | -------- |
| FPS              | 60       |
| Initial Load     | < 5 s    |
| Scene Transition | < 1 s    |
| Autosave         | < 250 ms |
| AI Turn          | < 5 s    |

Performance should remain stable on mid-range Android devices.

---

# 11. Error Handling

Every manager should:

* Validate inputs.
* Log recoverable errors.
* Fail gracefully.
* Avoid crashing the game.

User-facing error messages should remain simple.

---

# 12. Coding Standards

All scripts must:

* Use Typed GDScript.
* Follow consistent naming.
* Include documentation.
* Avoid duplicated code.
* Prefer composition over inheritance.
* Use exported variables for configuration.

---

# 13. Dependency Rules

Allowed:

Manager → Resource

Manager → Signal

Manager → Utility

Not Allowed:

Manager → UI internals

BoardManager → Economy calculations

BattleManager → Save file writing

Managers should collaborate, not control one another.

---

# 14. Testing Strategy

Every gameplay system requires:

* Unit Tests
* Integration Tests
* Regression Tests
* Edge Case Tests

Every new feature should include test coverage before completion.

---

# 15. Logging

Development builds should log:

* Turn progression
* Battle results
* AI decisions
* Save operations
* Event resolution

Release builds should disable verbose logging.

---

# 16. Build Targets

Primary Platform

Android

Future Targets

* iOS
* Steam
* Nintendo Switch (Evaluation)
* Web (Prototype)

Platform-specific code should remain isolated.

---

# 17. Codex Implementation Notes

Codex should:

* Build one manager at a time.
* Write reusable code.
* Never hardcode gameplay values.
* Prefer Resources over constants.
* Use Signals for communication.
* Keep files under manageable size.
* Document every public method.

When uncertain, preserve modularity over convenience.

---

# 18. Future Expansion

The architecture is designed to support:

* Online Multiplayer
* Live Events
* DLC Content
* Additional Kingdoms
* Campaign Mode
* Cloud Saves
* Mod Support (Long-term)
* Analytics
* Cross-platform synchronization

No future feature should require rewriting the core architecture.

---

# 19. Design Principle

A well-designed architecture should make adding new gameplay systems straightforward.

The goal is not only to build Project Velir Version 1, but to establish a foundation capable of supporting years of future development while remaining understandable to both human developers and AI coding assistants.

---

**Document ID:** PV-017

**Version:** 1.0

**Status:** Complete
