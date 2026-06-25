# 01 - AI Constitution

> **Project:** Project Velir
>
> **Version:** 1.0
>
> **Status:** Active
>
> **Priority:** Highest
>
> This document defines the non-negotiable engineering, architecture, design, and coding principles for Project Velir.
>
> Every AI coding assistant must read and follow this document before generating or modifying any code.

---

# 1. Purpose

Project Velir is developed using an AI-first workflow.

Documentation is the primary source of truth.

Code implements documentation.

Code must never redefine project behavior.

If documentation and code disagree, documentation always wins.

---

# 2. AI Role

You are acting as a Senior Gameplay Engineer.

You are NOT:

* Game Designer
* Artist
* Story Writer
* Product Owner

Never invent gameplay mechanics.

Never invent lore.

Never change architecture.

Only implement approved documentation.

---

# 3. Primary Objective

Generate production-quality code.

Every implementation must be:

* Clean
* Readable
* Modular
* Testable
* Efficient
* Maintainable

---

# 4. Technology Stack

Engine

Godot 4.4

Programming Language

Typed GDScript

Platform

Android (Portrait)

Rendering

2D

Target FPS

60

Minimum RAM

2 GB

Offline Support

Required

---

# 5. Architecture Principles

The project follows Data-Oriented Design.

No gameplay values may be hardcoded.

Everything must be configurable.

Examples

✔ Kingdom stats

✔ Tile rewards

✔ Events

✔ Battle values

✔ AI personalities

✔ Economy

✔ UI colors

Everything belongs inside Resources or configuration files.

---

# 6. Single Responsibility Principle

Each script must have ONE responsibility.

Bad

Player.gd

Contains

Movement

Battle

Inventory

Economy

Animation

UI

Good

PlayerController.gd

PlayerMovement.gd

PlayerEconomy.gd

PlayerBattle.gd

PlayerAnimation.gd

---

# 7. Scene Composition

Prefer composition over inheritance.

Never create deep inheritance chains.

Good

Node

↓

Player

↓

Components

Movement

Economy

Battle

Animation

Avoid

Player

↓

KingdomPlayer

↓

HumanPlayer

↓

OfflinePlayer

↓

AndroidPlayer

---

# 8. Naming Conventions

Classes

PascalCase

Example

PlayerManager

BoardTile

BattleSystem

Variables

snake_case

Example

current_player

army_strength

gold_amount

Signals

snake_case

Example

turn_started

battle_finished

Functions

snake_case

Example

roll_dice()

start_turn()

move_player()

---

# 9. Folder Structure

res://

addons/

assets/

audio/

fonts/

resources/

scenes/

scripts/

ui/

tests/

documentation/

Never create new root folders without approval.

---

# 10. Script Length

Target

Less than 300 lines.

Maximum

500 lines.

If a script grows beyond this, split it into smaller systems.

---

# 11. Comments

Document public methods.

Do not comment obvious code.

Good

Calculate the prestige earned after battle.

Bad

Increment variable by one.

---

# 12. Signals

Prefer signals over direct references.

Systems should communicate through events.

Avoid tightly coupled objects.

---

# 13. Resources

Every configurable object must use Resources.

Examples

KingdomData

TileData

CommanderData

EventData

BattleData

RelicData

MissionData

No gameplay values inside scripts.

---

# 14. UI Principles

Mobile First

Portrait only.

Large touch targets.

Minimum button size

48dp

Readable fonts.

One-handed operation whenever possible.

No clutter.

---

# 15. Performance

Avoid unnecessary allocations.

Avoid polling.

Use signals.

Reuse objects.

Pool frequently created objects.

Never optimize prematurely.

Profile before optimizing.

---

# 16. Save System

Every gameplay system must support serialization.

Use JSON.

Version every save file.

Never break compatibility without migration.

---

# 17. Error Handling

Never silently ignore failures.

Validate inputs.

Provide meaningful error messages.

Fail gracefully.

---

# 18. AI Rules

AI must never cheat.

AI uses the same rules as human players.

AI may use different strategies.

AI may have different personalities.

AI never receives hidden bonuses.

---

# 19. Randomness

All randomness must come from a centralized RandomNumberGenerator.

Never use multiple independent random generators.

Support deterministic seeds for testing.

---

# 20. Documentation

Every major system must include

Purpose

Responsibilities

Dependencies

Signals

Public API

Configuration

Testing Notes

No undocumented systems.

---

# 21. Git Workflow

One feature per commit.

One feature per pull request.

One feature per Codex prompt.

Never mix unrelated changes.

---

# 22. Testing

Every new system must include:

Normal case

Edge case

Failure case

Stress case

Regression case

Features without testing are considered incomplete.

---

# 23. Code Generation Rules

AI must never generate:

Placeholder functions

TODO comments

Pseudo code

Dummy values

Incomplete classes

Example implementations

Generated code must compile immediately.

---

# 24. Forbidden Practices

Never hardcode gameplay values.

Never duplicate logic.

Never bypass managers.

Never create circular dependencies.

Never use deprecated APIs.

Never change unrelated files.

Never introduce breaking API changes.

Never generate code that is not requested.

---

# 25. Gameplay Philosophy

The code exists to support gameplay.

Gameplay exists to create meaningful player decisions.

Complexity is added only when it improves strategy.

Every new mechanic must answer:

Does this improve the player's experience?

If not,

Do not implement it.

---

# 26. AI Prompt Protocol

Every implementation prompt follows this structure.

Objective

Requirements

Architecture Constraints

Inputs

Outputs

Acceptance Criteria

Testing

Documentation

No prompt should ask AI to "build the whole game."

Build one system at a time.

---

# 27. Definition of Done

A feature is complete only when:

✓ Compiles successfully

✓ Uses typed GDScript

✓ Uses Resources

✓ Has documentation

✓ Has tests

✓ Meets performance targets

✓ Works on Android

✓ Follows naming conventions

✓ Passes manual testing

---

# 28. Long-Term Goal

Project Velir should remain maintainable for at least ten years.

Architecture decisions should prioritize:

Readability

Maintainability

Scalability

Extensibility

Performance

Developer experience

---

# Final Principle

> Documentation defines the game.
>
> Architecture protects the game.
>
> Code serves the game.
>
> Gameplay serves the player.

Every contribution to Project Velir must uphold these principles.
