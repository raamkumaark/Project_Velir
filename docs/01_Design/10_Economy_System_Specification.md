# PV-010 — Economy System Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Game Director

**Related Documents**

* PV-002 Master Game Specification
* PV-005 Gameplay Systems
* PV-007 Kingdom System Specification
* PV-009 Battle System Specification

**Last Updated:** June 2026

---

# 1. Purpose

The Economy System governs how kingdoms generate, spend, and manage wealth throughout a match.

A strong economy enables military expansion, exploration, and strategic flexibility, but it should never guarantee victory on its own.

Players should constantly choose between immediate gains and long-term investments.

---

# 2. Design Philosophy

The economy follows three principles:

* Simple to understand.
* Difficult to optimize.
* Always strategically meaningful.

Every coin earned should create an interesting decision.

---

# 3. Core Resources

The Economy System manages four primary resources.

| Resource  | Purpose             |
| --------- | ------------------- |
| Gold      | Primary currency    |
| Army      | Military strength   |
| Influence | Political authority |
| Prestige  | Victory progress    |

Although all four resources interact, Gold serves as the foundation of the economy.

---

# 4. Gold Generation

Players earn Gold through multiple sources.

### Trade Tiles

Provides consistent income.

Default Reward:

+20 Gold

---

### Market Tiles

Represents commercial activity.

Default Reward:

+30 Gold

---

### Harbor Tiles

Represents overseas maritime trade.

Default Reward:

+25 Gold

Future versions may include international trade bonuses.

---

### Tax Tiles

Represents tax collection.

Default Reward:

+15 Gold

Tax income is reliable but lower than trade.

---

### Event Cards

Economic events may provide:

* Merchant caravans
* Treasure discoveries
* Royal gifts
* Trade agreements

Reward values vary.

---

### Ancient Sites

Merchant Archives within Velir Aram provide significant economic rewards.

---

# 5. Gold Expenditure

Gold is primarily spent on:

| Action              | Default Cost |
| ------------------- | -----------: |
| Recruit Army        |      20 Gold |
| Enter Special Event |     Variable |
| Ancient Exploration |     Variable |
| Future Buildings    |     Variable |

Version 1 intentionally limits spending options.

Future updates will greatly expand economic depth.

---

# 6. Passive Income

At the end of every round, kingdoms receive passive income.

Sources include:

* Trade Routes
* Controlled Ancient Sites
* Kingdom Passive Abilities
* Future Buildings

Passive income rewards long-term planning.

---

# 7. Resource Balance

Resources should remain interconnected.

Examples:

Gold recruits Army.

Army wins Battles.

Battles earn Prestige.

Prestige wins the game.

No resource should exist independently.

---

# 8. Spending Priorities

Players constantly balance competing needs.

Example decisions:

* Recruit soldiers?
* Save for future opportunities?
* Explore Velir Aram?
* Prepare for battle?
* Wait for better timing?

There should rarely be an obvious answer.

---

# 9. Income Sources

```text
Trade

↓

Market

↓

Harbor

↓

Taxes

↓

Ancient Sites

↓

Events
```

Players should diversify income whenever possible.

---

# 10. Economic Flow

```text
Earn Gold

↓

Evaluate Situation

↓

Spend Gold

↓

Gain Strategic Advantage

↓

Earn More Resources

↓

Increase Prestige
```

The economy should reinforce the overall gameplay loop.

---

# 11. Kingdom Economic Identity

Each kingdom interacts with the economy differently.

### Chola

* Expansion-oriented
* Trade bonuses
* Fast economic growth

---

### Chera

* Merchant specialists
* Highest trading efficiency
* Stable income

---

### Pandya

* Temple-based prestige economy
* Balanced spending

---

### Pallava

* Defensive economy
* Efficient military spending
* Lower losses

Passive abilities should encourage distinct strategies without disrupting balance.

---

# 12. Runtime Data

EconomyManager tracks:

* Current Gold
* Income this Round
* Expenses this Round
* Total Lifetime Income
* Total Lifetime Spending
* Passive Income
* Resource Modifiers

This data supports statistics, achievements, and balancing.

---

# 13. Data Resources

## EconomyConfig

Stores:

* Starting Gold
* Trade Rewards
* Market Rewards
* Harbor Rewards
* Tax Rewards
* Passive Income Values
* Spending Costs

---

## RewardData

Stores:

* Reward Type
* Amount
* Source
* Description

All economy values should remain configurable.

---

# 14. Signals

EconomyManager exposes:

* gold_added
* gold_spent
* income_received
* passive_income_awarded
* economy_updated

Other systems subscribe without directly modifying Gold values.

---

# 15. AI Economy

AI should:

* Save strategically.
* Avoid unnecessary spending.
* Recruit Army only when beneficial.
* Preserve reserves for important opportunities.

AI should never receive hidden Gold.

---

# 16. Edge Cases

The Economy System must correctly handle:

* Spending all available Gold.
* Receiving multiple rewards simultaneously.
* Negative rewards.
* Event-based income.
* Save/load during economic updates.
* Passive income after victory checks.

---

# 17. Performance Requirements

Economy calculations:

Instant

Resource updates:

Immediate

HUD updates:

< 50 ms

Frame rate:

60 FPS

---

# 18. Testing Checklist

The following tests must pass:

* Gold increases correctly.
* Gold spending updates immediately.
* Passive income functions.
* Trade rewards apply.
* Market rewards apply.
* Harbor rewards apply.
* AI spends responsibly.
* Save/load restores economy.

---

# 19. Codex Implementation Notes

Create a dedicated **EconomyManager**.

Responsibilities:

* Track all resources.
* Calculate income.
* Process expenses.
* Apply passive income.
* Notify HUD updates.
* Maintain economy statistics.

EconomyManager should never contain battle logic or board logic.

Every configurable value should come from EconomyConfig Resources.

---

# 20. Future Expansion

Future economic systems may include:

* Dynamic Markets
* Supply and Demand
* International Trade Routes
* Merchant Guilds
* Kingdom Investments
* Building Construction
* Provincial Taxes
* Inflation
* Economic Crises
* Trade Embargoes

These systems should extend the existing economy rather than replace it.

---

# 21. Design Principle

The Economy System should create constant strategic tension.

Players should never have enough Gold to do everything they want.

Every spending decision should feel meaningful, and every investment should shape the future of their kingdom.

---

**Document ID:** PV-010

**Version:** 1.0

**Status:** Complete
