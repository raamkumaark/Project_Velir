---
Document ID: PV-004
Document Name: Core Gameplay Loop
Project: Project Velir
Version: 1.0
Status: Draft
Owner: Game Director

Related Documents:
- PV-000 Project Vision
- PV-001 AI Constitution
- PV-002 Master Game Specification
- PV-003 Game Pillars

Last Updated: June 2026
---

# 04 - Core Gameplay Loop

> "Every turn should be fast, meaningful, and leave the player eager for the next one."

---

# Purpose

This document defines the complete gameplay flow of Project Velir.

It explains exactly what happens:

- When the game starts
- During a match
- During every turn
- During every player action
- When the match ends

This document serves as the blueprint for implementing GameManager, TurnManager, PlayerManager, and related gameplay systems.

---

# Design Objectives

The gameplay loop should:

- Be easy to understand
- Keep players engaged
- Minimize waiting time
- Encourage strategic decisions
- Support both Human and AI players
- Keep matches under 20 minutes

---

# High-Level Gameplay Loop

```
Launch Game
      ↓
Main Menu
      ↓
Create Match
      ↓
Choose Kingdom
      ↓
Initialize Match
      ↓
Gameplay Loop
      ↓
Victory
      ↓
Statistics
      ↓
Main Menu
```

---

# Match Initialization

When a new game begins, the following steps occur.

## Step 1

Load Player Settings

- Audio
- Graphics
- Language
- Accessibility

---

## Step 2

Generate Match

- Generate board
- Load kingdom data
- Create players
- Initialize resources

---

## Step 3

Assign Kingdoms

Each player receives:

- Kingdom
- Commander
- Color
- Banner
- Starting resources

---

## Step 4

Determine Turn Order

Randomly select the first player.

Subsequent turns proceed clockwise.

---

## Step 5

Start Round One

Display:

"Round 1"

Begin first player's turn.

---

# Match Loop

The game repeats the following sequence until a victory condition is met.

```
Round

↓

Player Turn

↓

Player Actions

↓

Next Player

↓

End of Round

↓

Repeat
```

---

# Round Structure

A round consists of one turn for every active kingdom.

Example

```
Round 5

↓

Chola

↓

Pandya

↓

Chera

↓

Pallava

↓

Round Complete
```

After the final kingdom acts:

- Passive income
- Event updates
- Victory check

---

# Player Turn

Every player's turn follows six phases.

```
Start Turn

↓

Roll Dice

↓

Move

↓

Resolve Tile

↓

Optional Actions

↓

End Turn
```

Every turn should take approximately 20–40 seconds.

---

# Phase 1 — Start Turn

Objectives

- Highlight active kingdom
- Focus camera
- Display HUD
- Enable Roll button

Player cannot perform actions before this phase completes.

---

# Phase 2 — Roll Dice

Player presses:

ROLL

Dice animation begins.

Random value generated.

Movement value locked.

Player cannot reroll.

---

# Phase 3 — Movement

The kingdom token moves tile by tile.

Movement should:

- Be smooth
- Be readable
- Trigger sound effects
- Highlight destination

Movement cannot be interrupted.

---

# Phase 4 — Tile Resolution

Landing tile activates immediately.

Examples

- Gain Gold
- Recruit Army
- Draw Event
- Trigger Battle
- Enter Velir Aram

Only one tile activates each turn.

---

# Phase 5 — Optional Actions

Depending on the current tile or game state, the player may:

- Recruit Army
- Spend Gold
- Enter Velir Aram
- Accept or decline an event
- View Kingdom information

Version 1 intentionally keeps this phase short.

---

# Phase 6 — End Turn

Perform:

- Autosave
- Update Resources
- Check Victory
- Pass turn to next kingdom

Turn ends.

---

# End of Round

After every kingdom completes its turn:

Update:

- Passive Income
- Temporary Effects
- Event Timers
- Round Counter

Then begin the next round.

---

# Match End

The match ends immediately when:

- Prestige reaches target
- Last kingdom remains

Display:

Victory Screen

↓

Statistics

↓

Play Again

or

Main Menu

---

# Player Decisions

Every turn should contain meaningful choices.

Examples

Spend Gold now?

Recruit Army?

Save resources?

Enter Velir Aram?

Prepare for battle?

Attack later?

The game should never play itself.

---

# Downtime

Waiting should be minimized.

Target waiting time

Less than 15 seconds

AI turns should complete quickly.

Animations should remain brief.

---

# Player Feedback

Every important action produces feedback.

Visual

- Highlight
- Animation
- Resource popup

Audio

- Dice
- Gold
- Battle
- Event

Haptic (Future)

- Dice
- Victory
- Battle

---

# Core Gameplay Formula

Project Velir follows this philosophy.

```
Random Opportunity

+

Player Decision

=

Outcome
```

Luck creates situations.

Players create victories.

---

# Game States

The game operates in one active state at a time.

```
Main Menu

↓

Loading

↓

Playing

↓

Paused

↓

Victory

↓

Statistics
```

No two gameplay states should overlap.

---

# State Diagram

```
Launch

↓

Main Menu

↓

Loading

↓

Gameplay

↓

Pause

↓

Gameplay

↓

Victory

↓

Statistics

↓

Main Menu
```

---

# Manager Responsibilities

## GameManager

Responsible for:

- Overall game state
- Match initialization
- Victory detection

---

## TurnManager

Responsible for:

- Turn order
- Round progression
- Active player

---

## PlayerManager

Responsible for:

- Player data
- Resources
- Kingdom information

---

## DiceManager

Responsible for:

- Dice animation
- Random number generation
- Dice results

---

## BoardManager

Responsible for:

- Tile layout
- Movement
- Tile lookup

---

## EventManager

Responsible for:

- Event cards
- Event queue
- Event resolution

---

## BattleManager

Responsible for:

- Battle calculation
- Rewards
- Penalties

---

# Signals

Recommended signals.

GameManager

```
game_started

game_paused

game_finished
```

TurnManager

```
turn_started

turn_finished

round_started

round_finished
```

DiceManager

```
dice_rolled
```

BoardManager

```
player_moved

tile_entered
```

BattleManager

```
battle_started

battle_finished
```

---

# Performance Goals

Average turn

20–40 seconds

Match duration

15–20 minutes

Frame rate

60 FPS

Loading

< 5 seconds

---

# Codex Notes

When implementing this system:

- Never skip gameplay phases.
- Never allow player input during movement.
- Keep managers independent.
- Use Signals.
- Avoid hardcoded player counts.
- Support future multiplayer.

---

# Acceptance Criteria

The Core Gameplay Loop is complete when:

✅ Match initializes correctly.

✅ Turn order functions correctly.

✅ Dice controls movement.

✅ Tiles resolve automatically.

✅ Resources update immediately.

✅ AI completes turns correctly.

✅ Victory conditions end the match.

✅ Autosave functions after every turn.

---

# Future Expansion

Future versions may include:

- Simultaneous turns (Multiplayer)
- Time-limited turns
- Replay system
- Turn history
- Spectator mode
- Campaign-specific gameplay loops

These systems should integrate without replacing the existing gameplay loop.

---

# Final Principle

Every turn should leave the player thinking:

> "Just one more turn."

That feeling is the foundation of Project Velir's gameplay.

---

## End of Document

Document ID: PV-004

Version: 1.0

Status: Complete
