---

Document ID: PV-024

Category: Engineering Design Document (EDD)

Document Name: Data Model

Project: Project Velir

Version: 1.0

Status: Draft

Owner: Technical Director

Related Documents

* PV-021 Class Diagram & Object Model
* PV-022 Scene Hierarchy
* PV-023 Signal Architecture
* PV-017 Technical Architecture

Last Updated: June 2026

---

# 1. Purpose

> "Every piece of information in Project Velir should have one defined location, one owner, and one lifecycle."

---

## Overview

The Data Model defines how information is represented, stored, accessed, and modified throughout Project Velir.

It specifies:

* Runtime Data
* Persistent Data
* Resource Data
* Data Ownership
* Relationships
* Serialization
* Validation
* Version Compatibility

This document acts as the authoritative specification for all game data.

---

## Objectives

The Data Model has six primary objectives.

### Consistency

Every gameplay value should exist in exactly one authoritative location.

Example

Player Gold

✓ Stored inside Player Runtime

✗ Not duplicated inside UI

---

### Separation

Different categories of information should remain independent.

Project Velir separates:

* Runtime State
* Configuration
* Save Data
* Presentation Data

Mixing these categories is prohibited.

---

### Scalability

Future gameplay systems should introduce new data models rather than modifying unrelated ones.

Examples

* DiplomacyData
* NavalData
* CampaignData

---

### Performance

The runtime model should minimize unnecessary allocations and duplication.

Only active gameplay data should remain in memory.

---

### Serialization

Every runtime object should be serializable for save/load functionality.

Serialization should be deterministic and version-compatible.

---

### AI Readability

Codex should immediately understand:

* Where data belongs.
* Who owns it.
* Who may modify it.
* When it is saved.
* When it is destroyed.

---

## Scope

This document defines:

* Runtime Data
* Resources
* Save Data
* Configuration
* Data Relationships
* Validation Rules

It does **not** define gameplay mechanics.

---

## Audience

This specification is intended for:

* Gameplay Engineers
* AI Coding Assistants
* QA Engineers
* Future Contributors

---

# 2. Data Philosophy

Project Velir follows a strict data-driven architecture.

Code should describe behaviour.

Data should describe gameplay.

---

## Principle 1

### Single Source of Truth

Every gameplay value has exactly one owner.

Example

```text
Gold

↓

Player Runtime
```

UI reads Gold.

SaveManager serializes Gold.

EconomyManager updates Gold.

Only Player Runtime stores Gold.

---

## Principle 2

### Immutable Configuration

Configuration data should never change during gameplay.

Examples

* Kingdom Bonuses
* Tile Types
* Event Definitions
* Battle Multipliers

Configuration belongs inside Resources.

---

## Principle 3

### Mutable Runtime

Runtime data changes continuously during gameplay.

Examples

* Current Gold
* Current Army
* Current Position
* Current Prestige

Runtime data exists only during an active match.

---

## Principle 4

### Separation of Concerns

Project Velir separates:

```text
Configuration

↓

Runtime

↓

Presentation

↓

Persistence
```

Each layer has one responsibility.

---

## Principle 5

### Explicit Ownership

Every data model answers:

Who creates me?

Who modifies me?

Who reads me?

Who saves me?

Who destroys me?

No ownership should be ambiguous.

---

## Principle 6

### Predictable Lifecycle

Every data model follows:

```text
Create

↓

Initialize

↓

Read

↓

Update

↓

Save

↓

Destroy
```

Every gameplay system follows the same lifecycle.

---

## Data Rules

Every data object should satisfy:

✓ One Owner

✓ One Responsibility

✓ Serializable

✓ Testable

✓ Version Compatible

---

# 3. High-Level Data Architecture

Project Velir separates all game information into four major categories.

---

## Architecture Diagram

```text
                 Game Data
                      │
      ┌───────────────┼───────────────┐
      │               │               │
 Runtime         Resources        Save Data
      │               │               │
      └───────────────┼───────────────┘
                      │
               Presentation Data
```

Each category has a unique purpose.

---

## Runtime Data

Contains mutable gameplay information.

Examples

* Current Turn
* Player Position
* Gold
* Army
* Prestige

Destroyed after gameplay ends.

---

## Resource Data

Contains static configuration.

Examples

* KingdomData
* TileData
* EventData
* AIProfile

Loaded during initialization.

Never modified during gameplay.

---

## Save Data

Contains serialized runtime state.

Examples

* Player Progress
* Match State
* Settings
* Statistics

Loaded only during Save and Load operations.

---

## Presentation Data

Contains visual information.

Examples

* Icons
* Animations
* Theme Colors
* Fonts

Presentation data should never affect gameplay calculations.

---

## Data Flow

```text
Resources

↓

Runtime Objects

↓

Managers

↓

UI

↓

Save Data
```

Information should always flow in a predictable direction.

---

## Data Ownership

```text
Player Runtime

↓

Owns

Gold

Army

Prestige

Influence

Position
```

No other object stores these values.

---

## Design Principle

Project Velir's data architecture is designed to be deterministic, modular, and data-driven.

A developer should always be able to answer:

* Where is this data stored?
* Who owns it?
* Who may modify it?
* How long does it exist?

without reading implementation code.

Maintaining this clarity ensures long-term maintainability, easier testing, reliable save/load functionality, and seamless AI-assisted development.

---

**End of Part 1**

**Next Sections (Part 2):**

* 4. Runtime Data Model
* 5. Persistent Data Model
* 6. Resource Data Model
# 4. Runtime Data Model

Runtime Data represents the current state of an active match.

Unlike Resources, Runtime Data changes continuously throughout gameplay.

Runtime Data exists only while a match is active.

When the match ends, Runtime Data is destroyed unless it is serialized by the SaveManager.

---

## Runtime Data Hierarchy

```text id="runtime_data_hierarchy"
GameRuntime
│
├── MatchRuntime
├── TurnRuntime
├── PlayerRuntime
├── BoardRuntime
├── BattleRuntime
├── EventRuntime
├── VelirAramRuntime
└── AIRuntime
```

Each runtime model owns only its own gameplay domain.

---

## GameRuntime

The highest-level runtime object.

Stores:

* Match State
* Current Phase
* Active Managers
* Match Timer
* Game Status

Owner

GameManager

---

## MatchRuntime

Stores information about the current match.

Example Fields

```text id="match_runtime"
match_id

seed

round

turn

difficulty

victory_condition
```

One MatchRuntime exists per game.

---

## TurnRuntime

Stores turn-specific information.

Example Fields

```text id="turn_runtime"
current_player

turn_number

round_number

dice_value

remaining_actions
```

Owner

TurnManager

---

## Runtime Rules

Runtime Data:

✓ Changes frequently

✓ Exists only during gameplay

✓ Is serializable

✓ Never stores configuration

---

# 5. Persistent Data Model

Persistent Data survives after gameplay ends.

It stores player progress and long-term information.

Persistent Data is loaded when the application starts and saved whenever appropriate.

---

## Persistent Categories

```text id="persistent_categories"
Save Slots

Settings

Statistics

Achievements (Future)

Profile (Future)
```

Persistent data is independent of any individual match.

---

## Save Slot Data

Each save slot stores:

```text id="save_slot_data"
slot_id

save_version

timestamp

match_state

player_progress
```

Only SaveManager may modify save slots.

---

## Settings Data

Stores user preferences.

Examples

```text id="settings_data"
music_volume

sfx_volume

language

graphics_quality

accessibility_options
```

Settings remain independent of gameplay.

---

## Statistics Data

Stores long-term statistics.

Examples

```text id="statistics_data"
games_played

games_won

games_lost

total_gold

battles_won

battles_lost
```

Statistics are updated only after a match ends.

---

## Persistent Rules

Persistent Data:

✓ Survives application restart

✓ Uses versioned serialization

✓ Never stores temporary runtime objects

---

# 6. Resource Data Model

Resources define static gameplay configuration.

Resources never change during an active match.

Managers read Resources during initialization and whenever configuration information is required.

---

## Resource Hierarchy

```text id="resource_hierarchy"
Resources
│
├── KingdomData
├── CommanderData
├── BoardData
├── TileData
├── EventData
├── BattleConfig
├── EconomyConfig
├── AIProfile
├── UITheme
└── AudioData
```

Each Resource is responsible for a single category of configuration.

---

## KingdomData

Stores:

```text id="kingdom_resource"
kingdom_id

name

banner

color

passive_ability

starting_bonus

description
```

Runtime values are excluded.

---

## BoardData

Stores:

* Number of Tiles
* Tile Connections
* Region Layout
* Ancient Site Locations

BoardData never stores player positions.

---

## TileData

Stores:

```text id="tile_resource"
tile_id

tile_type

reward

icon

description

special_rules
```

Ownership is determined during gameplay, not inside TileData.

---

## EventData

Stores:

* Event Name
* Category
* Description
* Probability
* Rewards
* Penalties

Events are defined once and reused across every match.

---

## BattleConfig

Stores:

* Battle Rewards
* Multipliers
* Difficulty Modifiers
* Balance Values

Battle results are stored in Runtime Data.

---

## AIProfile

Stores:

```text id="ai_profile"
aggression

expansion_priority

risk_tolerance

resource_priority

exploration_priority
```

AI behaviour changes by selecting different profiles rather than changing code.

---

## UITheme

Stores:

* Colors
* Fonts
* Icons
* HUD Layout
* Button Styles

Gameplay systems should never reference UITheme directly.

---

## Resource Rules

Every Resource must satisfy:

✓ Immutable

✓ Serializable

✓ Human Readable

✓ Independently Reusable

✓ Version Compatible

---

## Resource Relationship Diagram

```text id="resource_relationship_diagram"
KingdomData

↓

CommanderData

↓

BattleConfig

↓

EconomyConfig

↓

AIProfile
```

Resources may reference other Resources but must never reference Runtime Data.

---

## Design Principle

Resources define the rules of the world.

Runtime Data records what is currently happening within that world.

Persistent Data preserves what should survive between play sessions.

Keeping these three categories strictly separated ensures that gameplay remains predictable, configurable, and maintainable throughout the lifetime of Project Velir.

---

**End of Part 2**

**Next Sections (Part 3):**

* 7. Kingdom Data Model
* 8. Board Data Model
* 9. Tile Data Model
# 7. Kingdom Data Model

The Kingdom Data Model defines every piece of information required to represent one playable kingdom.

KingdomData is a configuration Resource.

KingdomRuntime stores the changing state during gameplay.

This separation allows the same KingdomData to be reused across every match.

---

## Kingdom Architecture

```text id="kingdom_architecture"
Kingdom
│
├── KingdomData
│
└── KingdomRuntime
```

Configuration and runtime state should never be mixed.

---

## KingdomData Structure

Stores immutable information.

```text id="kingdom_data_fields"
kingdom_id

display_name

description

banner

symbol

primary_color

secondary_color

starting_gold

starting_army

starting_prestige

passive_ability

kingdom_theme

ai_profile
```

These values never change during gameplay.

---

## KingdomRuntime Structure

Stores mutable gameplay state.

```text id="kingdom_runtime_fields"
player_id

current_gold

current_army

current_prestige

current_influence

owned_tiles

current_position

active_effects
```

Owner

PlayerManager

---

## Relationship

```text id="kingdom_relationship"
KingdomData

↓

Create

↓

KingdomRuntime

↓

Gameplay Updates

↓

SaveManager
```

---

## Kingdom Rules

Every kingdom must have:

✓ Unique ID

✓ Unique Banner

✓ Unique Passive Ability

✓ Dedicated AI Profile

✓ Balanced Starting Resources

---

# 8. Board Data Model

The Board Data Model defines the complete structure of the Project Velir game board.

Unlike BoardRuntime, BoardData never changes during gameplay.

---

## Board Structure

```text id="board_structure"
BoardData
│
├── Regions
├── Tiles
├── Connections
├── Ancient Sites
└── Spawn Points
```

---

## BoardData Fields

```text id="board_fields"
board_id

board_name

tile_count

region_count

spawn_locations

ancient_sites

board_theme
```

---

## Region Structure

Each region stores:

```text id="region_fields"
region_id

region_name

kingdom

tile_ids

background

music_theme
```

Version 1 includes:

* Chola
* Chera
* Pandya
* Pallava
* Velir Aram

---

## Connection Data

Stores valid movement paths.

```text id="connection_fields"
from_tile

to_tile

movement_cost

connection_type
```

Examples

* Road
* River Crossing
* Ancient Path

Future versions may introduce restricted routes.

---

## Spawn Data

Stores starting positions.

```text id="spawn_fields"
player_id

spawn_tile

kingdom
```

Spawn positions are assigned during match initialization.

---

## Board Rules

BoardData should:

✓ Never store player positions

✓ Never store runtime ownership

✓ Remain reusable

✓ Support multiple board layouts

---

# 9. Tile Data Model

Every tile on the board is defined using TileData.

Tiles are one of the most reusable data structures in the game.

---

## Tile Architecture

```text id="tile_architecture"
TileData

↓

TileRuntime

↓

Tile Scene
```

Each layer has one responsibility.

---

## TileData Fields

```text id="tile_data_fields"
tile_id

tile_name

tile_type

region

reward_type

reward_value

special_rule

icon

sprite

description
```

---

## Tile Types

Version 1 supports:

```text id="tile_types"
Trade

Battle

Tax

Village

Fort

Temple

Ancient

Kingdom

Neutral

Mystery
```

New tile types can be added without changing the Tile Scene.

---

## TileRuntime Fields

```text id="tile_runtime_fields"
occupied

occupying_player

visited

active_effect

temporary_modifier
```

Owner

BoardManager

---

## Reward Structure

Example

```text id="reward_structure"
reward_type

↓

Gold

Prestige

Army

Influence

Relic

Event

Nothing
```

Rewards are configured using TileData.

EconomyManager applies them during gameplay.

---

## Special Rules

Tiles may contain optional gameplay modifiers.

Examples

* Double Reward
* Battle Bonus
* Safe Zone
* Extra Turn
* Ancient Trigger

Special rules remain configurable.

---

## Tile Relationship

```text id="tile_relationship"
BoardData

↓

TileData

↓

TileRuntime

↓

Tile Scene
```

The hierarchy always flows downward.

---

## Tile Rules

Every tile must satisfy:

✓ Unique Tile ID

✓ One Tile Type

✓ One Region

✓ One Reward Definition

✓ Optional Special Rule

---

## Data Dependency Diagram

```text id="data_dependency"
KingdomData

↓

BoardData

↓

TileData

↓

TileRuntime

↓

PlayerRuntime
```

Managers coordinate interactions between these models.

---

## Design Principle

Kingdoms, Boards, and Tiles together define the physical world of Project Velir.

Static Resources describe how the world is built.

Runtime Data records what is happening within that world.

By separating immutable configuration from mutable runtime state, the game becomes easier to balance, test, serialize, and expand with new kingdoms, boards, and tile types.

---

**End of Part 3**

**Next Sections (Part 4):**

* 10. Player Data Model
* 11. Economy Data Model
* 12. Battle Data Model
# 10. Player Data Model

The Player Data Model represents the complete state of a player during an active match.

Unlike KingdomData, which defines a kingdom's identity, PlayerRuntime stores the current state of that kingdom in a specific game session.

Each player owns exactly one PlayerRuntime.

PlayerRuntime is managed exclusively by **PlayerManager**.

---

## Player Architecture

```text
Player
│
├── KingdomData
│
├── PlayerRuntime
│
└── PlayerScene
```

Each layer has a distinct responsibility.

* KingdomData defines the kingdom.
* PlayerRuntime stores gameplay state.
* PlayerScene presents the player visually.

---

## PlayerRuntime Structure

```text
player_id

player_name

kingdom_id

player_type

difficulty

current_tile

gold

army

prestige

influence

action_points

movement_points

owned_regions

owned_relics

active_effects

status
```

PlayerRuntime contains only mutable gameplay information.

---

## Player Types

Version 1 supports:

```text
Human

AI
```

Future versions may include:

```text
Network Player

Spectator

Replay Ghost
```

---

## Player Status

Supported states:

```text
Waiting

Active

Moving

Battling

Exploring

Paused

Defeated
```

Only one status should be active at any time.

---

## Player Relationships

```text
PlayerRuntime

↓

Current Tile

↓

Economy

↓

Army

↓

Battles

↓

Events
```

PlayerRuntime acts as the central runtime representation of a kingdom.

---

## Player Rules

Every player must satisfy:

✓ Unique Player ID

✓ One Kingdom

✓ One Runtime Object

✓ One Current Position

✓ Serializable

---

# 11. Economy Data Model

The Economy Data Model defines all resources that influence player progression.

Economy data is divided into:

* Configuration
* Runtime
* Statistics

This separation simplifies balancing and save/load functionality.

---

## Economy Architecture

```text
EconomyConfig

↓

EconomyRuntime

↓

EconomyStatistics
```

Each layer serves a different purpose.

---

## EconomyConfig

Stores static balance values.

```text
starting_gold

maximum_gold

battle_reward

trade_reward

tax_reward

maintenance_cost

recruitment_cost
```

These values are read-only during gameplay.

---

## EconomyRuntime

Stores the current resource values for each player.

```text
gold

income

expenses

prestige

influence

army_size

resource_multiplier
```

Owner

EconomyManager

---

## Economy Statistics

Tracks long-term information.

```text
gold_earned

gold_spent

highest_gold

total_income

total_expenses

average_income
```

Statistics are updated throughout the match and saved at the end.

---

## Resource Categories

Version 1 includes:

```text
Gold

Army

Prestige

Influence
```

Future versions may introduce:

```text
Food

Wood

Stone

Iron

Faith

Population
```

The model supports expansion without structural changes.

---

## Economy Rules

Economy data should:

✓ Be owned by EconomyManager

✓ Be serializable

✓ Never be duplicated inside the UI

✓ Update only through EconomyManager

---

# 12. Battle Data Model

The Battle Data Model represents every combat encounter during gameplay.

BattleRuntime exists only while a battle is active.

After combat ends, it is destroyed.

---

## Battle Architecture

```text
BattleConfig

↓

BattleRuntime

↓

BattleResult
```

Each stage represents a different aspect of combat.

---

## BattleConfig

Stores static combat rules.

```text
base_attack

base_defense

critical_chance

battle_reward

prestige_reward

difficulty_modifier
```

Configuration remains constant throughout the match.

---

## BattleRuntime

Stores temporary combat state.

```text
battle_id

attacker

defender

battle_type

attacker_strength

defender_strength

terrain_modifier

battle_state
```

Owner

BattleManager

---

## Battle States

Supported states:

```text
Preparing

Calculating

Animating

Resolving

Completed
```

Only one state may be active.

---

## BattleResult

Stores the outcome.

```text
winner

loser

gold_reward

prestige_reward

army_losses

experience

battle_duration
```

BattleResult is forwarded to:

* EconomyManager
* StatisticsManager
* SaveManager

---

## Combat Flow

```text
Battle Requested

↓

BattleRuntime Created

↓

Battle Calculated

↓

Result Generated

↓

Rewards Applied

↓

BattleRuntime Destroyed
```

The runtime object exists only for the duration of combat.

---

## Battle Rules

Every battle must satisfy:

✓ One Attacker

✓ One Defender

✓ One Result

✓ One Reward Calculation

✓ One Completion Event

---

## Data Relationship Diagram

```text
PlayerRuntime

↓

BattleRuntime

↓

BattleResult

↓

EconomyRuntime

↓

Statistics
```

This sequence ensures that combat data flows cleanly through the gameplay systems.

---

## Design Principle

Player, Economy, and Battle data models represent the dynamic core of Project Velir.

These models change constantly throughout a match and therefore require strict ownership, predictable lifecycles, and clear separation from configuration data.

By isolating mutable runtime state from static Resources and long-term Persistent Data, Project Velir ensures reliable gameplay, accurate save/load functionality, easier balancing, and a robust foundation for future systems such as diplomacy, multiplayer, commander progression, and advanced resource management.

---

**End of Part 4**

**Next Sections (Part 5):**

* 13. Event Data Model
* 14. AI Data Model
* 15. Save Data Model
* 16. Serialization & Versioning
# 13. Event Data Model

The Event Data Model defines every gameplay event that may occur during a match.

Events provide variety, strategic depth, and replayability while remaining completely data-driven.

Every event is defined as a Resource and instantiated as a Runtime Event only when triggered.

---

## Event Architecture

```text id="event_architecture"
EventData
│
├── EventRuntime
│
└── EventResult
```

Each layer has a unique responsibility.

---

## EventData

Stores immutable event definitions.

```text
event_id

event_name

event_category

rarity

probability

description

requirements

rewards

penalties

icon

artwork
```

Owner

EventManager

---

## Event Categories

Version 1 supports:

```text
Trade

Battle

Kingdom

Ancient

Economy

Mystery

Disaster

Opportunity
```

Future versions may introduce:

```text
Diplomacy

Campaign

Seasonal

Multiplayer
```

---

## EventRuntime

Created only while an event is active.

```text
runtime_id

player_id

event_id

start_time

current_state

selected_option

temporary_rewards
```

Destroyed immediately after event completion.

---

## EventResult

Stores the outcome of the event.

```text
completed

reward_type

reward_amount

prestige_change

gold_change

army_change

next_event
```

The EventResult is forwarded to:

* EconomyManager
* PlayerManager
* StatisticsManager
* SaveManager

---

## Event Lifecycle

```text
Tile Resolved

↓

Select Event

↓

Create Runtime

↓

Player Choice

↓

Resolve

↓

Apply Rewards

↓

Destroy Runtime
```

---

## Event Rules

Every event must satisfy:

✓ Unique Event ID

✓ Category

✓ Probability

✓ Reward Definition

✓ Serializable

✓ Data Driven

---

# 14. AI Data Model

The AI Data Model defines how AI kingdoms make strategic decisions.

Rather than hardcoding behaviour, AI uses configurable profiles and runtime state.

---

## AI Architecture

```text
AIProfile

↓

AIRuntime

↓

AIDecision

↓

AIStatistics
```

---

## AIProfile

Stores configuration values.

```text
profile_id

difficulty

aggression

expansion_priority

economy_priority

battle_priority

exploration_priority

risk_tolerance

decision_delay
```

Profiles never change during gameplay.

---

## AIRuntime

Stores temporary AI state.

```text
current_goal

current_target

available_actions

evaluation_score

decision_timer

last_action

current_strategy
```

Owner

AIManager

---

## AIDecision

Represents one calculated action.

```text
decision_type

priority

target_tile

expected_reward

confidence_score
```

Decision Types

```text
Move

Attack

Trade

Recruit

Explore

End Turn
```

---

## AI Statistics

Tracks long-term AI behaviour.

```text
turns_played

battles_won

gold_earned

events_completed

tiles_explored
```

Used for balancing future AI improvements.

---

## AI Lifecycle

```text
Turn Begins

↓

Evaluate Board

↓

Generate Decisions

↓

Select Best Action

↓

Execute

↓

Update Statistics
```

---

## AI Rules

AI data should:

✓ Be deterministic

✓ Use configuration profiles

✓ Never cheat

✓ Never access hidden information

---

# 15. Save Data Model

The Save Data Model defines exactly what information is written to disk.

Save files must contain enough information to restore the game completely.

---

## Save Architecture

```text
SaveGame
│
├── Metadata
├── Match Data
├── Player Data
├── Board Data
├── Economy Data
├── Event Data
├── AI Data
└── Statistics
```

---

## Metadata

```text
save_version

save_time

game_version

play_time

checksum
```

Metadata is used before loading.

---

## Match Data

```text
match_seed

difficulty

current_round

current_turn

victory_condition

active_player
```

---

## Player Save Data

For every player:

```text
player_id

kingdom

gold

army

prestige

influence

current_tile

owned_relics

active_effects
```

---

## Board Save Data

```text
visited_tiles

captured_tiles

active_events

ancient_sites

temporary_modifiers
```

---

## Economy Save Data

```text
gold

income

expenses

multipliers
```

---

## AI Save Data

```text
current_goal

current_strategy

last_action

difficulty
```

---

## Save Rules

Save files should:

✓ Be versioned

✓ Be deterministic

✓ Be platform independent

✓ Never contain temporary scene references

✓ Never contain Node paths

---

# 16. Serialization & Versioning

Serialization converts runtime data into a format suitable for storage.

Versioning ensures future releases remain compatible with older save files.

---

## Serialization Flow

```text
Runtime Objects

↓

Save Objects

↓

Serialize

↓

Write File
```

Loading reverses the same process.

---

## Serialization Rules

Serialize only:

* Runtime values
* Player progress
* Match state
* Statistics
* Settings

Do not serialize:

* Scene Nodes
* Signals
* Animation Players
* Cached references

---

## Save Version

Every save file includes:

```text
major_version

minor_version

build_number
```

Example

```text
1.0.0
```

---

## Version Compatibility

Future versions should:

* Detect older saves
* Upgrade data automatically where possible
* Warn the player if migration is impossible

---

## Data Integrity

Every save file should include:

* Checksum
* Validation Status
* Save Timestamp

This prevents loading corrupted or incomplete save data.

---

## Serialization Checklist

Every serialized object must satisfy:

✓ Serializable

✓ Version Compatible

✓ Platform Independent

✓ Human Readable (Debug Builds)

✓ Restorable

---

## Design Principle

Event, AI, and Save Data complete the information architecture of Project Velir.

Together with Runtime Data, Resource Data, and Persistent Data, these models ensure that every piece of information in the game has a clearly defined owner, lifecycle, and storage strategy.

By separating transient gameplay state from permanent configuration and serialized save information, Project Velir establishes a robust data architecture that supports reliable gameplay, seamless save/load functionality, efficient debugging, future content updates, and AI-assisted development.

---

**End of Part 5**

**Next Sections (Final Part):**

* 17. Data Validation Rules
* 18. Acceptance Criteria
* 19. Codex Implementation Notes
* 20. Future Expansion
* 21. Data Architecture Best Practices
* 22. Design Principle & Conclusion
# 17. Data Validation Rules

Every data object in Project Velir must be validated before being used during gameplay.

Validation ensures data integrity, prevents corrupted runtime states, and simplifies debugging.

Every Resource, Runtime object, and Save object must pass validation before becoming active.

---

## Validation Philosophy

Validation should occur as early as possible.

Preferred sequence:

```text
Load Data

↓

Validate

↓

Initialize

↓

Use
```

Invalid data should never enter the gameplay loop.

---

## Resource Validation

Every Resource should verify:

✓ Required fields exist

✓ IDs are unique

✓ References are valid

✓ Values are within allowed ranges

✓ Required assets are available

Example

```text
KingdomData

↓

Validate Banner

↓

Validate Passive Ability

↓

Validate Starting Resources

↓

Ready
```

---

## Runtime Validation

Runtime objects should verify:

✓ Valid owner

✓ Valid references

✓ Current state

✓ Position

✓ Resource values

Example

```text
PlayerRuntime

↓

Current Tile Exists

↓

Gold ≥ 0

↓

Army ≥ 0

↓

Status Valid
```

---

## Save Validation

Before loading a save:

Verify

```text
Save Version

↓

Checksum

↓

Metadata

↓

Serialized Objects

↓

Restore
```

If validation fails:

* Display an error
* Abort loading
* Preserve the current game state

---

## Data Constraints

Examples

Gold

```text
Minimum = 0
```

Army

```text
Minimum = 0
```

Prestige

```text
Minimum = 0
```

Influence

```text
Minimum = 0
```

Tile ID

Must exist inside BoardData.

Player ID

Must reference an active player.

---

## Validation Rules

Every data model should satisfy:

✓ Consistent

✓ Complete

✓ Serializable

✓ Restorable

✓ Deterministic

---

# 18. Acceptance Criteria

The Data Model specification is considered complete when:

✓ Every major data category is documented.

✓ Every runtime object has an owner.

✓ Every Resource is defined.

✓ Save data is fully documented.

✓ Validation rules are established.

✓ Serialization strategy is documented.

✓ Version compatibility is defined.

✓ Data relationships are clearly described.

✓ Future expansion points are identified.

Any new gameplay system introduced into Project Velir should extend this document before implementation begins.

---

# 19. Codex Implementation Notes

Codex should treat this document as the authoritative reference for every data structure in Project Velir.

Before implementing a new gameplay system, verify:

* Which data model owns the information.
* Whether the information is Runtime, Resource, or Persistent.
* Which manager is responsible for modifications.
* Whether the data should be serialized.

---

## Implementation Rules

Every data model should:

* Have one owner.
* Have one responsibility.
* Be fully documented.
* Be serializable when required.
* Avoid duplicated values.
* Prefer Resources for configuration.
* Prefer Runtime objects for mutable gameplay state.

Never hardcode gameplay values inside managers when a Resource is more appropriate.

---

## Naming Conventions

Data classes should follow consistent naming.

Examples

```text
PlayerRuntime

KingdomData

BattleConfig

EconomyRuntime

EventData

SaveGame

AIProfile
```

Avoid ambiguous names such as:

```text
Data

Info

Object

ManagerData
```

Every name should clearly communicate its purpose.

---

# 20. Future Expansion

The Data Model has been designed to support future systems without requiring architectural redesign.

Future data models may include:

---

## Gameplay

```text
DiplomacyData

ProvinceData

NavalData

CommanderData

QuestData
```

---

## Multiplayer

```text
LobbyData

NetworkPlayerData

MatchmakingData

ReplayData
```

---

## Live Operations

```text
SeasonData

DailyRewardData

LeaderboardData

CloudSaveData
```

---

## Accessibility

```text
AccessibilityProfile

ControlProfile

AudioProfile

ThemeProfile
```

Each future data model should follow the same ownership, lifecycle, validation, and serialization principles defined in this document.

---

# 21. Data Architecture Best Practices

The following practices should guide every data-related implementation in Project Velir.

---

## Ownership

Every value has one owner.

Never duplicate mutable data across multiple systems.

---

## Separation

Keep configuration, runtime state, presentation, and persistence separate.

Each category serves a different purpose.

---

## Serialization

Only serialize information required to restore gameplay.

Do not serialize:

* Nodes
* Signals
* Scene references
* Animation state
* Cached calculations

---

## Performance

Avoid unnecessary allocations.

Reuse runtime objects where practical.

Prefer lightweight Resources for static configuration.

---

## Documentation

Whenever a new variable is introduced:

* Document it.
* Define its owner.
* Define its lifecycle.
* Define its serialization requirements.

The documentation should remain synchronized with implementation throughout development.

---

# 22. Design Principle & Conclusion

The Data Model is the foundation of every gameplay system in Project Velir.

Every manager, runtime object, resource, and save file ultimately depends on the consistency of the underlying data architecture.

By enforcing:

* Single ownership
* Clear responsibilities
* Data-driven configuration
* Predictable lifecycles
* Reliable serialization
* Strong validation

Project Velir establishes a robust foundation capable of supporting future gameplay systems, AI enhancements, multiplayer functionality, live content, and long-term maintenance.

A developer or AI coding assistant should be able to determine where any piece of information belongs without reading implementation code.

This document, together with:

* **PV-021 — Class Diagram & Object Model**
* **PV-022 — Scene Hierarchy Specification**
* **PV-023 — Signal Architecture**

forms the core engineering blueprint for Project Velir's software architecture.

---

## End of Document

**Document ID:** PV-024

**Category:** Engineering Design Document (EDD)

**Document Name:** Data Model

**Version:** 1.0

**Status:** Complete
