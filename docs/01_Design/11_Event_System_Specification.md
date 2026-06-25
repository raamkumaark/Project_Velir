# PV-011 — Event System Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Game Director

**Related Documents**

* PV-002 Master Game Specification
* PV-005 Gameplay Systems
* PV-006 Board System Specification
* PV-008 Velir Aram System Specification
* PV-010 Economy System Specification

**Last Updated:** June 2026

---

# 1. Purpose

The Event System introduces uncertainty, narrative, and replayability into Project Velir.

Rather than relying solely on player interaction, events simulate the political, economic, military, cultural, and environmental changes that shaped ancient Tamilakam.

Events should create memorable stories without making players feel powerless.

---

# 2. Design Philosophy

The Event System follows four principles:

* Every event tells a story.
* Events should influence strategy, not replace it.
* Positive and negative outcomes should remain balanced.
* Players should adapt rather than feel punished.

Events exist to change the current situation, not decide the winner.

---

# 3. Event Categories

Version 1 contains six event categories.

| Category  | Primary Effect |
| --------- | -------------- |
| Economic  | Gold           |
| Military  | Army           |
| Political | Influence      |
| Cultural  | Prestige       |
| Natural   | Mixed          |
| Ancient   | Velir Aram     |

Each category has its own artwork and event pool.

---

# 4. Event Trigger

Events occur when a player:

* Lands on an Event Tile.
* Explores Velir Aram.
* Activates a Special Tile.
* Completes a future objective.

Only one event resolves at a time.

---

# 5. Event Resolution Flow

```text
Player Lands on Event Tile
          ↓
Random Event Selected
          ↓
Display Event Card
          ↓
Apply Effects
          ↓
Update Resources
          ↓
Continue Turn
```

The entire process should complete within a few seconds.

---

# 6. Economic Events

Examples:

### Roman Merchant Caravan

Effect

+40 Gold

---

### Trade Boom

Effect

Gain bonus Gold from the next Trade Tile.

---

### Lost Treasure

Effect

Receive immediate Gold reward.

---

### Tax Revolt

Effect

Lose Gold.

---

# 7. Military Events

Examples:

### Veteran Warriors

Effect

Gain Army.

---

### Border Raid

Effect

Lose Army.

---

### Mercenary Camp

Effect

Recruit additional soldiers.

---

### Desertion

Effect

Army decreases.

---

# 8. Political Events

Examples:

### Royal Marriage

Effect

Gain Influence.

---

### Diplomatic Envoy

Effect

Influence increases.

---

### Noble Rebellion

Effect

Influence decreases.

---

### Council Dispute

Effect

Temporary political penalty.

---

# 9. Cultural Events

Examples:

### Temple Festival

Effect

Gain Prestige.

---

### Sangam Assembly

Effect

Prestige increases.

---

### Royal Donation

Effect

Influence and Prestige increase.

---

### Literary Celebration

Effect

Receive cultural reward.

---

# 10. Natural Events

Examples:

### Good Harvest

Gain Gold.

---

### Flood

Lose Gold.

---

### Drought

Reduced economic reward.

---

### Cyclone

Temporary movement penalty (Future).

Natural events affect every kingdom equally whenever appropriate.

---

# 11. Ancient Events

Exclusive to Velir Aram.

Examples:

* Hidden Chamber
* Forgotten Treasury
* Ancient Curse
* Sacred Inscription
* Guardian Awakens

Ancient Events generally offer greater rewards alongside greater risks.

---

# 12. Event Card Structure

Every Event Card contains:

* Event ID
* Title
* Category
* Description
* Artwork
* Reward
* Penalty
* Probability
* Flavor Text

Cards should be readable within a few seconds.

---

# 13. Event Probability

Events use weighted random selection.

Example:

| Rarity    | Probability |
| --------- | ----------: |
| Common    |         60% |
| Uncommon  |         25% |
| Rare      |         10% |
| Legendary |          5% |

Legendary events should feel exciting and memorable.

---

# 14. Event Deck

Each category maintains an independent deck.

Example

```text
Economic Deck

↓

Military Deck

↓

Political Deck

↓

Cultural Deck

↓

Natural Deck

↓

Ancient Deck
```

Future updates may expand each deck independently.

---

# 15. Runtime Data

EventManager tracks:

* Triggered Events
* Active Event
* Remaining Deck
* Event History
* Event Statistics

This information supports save/load and future balancing.

---

# 16. Data Resources

## EventData

Stores:

* Event ID
* Event Name
* Category
* Description
* Artwork
* Reward
* Penalty
* Probability
* Flavor Text

---

## EventDeckData

Stores:

* Deck Name
* Event List
* Selection Rules
* Shuffle Rules

Every event should be data-driven.

---

# 17. Signals

EventManager exposes:

* event_triggered
* event_displayed
* event_resolved
* reward_applied
* penalty_applied
* deck_shuffled

Other managers should react through these signals.

---

# 18. AI Behaviour

AI experiences the same events as human players.

AI must:

* Apply rewards.
* Apply penalties.
* Adapt strategy.
* Never receive special event treatment.

The AI should never know upcoming events.

---

# 19. Edge Cases

The Event System must correctly handle:

* Empty event decks.
* Consecutive identical events.
* Save/load during event resolution.
* Multiple rewards.
* Multiple penalties.
* Event chains.

All event outcomes must remain deterministic.

---

# 20. Performance Requirements

Event Selection

< 10 ms

Event Display

< 2 seconds

Animation

Skippable

Frame Rate

60 FPS

---

# 21. Testing Checklist

The following tests must pass:

* Event triggers correctly.
* Correct deck selected.
* Weighted probability functions.
* Rewards applied.
* Penalties applied.
* Ancient events trigger only inside Velir Aram.
* Save/load restores event state.
* AI resolves events correctly.

---

# 22. Codex Implementation Notes

Create a dedicated **EventManager**.

Responsibilities:

* Load EventDeckData.
* Select events using weighted randomness.
* Display Event Cards.
* Apply rewards and penalties.
* Maintain event history.
* Notify other systems through signals.

Do not embed event logic inside BoardManager or TurnManager.

---

# 23. Future Expansion

Future versions may include:

* Multi-turn Events
* Seasonal Festivals
* Kingdom-specific Events
* Story Events
* Cooperative Events
* World Events
* Event Chains
* Player Choice Events
* Community Events
* Limited-Time Events

The Event System should remain modular so new event categories can be added without modifying existing gameplay logic.

---

# 24. Design Principle

Events should make every match feel unique.

Players should remember the stories created by unexpected discoveries, political upheavals, military triumphs, and ancient mysteries long after the match ends.

Randomness should create memorable moments—not unfair outcomes.

---

**Document ID:** PV-011

**Version:** 1.0

**Status:** Complete
