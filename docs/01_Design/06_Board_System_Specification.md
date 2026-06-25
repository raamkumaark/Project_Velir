---
Document ID: PV-006
Document Name: Board System Specification
Project: Project Velir
Version: 1.0
Status: Draft
Owner: Game Director

Related Documents:
- PV-002 Master Game Specification
- PV-004 Core Gameplay Loop
- PV-005 Gameplay Systems

Last Updated: June 2026
---

# 06 - Board System Specification

> "The board is the battlefield where kingdoms compete for the future of Tamilakam."

---

# Purpose

The Board System is the foundation of Project Velir.

It defines:

- Player movement
- Tile locations
- Kingdom regions
- Strategic positioning
- Velir Aram access
- Resource distribution

Every match is played on the same board.

The board remains static.

Gameplay becomes dynamic through player interaction.

---

# Design Goals

The board should be:

✔ Easy to understand

✔ Beautiful

✔ Historically inspired

✔ Strategically balanced

✔ Mobile friendly

✔ Replayable

---

# Board Overview

The board consists of five major regions.

```
             CHERA

      ■ ■ ■ ■ ■ ■ ■

   ■                 ■

PALLAVA     VELIR ARAM     CHOLA

   ■                 ■

      ■ ■ ■ ■ ■ ■ ■

             PANDYA
```

The four kingdoms surround the ancient ruins of Velir Aram.

---

# Board Components

The board contains:

- 48 Perimeter Tiles
- 4 Kingdom Gates
- 4 Velir Gates
- 1 Central Region
- 5 Ancient Sites

---

# Tile Numbering

Tiles are numbered clockwise.

```
0 → 47
```

Example

```
      44 45 46 47

40              0

39    CENTER    1

38              2

34 33 32 31
```

Tile numbering never changes.

---

# Kingdom Regions

Each kingdom controls one corner.

| Kingdom | Starting Tile |
|----------|--------------|
| Chola | 0 |
| Pandya | 12 |
| Pallava | 24 |
| Chera | 36 |

These remain fixed.

---

# Region Identity

Each region contains unique artwork.

Gameplay remains balanced.

Visual differences include:

- Architecture
- Banner
- Vegetation
- Stone color

Mechanics remain identical.

---

# Board Zones

The board is divided into:

Kingdom Region

↓

Neutral Region

↓

Trade Region

↓

Velir Gate

↓

Ancient Route

↓

Repeat

This creates a natural gameplay rhythm.

---

# Tile Categories

Version 1 includes:

Trade

Temple

Village

Market

Battle

Event

Tax

Harbor

Ancient Site

Velir Gate

Neutral

---

# Tile Distribution

Recommended layout

| Tile | Count |
|------|------|
| Trade | 8 |
| Village | 6 |
| Temple | 4 |
| Market | 4 |
| Event | 8 |
| Battle | 6 |
| Harbor | 4 |
| Tax | 4 |
| Velir Gate | 4 |

Total

48 Tiles

This distribution will be balanced during testing.

---

# Tile Size

Logical Size

128 × 128

Actual rendered size depends on screen resolution.

---

# Movement Rules

Players always move clockwise.

Movement equals:

Dice Result

Player stops immediately after movement.

Landing tile activates automatically.

---

# Passing Tiles

Version 1

Passing a tile produces no effect.

Only the destination tile activates.

Future versions may introduce:

- Pass Bonuses
- Trade Routes
- Toll Gates

---

# Tile Ownership

Most tiles remain neutral.

Only selected locations can become controlled.

Examples

Ancient Sites

Trade Posts

Future Forts

Version 1 does not include territory capture.

---

# Velir Gates

There are four entrances.

One near each kingdom.

Players must land on a Velir Gate to enter Velir Aram.

---

# Central Region

Velir Aram occupies the center.

Contains:

Hall of Kings

Lost Library

Merchant Archives

Warrior Necropolis

Sacred Reservoir

These are represented as separate interactive nodes.

---

# Board Generation

Version 1 uses:

Static Board

No procedural generation.

Future versions may introduce:

Random tile layouts

Seasonal boards

Campaign boards

---

# Visual Style

Board resembles:

An engraved stone map.

Materials

Granite

Bronze

Sandstone

Temple carvings

Palm leaf motifs

No modern visual elements.

---

# User Interaction

Players may:

Tap tiles

View tile information

Highlight destinations

Zoom (future)

Rotate (not supported)

---

# Camera

Fixed Orthographic Camera.

Portrait Orientation.

No manual camera controls.

Camera movement only occurs during:

- Match Start
- Victory
- Velir Aram Entry

---

# Board State

Each tile stores:

Tile ID

Tile Type

Current Occupant

Owner

Reward

Penalty

Enabled

Visited

---

# Data Structure

TileData Resource

```
Tile ID

Tile Name

Tile Type

Description

Reward

Penalty

Sprite

Icon
```

BoardData Resource

```
Board Name

Tile List

Kingdom Positions

Velir Gate Positions

Ancient Sites
```

---

# Signals

BoardManager

```
board_generated

player_entered_tile

player_left_tile

tile_resolved

board_reset
```

---

# Performance Goals

Board generation

< 500 ms

Tile lookup

O(1)

Movement

60 FPS

Memory

Minimal allocations

---

# Edge Cases

Player lands exactly on Velir Gate.

Player lands on occupied Battle Tile.

Player resumes after loading save.

Player reaches victory during tile resolution.

Multiple events trigger simultaneously.

These must be handled deterministically.

---

# Testing Checklist

□ Board loads correctly.

□ 48 tiles created.

□ Tile numbering correct.

□ Kingdom positions correct.

□ Velir Gates functional.

□ Movement wraps correctly.

□ Tile lookup correct.

□ Save restores board state.

---

# Codex Implementation Notes

BoardManager should:

Generate board from BoardData.

Never hardcode tile positions.

Support future board themes.

Support future procedural boards.

Keep Board independent from TurnManager.

BoardManager only manages:

- Tiles
- Positions
- Movement lookup

Gameplay logic belongs elsewhere.

---

# Future Expansion

Future board features:

- Seasonal Boards

- River Crossings

- Mountain Passes

- Dynamic Trade Routes

- Weather Zones

- Hidden Paths

- Campaign Maps

- Multiple Board Sizes

---

# Final Principle

The board should feel like a living representation of ancient Tamilakam.

Players should recognize strategic locations instantly while continuously discovering new opportunities as the match evolves.

---

## End of Document

Document ID: PV-006

Version: 1.0

Status: Complete
