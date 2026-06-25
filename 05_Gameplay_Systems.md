---
Document ID: PV-005
Document Name: Gameplay Systems
Project: Project Velir
Version: 1.0
Status: Draft
Owner: Game Director

Related Documents:
- PV-002 Master Game Specification
- PV-003 Game Pillars
- PV-004 Core Gameplay Loop

Last Updated: June 2026
---

# 05 - Gameplay Systems

> "Simple mechanics. Deep strategy."

---

# Purpose

This document defines the fundamental gameplay systems of Project Velir.

These systems work together to create meaningful strategic gameplay while remaining accessible to new players.

Every mechanic in the game should reinforce one or more Game Pillars.

---

# Gameplay Philosophy

Project Velir follows a layered gameplay philosophy.

```

Simple Rules
↓
Strategic Decisions
↓
Kingdom Development
↓
Political Competition
↓
Victory

```

Players should never feel overwhelmed.

Instead, complexity emerges naturally from combining multiple simple systems.

---

# Core Gameplay Systems

Version 1 consists of the following systems.

1. Movement

2. Turn System

3. Dice System

4. Resources

5. Tile Interaction

6. Battles

7. Events

8. Velir Aram

9. Prestige

Each system is independent and communicates through the Game Managers.

---

# Gameplay Cycle

Each turn follows the same structure.

```

Roll Dice

↓

Move

↓

Resolve Tile

↓

Resolve Event

↓

Optional Action

↓

End Turn

```

This cycle repeats until victory.

---

# Movement System

## Purpose

Movement determines player progression around the board.

Movement should:

- Be easy to understand.
- Feel satisfying.
- Create strategic opportunities.

---

## Rules

Players move:

Clockwise

Movement equals:

Dice Result

Movement cannot be cancelled.

Movement cannot be interrupted.

Landing position always matters.

---

## Strategic Importance

Movement determines access to:

- Resources
- Battles
- Velir Aram
- Ancient Sites
- Event Cards

Planning movement is one of the game's primary strategic elements.

---

# Resource System

Players manage four primary resources.

## Gold

Used for:

- Recruitment
- Trade
- Future Upgrades

---

## Army

Represents military strength.

Required for:

- Battles
- Defense

---

## Influence

Represents political power.

Used for:

- Diplomacy (Future)
- Kingdom Events
- Special Actions

---

## Prestige

Represents national greatness.

Primary victory resource.

---

# Tile Interaction

Every landed tile performs exactly one primary action.

Examples

Trade

Temple

Battle

Event

Village

Market

Harbor

Ancient Site

Players should immediately understand what each tile does.

---

# Battle System

Battles occur when kingdoms compete directly.

Battle Formula

```

Army

+

Commander Bonus

+

Dice

=

Battle Strength

```

Winner receives:

Prestige

Loser loses Army.

Battles should resolve quickly.

---

# Event System

Events introduce uncertainty.

Events may:

Reward

Challenge

Interrupt

Benefit

Punish

Events should encourage adaptation rather than frustration.

---

# Velir Aram

Velir Aram represents the highest-value area of the board.

Players enter to obtain:

- Ancient Relics
- Prestige
- Rare Rewards

High reward always comes with increased risk.

---

# Prestige System

Prestige represents overall kingdom success.

Prestige is earned through:

Winning Battles

Ancient Discoveries

Important Events

Temple Activities

Special Objectives

Prestige is the primary victory condition.

---

# Decision Density

Every turn should contain at least one meaningful decision.

Examples

Recruit?

Attack?

Save Gold?

Explore?

Race for Prestige?

No turn should become routine.

---

# Randomness

Randomness creates opportunities.

It should never determine victory alone.

Sources of randomness

Dice

Events

Ancient Discoveries

Player decisions should outweigh randomness over the course of a full match.

---

# Kingdom Balance

Each kingdom possesses:

One Passive Ability

One Strategic Identity

Equal Starting Resources

Equal Victory Opportunity

No kingdom should dominate every playstyle.

---

# Player Interaction

Players interact through:

Competition

Battles

Resource races

Prestige races

Velir Aram

Future diplomacy

Interaction should remain constant throughout the match.

---

# Gameplay Principles

Every mechanic must satisfy these questions.

Does it improve strategy?

Does it create decisions?

Does it increase replayability?

Does it fit the historical theme?

Does it work on mobile?

If the answer is "No", reconsider the mechanic.

---

# Gameplay Hierarchy

```

Core Loop

↓

Movement

↓

Tile

↓

Resources

↓

Strategy

↓

Victory

```

Every mechanic ultimately contributes toward Prestige.

---

# Version 1 Scope

Included

✔ Dice

✔ Board

✔ Resources

✔ Battles

✔ Events

✔ Velir Aram

✔ AI

✔ Prestige

Excluded

✘ Diplomacy

✘ Technology Trees

✘ Buildings

✘ Naval Warfare

✘ Commander Skills

✘ Kingdom Missions

---

# Codex Notes

Every gameplay system should:

Be modular.

Communicate through Signals.

Use configurable Resources.

Support Save/Load.

Avoid hardcoded values.

Remain independently testable.

---

# Acceptance Criteria

Gameplay Systems are complete when:

✅ Every turn follows the gameplay loop.

✅ Resources update correctly.

✅ Battles resolve consistently.

✅ Events trigger correctly.

✅ Prestige determines victory.

✅ Every kingdom remains balanced.

---

# Future Expansion

Future systems may include:

- Diplomacy
- Alliances
- Kingdom Technologies
- Cities
- Fortifications
- Commander Progression
- Trade Routes
- Naval Battles
- Religious Influence

These systems should extend existing mechanics rather than replace them.

---

# Final Principle

Project Velir succeeds when players feel that every decision contributes to the story of their kingdom.

Simple mechanics should combine to create complex strategic experiences.

---

## End of Document

Document ID: PV-005

Version: 1.0

Status: Complete
