# PV-007 — Kingdom System Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Game Director

**Related Documents**

* PV-002 Master Game Specification
* PV-005 Gameplay Systems
* PV-006 Board System Specification

**Last Updated:** June 2026

---

# 1. Purpose

The Kingdom System defines the four playable civilizations of Project Velir.

A kingdom is more than a visual skin. It determines:

* Player identity
* Passive abilities
* AI behavior
* Theme and aesthetics
* Commander assignment
* Strategic playstyle

All kingdoms are balanced to ensure no kingdom has an inherent advantage over another.

---

# 2. Design Philosophy

Each kingdom should feel unique without changing the core rules of the game.

The differences between kingdoms should encourage different strategies rather than create stronger or weaker factions.

The guiding principle is:

> **Different Playstyle. Equal Strength.**

---

# 3. Playable Kingdoms

Version 1 includes four major Tamil kingdoms.

| Kingdom | Identity          | Primary Strength |
| ------- | ----------------- | ---------------- |
| Chola   | Maritime Empire   | Expansion        |
| Chera   | Trade Kingdom     | Economy          |
| Pandya  | Cultural Kingdom  | Prestige         |
| Pallava | Knowledge Kingdom | Defense          |

Each kingdom has a unique visual identity and passive ability.

---

# 4. Historical Inspiration

The game is inspired by history but is **not** a historical simulation.

The kingdoms represent the spirit of ancient Tamilakam while allowing balanced and enjoyable gameplay.

Historical inspiration includes:

* Sangam literature
* Ancient Tamil trade
* Temple architecture
* Kingdom rivalries
* Maritime influence
* Cultural achievements

Gameplay always takes priority over historical accuracy.

---

# 5. Kingdom Identity

## Chola

### Theme

Expansion and conquest.

### Characteristics

* Ambitious
* Military focused
* Maritime influence
* Aggressive growth

### Recommended Playstyle

Expand quickly and secure strategic locations before opponents.

---

## Chera

### Theme

Trade and prosperity.

### Characteristics

* Merchant culture
* Economic strength
* Diplomatic influence
* Stable development

### Recommended Playstyle

Accumulate wealth and dominate through resource management.

---

## Pandya

### Theme

Culture and prestige.

### Characteristics

* Temples
* Literature
* Festivals
* Public influence

### Recommended Playstyle

Earn Prestige efficiently while maintaining balanced growth.

---

## Pallava

### Theme

Knowledge and architecture.

### Characteristics

* Fortifications
* Scholarship
* Planning
* Defensive strategy

### Recommended Playstyle

Build a resilient kingdom capable of surviving long matches.

---

# 6. Starting Resources

Every kingdom begins with identical starting values.

| Resource  | Starting Value |
| --------- | -------------: |
| Gold      |            100 |
| Army      |             20 |
| Influence |             10 |
| Prestige  |              0 |

Balanced starting conditions ensure fair competition.

---

# 7. Passive Abilities

Each kingdom receives one passive ability.

## Chola

**Imperial Expansion**

Gain a small Prestige bonus after winning battles.

---

## Chera

**Master Merchants**

Earn additional Gold from Trade and Market tiles.

---

## Pandya

**Patrons of Culture**

Gain bonus Prestige from Temple tiles and Cultural Events.

---

## Pallava

**Fortified Realm**

Reduce Army losses after battles.

Passive abilities should influence strategy without becoming mandatory.

---

# 8. Kingdom Colors

Each kingdom uses a dedicated color palette.

| Kingdom | Primary Color |
| ------- | ------------- |
| Chola   | Crimson Red   |
| Chera   | Emerald Green |
| Pandya  | Royal Blue    |
| Pallava | Golden Yellow |

These colors are used consistently across:

* Player Tokens
* UI
* Banners
* Notifications
* Scoreboards

---

# 9. Kingdom Banner

Each kingdom has its own banner consisting of:

* Historical-inspired emblem
* Decorative border
* Primary color
* Secondary accent
* Cloth texture

Banners are displayed in:

* Main HUD
* Turn Indicator
* Victory Screen
* Match Summary

---

# 10. Commander Assignment

Each kingdom begins with one commander.

Version 1 includes one commander per kingdom.

Future versions may introduce multiple commanders with unique abilities.

Commander responsibilities include:

* Battle bonuses
* Portrait representation
* Strategic identity

---

# 11. AI Personality

Each AI kingdom follows a preferred strategy.

| Kingdom | AI Priority |
| ------- | ----------- |
| Chola   | Expansion   |
| Chera   | Economy     |
| Pandya  | Prestige    |
| Pallava | Defense     |

AI personalities affect priorities rather than granting bonuses.

---

# 12. Kingdom Selection

Before every match, players select a kingdom.

Selection screen displays:

* Banner
* Description
* Passive Ability
* Commander Portrait
* Difficulty Recommendation

Players may also choose Random Kingdom.

---

# 13. Kingdom Progression

Version 1 does not include permanent progression.

Every match starts equally.

Future progression may include:

* Cosmetic unlocks
* Alternate banners
* Commander skins
* Historical artwork

Gameplay advantages are never tied to progression.

---

# 14. Data Resources

## KingdomData Resource

Each kingdom stores:

* Kingdom ID
* Name
* Description
* Banner
* Primary Color
* Secondary Color
* Passive Ability
* Starting Resources
* Commander Reference
* AI Personality

All kingdom information should be loaded from data resources.

---

# 15. Runtime State

During gameplay, each kingdom maintains:

* Current Gold
* Current Army
* Current Influence
* Current Prestige
* Current Position
* Controlled Ancient Sites
* Active Effects

Runtime state is stored separately from static kingdom data.

---

# 16. Signals

KingdomManager exposes:

* kingdom_selected
* kingdom_initialized
* passive_triggered
* commander_changed
* kingdom_eliminated

Other systems subscribe to these signals as required.

---

# 17. Balance Principles

Kingdom balance follows these rules:

* Equal starting resources.
* Equal victory potential.
* One passive ability only.
* No exclusive mechanics.
* No hidden bonuses.

Balance is achieved through playstyle diversity.

---

# 18. Performance Requirements

Kingdom initialization:

< 50 ms

Memory usage:

Minimal

All kingdom assets should be preloaded before match start.

---

# 19. Edge Cases

The Kingdom System must correctly handle:

* Random kingdom selection.
* Duplicate AI selections prevented.
* Save and load restoration.
* Passive ability activation.
* Match restart.

All outcomes should remain deterministic.

---

# 20. Testing Checklist

The following tests must pass:

* Four kingdoms load correctly.
* Passive abilities function.
* Starting resources are correct.
* Kingdom colors display correctly.
* Commander assignment succeeds.
* AI personalities initialize.
* Save and load preserve kingdom state.

---

# 21. Codex Implementation Notes

Create a dedicated `KingdomManager`.

Responsibilities:

* Load KingdomData resources.
* Initialize player kingdoms.
* Apply passive abilities.
* Expose runtime state.
* Notify other systems through signals.

Avoid embedding kingdom logic inside unrelated managers.

---

# 22. Future Expansion

Future updates may introduce:

* Additional Tamil dynasties
* Sri Lankan kingdoms
* Deccan kingdoms
* Campaign-exclusive factions
* Alternate commanders
* Dynasty-specific events
* Cosmetic kingdom skins

The architecture should support adding new kingdoms without modifying existing gameplay systems.

---

# 23. Design Principle

Every kingdom should feel immediately recognizable through its visual identity, strategic focus, and passive ability while remaining competitively balanced.

Players should choose kingdoms based on preferred playstyle rather than perceived strength.

---

**Document ID:** PV-007
**Version:** 1.0
**Status:** Complete
