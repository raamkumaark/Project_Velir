---

Document ID: PV-021

Category: Engineering Design Document (EDD)

Document Name: Class Diagram & Object Model

Project: Project Velir

Version: 1.0

Status: Draft

Owner: Technical Director

Related Documents:

* PV-002 Master Game Specification
* PV-004 Core Gameplay Loop
* PV-005 Gameplay Systems
* PV-017 Technical Architecture

Last Updated: June 2026

---

# 1. Purpose

> *"A game's architecture determines how easily it can grow."*

---

## Overview

This document defines the complete software architecture of Project Velir.

Unlike the previous design documents, which describe **what the game should do**, this document describes **how the game is constructed internally**.

It serves as the master blueprint for:

* Runtime objects
* Managers
* Resources
* Scene ownership
* Object relationships
* Dependencies
* Communication rules
* Future scalability

Every gameplay system implemented throughout Project Velir should conform to the architecture described in this document.

---

## Primary Goals

The architecture is designed to achieve the following objectives.

### Scalability

New gameplay systems should be added without requiring major modifications to existing code.

Example

Adding Diplomacy should not require rewriting BattleManager.

Adding Naval Battles should not require changing TurnManager.

---

### Modularity

Every gameplay system should exist as an independent module.

Examples

* Board System
* Economy System
* Battle System
* Event System

Each system should be removable, replaceable, or expandable with minimal impact on the rest of the project.

---

### Maintainability

Code should remain understandable after years of development.

Future contributors should understand the project primarily through documentation rather than reverse-engineering source code.

---

### Testability

Every manager should be independently testable.

The architecture intentionally minimizes hidden dependencies to make automated testing straightforward.

---

### AI Compatibility

Project Velir is designed specifically for AI-assisted software engineering.

The architecture should enable tools such as Codex to:

* Understand ownership
* Understand dependencies
* Generate isolated features
* Refactor safely
* Write tests
* Extend gameplay

Every system should have clearly defined responsibilities.

---

## Scope

This document defines the architecture for Version 1 of Project Velir.

It covers:

* Runtime architecture
* Manager hierarchy
* Resource ownership
* Object lifecycle
* Communication model

It does **not** define gameplay mechanics.

Gameplay behavior is documented separately in the Design Documentation.

---

## Audience

This document is intended for:

* Gameplay Programmers
* Technical Artists
* AI Coding Assistants
* QA Engineers
* Future Contributors

Readers are expected to understand basic object-oriented programming concepts.

---

## Architectural Vision

Project Velir follows a **Manager-Based, Data-Driven, Event-Oriented Architecture**.

Three principles guide every implementation.

```
Data

↓

Logic

↓

Presentation
```

Gameplay data should never depend on user interface elements.

User interface elements should never contain gameplay logic.

Managers coordinate gameplay.

Resources store configuration.

Scenes present information.

---

## Architecture Success Criteria

The architecture is considered successful when:

✓ Every gameplay system has a single owner.

✓ Every manager has one responsibility.

✓ No circular dependencies exist.

✓ Systems communicate through Signals.

✓ Gameplay values remain data-driven.

✓ New features integrate without architectural redesign.

---

# 2. Engineering Philosophy

The software architecture of Project Velir is guided by a small number of strict engineering principles.

Every implementation should reinforce these principles.

If a proposed feature violates multiple principles, the implementation should be redesigned.

---

## Principle 1

### Single Responsibility

Every manager owns one gameplay domain.

Examples

GameManager

Responsible only for overall game state.

TurnManager

Responsible only for turn progression.

BattleManager

Responsible only for battle resolution.

EconomyManager

Responsible only for resource management.

Managers should never absorb unrelated responsibilities.

---

## Principle 2

### Composition Over Inheritance

Project Velir favors composition whenever possible.

Preferred

```
GameManager

↓

BoardManager

↓

Tile Objects
```

Avoid

```
BoardManager

↓

AdvancedBoardManager

↓

UltimateBoardManager
```

Complex inheritance hierarchies reduce flexibility and increase maintenance cost.

---

## Principle 3

### Data-Driven Design

Gameplay behavior should be controlled through Resources rather than hardcoded values.

Example

Instead of

```
Battle Reward = 25
```

Store

```
BattleConfig.tres

Reward = 25
```

Changing balance should rarely require code changes.

---

## Principle 4

### Event-Oriented Communication

Managers communicate through Signals rather than direct ownership.

Preferred

```
DiceManager

↓

dice_rolled

↓

TurnManager
```

Avoid

```
DiceManager

↓

TurnManager.move_player()

↓

BoardManager

↓

UIManager
```

Signal-based communication improves modularity.

---

## Principle 5

### Loose Coupling

Managers should know as little as possible about one another.

Example

BattleManager should not directly modify UI.

Instead

```
battle_finished

↓

UIManager updates interface
```

This allows gameplay systems to evolve independently.

---

## Principle 6

### High Cohesion

Every script should solve one clearly defined problem.

If a script becomes responsible for multiple unrelated systems, it should be divided.

Target script size

Approximately 300–600 lines.

Managers exceeding 1,000 lines should be evaluated for refactoring.

---

## Principle 7

### Predictable Runtime

Gameplay should remain deterministic.

Given identical:

* Board State
* Dice Rolls
* Player Decisions

the game should always produce identical results.

This simplifies debugging, testing, and multiplayer synchronization.

---

## Principle 8

### Documentation Before Implementation

No gameplay system should be implemented without a corresponding engineering specification.

Documentation defines architecture.

Code implements architecture.

---

## Engineering Checklist

Every new system should satisfy the following questions.

| Question                  | Required |
| ------------------------- | -------- |
| Single Responsibility?    | ✓        |
| Uses Resources?           | ✓        |
| Uses Signals?             | ✓        |
| Independently Testable?   | ✓        |
| No Circular Dependencies? | ✓        |
| Mobile Friendly?          | ✓        |
| AI Readable?              | ✓        |

Features failing multiple checks should be redesigned before implementation.

---

# 3. High-Level Architecture

Project Velir follows a layered software architecture.

Each layer has clearly defined responsibilities.

No layer should bypass another.

---

## Architectural Layers

```
Player

↓

User Interface

↓

Gameplay Managers

↓

Runtime Objects

↓

Data Resources

↓

Godot Engine
```

Each layer communicates only with its neighboring layers.

---

## Layer Responsibilities

### Layer 1

Player

Provides input.

Makes strategic decisions.

Receives feedback.

---

### Layer 2

User Interface

Displays information.

Receives touch input.

Sends gameplay requests.

Contains **no gameplay logic**.

---

### Layer 3

Gameplay Managers

Coordinate every gameplay system.

Examples

* TurnManager
* EconomyManager
* BattleManager

Managers act as the brain of the application.

---

### Layer 4

Runtime Objects

Represent active gameplay entities.

Examples

* Players
* Tiles
* Dice
* Ancient Sites

These objects maintain the current match state.

---

### Layer 5

Resources

Store static configuration.

Examples

* KingdomData
* TileData
* BattleConfig
* EventData

Resources never store runtime state.

---

### Layer 6

Godot Engine

Responsible for:

* Rendering
* Physics
* Input
* Audio
* Scene Management

The engine provides infrastructure.

Gameplay remains independent.

---

## Complete Architecture Diagram

```
                 PLAYER
                    │
                    ▼
            USER INTERFACE
                    │
                    ▼
             GAME MANAGERS
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
   Runtime      Runtime     Runtime
   Objects      Objects     Objects
        │           │           │
        └───────────┼───────────┘
                    ▼
             DATA RESOURCES
                    │
                    ▼
              GODOT ENGINE
```

---

## Information Flow

Information should always travel downward.

```
Player

↓

UI

↓

Manager

↓

Runtime Object

↓

Resource Lookup

↓

Manager

↓

UI

↓

Player
```

No shortcuts should bypass architectural layers.

---

## Architectural Boundaries

The following boundaries are mandatory.

UI cannot modify Resources.

Resources cannot reference Managers.

Managers cannot depend on UI implementation.

Runtime Objects cannot own Managers.

These boundaries preserve long-term maintainability.

---

## Design Principle

The architecture of Project Velir should remain understandable even after years of expansion.

Every new gameplay feature should naturally fit into the existing structure without requiring major redesign.

A developer reading this document should understand where every future system belongs before writing a single line of code.

---

**End of Part 1**

**Next Sections (Part 2):**

* 4. Runtime Object Model
* 5. Manager Hierarchy
* 6. Resource Hierarchy
# 4. Runtime Object Model

The Runtime Object Model defines every object that exists while a match is being played.

Unlike Resources, which contain static configuration, Runtime Objects represent the changing state of the current game.

Every Runtime Object has:

* A clearly defined owner.
* A defined lifetime.
* A single responsibility.
* A predictable creation and destruction sequence.

---

## Runtime Hierarchy

```text
Game Session
│
├── GameManager
│
├── Player Objects
│   ├── Chola
│   ├── Chera
│   ├── Pandya
│   └── Pallava
│
├── Board
│   ├── Tiles
│   ├── Ancient Sites
│   └── Connections
│
├── Dice
│
├── Active Events
│
├── Battle Context
│
└── UI Runtime
```

Every runtime object exists only during an active match.

---

## Runtime Object Categories

### Session Objects

Created once.

Destroyed when the match ends.

Examples

* GameManager
* TurnManager
* BoardManager
* EconomyManager

---

### Match Objects

Created at match start.

Destroyed when returning to Main Menu.

Examples

* Player
* Kingdom Runtime
* Board Runtime
* Ancient Site Runtime

---

### Temporary Objects

Created only when required.

Destroyed immediately after use.

Examples

* Battle Context
* Event Popup
* Reward Animation
* Dice Roll Animation
* Tooltip

Temporary objects should never become permanent.

---

## Runtime Ownership

Every runtime object must have exactly one owner.

Example

```text
GameManager

└── PlayerManager

      └── Player Runtime
```

Ownership determines:

* Creation
* Updates
* Cleanup
* Save State

Objects should never have multiple owners.

---

## Runtime Lifecycle

```text
Create

↓

Initialize

↓

Register

↓

Update

↓

Deactivate

↓

Destroy
```

Every object follows this lifecycle.

Skipping stages is not permitted.

---

## Runtime Responsibilities

Runtime objects are responsible only for mutable state.

Examples

Player Runtime

Stores:

* Current Gold
* Army
* Prestige
* Influence
* Position

Does NOT store:

* Kingdom Artwork
* Passive Description
* Colors

Those belong inside Resources.

---

## Runtime Object Rules

All runtime objects must satisfy:

✓ Single Owner

✓ Single Responsibility

✓ Predictable Lifecycle

✓ Save Compatible

✓ Testable

---

# 5. Manager Hierarchy

Managers coordinate gameplay.

Managers never represent gameplay themselves.

Instead, they orchestrate interactions between runtime objects and data resources.

---

## Core Manager Architecture

```text
GameManager
│
├── TurnManager
├── PlayerManager
├── BoardManager
├── DiceManager
├── EconomyManager
├── BattleManager
├── EventManager
├── VelirAramManager
├── AIManager
├── SaveManager
├── UIManager
└── AudioManager
```

GameManager acts as the root coordinator.

Managers should never own each other directly.

---

## Manager Responsibilities

### GameManager

Owns:

* Match lifecycle
* Initialization
* Shutdown
* Global State

Never performs gameplay calculations.

---

### TurnManager

Owns:

* Turn Order
* Round Progression
* Active Player

Never modifies resources.

---

### PlayerManager

Owns:

* Player Runtime Objects
* Kingdom Runtime
* Player Statistics

Never controls UI.

---

### BoardManager

Owns:

* Tile Runtime
* Player Movement
* Tile Lookup
* Tile Resolution

Never resolves battles.

---

### DiceManager

Owns:

* Dice Roll
* Random Generation
* Dice Animation Requests

Never moves players directly.

---

### EconomyManager

Owns:

* Gold
* Income
* Spending
* Resource Updates

Never modifies board state.

---

### BattleManager

Owns:

* Battle Resolution
* Battle Rewards
* Battle Statistics

Never updates UI directly.

---

### EventManager

Owns:

* Event Deck
* Event Selection
* Event Resolution

Never stores player data.

---

### VelirAramManager

Owns:

* Ancient Region
* Ancient Exploration
* Relics
* Ancient Discoveries

Never manages economy.

---

### AIManager

Owns:

* AI Decisions
* Difficulty
* Utility Evaluation

Never bypasses gameplay rules.

---

### SaveManager

Owns:

* Save
* Load
* Serialization
* Version Migration

Never changes gameplay values.

---

### UIManager

Owns:

* HUD
* Menus
* Popups
* Notifications

Contains no gameplay logic.

---

### AudioManager

Owns:

* Music
* Sound Effects
* Audio Buses
* Volume Settings

Never receives direct gameplay ownership.

---

## Manager Dependency Rules

Managers communicate only through:

* Signals
* Public APIs

Managers must never directly manipulate another manager's internal variables.

Correct

```text
BattleManager

↓

battle_finished

↓

EconomyManager
```

Incorrect

```text
BattleManager

↓

EconomyManager.gold += 50
```

---

## Manager Lifecycle

```text
Instantiate

↓

Initialize

↓

Connect Signals

↓

Ready

↓

Runtime Updates

↓

Shutdown

↓

Cleanup
```

All managers follow the same lifecycle.

---

## Manager Design Rules

Every manager must:

* Own one system.
* Expose a minimal public API.
* Hide implementation details.
* Be independently testable.
* Remain under approximately 600 lines where practical.

Large managers should be split into helper classes rather than expanding indefinitely.

---

# 6. Resource Hierarchy

Resources define static game data.

They are the foundation of Project Velir's data-driven architecture.

Resources should never store runtime information.

---

## Resource Categories

```text
Resources
│
├── KingdomData
├── CommanderData
├── TileData
├── BoardData
├── EventData
├── BattleConfig
├── EconomyConfig
├── AIProfile
├── AudioData
└── UITheme
```

Every gameplay configuration belongs inside one of these Resources.

---

## Kingdom Resources

Each kingdom has a dedicated resource.

Stores:

* Name
* Banner
* Color
* Passive Ability
* Description
* Artwork
* Starting Bonuses

Runtime values are excluded.

---

## Tile Resources

Each tile stores:

* Tile ID
* Tile Type
* Reward
* Description
* Icon
* Special Rules

Tiles never store ownership.

Ownership exists only during runtime.

---

## Event Resources

Each event contains:

* Title
* Description
* Category
* Probability
* Rewards
* Penalties
* Artwork

Events remain reusable across matches.

---

## Battle Resources

BattleConfig stores:

* Reward Values
* Victory Conditions
* Battle Multipliers
* Difficulty Modifiers

No runtime battle information is stored.

---

## AI Resources

AIProfile stores:

* Aggression
* Risk Tolerance
* Spending Preferences
* Utility Weights
* Expansion Priority

Changing AI behaviour should require editing Resources rather than code.

---

## Resource Dependency Model

```text
Managers

↓

Resources

↓

Configuration

↓

Runtime Objects
```

Managers read Resources.

Runtime objects use the values supplied by managers.

Resources never reference runtime objects.

---

## Resource Rules

Every Resource must satisfy:

✓ Immutable during gameplay

✓ Serializable

✓ Human readable

✓ Version compatible

✓ Independently reusable

---

## Design Principle

Resources define **what the game is**.

Runtime Objects define **what is happening right now**.

Managers define **how the game behaves**.

Maintaining this separation is one of the most important architectural principles of Project Velir.

---

**End of Part 2**

**Next Sections (Part 3):**

* 7. Scene Ownership
* 8. Class Relationships
* 9. Dependency Rules
# 7. Scene Ownership

Project Velir uses Godot's scene system to organize the game into reusable, modular components.

Every scene has one owner.

Every scene has one responsibility.

Scenes should never become responsible for gameplay decisions.

Managers control gameplay.

Scenes display gameplay.

---

## Scene Ownership Model

```text id="scene_owner_model"
Gameplay Scene
│
├── Managers
│
├── Board
│
├── Players
│
├── UI
│
├── Audio
│
└── Camera
```

The Gameplay scene is the root scene of every match.

---

## Root Scene

Gameplay.tscn

Responsibilities

* Instantiate managers
* Load the board
* Spawn players
* Initialize UI
* Connect gameplay systems
* Start the first turn

Gameplay.tscn should contain almost no gameplay logic.

---

## Board Scene

Board.tscn

Owned By

BoardManager

Contains

* Tile Nodes
* Tile Highlights
* Board Decorations
* Movement Paths

Board.tscn never performs gameplay calculations.

---

## Player Scene

Player.tscn

Owned By

PlayerManager

Contains

* Kingdom Token
* Movement Animation
* Visual Effects

The Player scene represents the visual state only.

Player Runtime Data remains inside PlayerManager.

---

## Tile Scene

Tile.tscn

Owned By

BoardManager

Contains

* Tile Sprite
* Highlight
* Selection Area
* Tile Animation

Tiles never decide rewards.

They simply notify BoardManager.

---

## UI Scene

HUD.tscn

Owned By

UIManager

Contains

* Top HUD
* Resource Bar
* Bottom Actions
* Notifications

HUD should only display data.

---

## Popup Scenes

Examples

* Battle Popup
* Event Card
* Reward Popup
* Pause Menu
* Victory Screen

Each popup exists as an independent reusable scene.

---

## Audio Scene

AudioRoot.tscn

Owned By

AudioManager

Contains

* Music Players
* SFX Players
* Audio Buses

No gameplay nodes belong here.

---

## Scene Independence

Every reusable scene should function independently.

Example

Tile.tscn

Can be instantiated anywhere.

Player.tscn

Can be reused for AI or Human players.

Reusable scenes reduce maintenance costs.

---

## Scene Communication

Scenes never communicate directly.

Instead

```text id="scene_comm"
Scene

↓

Manager

↓

Signal

↓

Manager

↓

Scene
```

This keeps visual presentation independent of gameplay.

---

## Scene Ownership Rules

Every scene must satisfy:

✓ Single Owner

✓ Single Responsibility

✓ Reusable

✓ Testable

✓ Independent

---

# 8. Class Relationships

Project Velir primarily uses composition rather than inheritance.

Gameplay systems collaborate through well-defined interfaces instead of large inheritance hierarchies.

---

## High-Level Class Diagram

```text id="class_relationships"
                 GameManager
                      │
      ┌───────────────┼───────────────┐
      │               │               │
 TurnManager    PlayerManager   BoardManager
      │               │               │
      │               │               │
 DiceManager    KingdomRuntime     TileRuntime
      │
      │
 BattleManager
      │
 EconomyManager
      │
 EventManager
      │
 VelirAramManager
      │
 AIManager
      │
 SaveManager
      │
 UIManager
      │
 AudioManager
```

Every manager owns a specific gameplay domain.

---

## Runtime Relationships

```text id="runtime_relationships"
Player

owns

Kingdom Runtime

occupies

Board Tile

interacts with

Event

receives

Resources

participates in

Battle
```

These relationships exist only during an active match.

---

## Resource Relationships

```text id="resource_relationships"
KingdomData

references

CommanderData

BoardData

contains

TileData

BattleConfig

references

EconomyConfig
```

Resources reference other Resources.

They never reference runtime objects.

---

## Ownership Relationships

Correct

```text id="ownership_correct"
BoardManager

owns

Board Runtime

Board Runtime

owns

Tile Runtime
```

Incorrect

```text id="ownership_wrong"
Tile Runtime

owns

BoardManager
```

Ownership always flows downward.

---

## Dependency Relationships

Managers may depend on:

* Resources
* Utility Classes
* Public Interfaces

Managers must never depend on:

* Internal UI Nodes
* Private Manager Variables
* Temporary Objects

---

## Composition Example

Preferred

```text id="composition"
BoardManager

contains

Tile Runtime

contains

TileData
```

Avoid

```text id="inheritance"
SuperTile

↓

TradeTile

↓

TempleTile

↓

SpecialTempleTradeTile
```

Deep inheritance reduces flexibility.

---

## Relationship Rules

Every relationship should be one of the following:

* Owns
* Uses
* Reads
* Emits Signal
* Listens to Signal

Relationships outside these categories should be carefully reviewed.

---

# 9. Dependency Rules

Dependency management is one of the most important architectural principles in Project Velir.

Poor dependency management leads to tightly coupled systems that become difficult to maintain.

---

## Allowed Dependency Direction

```text id="dependency_flow"
UI

↓

Managers

↓

Runtime Objects

↓

Resources
```

Dependencies always flow downward.

---

## Forbidden Dependency Direction

Resources

✗ cannot reference Managers.

Runtime Objects

✗ cannot own Managers.

UI

✗ cannot modify gameplay state directly.

Managers

✗ cannot manipulate another manager's private variables.

---

## Circular Dependencies

Circular dependencies are prohibited.

Incorrect

```text id="circular_dependency"
BoardManager

↓

BattleManager

↓

EconomyManager

↓

BoardManager
```

Correct

```text id="signal_dependency"
BoardManager

↓

Signal

↓

EconomyManager
```

Signals remove direct dependencies.

---

## Dependency Injection

Managers receive references during initialization.

Example

```text id="dependency_injection"
GameManager

↓

Initialize Managers

↓

Inject Required References

↓

Connect Signals

↓

Begin Gameplay
```

Managers should not search the scene tree repeatedly for dependencies.

---

## Public Interface Rule

Managers expose only the methods required by other systems.

Example

PlayerManager

Public

* get_player()
* get_active_player()
* update_resource()

Private

* _calculate_statistics()
* _refresh_cache()

Implementation details remain hidden.

---

## Dependency Validation Checklist

Every new dependency should answer:

| Question                              | Required |
| ------------------------------------- | -------- |
| Is this dependency necessary?         | ✓        |
| Can this be replaced by a Signal?     | ✓        |
| Does this create circular ownership?  | ✗        |
| Is the dependency testable?           | ✓        |
| Does it respect architectural layers? | ✓        |

---

## Anti-Patterns

Avoid the following:

### God Objects

One manager controlling every gameplay system.

---

### Deep Inheritance

More than two or three inheritance levels.

---

### Hidden Dependencies

Managers relying on undocumented scene paths.

---

### Global State Abuse

Using global variables instead of managed state.

---

### Hardcoded References

Searching for nodes using fixed scene paths throughout the project.

---

## Architecture Health

The architecture should remain understandable at every stage of development.

If adding a new feature requires modifying numerous unrelated managers, the architecture should be reconsidered before implementation.

Well-designed systems become easier to extend over time rather than more difficult.

---

## Design Principle

The architecture of Project Velir should enable developers to add new gameplay systems with confidence.

Every manager should know exactly what it owns, every scene should know exactly what it displays, and every dependency should be intentional, documented, and easy to trace.

Strong architectural discipline during Version 1 will make future expansions such as diplomacy, naval warfare, online multiplayer, and additional kingdoms possible without restructuring the core engine.

---

**End of Part 3**

**Next Sections (Part 4):**

* 10. Object Lifetime
* 11. Composition vs Inheritance
* 12. Godot Class Mapping
# 7. Scene Ownership

Project Velir uses Godot's scene system to organize the game into reusable, modular components.

Every scene has one owner.

Every scene has one responsibility.

Scenes should never become responsible for gameplay decisions.

Managers control gameplay.

Scenes display gameplay.

---

## Scene Ownership Model

```text id="scene_owner_model"
Gameplay Scene
│
├── Managers
│
├── Board
│
├── Players
│
├── UI
│
├── Audio
│
└── Camera
```

The Gameplay scene is the root scene of every match.

---

## Root Scene

Gameplay.tscn

Responsibilities

* Instantiate managers
* Load the board
* Spawn players
* Initialize UI
* Connect gameplay systems
* Start the first turn

Gameplay.tscn should contain almost no gameplay logic.

---

## Board Scene

Board.tscn

Owned By

BoardManager

Contains

* Tile Nodes
* Tile Highlights
* Board Decorations
* Movement Paths

Board.tscn never performs gameplay calculations.

---

## Player Scene

Player.tscn

Owned By

PlayerManager

Contains

* Kingdom Token
* Movement Animation
* Visual Effects

The Player scene represents the visual state only.

Player Runtime Data remains inside PlayerManager.

---

## Tile Scene

Tile.tscn

Owned By

BoardManager

Contains

* Tile Sprite
* Highlight
* Selection Area
* Tile Animation

Tiles never decide rewards.

They simply notify BoardManager.

---

## UI Scene

HUD.tscn

Owned By

UIManager

Contains

* Top HUD
* Resource Bar
* Bottom Actions
* Notifications

HUD should only display data.

---

## Popup Scenes

Examples

* Battle Popup
* Event Card
* Reward Popup
* Pause Menu
* Victory Screen

Each popup exists as an independent reusable scene.

---

## Audio Scene

AudioRoot.tscn

Owned By

AudioManager

Contains

* Music Players
* SFX Players
* Audio Buses

No gameplay nodes belong here.

---

## Scene Independence

Every reusable scene should function independently.

Example

Tile.tscn

Can be instantiated anywhere.

Player.tscn

Can be reused for AI or Human players.

Reusable scenes reduce maintenance costs.

---

## Scene Communication

Scenes never communicate directly.

Instead

```text id="scene_comm"
Scene

↓

Manager

↓

Signal

↓

Manager

↓

Scene
```

This keeps visual presentation independent of gameplay.

---

## Scene Ownership Rules

Every scene must satisfy:

✓ Single Owner

✓ Single Responsibility

✓ Reusable

✓ Testable

✓ Independent

---

# 8. Class Relationships

Project Velir primarily uses composition rather than inheritance.

Gameplay systems collaborate through well-defined interfaces instead of large inheritance hierarchies.

---

## High-Level Class Diagram

```text id="class_relationships"
                 GameManager
                      │
      ┌───────────────┼───────────────┐
      │               │               │
 TurnManager    PlayerManager   BoardManager
      │               │               │
      │               │               │
 DiceManager    KingdomRuntime     TileRuntime
      │
      │
 BattleManager
      │
 EconomyManager
      │
 EventManager
      │
 VelirAramManager
      │
 AIManager
      │
 SaveManager
      │
 UIManager
      │
 AudioManager
```

Every manager owns a specific gameplay domain.

---

## Runtime Relationships

```text id="runtime_relationships"
Player

owns

Kingdom Runtime

occupies

Board Tile

interacts with

Event

receives

Resources

participates in

Battle
```

These relationships exist only during an active match.

---

## Resource Relationships

```text id="resource_relationships"
KingdomData

references

CommanderData

BoardData

contains

TileData

BattleConfig

references

EconomyConfig
```

Resources reference other Resources.

They never reference runtime objects.

---

## Ownership Relationships

Correct

```text id="ownership_correct"
BoardManager

owns

Board Runtime

Board Runtime

owns

Tile Runtime
```

Incorrect

```text id="ownership_wrong"
Tile Runtime

owns

BoardManager
```

Ownership always flows downward.

---

## Dependency Relationships

Managers may depend on:

* Resources
* Utility Classes
* Public Interfaces

Managers must never depend on:

* Internal UI Nodes
* Private Manager Variables
* Temporary Objects

---

## Composition Example

Preferred

```text id="composition"
BoardManager

contains

Tile Runtime

contains

TileData
```

Avoid

```text id="inheritance"
SuperTile

↓

TradeTile

↓

TempleTile

↓

SpecialTempleTradeTile
```

Deep inheritance reduces flexibility.

---

## Relationship Rules

Every relationship should be one of the following:

* Owns
* Uses
* Reads
* Emits Signal
* Listens to Signal

Relationships outside these categories should be carefully reviewed.

---

# 9. Dependency Rules

Dependency management is one of the most important architectural principles in Project Velir.

Poor dependency management leads to tightly coupled systems that become difficult to maintain.

---

## Allowed Dependency Direction

```text id="dependency_flow"
UI

↓

Managers

↓

Runtime Objects

↓

Resources
```

Dependencies always flow downward.

---

## Forbidden Dependency Direction

Resources

✗ cannot reference Managers.

Runtime Objects

✗ cannot own Managers.

UI

✗ cannot modify gameplay state directly.

Managers

✗ cannot manipulate another manager's private variables.

---

## Circular Dependencies

Circular dependencies are prohibited.

Incorrect

```text id="circular_dependency"
BoardManager

↓

BattleManager

↓

EconomyManager

↓

BoardManager
```

Correct

```text id="signal_dependency"
BoardManager

↓

Signal

↓

EconomyManager
```

Signals remove direct dependencies.

---

## Dependency Injection

Managers receive references during initialization.

Example

```text id="dependency_injection"
GameManager

↓

Initialize Managers

↓

Inject Required References

↓

Connect Signals

↓

Begin Gameplay
```

Managers should not search the scene tree repeatedly for dependencies.

---

## Public Interface Rule

Managers expose only the methods required by other systems.

Example

PlayerManager

Public

* get_player()
* get_active_player()
* update_resource()

Private

* _calculate_statistics()
* _refresh_cache()

Implementation details remain hidden.

---

## Dependency Validation Checklist

Every new dependency should answer:

| Question                              | Required |
| ------------------------------------- | -------- |
| Is this dependency necessary?         | ✓        |
| Can this be replaced by a Signal?     | ✓        |
| Does this create circular ownership?  | ✗        |
| Is the dependency testable?           | ✓        |
| Does it respect architectural layers? | ✓        |

---

## Anti-Patterns

Avoid the following:

### God Objects

One manager controlling every gameplay system.

---

### Deep Inheritance

More than two or three inheritance levels.

---

### Hidden Dependencies

Managers relying on undocumented scene paths.

---

### Global State Abuse

Using global variables instead of managed state.

---

### Hardcoded References

Searching for nodes using fixed scene paths throughout the project.

---

## Architecture Health

The architecture should remain understandable at every stage of development.

If adding a new feature requires modifying numerous unrelated managers, the architecture should be reconsidered before implementation.

Well-designed systems become easier to extend over time rather than more difficult.

---

## Design Principle

The architecture of Project Velir should enable developers to add new gameplay systems with confidence.

Every manager should know exactly what it owns, every scene should know exactly what it displays, and every dependency should be intentional, documented, and easy to trace.

Strong architectural discipline during Version 1 will make future expansions such as diplomacy, naval warfare, online multiplayer, and additional kingdoms possible without restructuring the core engine.

---

**End of Part 3**

**Next Sections (Part 4):**

* 10. Object Lifetime
* 11. Composition vs Inheritance
* 12. Godot Class Mapping
# 10. Object Lifetime

Object Lifetime defines when every runtime object is created, initialized, updated, suspended, resumed, and destroyed.

A predictable lifecycle prevents memory leaks, invalid references, and inconsistent gameplay state.

Every runtime object in Project Velir follows the same lifecycle model.

---

## Standard Lifecycle

```text id="object_lifecycle"
Instantiate
      │
      ▼
Initialize
      │
      ▼
Register
      │
      ▼
Active Runtime
      │
      ▼
Suspend (Optional)
      │
      ▼
Resume
      │
      ▼
Shutdown
      │
      ▼
Destroy
```

Every runtime object should move through these stages in order.

---

## Creation Order

At the start of a match, objects are created in the following sequence.

```text id="creation_order"
GameManager
      │
TurnManager
      │
BoardManager
      │
PlayerManager
      │
DiceManager
      │
EconomyManager
      │
EventManager
      │
BattleManager
      │
VelirAramManager
      │
AIManager
      │
UIManager
      │
AudioManager
```

Managers should never initialize before GameManager.

---

## Initialization Rules

During initialization, managers may:

* Load Resources
* Connect Signals
* Validate configuration
* Allocate runtime objects

Managers must **not**:

* Start gameplay
* Modify player resources
* Trigger battles
* Display UI popups

Initialization prepares the game but does not begin it.

---

## Runtime State

After initialization, managers enter Active Runtime.

Responsibilities include:

* Processing player actions
* Updating runtime objects
* Emitting signals
* Handling gameplay events

Only active managers participate in gameplay.

---

## Suspension

Gameplay may temporarily pause.

Examples:

* Pause Menu
* Save Process
* Incoming Phone Call
* Application Background

During suspension:

* Timers pause
* Input pauses
* Animations pause
* Managers stop processing gameplay

Runtime state remains unchanged.

---

## Shutdown Sequence

When a match ends:

```text id="shutdown_order"
Stop Input

↓

Finish Animations

↓

Disconnect Signals

↓

Save Statistics

↓

Destroy Runtime Objects

↓

Unload Scene
```

Shutdown should occur gracefully without leaving dangling references.

---

## Lifetime Rules

Every runtime object must:

✓ Be created once.

✓ Have one owner.

✓ Be destroyed once.

✓ Never outlive its owner.

---

# 11. Composition vs Inheritance

Project Velir strongly favors **composition** over deep inheritance.

This principle improves flexibility, testing, and long-term maintainability.

---

## Preferred Approach

Objects are assembled from smaller components.

Example

```text id="composition_model"
Player

├── KingdomData

├── RuntimeStats

├── MovementComponent

├── BattleComponent

└── VisualComponent
```

Each component has one responsibility.

---

## Avoid Deep Inheritance

Do **not** create hierarchies such as:

```text id="bad_inheritance"
Entity

↓

Player

↓

King

↓

CholaKing

↓

SpecialCholaKing

↓

LegendaryCholaKing
```

Such hierarchies become difficult to extend and maintain.

---

## Manager Composition

Managers collaborate rather than inherit.

Example

```text id="manager_composition"
BattleManager

uses

EconomyManager

uses

PlayerManager

uses

BoardManager
```

No manager subclasses another manager.

---

## Resource Composition

Resources may reference other Resources.

Example

```text id="resource_composition"
KingdomData

contains

CommanderData

contains

PassiveAbilityData
```

This allows independent reuse of game data.

---

## Benefits

Composition provides:

* Easier testing
* Better reuse
* Smaller scripts
* Cleaner dependencies
* Flexible expansion

These advantages become increasingly important as the project grows.

---

## Design Rule

Whenever choosing between inheritance and composition:

Choose composition unless inheritance clearly provides a simpler and more maintainable solution.

---

# 12. Godot Class Mapping

This section defines how the architecture maps onto Godot Engine classes.

Using consistent base classes makes the project predictable for both developers and AI coding assistants.

---

## Manager Classes

Every manager extends:

```text id="manager_mapping"
Node
```

Examples:

* GameManager
* BoardManager
* TurnManager
* BattleManager

Managers do not require rendering capabilities.

---

## Visual Gameplay Objects

Visual gameplay scenes generally extend:

```text id="visual_mapping"
Node2D
```

Examples:

* Board
* Tile
* Player Token
* Ancient Site

These objects exist in the game world.

---

## User Interface

UI scenes extend:

```text id="ui_mapping"
Control
```

Examples:

* HUD
* Buttons
* Resource Bar
* Popups
* Menus

UI remains independent from gameplay logic.

---

## Configuration Resources

Game configuration extends:

```text id="resource_mapping"
Resource
```

Examples:

* KingdomData
* TileData
* EventData
* BattleConfig
* EconomyConfig

Resources are loaded by managers during initialization.

---

## Utility Classes

Helper classes should use:

```text id="utility_mapping"
RefCounted
```

Examples:

* Path Calculators
* Probability Utilities
* Math Helpers
* Serialization Helpers

Utility classes should contain no scene references.

---

## Autoload Singletons

Only a small number of systems should be Autoloads.

Recommended:

```text id="autoloads"
GameManager

SettingsManager (Future)

LocalizationManager (Future)
```

Avoid making every manager an Autoload.

---

## Scene Mapping

```text id="scene_mapping"
Gameplay.tscn

↓

Board.tscn

↓

Tile.tscn

↓

Player.tscn

↓

HUD.tscn
```

Every scene corresponds to one primary runtime responsibility.

---

## Script Organization

```text id="script_structure"
scripts/

managers/

gameplay/

resources/

ui/

utilities/
```

Each script belongs to exactly one category.

---

## Mapping Summary

| Architecture Element | Godot Base Class |
| -------------------- | ---------------- |
| Managers             | Node             |
| Board Objects        | Node2D           |
| Player Tokens        | Node2D           |
| UI                   | Control          |
| Configuration        | Resource         |
| Utilities            | RefCounted       |

This mapping should remain consistent throughout the project.

---

## Design Principle

Godot's node system should support the architecture—not define it.

Managers coordinate gameplay.

Scenes present gameplay.

Resources define gameplay.

Keeping these responsibilities separate ensures that Project Velir remains modular, scalable, and easy to extend throughout future development.

---

**End of Part 4**

**Next Sections (Part 5):**

* 13. Manager Responsibilities Matrix
* 14. Runtime Initialization Sequence
* 15. Shutdown & Cleanup Sequence
# 13. Manager Responsibilities Matrix

The Manager Responsibilities Matrix provides a single source of truth for ownership across the entire application.

Every gameplay feature must have one and only one manager responsible for it.

If ownership is unclear, the architecture should be revised before implementation.

---

## Core Responsibility Matrix

| Gameplay Feature     | Primary Manager  | Secondary Manager      |
| -------------------- | ---------------- | ---------------------- |
| Game Lifecycle       | GameManager      | TurnManager            |
| Match Initialization | GameManager      | BoardManager           |
| Match Shutdown       | GameManager      | SaveManager            |
| Turn Order           | TurnManager      | PlayerManager          |
| Player Runtime       | PlayerManager    | EconomyManager         |
| Kingdom Runtime      | PlayerManager    | AIManager              |
| Board Generation     | BoardManager     | GameManager            |
| Tile Resolution      | BoardManager     | EventManager           |
| Dice Rolling         | DiceManager      | TurnManager            |
| Resource Updates     | EconomyManager   | PlayerManager          |
| Battle Resolution    | BattleManager    | EconomyManager         |
| Event Resolution     | EventManager     | BoardManager           |
| Ancient Exploration  | VelirAramManager | EventManager           |
| AI Decision Making   | AIManager        | PlayerManager          |
| Save / Load          | SaveManager      | GameManager            |
| HUD Updates          | UIManager        | All Managers (Signals) |
| Audio Playback       | AudioManager     | UIManager              |

Only the Primary Manager may modify the core state of its domain.

---

## Ownership Rules

Every gameplay system must answer four questions.

### Who Creates It?

Example

Player Runtime

Created by

PlayerManager

---

### Who Updates It?

Example

Board Runtime

Updated by

BoardManager

---

### Who Saves It?

Example

Economy State

Saved by

SaveManager

using

EconomyManager.save_state()

---

### Who Destroys It?

Example

Battle Context

Destroyed by

BattleManager

Ownership should never be ambiguous.

---

## Responsibility Boundaries

Example

EconomyManager

Allowed

* Add Gold
* Spend Gold
* Update Resources
* Emit Resource Signals

Not Allowed

* Move Players
* Resolve Battles
* Display Popups
* Play Audio

Every manager follows the same pattern.

---

## Cross-System Interaction

Managers collaborate through well-defined interfaces.

Example

```text id="manager_interaction"
BoardManager

↓

tile_resolved

↓

EventManager

↓

event_completed

↓

EconomyManager

↓

resources_updated

↓

UIManager
```

Managers never "take over" another manager's responsibilities.

---

# 14. Runtime Initialization Sequence

Initialization is one of the most critical phases of the application.

Improper initialization leads to missing references, race conditions, and inconsistent gameplay.

Project Velir follows a strict initialization order.

---

## Complete Startup Sequence

```text id="startup_sequence"
Launch Application

↓

Load Project Settings

↓

Load Main Menu

↓

Start Match

↓

Load Gameplay Scene

↓

Create Managers

↓

Load Resources

↓

Create Runtime Objects

↓

Connect Signals

↓

Initialize Board

↓

Spawn Players

↓

Initialize UI

↓

Start Turn System

↓

Gameplay Begins
```

No gameplay begins until initialization is fully complete.

---

## Manager Initialization Order

Managers initialize in this order.

```text id="manager_init"
1. GameManager

2. SaveManager

3. BoardManager

4. PlayerManager

5. TurnManager

6. DiceManager

7. EconomyManager

8. EventManager

9. BattleManager

10. VelirAramManager

11. AIManager

12. UIManager

13. AudioManager
```

Each manager must complete initialization before the next begins.

---

## Initialization Responsibilities

### GameManager

* Create managers
* Load configuration
* Validate project state

---

### BoardManager

* Load BoardData
* Create tile runtime
* Validate tile connections

---

### PlayerManager

* Create kingdoms
* Assign starting positions
* Assign starting resources

---

### TurnManager

* Determine player order
* Set Round = 1
* Set Turn = 1

---

### UIManager

* Build HUD
* Display player information
* Connect UI signals

---

### AudioManager

* Load music
* Prepare SFX
* Start ambient audio

---

## Validation Stage

Before gameplay starts, perform validation.

Checklist

✓ Board Loaded

✓ Resources Loaded

✓ Players Spawned

✓ Signals Connected

✓ UI Ready

✓ Audio Ready

✓ Save System Ready

If any validation fails, gameplay should not begin.

---

# 15. Shutdown & Cleanup Sequence

A controlled shutdown ensures that no runtime objects remain after the match ends.

Cleanup should be deterministic and complete.

---

## Shutdown Flow

```text id="shutdown_flow"
Player Wins

↓

Stop Input

↓

Finish Animations

↓

Save Statistics

↓

Disconnect Signals

↓

Destroy Temporary Objects

↓

Destroy Runtime Objects

↓

Unload Gameplay Scene

↓

Return to Main Menu
```

The shutdown process should always complete in this order.

---

## Cleanup Responsibilities

### UIManager

* Close popups
* Stop animations
* Remove notifications

---

### AudioManager

* Fade music
* Stop ambient audio
* Release temporary sound players

---

### BattleManager

* Destroy active battle context
* Clear temporary combat data

---

### EventManager

* Clear active event
* Empty temporary event queue

---

### PlayerManager

* Destroy player runtime objects
* Clear runtime statistics

---

### BoardManager

* Destroy tile runtime
* Release board references

---

### GameManager

* Verify cleanup
* Return to Main Menu

---

## Signal Cleanup

Before destruction:

Every manager must disconnect all signal connections.

Example

```text id="signal_cleanup"
Disconnect

↓

Release References

↓

Destroy Object
```

This prevents invalid callback errors.

---

## Memory Cleanup Rules

Every runtime object must satisfy:

✓ No dangling references

✓ No connected signals

✓ No orphan nodes

✓ No active timers

✓ No active tweens

✓ No temporary animations

The Scene Tree should be clean after every match.

---

## Shutdown Verification

After cleanup:

Verify

* No runtime managers remain.
* No temporary scenes remain.
* No active gameplay timers exist.
* Memory usage returns to idle baseline.
* Main Menu loads successfully.

---

## Design Principle

Initialization and shutdown should be completely predictable.

Regardless of how a match ends—victory, defeat, application close, or unexpected interruption—the game should always enter and leave gameplay through the same well-defined lifecycle.

A disciplined lifecycle reduces bugs, improves stability, simplifies debugging, and provides a reliable foundation for future features such as online multiplayer, replay systems, and hot-loading of game content.

---

**End of Part 5**

**Next Sections (Final Part):**

* 16. Memory Ownership
* 17. Dependency Injection Strategy
* 18. UML Reference Diagram
* 19. Acceptance Criteria
* 20. Codex Implementation Notes
* 21. Future Extensibility
* 22. Design Principle & Conclusion
# 16. Memory Ownership

Memory ownership defines which system is responsible for creating, maintaining, and destroying every runtime object.

Clear ownership prevents:

* Memory leaks
* Duplicate objects
* Invalid references
* Orphan nodes
* Difficult debugging

Every object in Project Velir must have exactly one owner.

---

## Ownership Hierarchy

```text id="memory_owner_tree"
GameManager
│
├── TurnManager
├── BoardManager
│     └── Board Runtime
│            └── Tile Runtime
│
├── PlayerManager
│     └── Player Runtime
│
├── BattleManager
│     └── Battle Context
│
├── EventManager
│     └── Active Event
│
├── UIManager
│     └── UI Scenes
│
└── AudioManager
      └── Audio Players
```

Ownership always flows downward.

---

## Ownership Rules

Every object must answer:

Who creates me?

Who updates me?

Who destroys me?

Who saves me?

If any answer is unclear, the architecture requires revision.

---

## Runtime Object Ownership

| Object               | Owner            |
| -------------------- | ---------------- |
| Board Runtime        | BoardManager     |
| Tile Runtime         | BoardManager     |
| Player Runtime       | PlayerManager    |
| Dice Runtime         | DiceManager      |
| Battle Context       | BattleManager    |
| Event Context        | EventManager     |
| Ancient Site Runtime | VelirAramManager |
| HUD                  | UIManager        |
| Popup Windows        | UIManager        |
| Audio Players        | AudioManager     |

Ownership should never overlap.

---

## Reference Rules

Managers may own:

* Runtime Objects
* Helper Classes

Managers may reference:

* Other Managers (Public API only)
* Resources

Managers must never own:

* Another Manager
* Resources
* Engine Singletons

---

## Lifetime Responsibility

The owner is responsible for:

* Allocation
* Initialization
* Updates
* Cleanup
* Serialization
* Destruction

No other system may destroy an object it does not own.

---

## Memory Safety Rules

Every owned object must be:

✓ Initialized

✓ Registered

✓ Referenced

✓ Released

✓ Destroyed

No orphaned objects should remain after gameplay ends.

---

# 17. Dependency Injection Strategy

Project Velir uses explicit dependency injection.

Managers receive required references during initialization.

Managers should never search the Scene Tree repeatedly during gameplay.

---

## Injection Flow

```text id="dependency_injection_flow"
GameManager

↓

Create Manager

↓

Inject Dependencies

↓

Connect Signals

↓

Initialize

↓

Ready
```

Dependencies are supplied once during startup.

---

## Example

Correct

```text id="correct_di"
GameManager

↓

BoardManager.initialize(
    player_manager,
    event_manager,
    economy_manager
)
```

Incorrect

```text id="incorrect_di"
BoardManager

↓

get_node("../../PlayerManager")

↓

get_node("../../EconomyManager")
```

Searching for dependencies repeatedly creates fragile code.

---

## Required Dependencies

Example

BoardManager

Requires

* PlayerManager
* EventManager
* TileData
* BoardData

Does not require:

* AudioManager
* UIManager

Managers should receive only the dependencies they actually use.

---

## Injection Rules

Dependencies should be:

* Explicit
* Documented
* Immutable during runtime

Changing injected references during gameplay is discouraged.

---

## Advantages

Dependency Injection provides:

* Easier testing
* Lower coupling
* Better readability
* Simpler refactoring
* AI-friendly architecture

---

# 18. UML Reference Diagram

The following diagram summarizes the core architecture.

```text id="uml_reference"

                    GameManager
                         │
      ┌──────────────────┼──────────────────┐
      │                  │                  │
 TurnManager      PlayerManager      BoardManager
      │                  │                  │
 DiceManager      EconomyManager      Tile Runtime
      │                  │                  │
 BattleManager     EventManager      Board Runtime
      │                  │
 VelirAramManager  AIManager
      │
 SaveManager
      │
 UIManager
      │
 AudioManager

────────────────────────────────────────────

Resources

KingdomData

TileData

BoardData

EventData

BattleConfig

EconomyConfig

AIProfile

AudioData

UITheme
```

This diagram represents the primary architectural relationships.

Detailed diagrams for individual systems are provided in later engineering documents.

---

## Relationship Types

| Relationship | Meaning                   |
| ------------ | ------------------------- |
| Owns         | Responsible for lifecycle |
| Uses         | Reads public interface    |
| References   | Temporary access          |
| Emits        | Sends signal              |
| Listens      | Receives signal           |

These five relationship types cover almost every interaction within Project Velir.

---

# 19. Acceptance Criteria

The Class Diagram & Object Model is considered complete when:

✓ Every manager has one responsibility.

✓ Every runtime object has one owner.

✓ Every Resource is independent.

✓ No circular dependencies exist.

✓ Dependency Injection is documented.

✓ Object lifecycles are defined.

✓ Scene ownership is documented.

✓ Godot class mapping is complete.

✓ Architecture diagrams are consistent.

✓ Future systems have defined extension points.

Any future architectural changes should update this document before implementation.

---

# 20. Codex Implementation Notes

Codex should treat this document as the architectural authority for Project Velir.

Before implementing any manager, verify:

* Ownership
* Dependencies
* Lifecycle
* Signals
* Public API
* Runtime responsibilities

Implementation Rules

* One manager per gameplay domain.
* No gameplay values hardcoded.
* Resources store configuration.
* Runtime objects store mutable state.
* Signals replace unnecessary direct method calls.
* Public APIs remain minimal.
* Private implementation details remain hidden.

Every manager should be independently testable.

Every feature should integrate without modifying unrelated systems.

---

# 21. Future Extensibility

The architecture has been designed to support future gameplay systems without restructuring existing code.

Examples include:

* Diplomacy System
* Naval Warfare
* Province Management
* Campaign Mode
* Story Mode
* Online Multiplayer
* Spectator Mode
* Replay System
* Seasonal Events
* Live Operations
* Mod Support

Each future system should integrate as a new manager or module while respecting the architectural principles established in this document.

---

# 22. Design Principle & Conclusion

The architecture of Project Velir is designed to prioritize **clarity, modularity, and longevity**.

Every class has a purpose.

Every manager has a single responsibility.

Every runtime object has a single owner.

Every dependency is intentional.

Every system communicates through well-defined interfaces.

By enforcing these principles from the beginning, Project Velir establishes a software foundation that can scale from a small mobile strategy game into a much larger and more sophisticated project without sacrificing maintainability.

This document serves as the architectural blueprint for every future implementation, whether written by human developers or AI coding assistants.

---

## End of Document

**Document ID:** PV-021

**Category:** Engineering Design Document (EDD)

**Document Name:** Class Diagram & Object Model

**Version:** 1.0

**Status:** Complete
