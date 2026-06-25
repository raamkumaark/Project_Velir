---

Document ID: PV-023

Category: Engineering Design Document (EDD)

Document Name: Signal Architecture

Project: Project Velir

Version: 1.0

Status: Draft

Owner: Technical Director

Related Documents

* PV-021 Class Diagram & Object Model
* PV-022 Scene Hierarchy
* PV-017 Technical Architecture
* PV-020 Codex Implementation Guide

Last Updated: June 2026

---

# 1. Purpose

> "Systems should communicate through events, not dependencies."

---

## Overview

This document defines the complete signal architecture used throughout Project Velir.

Signals form the primary communication mechanism between gameplay managers, runtime objects, and user interface components.

A well-designed signal architecture minimizes coupling while maximizing modularity, maintainability, and extensibility.

Every gameplay event should be represented by a clearly defined signal.

---

## Objectives

The Signal Architecture has five primary goals.

### Decoupling

Managers should communicate without knowing each other's internal implementation.

Signals replace unnecessary direct method calls.

---

### Modularity

Gameplay systems should be independently replaceable.

Replacing the Battle System should not require changes to the Economy System.

---

### Scalability

Future systems such as Diplomacy, Multiplayer, and Naval Warfare should integrate simply by listening to existing signals or introducing new ones.

---

### Testability

Signals make automated testing significantly easier.

A test can emit a signal without needing to instantiate unrelated gameplay systems.

---

### AI Readability

Codex should immediately understand:

* Which manager emits a signal.
* Which managers receive it.
* What information the signal carries.
* When the signal is emitted.

---

## Scope

This document defines:

* Global Signals
* Gameplay Signals
* UI Signals
* Signal Ownership
* Signal Naming
* Signal Lifecycle
* Signal Flow
* Best Practices

It does not define gameplay mechanics.

---

## Audience

This specification is intended for:

* Gameplay Engineers
* UI Engineers
* AI Coding Assistants
* QA Engineers
* Future Contributors

---

# 2. Event-Driven Philosophy

Project Velir follows an event-driven architecture.

Gameplay systems react to events rather than directly controlling one another.

---

## Traditional Architecture

Poor example

```text
BoardManager

↓

BattleManager.attack()

↓

EconomyManager.add_gold()

↓

UIManager.show_popup()

↓

AudioManager.play_sound()
```

Problems

* Tight coupling
* Difficult testing
* Hidden dependencies
* Difficult maintenance

---

## Event Architecture

Preferred

```text
Battle Finished

↓

battle_finished

↓

EconomyManager

↓

gold_updated

↓

UIManager

↓

popup_requested

↓

AudioManager
```

Each manager reacts independently.

---

## Signal Chain

Signals naturally create gameplay flow.

Example

```text
Dice Rolled

↓

Player Moved

↓

Tile Resolved

↓

Battle Started

↓

Battle Finished

↓

Rewards Granted

↓

Turn Ended
```

Each stage remains independent.

---

## Event Ownership

Every signal has exactly one emitter.

Many listeners are allowed.

Example

```text
BattleManager

↓

battle_finished
```

Listeners

* EconomyManager
* UIManager
* AudioManager
* StatisticsManager (Future)

Only BattleManager emits the signal.

---

## Event Independence

Signals should describe **what happened**, not **what should happen**.

Good

```text
battle_finished
```

Bad

```text
give_player_gold
```

Signals report facts.

Managers decide responses.

---

## Event Rules

Signals should:

✓ Describe completed events

✓ Use consistent naming

✓ Remain independent

✓ Carry only required data

✓ Never expose private implementation

---

# 3. High-Level Signal Architecture

Signals connect every gameplay system.

They act as the communication backbone of Project Velir.

---

## Architecture Diagram

```text
                    GameManager
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
  TurnManager      PlayerManager    BoardManager
        │                │                │
        └────────────────┼────────────────┘
                         │
                    Signal Bus
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
 EconomyManager    BattleManager    EventManager
        │                │                │
        └────────────────┼────────────────┘
                         │
                    UIManager
                         │
                    AudioManager
```

Signals move through the system.

Managers remain independent.

---

## Signal Categories

Project Velir organizes signals into categories.

```text
Global

Gameplay

Board

Player

Battle

Economy

Events

Velir Aram

AI

UI

Audio

Save System
```

Each manager owns its category.

---

## Signal Direction

Signals always travel outward.

```text
Manager

↓

Signal

↓

Listeners
```

Signals never travel upward through ownership.

---

## Signal Naming Convention

Signals use snake_case.

Examples

```text
game_started

turn_started

dice_rolled

player_moved

tile_resolved

battle_started

battle_finished

gold_updated

event_triggered

save_completed
```

Signal names describe completed events.

---

## Signal Payload

Signals should include only the data required by listeners.

Example

```gdscript
signal player_moved(player_id, from_tile, to_tile)
```

Avoid passing unnecessary objects or large data structures.

---

## Design Principle

Signals are the nervous system of Project Velir.

Managers should communicate by broadcasting meaningful events rather than calling each other's internal methods.

A clean signal architecture allows systems to evolve independently, improves testing, simplifies debugging, and provides an ideal foundation for future features such as online multiplayer, replays, and live game analytics.

---

**End of Part 1**

**Next Sections (Part 2):**

* 4. Global Signals
* 5. Gameplay Signals
* 6. Board Signals
# 4. Global Signals

Global Signals represent events that affect the entire game session.

These signals are owned primarily by GameManager and are received by multiple managers.

Global Signals should be emitted sparingly and only for significant state changes.

---

## Game Lifecycle Signals

### game_initialized

**Emitter**

GameManager

**Purpose**

Emitted after all managers have been initialized and the game is ready to begin.

**Listeners**

* TurnManager
* BoardManager
* UIManager
* AudioManager

---

### game_started

**Emitter**

GameManager

**Purpose**

Marks the official beginning of gameplay.

**Listeners**

* TurnManager
* UIManager
* AudioManager

---

### game_paused

**Emitter**

GameManager

**Purpose**

Temporarily suspends gameplay.

**Listeners**

All Managers

---

### game_resumed

**Emitter**

GameManager

**Purpose**

Resumes gameplay after a pause.

---

### game_finished

**Emitter**

GameManager

**Purpose**

Signals that the match has ended.

**Listeners**

* SaveManager
* UIManager
* AudioManager
* StatisticsManager (Future)

---

## Global Signal Flow

```text id="global_signal_flow"
GameManager

↓

game_started

↓

TurnManager

↓

turn_started

↓

Gameplay
```

Global signals should always originate from GameManager.

---

## Global Signal Rules

Global signals should:

✓ Affect the entire application

✓ Be emitted once per event

✓ Never represent UI-only events

✓ Never contain gameplay calculations

---

# 5. Gameplay Signals

Gameplay Signals coordinate the core flow of every match.

These signals define the sequence of play from one turn to the next.

---

## Turn Signals

### turn_started

**Emitter**

TurnManager

**Payload**

```text id="turn_started_payload"
player_id

round_number

turn_number
```

---

### turn_ended

**Emitter**

TurnManager

**Purpose**

Indicates the active player's turn has ended.

---

### round_started

**Emitter**

TurnManager

Occurs once every complete round.

---

### round_completed

**Emitter**

TurnManager

Occurs after every kingdom has completed its turn.

---

## Dice Signals

### dice_roll_requested

**Emitter**

UIManager

Purpose

Player pressed Roll Dice.

---

### dice_rolled

**Emitter**

DiceManager

Payload

```text id="dice_payload"
player_id

dice_value
```

Listeners

* TurnManager
* BoardManager
* UIManager
* AudioManager

---

## Gameplay Flow

```text id="gameplay_signal_chain"
turn_started

↓

dice_roll_requested

↓

dice_rolled

↓

player_move_requested

↓

player_moved

↓

tile_resolved

↓

turn_ended
```

This represents the normal gameplay cycle.

---

## Gameplay Signal Rules

Gameplay signals should:

✓ Follow chronological order

✓ Represent completed actions

✓ Never bypass TurnManager

---

# 6. Board Signals

BoardManager owns every signal related to movement and board interaction.

Board signals describe what occurs on the game board.

---

## Movement Signals

### player_move_requested

**Emitter**

TurnManager

Purpose

Requests BoardManager to move the active player.

---

### player_moved

**Emitter**

BoardManager

Payload

```text id="player_moved_payload"
player_id

start_tile

destination_tile
```

Listeners

* EventManager
* BattleManager
* UIManager

---

### movement_completed

**Emitter**

BoardManager

Purpose

Player movement animation has completed.

---

## Tile Signals

### tile_selected

**Emitter**

BoardManager

Occurs when a tile is selected.

---

### tile_entered

**Emitter**

BoardManager

Occurs when a player reaches a tile.

---

### tile_resolved

**Emitter**

BoardManager

Payload

```text id="tile_payload"
tile_id

tile_type

player_id
```

Listeners

* EventManager
* EconomyManager
* BattleManager
* VelirAramManager

---

### board_loaded

**Emitter**

BoardManager

Occurs after the board has been successfully generated.

---

### board_reset

**Emitter**

BoardManager

Occurs when a new match begins.

---

## Board Signal Flow

```text id="board_signal_flow"
dice_rolled

↓

player_move_requested

↓

player_moved

↓

movement_completed

↓

tile_entered

↓

tile_resolved
```

Each event occurs only after the previous one has completed.

---

## Board Signal Rules

Board signals should:

✓ Represent board events only

✓ Never modify player resources

✓ Never trigger UI directly

✓ Always originate from BoardManager

---

## Signal Naming Summary

| Signal                | Emitter      |
| --------------------- | ------------ |
| game_initialized      | GameManager  |
| game_started          | GameManager  |
| game_finished         | GameManager  |
| turn_started          | TurnManager  |
| turn_ended            | TurnManager  |
| round_started         | TurnManager  |
| round_completed       | TurnManager  |
| dice_roll_requested   | UIManager    |
| dice_rolled           | DiceManager  |
| player_move_requested | TurnManager  |
| player_moved          | BoardManager |
| movement_completed    | BoardManager |
| tile_selected         | BoardManager |
| tile_entered          | BoardManager |
| tile_resolved         | BoardManager |
| board_loaded          | BoardManager |
| board_reset           | BoardManager |

---

## Design Principle

Global, Gameplay, and Board Signals establish the primary flow of every match.

These signals represent the backbone of Project Velir's event-driven architecture. They ensure that managers remain loosely coupled while gameplay progresses through a predictable sequence of events.

By restricting each signal to a single emitter and clearly defining its listeners, the architecture remains scalable, testable, and straightforward for both human developers and AI coding assistants.

---

**End of Part 2**

**Next Sections (Part 3):**

* 7. Player Signals
* 8. Economy Signals
* 9. Battle Signals
# 7. Player Signals

Player Signals communicate changes related to player state during a match.

These signals are owned by **PlayerManager** and are emitted whenever a player's runtime state changes.

Player signals should describe what has happened to a player, not what another manager should do.

---

## Active Player Signals

### active_player_changed

**Emitter**

PlayerManager

**Purpose**

Emitted whenever the turn changes to another kingdom.

**Payload**

```text
player_id

kingdom

turn_number
```

**Listeners**

* UIManager
* AudioManager
* AIManager

---

### player_initialized

**Emitter**

PlayerManager

Occurs after all player runtime objects have been created.

---

### player_eliminated (Future)

**Emitter**

PlayerManager

Occurs if a kingdom is completely defeated.

---

## Position Signals

### player_position_changed

**Emitter**

PlayerManager

Payload

```text
player_id

previous_tile

current_tile
```

This signal is emitted after BoardManager confirms movement.

---

## Statistics Signals

### player_statistics_updated

**Emitter**

PlayerManager

Occurs whenever runtime statistics change.

Examples

* Prestige
* Influence
* Army

---

## Player Signal Flow

```text id="player_signal_flow"
player_moved

↓

player_position_changed

↓

player_statistics_updated

↓

active_player_changed
```

---

## Player Signal Rules

Player signals should:

✓ Represent player state changes

✓ Never calculate gameplay

✓ Never trigger battles

✓ Remain independent of UI

---

# 8. Economy Signals

Economy Signals communicate every change related to resources.

Only **EconomyManager** owns these signals.

---

## Gold Signals

### gold_updated

**Emitter**

EconomyManager

Payload

```text
player_id

previous_gold

current_gold

change_amount
```

Listeners

* UIManager
* AudioManager
* StatisticsManager (Future)

---

### gold_received

Occurs whenever a player gains gold.

---

### gold_spent

Occurs whenever a player spends gold.

---

## Prestige Signals

### prestige_updated

Payload

```text
player_id

previous_value

current_value
```

---

## Influence Signals

### influence_updated

Used whenever Influence changes.

---

## Army Signals

### army_updated

Occurs after:

* Recruitment
* Battle
* Event

---

## Economy Flow

```text id="economy_flow"
battle_finished

↓

gold_received

↓

gold_updated

↓

UI Updated
```

---

## Economy Rules

Economy signals should:

✓ Contain resource changes only

✓ Never trigger movement

✓ Never resolve events

✓ Always originate from EconomyManager

---

# 9. Battle Signals

Battle Signals coordinate every combat encounter in Project Velir.

BattleManager is the only manager permitted to emit battle-related signals.

---

## Battle Lifecycle

### battle_requested

**Emitter**

BoardManager

Purpose

Requests BattleManager to evaluate combat.

---

### battle_started

**Emitter**

BattleManager

Payload

```text
attacker

defender

battle_type
```

Listeners

* UIManager
* AudioManager

---

### battle_resolved

Occurs after all calculations have completed.

---

### battle_finished

Payload

```text
winner

loser

gold_reward

prestige_reward
```

Listeners

* EconomyManager
* EventManager
* UIManager
* AudioManager

---

### battle_cancelled

Occurs when combat cannot begin.

Examples

* Friendly Tile
* Protected Region
* Invalid Target

---

## Battle Flow

```text id="battle_signal_flow"
tile_resolved

↓

battle_requested

↓

battle_started

↓

battle_resolved

↓

battle_finished
```

---

## Reward Flow

```text id="battle_reward_flow"
battle_finished

↓

gold_updated

↓

prestige_updated

↓

notification_requested
```

BattleManager never updates resources directly.

EconomyManager owns every resource modification.

---

## Battle Rules

Battle signals should:

✓ Describe combat only

✓ Never update UI directly

✓ Never update economy directly

✓ Emit one completion signal

---

## Signal Dependency Diagram

```text id="battle_dependencies"
BoardManager

↓

battle_requested

↓

BattleManager

↓

battle_finished

↓

EconomyManager

↓

gold_updated

↓

UIManager

↓

notification_requested

↓

AudioManager
```

Each manager performs one responsibility before notifying the next system.

---

## Signal Naming Summary

| Signal                       | Emitter        |
| ---------------------------- | -------------- |
| active_player_changed        | PlayerManager  |
| player_initialized           | PlayerManager  |
| player_position_changed      | PlayerManager  |
| player_statistics_updated    | PlayerManager  |
| player_eliminated *(Future)* | PlayerManager  |
| gold_updated                 | EconomyManager |
| gold_received                | EconomyManager |
| gold_spent                   | EconomyManager |
| prestige_updated             | EconomyManager |
| influence_updated            | EconomyManager |
| army_updated                 | EconomyManager |
| battle_requested             | BoardManager   |
| battle_started               | BattleManager  |
| battle_resolved              | BattleManager  |
| battle_finished              | BattleManager  |
| battle_cancelled             | BattleManager  |

---

## Design Principle

Player, Economy, and Battle Signals define the strategic progression of every turn.

Each manager reports only the events within its own domain, allowing other systems to react independently through signals rather than direct method calls.

This separation keeps the gameplay architecture modular, predictable, and scalable while making debugging, automated testing, and future feature additions significantly easier.

---

**End of Part 3**

**Next Sections (Part 4):**

* 10. Event Signals
* 11. Velir Aram Signals
* 12. AI Signals
# 10. Event Signals

Event Signals coordinate all gameplay events triggered during a match.

These include:

* Random Events
* Kingdom Events
* Trade Events
* Disaster Events
* Opportunity Events
* Special Ancient Events

Only **EventManager** may emit Event Signals.

---

## Event Lifecycle

### event_requested

**Emitter**

BoardManager

**Purpose**

Requests EventManager to evaluate whether an event should occur.

**Payload**

```text id="event_requested_payload"
player_id

tile_id

tile_type
```

---

### event_selected

**Emitter**

EventManager

**Purpose**

A valid event has been selected from the event database.

**Payload**

```text id="event_selected_payload"
event_id

event_type

event_rarity
```

---

### event_started

**Emitter**

EventManager

**Purpose**

The event begins.

UI should display the Event Popup.

---

### event_completed

**Emitter**

EventManager

**Purpose**

The player has resolved the event.

---

### event_cancelled

Occurs if:

* No valid event exists.
* Event probability fails.
* Requirements are not satisfied.

---

## Event Reward Signals

### event_reward_granted

Payload

```text id="event_reward_payload"
player_id

reward_type

reward_amount
```

Listeners

* EconomyManager
* UIManager
* AudioManager

---

## Event Signal Flow

```text id="event_signal_flow"
tile_resolved

↓

event_requested

↓

event_selected

↓

event_started

↓

event_completed

↓

event_reward_granted
```

---

## Event Rules

Event signals should:

✓ Represent event progression only

✓ Never modify economy directly

✓ Never resolve battles

✓ Always originate from EventManager

---

# 11. Velir Aram Signals

Velir Aram is the central ancient civilization region of Project Velir.

Its gameplay systems remain independent from standard board mechanics.

Only **VelirAramManager** may emit these signals.

---

## Exploration Signals

### ancient_site_entered

**Emitter**

VelirAramManager

Occurs when a kingdom enters Velir Aram.

---

### exploration_started

Payload

```text id="exploration_payload"
player_id

site_id
```

---

### exploration_completed

Occurs after exploration finishes.

---

## Relic Signals

### relic_discovered

Payload

```text id="relic_payload"
player_id

relic_id

relic_rarity
```

Listeners

* UIManager
* AudioManager
* EconomyManager

---

### relic_collected

Occurs after the player accepts the relic.

---

### relic_lost

Future expansion.

Occurs if relics can later be stolen or destroyed.

---

## Ancient Event Signals

### ancient_event_triggered

Occurs when an Ancient Event begins.

---

### ancient_event_completed

Occurs after completion.

---

## Velir Aram Flow

```text id="velir_flow"
ancient_site_entered

↓

exploration_started

↓

relic_discovered

↓

exploration_completed

↓

relic_collected
```

---

## Velir Aram Rules

Velir Aram signals should:

✓ Remain isolated from standard events

✓ Represent ancient gameplay only

✓ Never update player statistics directly

---

# 12. AI Signals

AI Signals coordinate decision-making for computer-controlled kingdoms.

Only **AIManager** owns these signals.

---

## Turn Signals

### ai_turn_started

**Emitter**

AIManager

Occurs when an AI kingdom begins its turn.

---

### ai_decision_started

Payload

```text id="ai_decision_payload"
player_id

difficulty

available_actions
```

---

### ai_decision_completed

Occurs after the AI chooses its action.

---

## Action Signals

### ai_move_selected

Payload

```text id="ai_move_payload"
destination_tile

priority_score
```

---

### ai_battle_selected

Occurs when the AI chooses combat.

---

### ai_trade_selected

Occurs when the AI chooses trade.

---

### ai_exploration_selected

Occurs when the AI decides to enter Velir Aram.

---

## Completion Signals

### ai_turn_finished

Occurs immediately before TurnManager advances to the next kingdom.

---

## AI Flow

```text id="ai_signal_flow"
ai_turn_started

↓

ai_decision_started

↓

decision_calculated

↓

ai_move_selected

↓

action_completed

↓

ai_turn_finished
```

---

## AI Rules

AI signals should:

✓ Represent decisions only

✓ Never bypass gameplay managers

✓ Use the same gameplay systems as human players

✓ Never modify runtime state directly

---

## AI Fairness Principle

The AI must play by exactly the same rules as the player.

AI systems should never:

* Receive hidden bonuses
* Ignore gameplay rules
* Access hidden information
* Manipulate random outcomes

Difficulty should arise from decision quality rather than unfair advantages.

---

## Signal Ownership Matrix

| Signal                  | Emitter          |
| ----------------------- | ---------------- |
| event_requested         | BoardManager     |
| event_selected          | EventManager     |
| event_started           | EventManager     |
| event_completed         | EventManager     |
| event_reward_granted    | EventManager     |
| event_cancelled         | EventManager     |
| ancient_site_entered    | VelirAramManager |
| exploration_started     | VelirAramManager |
| exploration_completed   | VelirAramManager |
| relic_discovered        | VelirAramManager |
| relic_collected         | VelirAramManager |
| relic_lost *(Future)*   | VelirAramManager |
| ancient_event_triggered | VelirAramManager |
| ancient_event_completed | VelirAramManager |
| ai_turn_started         | AIManager        |
| ai_decision_started     | AIManager        |
| ai_decision_completed   | AIManager        |
| ai_move_selected        | AIManager        |
| ai_battle_selected      | AIManager        |
| ai_trade_selected       | AIManager        |
| ai_exploration_selected | AIManager        |
| ai_turn_finished        | AIManager        |

---

## Design Principle

Event, Velir Aram, and AI Signals introduce depth and unpredictability while preserving a clean event-driven architecture.

Each subsystem remains autonomous, emitting only signals related to its own gameplay domain. This separation ensures that new event types, relic systems, AI strategies, or future gameplay expansions can be introduced without modifying the core communication model.

---

**End of Part 4**

**Next Sections (Part 5):**

* 13. UI Signals
* 14. Save System Signals
* 15. Audio Signals
* 16. Signal Lifecycle
# 13. UI Signals

UI Signals coordinate communication between gameplay systems and the presentation layer.

The UI should never poll managers continuously for information.

Instead, managers emit signals whenever relevant gameplay changes occur.

Only **UIManager** owns UI-specific signals.

---

## Notification Signals

### notification_requested

**Emitter**

UIManager

**Purpose**

Requests a temporary gameplay notification.

**Payload**

```text id="notification_payload"
title

message

icon

duration
```

Examples

* Gold Gained
* Battle Won
* Relic Discovered
* Turn Started

---

### notification_displayed

Occurs after the notification becomes visible.

---

### notification_closed

Occurs after the notification animation finishes.

---

## Popup Signals

### popup_requested

Payload

```text id="popup_payload"
popup_type

popup_data
```

Examples

* Battle Popup
* Event Popup
* Reward Popup
* Confirmation Popup

---

### popup_opened

Occurs after the popup animation completes.

---

### popup_closed

Occurs after the popup has completely disappeared.

---

## HUD Signals

### hud_refresh_requested

Occurs whenever gameplay values change.

Listeners

* HUD
* Resource Panel
* Kingdom Panel

---

### active_player_display_changed

Occurs whenever the active kingdom changes.

---

### resource_display_updated

Occurs after HUD values refresh.

---

## UI Flow

```text id="ui_flow"
gold_updated

↓

hud_refresh_requested

↓

resource_display_updated

↓

notification_requested

↓

notification_closed
```

---

## UI Rules

UI signals should:

✓ Never modify gameplay

✓ Never calculate rewards

✓ Only affect presentation

✓ Be emitted by UIManager

---

# 14. Save System Signals

The Save System communicates through signals whenever game data is stored or restored.

Only **SaveManager** owns Save Signals.

---

## Save Signals

### save_requested

**Emitter**

GameManager

Occurs when gameplay requests a save.

---

### save_started

**Emitter**

SaveManager

Indicates serialization has begun.

---

### save_completed

Payload

```text id="save_completed_payload"
slot_id

timestamp

success
```

Listeners

* UIManager
* StatisticsManager (Future)

---

### save_failed

Payload

```text id="save_failed_payload"
error_code

description
```

---

## Load Signals

### load_requested

Occurs before loading.

---

### load_started

Occurs when loading begins.

---

### load_completed

Occurs after runtime restoration finishes.

---

### load_failed

Occurs if loading cannot continue.

---

## Save Flow

```text id="save_flow"
save_requested

↓

save_started

↓

serialize

↓

save_completed
```

---

## Save Rules

Save signals should:

✓ Never pause gameplay unexpectedly

✓ Always return success or failure

✓ Never expose file implementation

---

# 15. Audio Signals

AudioManager reacts to gameplay through signals.

No gameplay manager should call audio methods directly.

---

## Music Signals

### music_play_requested

Payload

```text id="music_payload"
track_name

loop
```

---

### music_started

Occurs after playback begins.

---

### music_stopped

Occurs after music fades out.

---

## Sound Effect Signals

### sfx_requested

Payload

```text id="sfx_payload"
sound_id

volume

pitch
```

Examples

* Dice Roll
* Gold Gain
* Sword Clash
* Button Click
* Victory

---

### sfx_played

Occurs after playback starts.

---

## Ambient Signals

### ambience_changed

Examples

* Main Menu
* Gameplay
* Ancient Region
* Victory

---

## Audio Flow

```text id="audio_flow"
battle_finished

↓

sfx_requested

↓

music_play_requested

↓

AudioManager

↓

Playback
```

---

## Audio Rules

Audio signals should:

✓ Be asynchronous

✓ Never delay gameplay

✓ Never modify game state

✓ Always originate from AudioManager or UIManager requests

---

# 16. Signal Lifecycle

Every signal follows the same lifecycle.

Understanding this lifecycle is essential for predictable communication.

---

## Lifecycle Diagram

```text id="signal_lifecycle"
Event Occurs

↓

Signal Emitted

↓

Listeners Receive

↓

Listeners Process

↓

Gameplay Continues
```

Signals should complete quickly.

---

## Emission Rules

Signals should be emitted only after:

* Validation
* Gameplay calculation
* Runtime update

Never emit signals before state has been updated.

---

## Listener Rules

Listeners should:

* Perform one responsibility
* Avoid long processing
* Avoid blocking gameplay
* Emit new signals only when appropriate

---

## Signal Ordering

Example

```text id="signal_order"
battle_started

↓

battle_resolved

↓

battle_finished

↓

gold_updated

↓

hud_refresh_requested

↓

notification_requested
```

Maintaining a predictable order simplifies debugging.

---

## Error Handling

Signal listeners should:

* Validate received data
* Ignore invalid payloads safely
* Never crash gameplay

One failing listener should not prevent other listeners from receiving the signal.

---

## Lifecycle Rules

Every signal should satisfy:

✓ One emitter

✓ Many listeners allowed

✓ Immutable payload

✓ Short execution

✓ Predictable ordering

---

## Design Principle

Signals are transient events, not stored data.

They communicate that something has happened at a specific moment in time.

Managers remain responsible for maintaining game state, while signals simply notify interested systems that a change has occurred.

This distinction keeps the architecture clean, efficient, and easy to extend.

---

**End of Part 5**

**Next Sections (Final Part):**

* 17. Signal Rules & Best Practices
* 18. Signal Validation Checklist
* 19. Acceptance Criteria
* 20. Codex Implementation Notes
* 21. Future Expansion
* 22. Design Principle & Conclusion
# 17. Signal Rules & Best Practices

The following rules apply to every signal used throughout Project Velir.

These rules ensure the signal architecture remains consistent, scalable, and easy to maintain.

---

## Rule 1

### One Emitter

Every signal must have exactly one owner.

Example

```text id="one_emitter"
battle_finished

Owner

BattleManager
```

Other managers may listen to the signal, but they must never emit it.

---

## Rule 2

### Multiple Listeners

A signal may have any number of listeners.

Example

```text id="multi_listener"
gold_updated

↓

UIManager

AudioManager

StatisticsManager

AchievementManager (Future)
```

Adding listeners should never require modifying the emitter.

---

## Rule 3

### Signals Report Facts

Signals describe something that has already happened.

Correct

```text id="good_signal_names"
player_moved

battle_finished

gold_updated

event_completed

save_completed
```

Incorrect

```text id="bad_signal_names"
move_player

start_battle

give_gold

play_music

show_popup
```

Signals report completed events rather than issuing commands.

---

## Rule 4

### Minimal Payload

Only transmit information that listeners genuinely require.

Preferred

```gdscript id="minimal_payload"
signal player_moved(
    player_id,
    from_tile,
    to_tile
)
```

Avoid passing large runtime objects or unnecessary data.

---

## Rule 5

### No Business Logic

Signals should never perform gameplay calculations.

Correct

```text id="signal_logic"
BattleManager

↓

battle_finished
```

EconomyManager decides how rewards are handled.

---

## Rule 6

### Never Emit Duplicate Signals

Each gameplay event should emit one signal only.

Example

One battle

↓

One

battle_finished

Avoid emitting identical signals multiple times.

---

## Rule 7

### Avoid Signal Loops

Incorrect

```text id="signal_loop"
Manager A

↓

Signal

↓

Manager B

↓

Same Signal

↓

Manager A
```

Signal loops can create infinite recursion.

---

## Rule 8

### Stable Naming

Signal names should remain stable throughout the project's lifetime.

Changing signal names unnecessarily increases maintenance costs.

---

# 18. Signal Validation Checklist

Every newly introduced signal should satisfy the following checklist before implementation.

---

## Ownership

✓ One emitter

✓ Documented owner

✓ Correct manager

---

## Naming

✓ snake_case

✓ Describes completed event

✓ Clear meaning

---

## Payload

✓ Minimal

✓ Immutable

✓ Well documented

✓ Version compatible

---

## Dependencies

✓ No circular dependencies

✓ Supports multiple listeners

✓ Independent of implementation details

---

## Performance

✓ Fast emission

✓ Lightweight payload

✓ No blocking operations

---

## Documentation

✓ Included in this document

✓ Referenced by manager documentation

✓ Referenced in implementation notes

---

## Validation Matrix

| Requirement            | Status |
| ---------------------- | ------ |
| Single Emitter         | ✓      |
| Multiple Listeners     | ✓      |
| Event-Based Naming     | ✓      |
| Minimal Payload        | ✓      |
| No Circular Dependency | ✓      |
| Documented             | ✓      |
| Testable               | ✓      |

---

# 19. Acceptance Criteria

The Signal Architecture is considered complete when:

✓ Every manager has documented signals.

✓ Every signal has exactly one emitter.

✓ Every payload is documented.

✓ Signal naming conventions are consistent.

✓ Signal flow diagrams are complete.

✓ Lifecycle is documented.

✓ Validation checklist is complete.

✓ No undocumented signal exists within the project.

Future gameplay systems should integrate by introducing new signals without modifying existing communication patterns.

---

# 20. Codex Implementation Notes

Codex should treat this document as the authoritative reference for communication between gameplay systems.

Before implementing any manager:

Verify

* Which signals it owns.
* Which signals it emits.
* Which signals it listens to.
* Signal payload definitions.
* Signal naming conventions.

Implementation Rules

* One emitter per signal.
* Signals represent completed events.
* Never hardcode manager dependencies when a signal is appropriate.
* Prefer signal-driven workflows over direct method chains.
* Document every new signal before implementation.

Every new signal added to the project should update this document.

---

# 21. Future Expansion

The Signal Architecture has been designed to support future gameplay systems without altering the existing communication model.

Examples include:

## Gameplay

* Diplomacy Signals
* Naval Combat Signals
* Province Management Signals
* Campaign Progress Signals

---

## Multiplayer

* Network Synchronization Signals
* Matchmaking Signals
* Player Connection Signals
* Chat Signals

---

## Live Operations

* Daily Reward Signals
* Seasonal Event Signals
* Online Leaderboard Signals
* Cloud Save Signals

---

## Accessibility

* UI Theme Changed
* Font Size Changed
* Color Profile Changed
* Audio Profile Changed

Each new system should introduce its own signals while following the same ownership, naming, and lifecycle principles defined in this document.

---

# 22. Design Principle & Conclusion

Signals are the communication backbone of Project Velir.

They enable managers, runtime objects, and presentation systems to collaborate without creating unnecessary dependencies.

A well-designed signal architecture provides:

* Loose coupling
* High cohesion
* Predictable gameplay flow
* Easier debugging
* Better automated testing
* Cleaner AI-generated code
* Long-term maintainability

Every gameplay event should be viewed as an opportunity to communicate through a well-defined signal rather than through tightly coupled method calls.

By adhering to the principles in this document, Project Velir establishes a scalable event-driven architecture capable of supporting future gameplay features, multiplayer functionality, live content, and AI-assisted development without compromising the integrity of the codebase.

This document, together with **PV-021 (Class Diagram & Object Model)** and **PV-022 (Scene Hierarchy Specification)**, forms the core engineering foundation of Project Velir.

---

## End of Document

**Document ID:** PV-023

**Category:** Engineering Design Document (EDD)

**Document Name:** Signal Architecture

**Version:** 1.0

**Status:** Complete
