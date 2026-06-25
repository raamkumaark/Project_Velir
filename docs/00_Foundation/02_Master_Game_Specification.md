---

Document ID: PV-002
Document Name: Master Game Specification
Project: Project Velir
Version: 1.0
Status: Draft
Owner: Game Director
Engine: Godot 4.4
Programming Language: Typed GDScript
Platform: Android
Target Orientation: Portrait
Target Match Length: 15–20 Minutes
Last Updated: June 2026

Related Documents:

* 00_Project_Vision.md
* 01_AI_Constitution.md

---

# 02 - Master Game Specification

> "Four Kingdoms. One Forgotten Civilization. Countless Paths to Glory."

---

# 1. Document Information

## Purpose

The Master Game Specification (MGS) is the primary design document for Project Velir.

It defines every gameplay system at a high level while providing enough technical information for AI coding assistants and human developers to begin implementation.

This document is intentionally concise in Version 1.0.

Future versions will expand each section into detailed engineering specifications.

---

## Scope

This document defines:

* Core gameplay
* Game rules
* Board structure
* Kingdom overview
* Resources
* Victory conditions
* Technical direction

Detailed implementation is covered in subsequent documents.

---

## Audience

This document is intended for:

* Game Director
* Gameplay Programmers
* AI Coding Assistants
* UI Designers
* Artists
* QA Testers

---

## Priority

If another document conflicts with this specification, the newest approved version of this document takes precedence.

---

# 2. Executive Summary

## Overview

Project Velir is a turn-based strategy board game inspired by the political, economic, and military history of ancient Tamilakam.

Players take control of one of four legendary kingdoms:

* Chola
* Chera
* Pandya
* Pallava

Each kingdom competes for Prestige by expanding influence, engaging in warfare, building trade networks, and uncovering the secrets hidden beneath the ancient ruins of Velir Aram.

The game combines the accessibility of classic board games with meaningful strategic decision-making.

The objective is to create short, replayable matches where every turn presents interesting choices.

---

## Vision Statement

Project Velir aims to become the definitive mobile strategy board game inspired by South Indian history.

Rather than recreating history, the game creates an alternate historical world where politics, trade, warfare, diplomacy, and exploration evolve differently every match.

---

## Design Philosophy

The game follows five principles.

1. Easy to Learn

Players should understand the core rules within five minutes.

2. Difficult to Master

Experienced players should continuously discover better strategies.

3. Every Turn Matters

Players should never feel that a turn is meaningless.

4. Historical Inspiration

Gameplay should feel authentically inspired by ancient Tamil civilization while remaining fictional.

5. Replayability

Every match should produce different stories.

---

# 3. High Concept

## Genre

Strategy Board Game

---

## Subgenre

Turn-Based Kingdom Strategy

---

## Theme

Ancient Tamil Kingdoms

---

## Camera

Top Down

Orthographic

Portrait Orientation

---

## Platform

Primary

Android

Future

iOS

Steam

Nintendo Switch (Potential)

---

## Match Duration

Quick Match

10–15 Minutes

Standard Match

15–20 Minutes

Extended Match

30 Minutes

---

## Target Audience

Primary

* Strategy Players
* Board Game Players
* Mobile Gamers

Secondary

* History Enthusiasts
* Casual Players
* Students

---

## Core Fantasy

The player should feel like the ruler of a growing kingdom making meaningful political, military, and economic decisions while competing against rival kingdoms for control of the legendary Velir Aram.

---

## Unique Selling Points

Project Velir differentiates itself by combining:

* Strategy board gameplay
* Tamil historical inspiration
* Dynamic kingdom politics
* Ancient civilization exploration
* AI-driven opponents
* Highly replayable matches

Rather than copying Monopoly, the game focuses on strategic decision-making with board-game accessibility.
# 4. Design Goals

## Primary Goal

Project Velir is designed to be a strategy board game where every decision has meaningful consequences.

Unlike traditional board games that rely heavily on luck, Project Velir encourages players to balance risk, long-term planning, diplomacy, economy, and military strength.

---

## Design Objectives

### DG-01 Easy to Learn

A new player should understand the basic rules within five minutes.

Core interactions must remain simple:

* Roll Dice
* Move
* Resolve Tile
* Make Decisions
* End Turn

The game should never overwhelm players with unnecessary complexity during the first match.

---

### DG-02 Difficult to Master

Although the controls are simple, strategic depth should emerge through:

* Kingdom abilities
* Resource management
* Player decisions
* Random events
* AI behavior
* Control of Velir Aram

Winning consistently should require planning rather than luck.

---

### DG-03 Meaningful Decisions

Every turn should present one or more meaningful choices.

Examples include:

* Recruit soldiers or save gold
* Attack or negotiate
* Expand territory or defend borders
* Invest in trade or pursue relics
* Enter Velir Aram or continue around the board

No action should feel automatic.

---

### DG-04 Replayability

Every match should feel different.

Replayability is achieved through:

* Four unique kingdoms
* Dynamic board state
* Random event cards
* AI personalities
* Different player strategies
* Variable relic discoveries

Players should be encouraged to immediately start another match after finishing one.

---

### DG-05 Mobile First

Project Velir is designed specifically for smartphones.

The interface must support:

* Portrait orientation
* One-handed operation
* Large touch targets
* Short play sessions
* Fast loading
* Clear information hierarchy

Desktop conventions should not dictate mobile gameplay.

---

### DG-06 Historical Identity

The game is inspired by ancient Tamilakam.

Historical inspiration includes:

* Architecture
* Trade
* Warfare
* Literature
* Temple culture
* Political rivalries

The game is fictional and prioritizes enjoyable gameplay over historical simulation.

---

### Success Criteria

The design is successful when:

* New players understand the game quickly.
* Experienced players continue discovering strategies.
* Every kingdom feels unique.
* Matches remain engaging from beginning to end.
* Players voluntarily replay multiple matches.

---

# 5. Player Experience

## Player Fantasy

The player is not merely moving a token around a board.

The player is the ruler of one of the great Tamil kingdoms.

Every decision represents the ambitions of an entire kingdom.

Players should feel responsible for:

* Prosperity
* Warfare
* Diplomacy
* Exploration
* Political influence

---

## Emotional Journey

A typical match should create the following emotional progression:

Curiosity

↓

Exploration

↓

Planning

↓

Competition

↓

Conflict

↓

Risk

↓

Discovery

↓

Triumph or Defeat

Players should constantly experience moments of anticipation and surprise.

---

## Decision Loop

Every turn should encourage questions such as:

* Should I attack now?
* Can I afford to lose this battle?
* Is another player becoming too powerful?
* Should I risk entering Velir Aram?
* Should I spend gold now or save it?
* Is diplomacy more valuable than war?

The game succeeds when players think before acting.

---

## Target Player Types

Project Velir should support multiple play styles.

### The Conqueror

Enjoys military expansion.

Prioritizes battles and territory.

---

### The Merchant

Focuses on wealth and economic growth.

Prefers trade over warfare.

---

### The Diplomat

Uses influence and negotiation.

Avoids unnecessary conflict.

---

### The Explorer

Searches for relics and hidden opportunities within Velir Aram.

---

### The Opportunist

Adapts strategy based on changing board conditions.

---

## Match Experience

Beginning

Players establish their kingdoms and gather resources.

Middle

Competition intensifies.

Borders become contested.

Economic choices become important.

End

Prestige races accelerate.

Control of Velir Aram becomes increasingly valuable.

Players compete for final victory.

---

## Accessibility Goals

The game should support:

* Color-blind friendly design
* Large readable fonts
* Simple icons
* Clear visual feedback
* Minimal text during gameplay

---

# 6. Core Gameplay Loop

## Overview

Project Velir follows a repeating gameplay loop.

Every turn reinforces strategic decision-making while keeping the pace fast.

---

## Match Flow

Start Match

↓

Choose Kingdom

↓

Generate Board

↓

Initialize Players

↓

Begin Round

↓

Player Turn

↓

Roll Dice

↓

Move Token

↓

Resolve Tile

↓

Receive Rewards or Penalties

↓

Optional Strategic Actions

↓

End Turn

↓

Next Player

↓

Repeat Until Victory

---

## Turn Loop

Each player's turn follows the same sequence.

### Step 1

Roll Dice

The player rolls one six-sided die.

Movement value is determined.

---

### Step 2

Move

The kingdom token moves clockwise around the board.

Movement animations should be smooth and readable.

---

### Step 3

Resolve Tile

The landed tile activates.

Possible outcomes include:

* Gold
* Army
* Prestige
* Event
* Battle
* Trade
* Temple
* Ancient Site

---

### Step 4

Resolve Additional Events

Certain tiles may trigger:

* Event Cards
* Battles
* Resource Changes
* Velir Aram Activities

---

### Step 5

Optional Decisions

Depending on the current state, players may:

* Recruit soldiers
* Spend gold
* Initiate diplomacy
* Enter Velir Aram
* Use relics (future)
* Upgrade structures (future)

---

### Step 6

End Turn

Temporary effects expire.

Autosave occurs.

Turn passes to the next player.

---

## Core Loop Goals

The gameplay loop should:

* Be easy to remember.
* Minimize downtime.
* Encourage strategic thinking.
* Maintain player engagement.
* Keep match duration within target limits.

---

## Design Rule

Every completed turn should leave the player feeling that they have:

* Progressed their kingdom,
* Responded to changing conditions,
* Made at least one meaningful decision,
* Prepared for the next round.

If a turn contains no meaningful decision, the gameplay loop should be reconsidered.

---
# 7. Gameplay Flow

## Overview

Gameplay in Project Velir follows a structured sequence from launching the game to declaring a winner. Every interaction should be intuitive, fast, and predictable while allowing strategic depth to emerge through player decisions.

---

## Game Start Flow

```text
Launch Game
      ↓
Splash Screen
      ↓
Main Menu
      ↓
Select Game Mode
      ↓
Choose Kingdom
      ↓
Configure Match
      ↓
Generate Board
      ↓
Initialize Players
      ↓
Start Match
```

---

## Match Initialization

When a new match begins, the game performs the following actions:

1. Generate the board.
2. Create player profiles.
3. Assign kingdoms.
4. Initialize resources.
5. Position kingdom tokens.
6. Randomize first player.
7. Display match introduction.
8. Begin Round One.

---

## Player Turn Flow

Every player follows the same sequence.

```text
Turn Starts
      ↓
Roll Dice
      ↓
Move Token
      ↓
Resolve Tile
      ↓
Resolve Events
      ↓
Optional Actions
      ↓
Update Resources
      ↓
End Turn
```

---

## Round Flow

A round is complete once every kingdom has finished its turn.

```text
Player 1
      ↓
Player 2
      ↓
Player 3
      ↓
Player 4
      ↓
Round Complete
```

At the end of each round:

* Passive income is awarded.
* Temporary effects are updated.
* Event timers decrease.
* Victory conditions are checked.

---

## Match End Flow

The match ends immediately when a victory condition is met.

```text
Victory Detected
      ↓
Display Winner
      ↓
Statistics Screen
      ↓
Rewards
      ↓
Return to Main Menu
```

---

## Design Requirements

Gameplay flow must:

* Never confuse players.
* Require minimal menus during matches.
* Keep transitions below one second.
* Allow players to understand whose turn it is at all times.

---

# 8. Game Modes

## Version 1 (MVP)

### Single Player

The player competes against AI-controlled kingdoms.

Features:

* 1 Human Player
* 3 AI Kingdoms
* Offline Play
* Full Game Rules
* Save/Load Support

This is the primary development target.

---

## Future Version

### Local Multiplayer

Supports multiple human players using a single device.

Features:

* Pass-and-Play
* 2–4 Players
* Shared Device

---

## Future Version

### Online Multiplayer

Players compete over the internet.

Planned Features:

* Public Matches
* Private Rooms
* Friend Invites
* Ranked Games
* Matchmaking
* Reconnection Support

---

## Future Version

### Historical Campaign

Narrative-driven scenarios inspired by Tamil history.

Examples:

* Rise of Karikalan
* Pandya Expansion
* Chera Trade Era
* Pallava Golden Age

Campaigns may introduce custom rules and objectives.

---

## Future Version

### Custom Match

Players can configure:

* AI Difficulty
* Match Length
* Starting Resources
* Event Frequency
* Victory Conditions

---

## Design Principles

Every game mode must reuse the same gameplay systems whenever possible.

Special rules should be added through configuration rather than duplicated code.

---

# 9. Board Overview

## Overview

The board is the central gameplay environment.

Players move around the perimeter while competing for resources, strategic positions, and access to Velir Aram.

The board itself becomes increasingly dynamic as the match progresses.

---

## Board Structure

The board consists of:

* Four Kingdom Regions
* Neutral Territories
* Strategic Routes
* Trade Locations
* Event Locations
* Central Region

At the center lies:

**Velir Aram**

The ancient civilization that serves as the most valuable location in the game.

---

## Board Layout

```text
                 CHERA

          □ □ □ □ □ □

      □                 □

PALLAVA      VELIR ARAM      CHOLA

      □                 □

          □ □ □ □ □ □

                PANDYA
```

This layout is conceptual.

The final visual board may change while preserving the same gameplay structure.

---

## Board Size

Version 1

* 48 Perimeter Tiles
* 1 Central Region

Future versions may introduce larger boards.

---

## Kingdom Positions

Each kingdom begins in its own home region.

| Kingdom | Starting Region |
| ------- | --------------- |
| Chera   | North           |
| Chola   | East            |
| Pandya  | South           |
| Pallava | West            |

Each starting region contains unique visual architecture while maintaining identical gameplay balance.

---

## Movement Direction

Players move clockwise around the perimeter.

Movement into Velir Aram requires landing on designated entry tiles.

---

## Board Objectives

The board should encourage players to:

* Travel continuously.
* Compete over valuable locations.
* Interact frequently.
* Revisit important areas.
* Return to Velir Aram throughout the match.

No area of the board should become permanently irrelevant.

---

## Board Design Principles

The board should satisfy the following goals:

* Easy to read.
* Visually attractive.
* Mobile friendly.
* Balanced travel distances.
* Clear tile identity.
* Minimal visual clutter.

Players should always understand their current location without zooming or rotating the board.

---

**Next Chapters (10–12):**

* **10. Kingdom Overview**
* **11. Resource System**
* **12. Dice System**

These chapters begin defining the actual gameplay systems and data structures that Codex will use to implement the first playable prototype.
# 10. Kingdom Overview

## Overview

Project Velir features four playable kingdoms inspired by the great Tamil dynasties.

Each kingdom follows the same core rules but possesses unique passive abilities, strategic advantages, and visual identity.

The objective is to encourage different playstyles while maintaining overall game balance.

No kingdom should feel objectively stronger than another.

---

## Playable Kingdoms

### Chola Kingdom

**Primary Focus**

Trade and Expansion

**Playstyle**

Aggressive economic growth with strong territorial expansion.

**Passive Ability (Version 1)**

Merchant Empire

* +20% Gold earned from Trade Tiles.
* Harbor bonuses increased.

**Strengths**

* Excellent economy
* Fast expansion
* Strong late game

**Weaknesses**

* Higher recruitment costs
* Requires careful resource management

---

### Chera Kingdom

**Primary Focus**

Diplomacy and Commerce

**Playstyle**

Balanced strategy focused on influence and trade.

**Passive Ability (Version 1)**

Diplomatic Legacy

* Gains additional Influence from diplomacy-related events.

**Strengths**

* High Influence generation
* Flexible strategy
* Stable economy

**Weaknesses**

* Moderate military growth

---

### Pandya Kingdom

**Primary Focus**

Treasury and Prosperity

**Playstyle**

Resource accumulation and efficient economic management.

**Passive Ability (Version 1)**

Royal Treasury

* Gains bonus Gold from taxation.

**Strengths**

* Strong economy
* Reliable income
* Excellent endurance

**Weaknesses**

* Limited offensive bonuses

---

### Pallava Kingdom

**Primary Focus**

Defense and Military

**Playstyle**

Fortification and battlefield control.

**Passive Ability (Version 1)**

Stone Fortresses

* Defensive battles receive a combat bonus.

**Strengths**

* Strong defense
* Efficient military

**Weaknesses**

* Slower economic growth

---

## Kingdom Balance Principles

Every kingdom must satisfy the following:

* Easy to understand
* Unique strategic identity
* No exclusive gameplay mechanics
* Balanced win rate
* Suitable for AI and human players

---

## Starting Conditions

Every kingdom begins with:

* Equal Prestige
* Equal Army
* Equal Gold
* Equal Influence
* One Kingdom Token
* One Commander

Only passive abilities differentiate kingdoms in Version 1.

---

## Future Expansion

Future versions may introduce:

* Unique Commanders
* Kingdom Technologies
* Special Units
* Unique Buildings
* Historical Leaders
* Kingdom Missions

---

# 11. Resource System

## Overview

Resources represent the strength and progress of each kingdom.

Every strategic decision affects one or more resources.

Resources should remain simple enough for casual players while supporting deeper strategic choices.

---

## Primary Resources

### Gold

**Purpose**

Primary economic resource.

Used for:

* Recruiting soldiers
* Paying taxes
* Trading
* Purchasing upgrades
* Future building construction

**Sources**

* Trade Tiles
* Markets
* Taxes
* Event Cards
* Ancient Treasures

---

### Army

Represents military strength.

Used for:

* Battles
* Territory control
* Defense

Army is not individual soldiers.

It is a single numerical value representing military power.

---

### Influence

Represents political authority.

Used for:

* Diplomacy
* Negotiations
* Future alliances
* Special events

Influence cannot directly win battles but provides strategic advantages.

---

### Prestige

Prestige represents the overall success of a kingdom.

Prestige is the primary victory resource.

Sources include:

* Winning battles
* Discovering relics
* Completing objectives
* Controlling important locations
* Historical events

---

## Resource Rules

Resources can increase or decrease throughout the match.

No resource may become negative.

Maximum values will be configurable through data files.

---

## Resource Display

The HUD displays:

* Gold
* Army
* Influence
* Prestige

Values should update immediately after any change.

---

## Resource Philosophy

Resources should encourage:

* Planning
* Trade-offs
* Long-term thinking

Players should rarely have enough resources to perform every desired action.

---

# 12. Dice System

## Overview

The dice determines player movement.

It introduces controlled randomness while preserving strategic decision-making.

Luck influences opportunities.

Player decisions determine success.

---

## Dice Type

Version 1 uses:

* One six-sided die (D6)

Possible outcomes:

* 1
* 2
* 3
* 4
* 5
* 6

Every value has equal probability.

---

## Roll Rules

Each player rolls exactly once during their turn.

The rolled value determines movement distance.

The player cannot reroll unless permitted by a future gameplay effect.

---

## Dice Animation

The roll should include:

* Button press
* Dice animation
* Sound effect
* Final result display

Total animation duration should remain under one second.

The objective is responsiveness rather than realism.

---

## Random Number Generation

The game uses a centralized random number generator.

Requirements:

* Uniform distribution
* Deterministic seeds for testing
* No multiple independent generators

---

## Movement

After rolling:

1. Dice value is locked.
2. Token begins movement.
3. Token moves one tile at a time.
4. Landing tile activates automatically.

Movement cannot be interrupted.

---

## User Interface

During a player's turn:

Visible:

* Roll Dice button
* Current player
* Dice result

Disabled while moving:

* Roll button
* End Turn button
* Other player actions

---

## AI Dice

AI follows the exact same rules.

No hidden bonuses.

No manipulated probabilities.

AI never cheats.

---

## Acceptance Criteria

The Dice System is considered complete when:

* Dice values are uniformly distributed.
* Players cannot roll twice.
* AI uses identical mechanics.
* Dice animation completes before movement begins.
* Movement always matches the rolled value.
* Save/Load correctly restores dice state if interrupted.

---

**End of Chapter 12**
# 13. Turn System

## Overview

The Turn System controls the order of play and ensures every player receives an equal opportunity to perform actions.

The system must be deterministic, easy to follow, and suitable for both human and AI players.

---

## Turn Order

Version 1 supports:

* 2 Players
* 3 Players
* 4 Players

The default game is:

* 1 Human
* 3 AI

The first player is selected randomly at the start of the match.

Turn order then continues clockwise.

Example:

```text
Round 1

Pandya

↓

Chola

↓

Pallava

↓

Chera

↓

Round Complete
```

Round 2 begins with Pandya again.

---

## Turn Phases

Each turn consists of six phases.

### Phase 1

Start Turn

Actions:

* Highlight active kingdom
* Focus camera
* Display kingdom information
* Enable Roll Dice button

---

### Phase 2

Roll Dice

Player rolls one D6.

Movement value is locked.

---

### Phase 3

Movement

Player token moves automatically.

Movement cannot be cancelled.

Movement always finishes before the next phase.

---

### Phase 4

Tile Resolution

Landing tile activates.

Examples:

* Gold
* Battle
* Temple
* Market
* Event
* Ancient Site

---

### Phase 5

Optional Actions

Depending on the situation the player may:

* Recruit Army
* Spend Gold
* Enter Velir Aram
* Perform Diplomacy (Future)
* Upgrade Structures (Future)

---

### Phase 6

End Turn

Actions:

* Save Game
* Update Resources
* Check Victory
* Pass control to next player

---

## Turn Indicators

The active player should always be obvious.

Display:

* Kingdom Banner
* Kingdom Color
* Player Name
* Current Resources

---

## Round Completion

A round finishes after every active kingdom completes one turn.

End-of-round events include:

* Passive income
* Temporary effect updates
* Event countdowns
* Victory check

---

## Turn Rules

Every player receives exactly one turn per round.

Players cannot skip another player's turn.

A player may only perform actions during their own turn.

---

## Future Expansion

Future versions may introduce:

* Extra Turns
* Stun Effects
* Turn Manipulation
* Time Limits
* Multiplayer Turn Timers

These mechanics are excluded from Version 1.

---

# 14. Tile System

## Overview

Tiles represent locations on the board.

Every tile performs a specific gameplay function when a player lands on it.

Tiles are the primary source of interaction throughout the match.

---

## Tile Philosophy

Each tile should immediately answer one question:

"What happens when I land here?"

Players should never need to memorize complicated rules.

---

## Tile Structure

Every tile contains:

* Tile ID
* Tile Name
* Tile Type
* Description
* Reward
* Penalty
* Owner (if applicable)
* Icon
* Artwork

---

## Version 1 Tile Types

### Trade Tile

Purpose

Earn Gold.

Reward

Gold based on kingdom bonuses.

---

### Temple Tile

Purpose

Gain Influence.

Represents religious and cultural prestige.

---

### Market Tile

Purpose

Trade resources.

Future versions may include dynamic prices.

---

### Village Tile

Purpose

Recruit soldiers.

Provides small Army increase.

---

### Fort Tile

Purpose

Military stronghold.

May trigger battles or provide defensive bonuses.

---

### Event Tile

Purpose

Draw an Event Card.

Event Cards create unpredictable situations.

---

### Tax Tile

Purpose

Collect taxes from the kingdom.

Provides immediate Gold.

---

### Harbor Tile

Purpose

Represents overseas trade.

Especially beneficial for the Chola kingdom.

---

### Ancient Site

Purpose

Discover relics.

Usually connected to Velir Aram.

Provides high-risk, high-reward opportunities.

---

### Velir Gate

Purpose

Entry point into Velir Aram.

Only accessible from designated board locations.

---

### Neutral Tile

Purpose

No immediate effect.

Provides movement pacing.

Future versions may attach additional mechanics.

---

## Tile Activation

A tile activates immediately after movement ends.

Only one tile activates per turn.

If multiple effects exist, they resolve in the following order:

1. Tile Effect
2. Event Card
3. Battle
4. Resource Update
5. Victory Check

---

## Tile Design Goals

Tiles should be:

* Easy to recognize
* Visually distinct
* Balanced
* Quick to understand

Players should identify tile function using icons before reading text.

---

# 15. Battle System

## Overview

Battles represent military conflicts between kingdoms.

Combat should be strategic without becoming overly complicated.

The system must be simple enough for casual players while allowing meaningful decisions.

---

## Battle Triggers

Battles occur when:

* A player lands on an occupied battle location.
* A player attacks another kingdom.
* A special Event Card initiates combat.
* A Velir Aram encounter requires combat.

Version 1 uses only direct kingdom battles.

---

## Battle Formula

Battle Strength is calculated as:

```
Army Strength

+

Commander Bonus

+

Dice Roll

=

Total Battle Strength
```

The kingdom with the highest total wins.

---

## Tie Rule

If both kingdoms obtain the same score:

The defending kingdom wins.

This encourages defensive play and prevents unnecessary randomness.

---

## Victory Rewards

Winning a battle grants:

* Prestige
* Gold (small reward)
* Military reputation

Future versions may include relics and captured territory.

---

## Defeat Penalties

The defeated kingdom loses:

* Army Strength
* Small amount of Prestige

The kingdom is never eliminated immediately.

Comeback opportunities should always exist.

---

## Commander Bonus

Each kingdom begins with one Commander.

Commanders provide passive combat bonuses.

Version 1 uses only static bonuses.

Future versions will introduce:

* Commander abilities
* Level progression
* Equipment
* Capture mechanics
* Injuries

---

## Battle Flow

```text
Battle Begins

↓

Calculate Army Strength

↓

Apply Commander Bonus

↓

Roll Dice

↓

Calculate Total Score

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

## Design Goals

Battles should:

* Resolve in under ten seconds.
* Feel exciting.
* Reward preparation.
* Never rely entirely on luck.

Army strength should matter more than dice rolls.

---

## AI Battles

AI follows identical combat rules.

No hidden bonuses.

No unfair advantages.

AI wins because of strategy, not cheating.

---

## Future Expansion

Future combat additions may include:

* Cavalry
* Elephants
* Naval Battles
* Fort Sieges
* Commander Skills
* Formation Bonuses
* Terrain Effects
* Multiple Unit Types

These mechanics are intentionally excluded from Version 1 to maintain accessibility.

---

**End of Chapter 15**
# 16. Velir Aram

## Overview

Velir Aram is the heart of Project Velir.

Unlike the four kingdoms, Velir Aram is not owned by any player at the start of a match.

It is an ancient ruined civilization believed to predate the Sangam Age and is the primary source of relics, prestige, and strategic advantages.

Every kingdom seeks to control Velir Aram because its forgotten secrets may determine the future ruler of Tamilakam.

---

## Lore

Ancient inscriptions describe Velir Aram as the final surviving remains of a civilization known only as **Ezhamandalam** — *The Seventh Realm*.

No kingdom knows its true history.

Each believes it is the rightful heir.

The ruins contain:

* Ancient temples
* Royal archives
* Hidden chambers
* Forgotten observatories
* Sacred reservoirs
* Underground passages

Future campaigns may gradually reveal its history.

---

## Gameplay Purpose

Velir Aram serves as:

* End-game objective
* High-risk exploration zone
* Source of ancient relics
* Strategic shortcut
* Prestige generator

Players should feel drawn toward Velir Aram throughout the match rather than ignoring the center of the board.

---

## Entry

Players cannot freely enter Velir Aram.

Entry is allowed only through designated **Velir Gates** located around the board.

Future versions may require:

* Influence
* Gold
* Keys
* Special Events

Version 1 allows entry through normal gameplay.

---

## Ancient Sites

Version 1 contains five discoverable locations.

### Hall of Kings

Reward

Prestige

Represents the former royal assembly.

---

### Lost Library

Reward

Influence

Contains forgotten knowledge.

---

### Merchant Archives

Reward

Gold

Stores records of ancient trade.

---

### Warrior Necropolis

Reward

Army

Ancient military burial grounds.

---

### Sacred Reservoir

Reward

Random Blessing

May restore resources or trigger special events.

---

## Control

Velir Aram itself cannot be permanently owned.

Players temporarily gain benefits by controlling Ancient Sites.

Control may change frequently during a match.

---

## Design Principles

Velir Aram should:

* Encourage exploration
* Reward risk
* Create player conflict
* Increase late-game tension
* Provide memorable moments

The center of the board should never become irrelevant.

---

## Future Expansion

Future versions may introduce:

* Underground maps
* Ancient bosses
* Puzzle chambers
* Legendary relics
* Cooperative expeditions
* Story discoveries

---

# 17. Event Card System

## Overview

Event Cards introduce unpredictability into every match.

Rather than relying entirely on player interaction, events simulate political, economic, military, and natural occurrences across ancient Tamilakam.

No two matches should experience identical sequences of events.

---

## Purpose

Event Cards provide:

* Variety
* Replayability
* Risk
* Opportunity
* Historical atmosphere

Events should influence strategy without determining the winner on their own.

---

## Event Categories

### Economic Events

Examples:

* Roman Trade Caravan
* Merchant Festival
* Tax Collection
* Market Boom

Effects:

Primarily modify Gold.

---

### Military Events

Examples:

* Border Skirmish
* Desertion
* Reinforcements
* Mercenary Arrival

Effects:

Modify Army.

---

### Political Events

Examples:

* Royal Marriage
* Diplomatic Envoy
* Noble Rebellion
* Court Intrigue

Effects:

Modify Influence.

---

### Cultural Events

Examples:

* Temple Festival
* Literary Assembly
* Royal Donation

Effects:

Increase Prestige.

---

### Natural Events

Examples:

* Flood
* Drought
* Cyclone
* Good Harvest

Effects:

Random resource changes.

---

### Ancient Events

Examples:

* Hidden Chamber
* Ancient Inscription
* Forgotten Treasury
* Sacred Relic

Exclusive to Velir Aram.

---

## Event Resolution

When a player lands on an Event Tile:

1. Draw one random card.
2. Display event artwork.
3. Apply effect.
4. Update resources.
5. Continue turn.

---

## Randomization

Cards should:

* Be shuffled.
* Avoid excessive repetition.
* Support weighted probabilities.

Rare events should remain exciting.

---

## Design Principles

Events should:

* Be understandable immediately.
* Resolve quickly.
* Feel rewarding or dramatic.
* Support storytelling.

Players should remember events long after the match ends.

---

## Future Expansion

Future versions may include:

* Kingdom-specific events
* Seasonal events
* Multi-turn events
* World events
* Cooperative events

---

# 18. Economy System

## Overview

The economy governs how kingdoms earn, spend, and manage resources throughout a match.

Economic strength should provide strategic flexibility but should never guarantee victory.

Players must balance spending today against preparing for future opportunities.

---

## Economic Philosophy

Project Velir follows a **Simple Economy, Deep Decisions** approach.

Players should understand the economy quickly while still facing meaningful financial choices.

---

## Income Sources

Gold may be earned through:

* Trade Tiles
* Markets
* Harbor Tiles
* Taxes
* Event Cards
* Ancient Treasures
* Velir Aram Discoveries
* Passive Kingdom Bonuses

---

## Expenses

Gold may be spent on:

* Recruiting Army
* Entering Ancient Sites
* Paying Ransom (Future)
* Diplomacy (Future)
* Building Upgrades (Future)
* Purchasing Relics (Future)

Version 1 focuses primarily on Army recruitment.

---

## Passive Income

At the end of every round, kingdoms receive passive income.

Sources include:

* Controlled Trade Routes
* Kingdom Bonuses
* Special Ancient Sites

Passive income rewards long-term planning.

---

## Inflation

Version 1 does **not** include inflation or fluctuating market prices.

The economy should remain predictable.

Future versions may introduce dynamic pricing.

---

## Resource Balance

Gold should always remain valuable.

Players should frequently face decisions such as:

* Recruit soldiers?
* Save for future opportunities?
* Risk exploring Velir Aram?

The economy succeeds when there is no obvious "correct" spending strategy.

---

## AI Economy

AI follows identical economic rules.

AI must:

* Spend responsibly.
* Save strategically.
* Avoid reckless purchases.

AI receives no hidden economic bonuses.

---

## Future Expansion

Future economic mechanics may include:

* Trade Agreements
* Resource Markets
* Building Construction
* Supply Lines
* Merchant Fleets
* Resource Production
* Provincial Taxes

These systems are intentionally excluded from Version 1 to keep gameplay accessible.

---

**End of Chapter 18**
# 19. AI System

## Overview

Artificial Intelligence (AI) is responsible for controlling non-human kingdoms during single-player matches.

The objective is not to create an unbeatable opponent.

The objective is to create believable rulers with distinct personalities, strategies, and priorities.

Each AI kingdom should feel like a rival kingdom rather than a computer following fixed rules.

---

## AI Design Philosophy

Project Velir follows three AI principles.

### Rule 1

AI Never Cheats.

The AI must follow the exact same gameplay rules as the player.

It cannot receive:

* Hidden Gold
* Extra Army
* Free Prestige
* Better Dice Rolls
* Secret Information

Victory should come from good decisions.

---

### Rule 2

AI Has Personality.

Each kingdom should make decisions according to its historical identity.

Players should eventually recognize different AI behaviors.

---

### Rule 3

AI Makes Understandable Decisions.

Even when the AI defeats the player, the player should understand why.

Poorly explained or seemingly random AI decisions reduce trust in the game.

---

## AI Personalities

### Chola AI

Focus

Expansion

Priorities

* Trade
* Gold
* Expansion
* Velir Aram

Behavior

Aggressive economic growth.

Prefers taking calculated risks.

---

### Chera AI

Focus

Diplomacy

Priorities

* Influence
* Balanced economy
* Strategic positioning

Behavior

Avoids unnecessary battles.

Looks for long-term advantages.

---

### Pandya AI

Focus

Economy

Priorities

* Treasury
* Resource efficiency
* Stable growth

Behavior

Rarely spends all available Gold.

Builds strength gradually.

---

### Pallava AI

Focus

Defense

Priorities

* Army
* Defensive positions
* Safe expansion

Behavior

Difficult to conquer.

Rarely starts risky conflicts.

---

## AI Decision Priorities

Every turn, the AI evaluates:

1. Current resources.
2. Relative military strength.
3. Nearby opportunities.
4. Threats from opponents.
5. Access to Velir Aram.
6. Victory progress.

The highest-priority action is selected.

---

## Difficulty Levels

### Easy

* Conservative decisions.
* Fewer strategic optimizations.
* Forgiving gameplay.

---

### Normal

Balanced behavior.

Represents the intended game experience.

---

### Hard

Improved planning.

Better economic decisions.

More effective use of opportunities.

No cheating.

---

## Future Difficulty

Future versions may add:

Expert

Legendary

Custom AI personalities

Machine-learning opponents

---

## AI Goals

The AI should actively compete for:

* Prestige
* Gold
* Army
* Ancient Sites
* Velir Aram

It should not simply react to the human player.

---

## Future Expansion

Future AI improvements may include:

* Diplomacy
* Alliances
* Betrayal
* Commander specialization
* Personality evolution
* Historical ruler behavior

---

# 20. Victory Conditions

## Overview

Project Velir is won through Prestige.

The objective is not to eliminate every opponent.

Instead, kingdoms compete to become the most respected and influential ruler of Tamilakam.

---

## Primary Victory

Prestige Victory

Version 1 Target

100 Prestige

The first kingdom to reach 100 Prestige immediately wins the match.

---

## Prestige Sources

Prestige may be earned through:

* Winning Battles
* Discovering Ancient Relics
* Controlling Ancient Sites
* Cultural Events
* Temple Activities
* Historical Events
* Kingdom Achievements

Future versions may include campaign objectives.

---

## Secondary Victory

Last Kingdom Standing

If every other kingdom is defeated, the remaining kingdom wins automatically.

This should occur rarely.

Prestige remains the primary victory path.

---

## Draw Conditions

Version 1 does not include draws.

If multiple players reach the victory requirement during the same round:

Highest Prestige wins.

If Prestige is tied:

Highest Gold wins.

If Gold is tied:

Highest Army wins.

If still tied:

Shared Victory.

---

## Match Completion

When a winner is declared:

The game displays:

* Winning Kingdom
* Final Prestige
* Match Statistics
* Resource Summary
* Battle Record
* Ancient Discoveries

Players may then:

* Play Again
* Return to Menu
* View Statistics

---

## Match Statistics

Statistics include:

* Turns Played
* Battles Won
* Gold Earned
* Army Recruited
* Events Triggered
* Ancient Sites Controlled
* Relics Discovered

Statistics encourage replayability and future balancing.

---

## Design Goals

Victory should reward:

* Strategy
* Planning
* Adaptation

Victory should never depend solely on luck.

---

## Future Expansion

Future versions may introduce:

* Campaign Victory
* Objective-Based Victory
* Cooperative Victory
* Time-Limited Matches
* Ranked Seasons
* Achievement-Based Wins

---

# 21. Save System

## Overview

Project Velir supports automatic and manual saving.

Players should be able to stop playing at any time and resume without losing progress.

The save system must be reliable, lightweight, and future-proof.

---

## Save Types

### Autosave

Occurs automatically:

* End of every turn
* Beginning of every round
* Before major events
* Before entering Velir Aram

Autosaves overwrite the previous autosave.

---

### Manual Save

Players may manually save from the Pause Menu.

Multiple save slots are supported.

---

## Save Data

The save file stores:

### Match Information

* Match ID
* Current Round
* Current Turn
* Active Player
* Difficulty
* Random Seed

---

### Player Information

For each kingdom:

* Position
* Gold
* Army
* Influence
* Prestige
* Commander
* Controlled Sites

---

### Board State

* Tile ownership
* Ancient Site status
* Event queue
* Active effects

---

### Game Settings

* Audio
* Language
* Accessibility
* Display preferences

---

## Save Format

Version 1 uses:

JSON

Requirements:

* Human readable
* Version controlled
* Easy to migrate

Future versions may use compression if needed.

---

## Save Rules

Saving must never:

* Corrupt a match.
* Lose player progress.
* Produce inconsistent game states.

Loading a save should restore the exact gameplay state prior to saving.

---

## Future Expansion

Future versions may introduce:

* Cloud Saves
* Cross-device synchronization
* Match Replay
* Save History
* Undo System (Campaign Mode)

---

**End of Chapter 21**
# 22. User Interface (UI) Overview

## Overview

The User Interface (UI) provides all gameplay information while remaining clean, readable, and optimized for portrait mobile devices.

The UI should support strategic gameplay without overwhelming the player.

The board must always remain the primary visual focus.

---

## Design Philosophy

The UI follows five principles.

### Simple

Only display information relevant to the current decision.

---

### Consistent

Buttons, colors, icons, and layouts remain consistent throughout the game.

---

### Mobile First

Designed specifically for portrait Android devices.

* Large touch targets
* One-handed operation
* Minimal scrolling
* Clear spacing

---

### Immediate Feedback

Every player action provides instant visual feedback.

Examples:

* Dice animation
* Resource increase
* Battle result
* Event notification

---

### Minimal Interruption

Popups should appear only when necessary.

Gameplay should flow naturally without excessive dialogs.

---

## Main Gameplay Layout

```text
---------------------------------

Current Player

Kingdom Banner

---------------------------------

Gold | Army | Influence | Prestige

---------------------------------

          BOARD

---------------------------------

Current Event

---------------------------------

Roll Dice

End Turn

Menu

---------------------------------
```

---

## Main HUD

Always Visible

* Current Kingdom
* Gold
* Army
* Influence
* Prestige
* Round Number
* Active Turn

---

## Temporary Windows

Examples

* Event Card
* Battle Result
* Ancient Discovery
* Victory
* Confirmation Dialog

These disappear automatically unless player input is required.

---

## Pause Menu

Contains

* Resume
* Save
* Load
* Settings
* Restart Match
* Main Menu

---

## Accessibility

Version 1 includes:

* Adjustable text size
* Color-blind friendly palette
* Icon-based information
* Clear button labels

Future versions may include:

* Screen reader support
* High contrast mode
* Animation reduction

---

## Design Goals

Players should always know:

* Whose turn it is.
* Current resources.
* Available actions.
* Progress toward victory.

No important information should be hidden behind multiple menus.

---

# 23. Audio Overview

## Overview

Audio enhances immersion without distracting from strategic gameplay.

The soundtrack should evoke the atmosphere of ancient Tamilakam while remaining subtle during long play sessions.

---

## Audio Categories

### Background Music

Purpose

Create atmosphere.

Music should evolve depending on match progression.

Examples:

* Main Menu Theme
* Peaceful Exploration
* Battle Theme
* Velir Aram Theme
* Victory Theme

---

### Sound Effects

Examples

* Dice Roll
* Button Click
* Gold Earned
* Battle Victory
* Battle Defeat
* Event Card
* Ancient Discovery
* Kingdom Notification

Every important gameplay action should produce a recognizable sound.

---

### Ambient Audio

Examples

* Temple Bells
* Wind
* Birds
* Marketplace
* Ocean Waves
* Fire
* Ancient Ruins

Ambient sounds should reinforce location identity.

---

## Music Style

Inspired by:

* Traditional Tamil percussion
* Flute
* Veena
* Mridangam
* Udukkai
* Temple ambience

The soundtrack should avoid stereotypical fantasy orchestral music.

---

## Audio Controls

Players may independently adjust:

* Master Volume
* Music Volume
* Sound Effects
* Ambient Volume

Settings are saved automatically.

---

## Future Expansion

Future versions may include:

* Dynamic music
* Voice narration
* Kingdom-specific themes
* Festival music
* Seasonal ambience

---

# 24. Art Direction

## Overview

Project Velir adopts a stylized historical art direction inspired by ancient Tamil architecture, sculpture, literature, and craftsmanship.

The visual identity should immediately distinguish the game from medieval European fantasy games.

---

## Artistic Vision

The game should feel:

* Ancient
* Noble
* Warm
* Historical
* Elegant
* Strategic

Players should recognize the cultural inspiration even without prior historical knowledge.

---

## Visual Style

Style

Stylized Realism

The game should prioritize readability over photorealism.

Characters, buildings, and icons should be visually simplified while retaining historical inspiration.

---

## Color Palette

Primary Colors

* Bronze
* Sandstone
* Deep Red
* Dark Green
* Royal Gold
* Granite Grey
* Palm Leaf Green

Each kingdom also receives its own accent color.

---

## Architectural Inspiration

Reference materials include:

* Brihadeeswara Temple
* Shore Temple
* Madurai Temple architecture
* Ancient Tamil inscriptions
* Stone mandapams
* Sangam-era settlements

Architecture should be inspired by history without copying specific monuments exactly.

---

## Character Design

Version 1 contains minimal character art.

Focus is placed on:

* Kingdom banners
* Commander portraits
* Icons
* Tokens

Future versions may introduce animated rulers.

---

## Board Design

The board should resemble:

An ancient engraved stone map placed upon a royal council table.

Visual elements include:

* Stone pathways
* Temple motifs
* Palm-leaf patterns
* Bronze decorations
* Ancient inscriptions

Velir Aram should visually dominate the center of the board.

---

## User Interface Style

The interface should resemble carved stone and polished bronze rather than modern plastic panels.

Buttons should feel handcrafted rather than futuristic.

---

## Future Expansion

Future artistic additions may include:

* Animated kingdoms
* Seasonal board themes
* Weather effects
* Day/Night cycle
* Cinematic introductions
* Animated commanders

---

**End of Chapter 24**
# 25. Technical Overview

## Overview

Project Velir is developed as a modular, data-driven game using Godot Engine 4.4.

The architecture prioritizes maintainability, scalability, and AI-assisted development.

Every gameplay system should be independent, testable, and configurable without modifying unrelated systems.

---

## Technology Stack

| Category           | Technology        |
| ------------------ | ----------------- |
| Engine             | Godot 4.4         |
| Language           | Typed GDScript    |
| Rendering          | 2D                |
| Platform           | Android (Primary) |
| Version Control    | Git               |
| Documentation      | Markdown          |
| Save Format        | JSON              |
| Development Method | AI-Assisted       |

---

## Architecture Principles

Project Velir follows these engineering principles:

### Modular Design

Every gameplay feature is developed as an independent module.

Example:

* BoardManager
* TurnManager
* DiceManager
* BattleManager
* EventManager
* EconomyManager

Each system performs one responsibility only.

---

### Data-Driven Development

Gameplay values must never be hardcoded.

Instead, configurable Resources define:

* Kingdoms
* Tiles
* Events
* Battles
* Commanders
* Relics

Changing gameplay should rarely require changing code.

---

### Event-Driven Communication

Systems communicate using Signals.

Avoid direct dependencies whenever possible.

Example

```text
DiceManager

↓

dice_rolled

↓

TurnManager

↓

PlayerMovement

↓

TileSystem
```

---

## Performance Goals

Target Device

Mid-range Android Phone

Requirements

* 60 FPS
* Low battery usage
* Fast loading
* Small memory footprint

Target APK Size

Less than 200 MB

---

## Scene Structure

Primary Scenes

* Splash Screen
* Main Menu
* Gameplay
* Settings
* Statistics

Gameplay Scene contains:

* Board
* Players
* UI
* Managers

---

## Resource Files

Every configurable object should exist as a Resource.

Examples

* KingdomData
* TileData
* EventData
* CommanderData
* BattleData
* AncientSiteData

---

## Future Expansion

The architecture should support:

* Multiplayer
* DLC
* Additional Kingdoms
* New Boards
* Campaign Mode
* Cloud Saves

without requiring major refactoring.

---

# 26. Data Model

## Overview

Project Velir stores gameplay information using Resources and runtime data objects.

Persistent information should be separated from temporary gameplay state.

---

## Primary Data Objects

### KingdomData

Stores:

* Name
* Banner
* Color
* Passive Ability
* Starting Resources
* Commander
* Description

---

### PlayerData

Stores:

* Kingdom
* Position
* Gold
* Army
* Influence
* Prestige
* Controlled Sites
* Active Effects

---

### TileData

Stores:

* Tile ID
* Tile Name
* Tile Type
* Reward
* Penalty
* Icon
* Description

---

### EventData

Stores:

* Event Name
* Category
* Description
* Probability
* Rewards
* Penalties

---

### BattleData

Stores:

* Attacker
* Defender
* Dice Values
* Commander Bonuses
* Final Score
* Winner

---

### CommanderData

Stores:

* Commander Name
* Portrait
* Passive Ability
* Combat Bonus
* Description

---

### AncientSiteData

Stores:

* Site Name
* Reward
* Owner
* Discovery Status
* Description

---

## Runtime Managers

Version 1 includes:

* GameManager
* TurnManager
* BoardManager
* DiceManager
* BattleManager
* EventManager
* EconomyManager
* SaveManager
* AudioManager
* UIManager

Each manager owns only one gameplay responsibility.

---

## Serialization

Only gameplay state should be serialized.

Resources remain static.

Player progress is saved separately.

---

## Design Goals

The data model should be:

* Modular
* Easy to extend
* AI readable
* Version compatible
* Independent of UI

---

# 27. MVP Scope

## Purpose

The Minimum Viable Product (MVP) defines the smallest complete version of Project Velir that delivers the intended gameplay experience.

Any feature outside this scope is intentionally postponed.

This prevents feature creep and accelerates development.

---

## Version 1 Features

### Core Gameplay

✔ Four Playable Kingdoms

* Chola
* Chera
* Pandya
* Pallava

---

✔ Dice Movement

* One D6
* Automatic movement
* Turn based

---

✔ Board

* 48 Tiles
* Central Velir Aram
* Kingdom Regions

---

✔ Resources

* Gold
* Army
* Influence
* Prestige

---

✔ Battles

Simple combat system

Army

*

Commander

*

Dice

---

✔ Event Cards

Economic

Military

Political

Natural

Ancient

---

✔ AI Opponents

Three AI kingdoms

Unique personalities

No cheating

---

✔ Save / Load

Autosave

Manual Save

JSON

---

✔ Victory System

Prestige

Primary Win Condition

---

## Version 1 Exclusions

The following systems are **not** part of Version 1.

✘ Online Multiplayer

✘ Local Multiplayer

✘ Campaign Mode

✘ Commander Progression

✘ Kingdom Technologies

✘ Building Construction

✘ Diplomacy System

✘ Naval Battles

✘ Elephants

✘ Character Animation

✘ Voice Acting

✘ Ranked Seasons

✘ Cloud Save

✘ Cosmetic Shop

✘ Achievements

---

## MVP Success Criteria

Version 1 is considered successful if:

* Players understand gameplay within five minutes.
* Average match lasts 15–20 minutes.
* AI provides an enjoyable challenge.
* Every kingdom feels different.
* Players willingly replay multiple matches.

The MVP should prove that the core gameplay is fun before expanding the project.

---

**End of Chapter 27**
# 28. Version Roadmap

## Overview

Project Velir is planned as a long-term strategy game platform.

Development will follow incremental milestones, ensuring that every version remains playable while introducing new mechanics gradually.

No future version should require rebuilding the core architecture established in Version 1.

---

# Version 0.1

## Foundation

Status

Completed

Objectives

* Repository Creation
* Documentation Structure
* Project Vision
* AI Constitution
* Master Game Specification

Deliverables

* Documentation Repository
* Development Roadmap
* Initial Project Architecture

---

# Version 0.2

## Playable Prototype

Objectives

* Board Generation
* Player Movement
* Dice System
* Turn Management
* Basic UI

Deliverables

A playable prototype where players can move around the board.

---

# Version 0.3

## Core Gameplay

Objectives

* Tile System
* Resources
* Battles
* Event Cards
* Victory Conditions

Deliverables

The first complete playable game loop.

---

# Version 0.4

## AI & Polish

Objectives

* AI Kingdoms
* Save System
* Audio
* Animations
* Visual Improvements

Deliverables

Single-player experience ready for internal testing.

---

# Version 0.5

## Feature Complete MVP

Objectives

* Bug Fixes
* Game Balance
* UI Polish
* Performance Optimization
* Tutorial

Deliverables

Closed testing version.

---

# Version 1.0

## Public Release

Objectives

* Android Release
* Store Assets
* Marketing
* Performance Validation

Deliverables

Official public launch.

---

# Version 1.5

## Content Expansion

Planned Features

* Additional Ancient Sites
* More Event Cards
* Commander Improvements
* New Board Themes

---

# Version 2.0

## Multiplayer Update

Planned Features

* Online Multiplayer
* Friend Matches
* Matchmaking
* Leaderboards
* Ranked Seasons

---

# Version 3.0

## Historical Campaign

Planned Features

* Story Campaign
* Historical Scenarios
* Kingdom Chronicles
* Progressive Unlocks

---

# Long-Term Vision

Project Velir is designed to evolve continuously.

Potential future additions include:

* Additional South Indian dynasties
* Sri Lankan kingdoms
* Trade campaigns
* Cooperative gameplay
* Steam release
* Cross-platform multiplayer
* Community-generated maps
* Tournament mode

---

# Development Strategy

Every version must satisfy three rules:

1. Remain playable.
2. Preserve backward compatibility whenever possible.
3. Improve gameplay before increasing complexity.

---

# 29. Codex Implementation Notes

## Purpose

This chapter defines how AI coding assistants should interpret and implement Project Velir.

These notes supplement the AI Constitution and provide project-specific implementation guidance.

---

## AI Role

The AI acts as a Senior Gameplay Engineer.

Responsibilities include:

* Writing production-ready code.
* Following documentation exactly.
* Preserving architecture.
* Maintaining code quality.

The AI must not redesign gameplay systems.

---

## Coding Principles

Every generated feature must be:

* Modular
* Typed
* Documented
* Testable
* Data-driven
* Android optimized

---

## Implementation Order

Codex should implement systems in the following order.

1. BoardManager

2. DiceManager

3. TurnManager

4. PlayerManager

5. TileSystem

6. EconomyManager

7. BattleManager

8. EventManager

9. AIManager

10. SaveManager

11. UIManager

12. AudioManager

This order minimizes dependencies.

---

## Required Coding Standards

Every script should:

* Use Typed GDScript.
* Export configurable values.
* Avoid duplicated logic.
* Use Signals.
* Follow SOLID principles.
* Support future expansion.

---

## Data Rules

Gameplay values must never be hardcoded.

Configuration belongs inside Resources.

Examples:

* KingdomData
* TileData
* EventData
* CommanderData

---

## Scene Rules

Each scene should have one responsibility.

Avoid creating large "god scenes."

Example

Good

* Board Scene
* UI Scene
* Player Scene

Bad

One scene containing every gameplay object.

---

## Testing Requirements

Every system must include:

* Normal Case
* Edge Case
* Failure Case
* Regression Test

A feature is not complete until tested.

---

## Documentation Requirements

Every generated script should include:

* Purpose
* Public API
* Signals
* Dependencies
* Configuration

Future developers should understand every script without reading implementation details.

---

## Performance Requirements

Target

60 FPS

Target Device

Mid-range Android phone.

Avoid unnecessary allocations.

Prefer event-driven architecture.

Profile before optimizing.

---

## Definition of Done

A feature is complete only when:

✓ Compiles successfully

✓ Matches documentation

✓ Passes testing

✓ Works on Android

✓ Uses Resources

✓ Uses Signals

✓ Has documentation

---

# 30. Future Expansion

## Overview

Project Velir is designed as a platform rather than a single standalone game.

The architecture should allow future content without major rewrites.

---

## Planned Gameplay Features

Future systems may include:

### Diplomacy

* Alliances
* Peace Treaties
* Trade Agreements
* Betrayals

---

### Commander Progression

* Experience
* Levels
* Equipment
* Skills
* Promotions

---

### Kingdom Development

* Cities
* Buildings
* Technologies
* Infrastructure

---

### Expanded Battles

* Cavalry
* War Elephants
* Naval Combat
* Fort Sieges
* Terrain Effects

---

### Velir Aram Expansion

The central ruins will become increasingly important.

Possible additions include:

* Hidden chambers
* Puzzle ruins
* Legendary relics
* Ancient guardians
* Multi-stage expeditions

---

### Historical Campaign

Narrative-driven campaigns inspired by Tamil history.

Players experience major historical events through strategic gameplay.

---

### Multiplayer

Future online features:

* Ranked Seasons
* Friend Matches
* Clan System
* Spectator Mode
* Tournament Support

---

### Cosmetic Content

Future cosmetic customization may include:

* Kingdom banners
* Board skins
* Dice skins
* Commander portraits
* Victory animations

Cosmetics will never provide gameplay advantages.

---

### Live Events

Potential future content:

* Seasonal festivals
* Limited-time events
* Historical commemorations
* Community challenges

---

## Modularity

Every future system should integrate using existing architecture.

Expansion should involve adding modules rather than replacing systems.

---

## Final Design Principle

Project Velir should remain faithful to its original vision:

A strategy board game inspired by the great kingdoms of ancient Tamilakam where every match creates a unique story through player decisions, strategic thinking, and exploration.

Complexity should always serve gameplay.

History should inspire gameplay, not restrict it.

The player should leave every match with a memorable story worth sharing.

---

# End of Document

**Document ID:** PV-002

**Document Name:** Master Game Specification

**Version:** 1.0

**Status:** Complete (Version 1)

---

## Change Log

### Version 1.0

Initial master specification completed.

This version establishes the foundation for all subsequent Project Velir documentation.

Future versions will expand each chapter with implementation details, balancing data, UI specifications, engineering notes, and gameplay refinements without changing the core design philosophy established in this document.

---

> **Project Motto**

**"Forge Your Kingdom. Uncover the Forgotten Past. Shape the Future of Tamilakam."**


---
