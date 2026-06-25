# PV-009 — Battle System Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Game Director

**Related Documents**

* PV-002 Master Game Specification
* PV-005 Gameplay Systems
* PV-007 Kingdom System Specification
* PV-008 Velir Aram System Specification

**Last Updated:** June 2026

---

# 1. Purpose

The Battle System resolves military conflicts between kingdoms.

Battles are designed to be fast, strategic, and rewarding without becoming overly complicated.

Players should feel that preparation and resource management determine victory more than luck.

---

# 2. Design Philosophy

Battles follow three principles:

* Easy to understand.
* Difficult to master.
* Resolve quickly.

The entire battle should take less than 10 seconds while still feeling impactful.

---

# 3. Battle Types

Version 1 includes:

* Kingdom vs Kingdom
* Ancient Guardian (Velir Aram)
* Event Battles

Future versions may introduce:

* Naval Battles
* Siege Battles
* Alliance Battles
* Tournament Battles

---

# 4. Battle Triggers

A battle begins when:

* A player lands on an occupied Battle Tile.
* An Event Card initiates combat.
* A Velir Aram encounter requires combat.
* A future special ability forces combat.

Battles always pause normal board movement until resolved.

---

# 5. Battle Participants

Every battle contains:

* Attacker
* Defender

Each participant contributes:

* Army Strength
* Commander Bonus
* Passive Ability
* Dice Roll

---

# 6. Battle Flow

```text id="7t2pkq"
Battle Starts
        ↓
Load Participants
        ↓
Calculate Army Strength
        ↓
Apply Passive Bonuses
        ↓
Apply Commander Bonuses
        ↓
Roll Battle Dice
        ↓
Calculate Final Score
        ↓
Determine Winner
        ↓
Award Rewards
        ↓
Apply Penalties
        ↓
Return to Board
```

---

# 7. Battle Formula

Battle Score is calculated as:

```text id="5r9kdt"
Battle Score

=

Army Strength

+

Commander Bonus

+

Passive Bonus

+

Battle Dice
```

Highest score wins.

---

# 8. Battle Dice

Version 1 uses one D6.

Possible values:

* 1
* 2
* 3
* 4
* 5
* 6

The battle die represents battlefield uncertainty.

Army strength remains the most important factor.

---

# 9. Tie Resolution

If both kingdoms have identical Battle Scores:

The defending kingdom wins.

Reason:

* Encourages defensive planning.
* Prevents unnecessary randomness.
* Simple for players to remember.

---

# 10. Victory Rewards

Winning a battle grants:

* Prestige
* Gold
* Battle Record
* Possible Ancient Reward (Velir Aram)

Default rewards:

| Reward   | Value |
| -------- | ----: |
| Prestige |    +5 |
| Gold     |   +20 |

These values remain configurable through data resources.

---

# 11. Defeat Penalties

The defeated kingdom loses:

* Army
* Small Prestige

Example:

| Resource | Default Loss |
| -------- | -----------: |
| Army     |           -5 |
| Prestige |           -2 |

No kingdom is permanently eliminated through a single battle.

---

# 12. Commander Bonus

Each commander provides a passive combat modifier.

Example:

| Commander Type | Bonus |
| -------------- | ----: |
| Military       |    +3 |
| Balanced       |    +2 |
| Defensive      |    +2 |
| Economic       |    +1 |

Future versions may add active commander skills.

---

# 13. Kingdom Passive Effects

Passive abilities modify battle outcomes.

Examples:

### Chola

Gain +1 Battle Score when attacking.

### Chera

Receive +10 Gold after victory.

### Pandya

Gain +2 Prestige after victory.

### Pallava

Reduce Army losses by 25%.

Passive abilities should complement playstyle without determining victory.

---

# 14. Battle Animation

Battle presentation should include:

* Commander portraits
* Kingdom banners
* Dice animation
* Score calculation
* Winner announcement

Target duration:

6–8 seconds

Players may skip animations.

---

# 15. Battle UI

Display:

Left Side

* Attacker Banner
* Army
* Commander
* Passive Ability

Right Side

* Defender Banner
* Army
* Commander
* Passive Ability

Center

* Dice
* Battle Score
* Result

---

# 16. Runtime Data

BattleData stores:

* Attacker
* Defender
* Army Values
* Dice Roll
* Commander Bonus
* Passive Bonus
* Winner
* Rewards
* Timestamp

Used for:

* Statistics
* Save System
* Match History

---

# 17. Data Resources

## BattleConfig

Stores:

* Base Rewards
* Base Penalties
* Dice Rules
* Tie Rules
* Animation Duration

---

## CommanderData

Stores:

* Name
* Portrait
* Bonus
* Description

---

# 18. Signals

BattleManager exposes:

* battle_started
* battle_finished
* battle_won
* battle_lost
* battle_draw
* rewards_applied

---

# 19. AI Behaviour

AI evaluates battles before engaging.

Decision factors:

* Army Strength
* Potential Rewards
* Current Prestige
* Remaining Gold
* Risk Level

AI should avoid unwinnable battles whenever possible.

---

# 20. Edge Cases

The Battle System must correctly handle:

* Equal scores.
* Zero Army.
* Simultaneous victory conditions.
* Save during battle.
* Interrupted animations.
* Battle triggered from Event Cards.

---

# 21. Performance Requirements

Battle loading:

< 100 ms

Battle calculation:

Instant

Battle animation:

6–8 seconds

Frame Rate:

60 FPS

---

# 22. Testing Checklist

The following tests must pass:

* Battles trigger correctly.
* Army values update.
* Commander bonuses apply.
* Passive abilities function.
* Dice rolls correctly.
* Tie rule works.
* Rewards apply.
* Penalties apply.
* Save/load restores battle state.

---

# 23. Codex Implementation Notes

Create a dedicated **BattleManager**.

Responsibilities:

* Initialize battles.
* Calculate Battle Score.
* Apply passive effects.
* Apply commander bonuses.
* Determine winner.
* Award rewards.
* Record battle statistics.

BattleManager must remain independent from BoardManager and TurnManager.

Use BattleConfig and CommanderData Resources for all configurable values.

---

# 24. Future Expansion

Future versions may include:

* War Elephants
* Cavalry Units
* Naval Warfare
* Siege Engines
* Terrain Advantages
* Weather Effects
* Commander Skills
* Multi-Round Battles
* Kingdom Alliances
* Heroic Events

These additions should extend the current combat framework rather than replace it.

---

# 25. Design Principle

Battles should create memorable moments without dominating the game.

Players should win because they prepared their kingdom wisely, managed resources effectively, and chose the right time to fight.

Luck should influence the battle—but never decide it alone.

---

**Document ID:** PV-009

**Version:** 1.0

**Status:** Complete
