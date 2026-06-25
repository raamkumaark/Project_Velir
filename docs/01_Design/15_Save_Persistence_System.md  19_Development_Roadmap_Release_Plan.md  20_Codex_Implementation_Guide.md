# PV-015 — Save & Persistence System Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Game Director

**Related Documents**

* PV-002 Master Game Specification
* PV-004 Core Gameplay Loop
* PV-006 Board System Specification
* PV-007 Kingdom System Specification
* PV-012 AI System Specification

**Last Updated:** June 2026

---

# 1. Purpose

The Save & Persistence System ensures that every Project Velir match can be safely paused, resumed, and restored without losing progress.

The system must guarantee that the loaded game exactly matches the saved game state.

Saving should be invisible to players and should never interrupt gameplay.

---

# 2. Design Philosophy

The Save System follows five principles.

### Reliable

Player progress must never be lost.

---

### Fast

Saving should occur instantly without noticeable delay.

---

### Automatic

The game should protect player progress using autosaves.

---

### Transparent

Players should understand when the game has been saved.

---

### Future-Proof

Save files should support future game versions through versioning and migration.

---

# 3. Save Types

Project Velir supports three save methods.

## Autosave

Automatically created during gameplay.

Triggers include:

* End of Turn
* End of Round
* Before entering Velir Aram
* Before Battles
* Before Major Events

Autosave always overwrites the previous autosave.

---

## Manual Save

Players may create save files from the Pause Menu.

Multiple save slots are supported.

---

## Quick Save (Future)

Reserved for desktop platforms.

Not included in Version 1.

---

# 4. Save Flow

```text id="save_flow"
Player Action
        ↓
Prepare Save Data
        ↓
Serialize Data
        ↓
Write JSON File
        ↓
Verify Save
        ↓
Display Save Icon
```

The save process should complete without interrupting gameplay.

---

# 5. Load Flow

```text id="load_flow"
Select Save
        ↓
Read Save File
        ↓
Validate Version
        ↓
Deserialize Data
        ↓
Restore Managers
        ↓
Resume Match
```

The restored game must be identical to the original state.

---

# 6. Save File Contents

Every save contains:

## Match Information

* Match ID
* Save Version
* Timestamp
* Difficulty
* Random Seed

---

## Player Information

For every kingdom:

* Position
* Gold
* Army
* Influence
* Prestige
* Commander
* Passive Effects

---

## Board Information

* Tile Ownership
* Ancient Site Control
* Event Queue
* Current Round
* Current Turn

---

## Runtime Systems

* Active Events
* AI State
* Economy State
* Battle State (if applicable)

---

## Player Settings

* Audio
* Language
* Accessibility
* Display Options

---

# 7. Save File Structure

Example:

```json
{
  "version": "1.0",
  "match_id": "PV2026-001",
  "round": 8,
  "current_player": "Chola",
  "players": [],
  "board": {},
  "economy": {},
  "events": {},
  "ai": {}
}
```

JSON is used for readability and debugging.

---

# 8. Save Versioning

Each save file contains:

* Save Version
* Game Version

Example

```text id="versioning"
Save Version : 1.0
Game Version : 1.0
```

Future updates should migrate older save files whenever possible.

---

# 9. Serialization

Only runtime state should be serialized.

Static Resources remain external.

Examples:

Serialize:

* Gold
* Army
* Tile Ownership
* AI State

Do Not Serialize:

* Artwork
* Icons
* Audio Files
* Static Kingdom Data

---

# 10. Runtime Managers

Each manager is responsible for saving its own state.

| Manager        | Saved Data    |
| -------------- | ------------- |
| GameManager    | Match State   |
| TurnManager    | Round & Turn  |
| PlayerManager  | Player Data   |
| BoardManager   | Tile State    |
| EconomyManager | Resources     |
| EventManager   | Event Queue   |
| BattleManager  | Active Battle |
| AIManager      | AI Runtime    |

---

# 11. Save Validation

Before loading, verify:

* Save Version
* Required Fields
* Resource Integrity
* Data Types
* Checksum (Future)

Invalid save files should never crash the game.

---

# 12. Autosave Rules

Autosave occurs:

✔ End Turn

✔ End Round

✔ Before Battle

✔ Before Ancient Exploration

Autosave should never occur during animations.

---

# 13. Error Recovery

If saving fails:

* Keep previous save.
* Notify player.
* Retry automatically.

If loading fails:

* Display error.
* Return to Main Menu.
* Preserve existing save files.

---

# 14. Runtime State

SaveManager tracks:

* Active Save Slot
* Autosave Timestamp
* Save Status
* Last Successful Save
* Current Save Version

---

# 15. Data Resources

## SaveMetadata

Stores:

* Save Version
* Creation Time
* Play Time
* Match Name
* Screenshot (Future)

---

## SaveSlot

Stores:

* Slot Number
* File Path
* Metadata
* Last Modified

---

# 16. Signals

SaveManager exposes:

* save_started
* save_completed
* save_failed
* load_started
* load_completed
* load_failed

Other systems should pause updates while save/load operations occur.

---

# 17. Performance Requirements

Autosave

< 250 ms

Manual Save

< 500 ms

Load Time

< 2 seconds

Target File Size

< 250 KB

Saving should never reduce frame rate noticeably.

---

# 18. Edge Cases

The Save System must correctly handle:

* Save during AI Turn.
* Save during Battle.
* Save after Event.
* Application closed unexpectedly.
* Corrupted save file.
* Future version migration.

Recovery should always preserve player progress where possible.

---

# 19. Testing Checklist

The following tests must pass:

* Autosave functions.
* Manual Save functions.
* Load restores exact match.
* AI state restored.
* Board restored.
* Economy restored.
* Event queue restored.
* Version validation works.
* Invalid saves handled safely.

---

# 20. Codex Implementation Notes

Create a dedicated **SaveManager**.

Responsibilities:

* Serialize runtime state.
* Deserialize save files.
* Coordinate manager restoration.
* Handle version migration.
* Manage save slots.

Each gameplay manager should expose:

```gdscript
save_state()

load_state(data)
```

SaveManager orchestrates the process but does not directly manipulate gameplay logic.

---

# 21. Future Expansion

Future persistence features may include:

* Cloud Saves
* Google Play Games synchronization
* Steam Cloud
* Cross-platform progression
* Match Replay System
* Save History
* Undo System
* Replay Timeline
* Automatic Backup Saves

The architecture should support these additions without changing the core save workflow.

---

# 22. Design Principle

Saving should feel effortless and trustworthy.

Players should never worry about losing progress, whether they close the app intentionally or receive a phone call during a match.

The Save System should quietly protect the player's kingdom at all times.

---

**Document ID:** PV-015

**Version:** 1.0

**Status:** Complete
