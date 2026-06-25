# PV-008 — Velir Aram System Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Game Director

**Related Documents**

* PV-002 Master Game Specification
* PV-006 Board System Specification
* PV-007 Kingdom System Specification

**Last Updated:** June 2026

---

# 1. Purpose

Velir Aram is the heart of Project Velir.

It is the mysterious ancient civilization located at the center of the game board.

Unlike kingdom territories, Velir Aram belongs to no ruler.

It represents the greatest opportunity, the greatest danger, and the primary source of prestige during the late stages of every match.

---

# 2. Design Philosophy

Velir Aram exists to encourage players to leave the safety of their kingdom.

Players must decide whether to:

* Continue expanding around the board.
* Risk entering the ruins.
* Compete with rival kingdoms.
* Search for forgotten relics.

High rewards always involve higher risks.

---

# 3. Historical Inspiration

Velir Aram is inspired by the mysterious settlements that existed before the Sangam Age.

Rather than representing a known historical city, Velir Aram combines inspiration from:

* Sangam literature
* Megalithic culture
* Early Tamil settlements
* Ancient trade routes
* Archaeological discoveries

It remains intentionally mysterious.

---

# 4. Layout

Velir Aram occupies the center of the board.

It contains five primary locations.

```
           Hall of Kings

Lost Library       Merchant Archives

Warrior Necropolis

      Sacred Reservoir
```

Each location functions as an independent gameplay node.

---

# 5. Entry System

Players cannot directly enter Velir Aram.

Entry requires landing on a Velir Gate.

Version 1 uses four gates.

Each kingdom has one nearby entrance.

---

# 6. Ancient Sites

Version 1 includes five sites.

## Hall of Kings

Primary Reward

Prestige

Description

Ancient royal assembly hall.

---

## Lost Library

Primary Reward

Influence

Description

Repository of forgotten knowledge.

---

## Merchant Archives

Primary Reward

Gold

Description

Ancient trade records and hidden wealth.

---

## Warrior Necropolis

Primary Reward

Army

Description

Sacred burial ground of legendary warriors.

---

## Sacred Reservoir

Primary Reward

Random Blessing

Description

Ancient water source believed to possess divine power.

---

# 7. Exploration

When entering Velir Aram, players explore one Ancient Site.

Possible outcomes include:

* Gain Gold
* Gain Prestige
* Gain Influence
* Recruit Army
* Trigger Ancient Event

Future versions may include puzzles and branching exploration.

---

# 8. Relics

Ancient Sites may reward relics.

Version 1 contains simple relics.

Examples

* Royal Seal
* Bronze Sword
* Palm Leaf Manuscript
* Temple Coin
* Sacred Ornament

Relics provide small passive bonuses.

---

# 9. Ancient Events

Velir Aram contains exclusive event cards.

Examples

* Hidden Chamber
* Ancient Curse
* Forgotten Treasury
* Guardian Statue
* Sacred Festival

These events cannot occur outside Velir Aram.

---

# 10. Site Control

Ancient Sites are temporarily controlled by the last kingdom to successfully explore them.

Control provides ongoing bonuses until another kingdom claims the site.

Ownership is never permanent.

---

# 11. Strategic Importance

Velir Aram offers:

* Highest Prestige rewards.
* Rare relics.
* Powerful events.
* Resource opportunities.

Ignoring Velir Aram should be a viable strategy, but controlling it should provide meaningful advantages.

---

# 12. Risk vs Reward

Entering Velir Aram exposes players to:

* Random events
* Rival kingdoms
* Lost opportunities elsewhere on the board

Potential rewards include:

* Large Prestige gains
* Powerful relics
* Significant resource bonuses

Players must weigh these risks carefully.

---

# 13. Runtime State

Each Ancient Site tracks:

* Site ID
* Current Controller
* Discovery Status
* Remaining Reward
* Cooldown (Future)

Runtime data is saved with the match.

---

# 14. Data Resources

## AncientSiteData

Stores:

* Site Name
* Description
* Reward Type
* Reward Amount
* Icon
* Artwork

---

## RelicData

Stores:

* Relic Name
* Passive Effect
* Description
* Icon
* Rarity

---

## VelirAramData

Stores:

* Entry Gates
* Ancient Sites
* Event Deck
* Relic Pool

---

# 15. Signals

VelirAramManager exposes:

* velir_entered
* site_discovered
* relic_found
* relic_lost
* ancient_event_triggered
* site_control_changed

---

# 16. Edge Cases

The system must correctly handle:

* Multiple players entering during consecutive turns.
* Save/load inside Velir Aram.
* Site already controlled.
* Empty relic pool.
* Ancient event chains.

---

# 17. Performance Requirements

Entering Velir Aram

< 300 ms

Site Resolution

< 100 ms

Animation

< 2 seconds

---

# 18. Testing Checklist

The following tests must pass.

* Player enters through Velir Gate.
* Ancient Site activates.
* Correct reward granted.
* Relic assigned correctly.
* Ancient events trigger.
* Site control updates.
* Save and load restore state.

---

# 19. Codex Implementation Notes

Create a dedicated **VelirAramManager**.

Responsibilities include:

* Managing entry.
* Loading AncientSiteData.
* Assigning relics.
* Triggering Ancient Events.
* Tracking site ownership.

Do not place Velir Aram logic inside BoardManager.

Velir Aram should function as an independent gameplay subsystem.

---

# 20. Future Expansion

Future updates may introduce:

* Underground chambers
* Hidden passages
* Multi-stage expeditions
* Ancient guardians
* Cooperative exploration
* Story-driven discoveries
* Legendary relic collections
* Seasonal archaeological expeditions

The architecture should support these features without altering the existing exploration framework.

---

# 21. Design Principle

Velir Aram should feel mysterious, valuable, and dangerous.

Every visit should create memorable stories and strategic decisions rather than predictable rewards.

Players should never know exactly what awaits them beneath the forgotten ruins.

---

**Document ID:** PV-008

**Version:** 1.0

**Status:** Complete
