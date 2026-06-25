---

Document ID: PV-022

Category: Engineering Design Document (EDD)

Document Name: Scene Hierarchy Specification

Project: Project Velir

Version: 1.0

Status: Draft

Owner: Technical Director

Related Documents:

* PV-021 Class Diagram & Object Model
* PV-017 Technical Architecture
* PV-013 UI System
* PV-020 Codex Implementation Guide

Last Updated: June 2026

---

# 1. Purpose

> "Scenes are the physical structure of the game. Managers control the logic, scenes present the world."

---

## Overview

This document defines every Godot Scene (`.tscn`) used in Project Velir.

It specifies:

* Scene hierarchy
* Node ownership
* Parent-child relationships
* Scene responsibilities
* Scene communication
* Scene lifecycle
* Reusability rules
* Loading strategy

This document serves as the authoritative reference for the physical organization of the Godot project.

---

## Primary Objectives

The Scene Hierarchy has been designed to achieve five goals.

### Modularity

Every scene should solve one problem.

Example

Board Scene

Responsible only for displaying the board.

Never controls gameplay.

---

### Reusability

Every gameplay scene should be reusable.

Example

Player.tscn

Can represent:

* Human Player
* AI Player
* Multiplayer Player

without modification.

---

### Maintainability

Scenes should remain small.

Large scenes become difficult to debug.

Target

* Under 50 nodes where practical.
* Under 5 direct responsibilities.

---

### Performance

Scenes should load quickly.

Unused scenes should not consume memory.

Only active scenes remain instantiated.

---

### AI Readability

Codex should immediately understand:

* Which scene owns which nodes.
* Which manager controls the scene.
* Which resources the scene depends upon.

---

## Scope

This document defines:

* Root scenes
* Gameplay scenes
* UI scenes
* Popup scenes
* Reusable component scenes

This document does **not** define gameplay mechanics.

Gameplay behavior is documented elsewhere.

---

## Audience

This specification is intended for:

* Gameplay Engineers
* UI Engineers
* Technical Artists
* AI Coding Assistants
* QA Engineers

---

# 2. Scene Philosophy

Project Velir follows a strict scene philosophy.

Scenes exist only to present information.

Gameplay decisions always belong to Managers.

---

## Principle 1

### One Scene

One Responsibility

Examples

Board.tscn

Displays the board.

HUD.tscn

Displays gameplay information.

BattlePopup.tscn

Displays battle results.

Each scene should have a single clearly defined purpose.

---

## Principle 2

### Composition

Scenes are assembled from smaller reusable scenes.

Preferred

```text
Gameplay

├── Board

├── HUD

├── Players

├── Camera

└── Audio
```

Avoid

One enormous Gameplay scene containing every node.

---

## Principle 3

### Manager Controlled

Scenes never perform gameplay logic.

Example

Correct

BoardManager

↓

Moves Player

↓

Player Scene animates

Incorrect

Player Scene

↓

Moves itself

↓

Updates Economy

↓

Starts Battle

---

## Principle 4

### Scene Independence

Every reusable scene should function independently.

Example

Tile.tscn

Should be instantiable anywhere.

Player.tscn

Should not depend on specific board layouts.

Independent scenes simplify testing and reuse.

---

## Principle 5

### Minimal Coupling

Scenes communicate through Managers.

Preferred

```text
Player Scene

↓

PlayerManager

↓

BoardManager

↓

Tile Scene
```

Avoid

```text
Player Scene

↓

Tile Scene

↓

HUD

↓

Battle Popup
```

Visual scenes should not directly control one another.

---

## Scene Quality Checklist

Every scene should satisfy:

✓ One Responsibility

✓ Reusable

✓ Manager Controlled

✓ Independent

✓ Lightweight

✓ Easy to Test

---

# 3. High-Level Scene Architecture

Project Velir consists of a small number of root scenes.

Each root scene owns an independent area of the application.

---

## Root Scene Structure

```text
Application

│

├── Boot

├── Main Menu

├── Gameplay

├── Loading

├── Settings

└── Credits
```

Only one root scene should be active at any given time.

---

## Gameplay Scene

Gameplay.tscn is the heart of the application.

It owns:

* Board
* Players
* UI
* Managers
* Audio
* Camera

All gameplay occurs inside this scene.

---

## Root Scene Flow

```text
Boot

↓

Main Menu

↓

Loading

↓

Gameplay

↓

Victory

↓

Main Menu
```

Scene transitions should remain predictable.

---

## Scene Layer Architecture

```text
Gameplay

│

├── Managers

├── World

├── Gameplay Objects

├── User Interface

├── Audio

└── Camera
```

Each layer has one responsibility.

---

## Scene Ownership

```text
Gameplay

│

├── Board

│     └── Tiles

│

├── Players

│     └── Tokens

│

├── UI

│     └── Popups

│

├── Audio

│

└── Camera
```

Ownership always flows downward.

---

## Architectural Boundaries

Managers

Own Gameplay Logic.

Scenes

Display Gameplay.

Resources

Store Configuration.

Runtime Objects

Store Match State.

Maintaining these boundaries keeps the project modular and scalable.

---

## Design Principle

The Scene Hierarchy should make the physical structure of Project Velir immediately understandable.

A developer opening the project for the first time should be able to locate any feature within seconds simply by following the scene hierarchy.

---

**End of Part 1**

**Next Sections (Part 2):**

* 4. Gameplay Scene
* 5. Main Menu Scene
* 6. Loading & Scene Transition Flow
# 4. Gameplay Scene

The Gameplay Scene is the primary runtime scene of Project Velir.

It acts as the root container for every gameplay system during an active match.

All gameplay managers, runtime objects, and presentation layers exist beneath this scene.

---

## Gameplay Scene Structure

```text
Gameplay
│
├── Managers
├── World
├── Players
├── UI
├── Audio
├── Camera
└── Effects
```

Gameplay.tscn is loaded once at the beginning of every match and unloaded when the match ends.

---

## Responsibilities

Gameplay.tscn is responsible for:

* Hosting gameplay managers
* Loading the game board
* Spawning player tokens
* Initializing UI
* Initializing Audio
* Starting gameplay

Gameplay.tscn should **never** contain gameplay calculations.

---

## Managers Node

```text
Managers
│
├── GameManager
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

Managers are children of a dedicated Managers node to simplify organization.

---

## World Node

Contains the visual world.

```text
World
│
├── Board
├── Decorations
├── Lighting
├── Environment
└── Ancient Region
```

No gameplay logic belongs here.

---

## Players Node

```text
Players
│
├── Player_01
├── Player_02
├── Player_03
└── Player_04
```

Player scenes display:

* Token
* Selection Highlight
* Movement Animation
* Status Effects

Player runtime data remains inside PlayerManager.

---

## Effects Node

Contains temporary visual effects.

Examples

* Gold Gain
* Battle Slash
* Dust
* Sparkles
* Fire
* Ancient Discovery

Effects should be dynamically instantiated and destroyed.

---

## Camera Node

Version 1 uses a single camera.

Responsibilities

* Follow gameplay
* Zoom (Future)
* Shake during battles
* Smooth transitions

The Camera should never modify gameplay.

---

## Gameplay Scene Rules

Gameplay.tscn should satisfy:

✓ Lightweight

✓ Modular

✓ Easy to Debug

✓ Manager Driven

✓ Scene Independent

---

# 5. Main Menu Scene

MainMenu.tscn is the player's entry point into Project Velir.

It exists independently from gameplay.

---

## Scene Structure

```text
MainMenu
│
├── Background
├── Logo
├── Buttons
├── Version
├── Settings Shortcut
└── Background Music
```

---

## Buttons

Version 1 includes:

* New Game
* Continue
* Settings
* Credits
* Exit

Future versions may add:

* Multiplayer
* Leaderboards
* Profile
* Achievements

---

## Responsibilities

MainMenu is responsible for:

* Displaying branding
* Starting a match
* Opening settings
* Loading save games

It never loads gameplay directly.

Instead

```text
Main Menu

↓

Loading Scene

↓

Gameplay
```

---

## Menu Rules

MainMenu should:

* Load quickly
* Use minimal memory
* Remain responsive
* Never instantiate gameplay systems

---

# 6. Loading & Scene Transition Flow

Project Velir uses controlled scene transitions.

Only one major scene exists in memory at a time.

---

## Loading Flow

```text
Boot

↓

Main Menu

↓

Loading

↓

Gameplay
```

---

## Returning Flow

```text
Gameplay

↓

Victory Screen

↓

Loading

↓

Main Menu
```

---

## Loading Scene

Loading.tscn contains:

```text
Loading
│
├── Background
├── Progress Indicator
├── Tip Text
└── Logo
```

The Loading Scene prepares gameplay without exposing initialization delays.

---

## Transition Rules

Scene transitions should:

* Fade Out
* Unload Previous Scene
* Free Memory
* Load New Scene
* Fade In

Abrupt transitions should be avoided.

---

## Scene Loading Strategy

Large scenes should be loaded asynchronously whenever possible.

Priority

1. Managers
2. Board
3. Players
4. UI
5. Audio
6. Effects

Gameplay begins only after every required system is ready.

---

## Memory During Transition

During loading:

Previous scene should be released before the next gameplay scene becomes active.

This minimizes memory usage on Android devices.

---

## Transition Diagram

```text
Current Scene

↓

Fade Out

↓

Unload Scene

↓

Load Next Scene

↓

Initialize

↓

Fade In

↓

Ready
```

---

## Transition Validation

Before entering Gameplay verify:

✓ Board Loaded

✓ Players Spawned

✓ Managers Initialized

✓ UI Ready

✓ Audio Ready

✓ Camera Ready

If any validation fails, remain inside the Loading Scene.

---

## Design Principle

Scene transitions should feel smooth, predictable, and invisible to the player.

The player should experience a seamless flow between menus, gameplay, and victory screens while the engine safely loads and unloads resources behind the scenes.

---

**End of Part 2**

**Next Sections (Part 3):**

* 7. Board Scene
* 8. Tile Scene
* 9. Player Scene
# 7. Board Scene

The Board Scene is the visual representation of the Project Velir game board.

It is one of the most important scenes in the project because every gameplay action ultimately occurs on the board.

The Board Scene is **owned entirely by BoardManager**.

---

## Scene Name

```text
Board.tscn
```

---

## Ownership

Owner

BoardManager

Responsibilities

* Display the board
* Display tiles
* Display movement paths
* Display region boundaries
* Display Velir Aram

The Board Scene never calculates gameplay rules.

---

## Node Hierarchy

```text
Board
│
├── Background
├── Regions
├── TileContainer
├── Connections
├── Decorations
├── Highlights
├── PathEffects
└── Overlay
```

Each node has a dedicated responsibility.

---

## Tile Container

Contains every board tile.

```text
TileContainer
│
├── Tile_001
├── Tile_002
├── Tile_003
...
└── Tile_040
```

Version 1 is expected to contain approximately **36–48 board tiles**, depending on final balancing.

Tiles are instantiated automatically from **BoardData**.

---

## Region Layer

Displays the four kingdoms.

```text
Regions
│
├── Chola
├── Chera
├── Pandya
├── Pallava
└── VelirAram
```

Each region provides only visual grouping.

Gameplay ownership is maintained by BoardManager.

---

## Connection Layer

Displays movement paths.

```text
Connections
│
├── Road Segments
├── Bridges
├── Junctions
└── Special Routes
```

Connections are visual only.

Movement logic remains inside BoardManager.

---

## Highlight Layer

Contains temporary highlights.

Examples

* Current Tile
* Possible Destination
* Selected Tile
* Ancient Site
* Battle Location

Highlights are created and removed dynamically.

---

## Overlay Layer

Displays temporary board overlays.

Examples

* Fog Effect (Future)
* Battle Area
* Event Highlight
* Kingdom Territory Glow

---

## Board Rules

Board Scene must satisfy:

✓ Read Only

✓ Manager Controlled

✓ Data Driven

✓ Reusable

✓ Lightweight

---

# 8. Tile Scene

Every board tile is an independent reusable scene.

Tile scenes are instantiated automatically during board generation.

---

## Scene Name

```text
Tile.tscn
```

---

## Ownership

Owner

BoardManager

Tile Runtime

Tile Runtime Object

Configuration

TileData Resource

---

## Node Hierarchy

```text
Tile
│
├── Sprite
├── Collision
├── Highlight
├── Icon
├── SelectionEffect
└── AnimationPlayer
```

Every tile follows this structure.

---

## Tile Responsibilities

Tile Scene is responsible only for:

* Displaying artwork
* Detecting touch input
* Playing animations
* Showing highlights

Tile Scene never determines:

* Rewards
* Battles
* Events
* Economy

Those responsibilities belong to managers.

---

## Tile Communication

Correct

```text
Tile Pressed

↓

BoardManager

↓

Resolve Tile

↓

Signal

↓

Other Managers
```

Incorrect

```text
Tile

↓

Starts Battle

↓

Updates Gold

↓

Shows Popup
```

---

## Tile Animation

Version 1 includes:

* Selection Glow
* Landing Pulse
* Ancient Activation
* Resource Flash

Animations should remain short.

Target duration

200–400 milliseconds.

---

## Tile Reusability

Every tile should be generated from data.

Example

```text
TileData

↓

Instantiate Tile Scene

↓

Assign Visuals

↓

Ready
```

This allows new boards to be created without changing Tile.tscn.

---

# 9. Player Scene

Each kingdom is represented by an independent Player Scene.

The Player Scene represents only the visual token.

Gameplay data remains inside PlayerManager.

---

## Scene Name

```text
Player.tscn
```

---

## Ownership

Owner

PlayerManager

---

## Node Hierarchy

```text
Player
│
├── Token
├── Shadow
├── Selection Ring
├── Kingdom Banner
├── AnimationPlayer
└── Effects
```

The Player Scene should remain lightweight.

---

## Responsibilities

Player Scene is responsible for:

* Displaying the token
* Movement animation
* Selection feedback
* Temporary visual effects

Player Scene should never:

* Roll Dice
* Spend Gold
* Resolve Battles
* Determine Events

---

## Token Display

Each player token displays:

* Kingdom Color
* Kingdom Symbol
* Current Position Indicator

Future versions may include animated commander models.

---

## Movement Animation

Movement follows this sequence.

```text
BoardManager

↓

Move Request

↓

Player Scene

↓

Movement Animation

↓

Animation Finished

↓

Signal

↓

BoardManager
```

Managers wait for animation completion before continuing gameplay.

---

## Selection Feedback

When selected:

Display

* Glow
* Ring
* Banner Highlight

When deselected:

Return to normal appearance.

---

## Runtime Synchronization

Player Scene synchronizes with Player Runtime.

Player Runtime stores:

* Position
* Gold
* Army
* Prestige
* Influence

Player Scene displays:

* Token
* Effects
* Animations

The two should remain clearly separated.

---

## Player Scene Rules

Every Player Scene must satisfy:

✓ Independent

✓ Lightweight

✓ Reusable

✓ Manager Controlled

✓ Animation Driven

---

## Design Principle

The Board, Tile, and Player scenes together form the visual foundation of Project Velir.

Their purpose is to faithfully present the current game state while remaining completely independent of gameplay logic.

This separation ensures that future visual upgrades, new board themes, or enhanced player animations can be introduced without modifying the underlying gameplay systems.

---

**End of Part 3**

**Next Sections (Part 4):**

* 10. HUD Scene
* 11. Popup Scene
* 12. Overlay & Effects Scene
# 10. HUD Scene

The HUD (Heads-Up Display) is the player's primary interface during gameplay.

It continuously displays important game information without obstructing the game board.

The HUD should remain clean, readable, and responsive.

---

## Scene Name

```text
HUD.tscn
```

---

## Ownership

Owner

UIManager

Manager Dependency

* PlayerManager
* TurnManager
* EconomyManager

The HUD never calculates gameplay values.

It only displays information received through signals.

---

## Node Hierarchy

```text
HUD
│
├── TopBar
├── ResourcePanel
├── TurnPanel
├── KingdomPanel
├── BottomActions
├── NotificationArea
└── SafeArea
```

---

## Top Bar

Displays permanent match information.

Contains:

* Current Round
* Current Turn
* Active Kingdom
* Pause Button

This information remains visible throughout the match.

---

## Resource Panel

Displays:

```text
Gold

Army

Influence

Prestige
```

Each resource consists of:

* Icon
* Numeric Value
* Animation
* Tooltip (Future)

Values update immediately after gameplay changes.

---

## Kingdom Panel

Displays:

* Kingdom Banner
* Kingdom Symbol
* Commander Portrait (Future)
* Passive Ability Indicator

Only the active player's kingdom is highlighted.

---

## Bottom Action Panel

Version 1 Buttons

```text
Roll Dice

End Turn

Menu
```

Future Buttons

```text
Recruit

Trade

Diplomacy

Inventory
```

Buttons enable or disable depending on gameplay state.

---

## Notification Area

Displays temporary messages.

Examples

```text
+20 Gold

Battle Won

Ancient Relic Found

Event Triggered

Round Complete
```

Notifications automatically disappear after a short duration.

---

## HUD Rules

HUD must satisfy:

✓ Always Visible

✓ Lightweight

✓ Responsive

✓ Gameplay Independent

✓ Manager Controlled

---

# 11. Popup Scene

Popup scenes temporarily interrupt gameplay to present important information.

Every popup is an independent reusable scene.

---

## Popup Types

Version 1 includes:

```text
Battle Popup

Event Popup

Reward Popup

Confirmation Popup

Pause Menu

Victory Screen
```

Each popup is loaded only when needed.

---

## Popup Hierarchy

```text
Popup
│
├── Background
├── Window
├── Content
├── Buttons
└── AnimationPlayer
```

Only one modal popup may exist at any time.

---

## Event Popup

Displays:

* Event Artwork
* Event Title
* Description
* Reward
* Continue Button

The popup waits for player acknowledgement before closing.

---

## Battle Popup

Displays:

* Attacker
* Defender
* Battle Animation
* Winner
* Rewards

Battle resolution is completed before the popup appears.

---

## Reward Popup

Displays:

Examples

```text
+40 Gold

+15 Prestige

Relic Acquired

Army Increased
```

Reward popups automatically disappear after a short animation.

---

## Confirmation Popup

Examples

```text
Exit Match?

Restart Game?

Overwrite Save?
```

Contains:

* Confirm
* Cancel

---

## Popup Rules

Every popup must:

✓ Pause gameplay if required

✓ Animate smoothly

✓ Close cleanly

✓ Release memory after closing

---

# 12. Overlay & Effects Scene

The Overlay Scene contains temporary visual effects that appear above gameplay.

These effects improve feedback without becoming permanent gameplay objects.

---

## Scene Name

```text
Overlay.tscn
```

---

## Ownership

Owner

UIManager

Temporary Effects

Managed dynamically.

---

## Scene Hierarchy

```text
Overlay
│
├── ResourceEffects
├── BattleEffects
├── AncientEffects
├── Weather (Future)
├── ScreenFlash
└── ParticleLayer
```

---

## Resource Effects

Examples

```text
Gold Sparkle

Prestige Glow

Influence Aura

Army Banner
```

Effects appear briefly before disappearing.

---

## Battle Effects

Examples

```text
Sword Slash

Shield Impact

Victory Burst

Defeat Fade
```

These effects are visual only.

Battle logic remains inside BattleManager.

---

## Ancient Effects

Used when exploring Velir Aram.

Examples

```text
Ancient Light

Relic Glow

Dust

Temple Energy

Stone Activation
```

Ancient effects should visually distinguish Velir Aram from the rest of the board.

---

## Screen Effects

Examples

```text
Screen Shake

Fade

Flash

Darken

Victory Glow
```

These effects should be subtle.

Players should always retain visibility of the board.

---

## Particle Layer

Contains lightweight particle systems.

Examples

* Dust
* Fire
* Falling Leaves
* Water Ripples
* Sparkles

Particles should be pooled whenever possible to minimize allocations.

---

## Overlay Rules

Overlay scenes:

✓ Never store gameplay state

✓ Never calculate gameplay

✓ Never remain permanently

✓ Automatically clean themselves after completion

---

## UI Layer Order

The complete UI rendering order should be:

```text
Top

↑

Notifications

Popup Windows

Overlay Effects

HUD

Gameplay Board

Background

↓

Bottom
```

This order should remain consistent across the project.

---

## Design Principle

The HUD, Popup, and Overlay scenes form the presentation layer of Project Velir.

They exist to communicate information, celebrate player actions, and improve visual clarity while remaining completely independent of gameplay logic.

By keeping the UI presentation layer separate from gameplay systems, Project Velir ensures that visual redesigns, new themes, accessibility improvements, and future UI features can be implemented without affecting the underlying game mechanics.

---

**End of Part 4**

**Next Sections (Part 5):**

* 13. Scene Loading Strategy
* 14. Scene Lifecycle
* 15. Memory Management
* 16. Scene Pooling Strategy
# 13. Scene Loading Strategy

Project Velir uses a structured scene loading strategy to minimize loading time, reduce memory usage, and provide a smooth user experience on Android devices.

Only the scenes required for the current game state should remain in memory.

---

## Loading Philosophy

The loading system follows four principles:

* Load only what is needed.
* Release unused scenes immediately.
* Avoid duplicate scene instances.
* Hide loading operations from the player whenever possible.

---

## Scene Loading Flow

```text id="scene_loading_flow"
Application Start
        │
        ▼
Boot Scene
        │
        ▼
Main Menu
        │
        ▼
Loading Scene
        │
        ▼
Gameplay Scene
        │
        ▼
Victory Screen
        │
        ▼
Main Menu
```

Each major scene transition passes through the Loading Scene.

---

## Loading Priority

Scenes should load in the following order.

```text id="loading_priority"
1. Managers

↓

2. Resources

↓

3. Board

↓

4. Players

↓

5. UI

↓

6. Audio

↓

7. Effects
```

Gameplay begins only after all required systems are initialized.

---

## Dynamic Scene Loading

Some scenes should only be instantiated when required.

Examples

* Battle Popup
* Event Popup
* Reward Popup
* Confirmation Dialog
* Ancient Discovery Window

Dynamic loading minimizes idle memory consumption.

---

## Preloaded Scenes

Frequently used scenes should remain preloaded.

Examples

```text id="preloaded_scenes"
Tile.tscn

Player.tscn

HUD.tscn

Notification.tscn
```

These scenes are instantiated repeatedly during gameplay.

---

## Lazy Loading

Future content may use lazy loading.

Examples

* Seasonal Assets
* Premium Themes
* Campaign Maps
* Additional Kingdoms

Lazy loading reduces startup time.

---

# 14. Scene Lifecycle

Every scene follows a consistent lifecycle.

Understanding this lifecycle is essential for predictable gameplay behavior.

---

## Lifecycle Diagram

```text id="scene_lifecycle"
Load

↓

Instantiate

↓

Initialize

↓

Ready

↓

Active

↓

Inactive (Optional)

↓

Cleanup

↓

Free Memory
```

Every reusable scene should follow this sequence.

---

## Initialization

During initialization a scene should:

* Load Resources
* Cache node references
* Connect signals
* Prepare animations

A scene should **not** perform gameplay logic during initialization.

---

## Active State

During Active State a scene may:

* Receive player input
* Display animations
* Update visuals
* Emit UI events

Gameplay calculations remain the responsibility of managers.

---

## Inactive State

Some scenes remain loaded but inactive.

Examples

* Hidden Popup
* Notification Queue
* Cached Player Scene

Inactive scenes should consume minimal CPU time.

---

## Cleanup

Before destruction a scene should:

* Stop animations
* Disconnect signals
* Clear temporary data
* Release references

Proper cleanup prevents memory leaks.

---

## Scene Lifecycle Rules

Every scene must:

✓ Initialize once

✓ Become active once

✓ Clean itself

✓ Free resources

✓ Leave no orphan nodes

---

# 15. Memory Management

Efficient memory usage is critical for Android devices.

Scenes should allocate memory only when necessary.

---

## Memory Ownership

Each scene owns:

* Child Nodes
* Animation Players
* Temporary Effects

Managers own gameplay state.

Scenes own presentation.

---

## Memory Allocation Rules

Allocate during:

* Scene Initialization
* Dynamic Instantiation

Avoid allocating memory every frame.

---

## Memory Release

Memory should be released:

* When popup closes
* When battle finishes
* When match ends
* When returning to Main Menu

Unused scenes should never remain in memory.

---

## Reference Management

Before freeing a scene:

* Disconnect signals
* Stop timers
* Stop tweens
* Release cached references

No invalid references should remain.

---

## Memory Validation

After unloading Gameplay:

Verify

✓ No gameplay scenes remain

✓ No popup scenes remain

✓ No orphan nodes

✓ Memory returns close to idle baseline

---

## Android Optimization

Recommendations

* Reuse scenes whenever possible.
* Use lightweight textures.
* Avoid large numbers of simultaneous particle effects.
* Free temporary scenes immediately after use.

Version 1 targets stable performance on mid-range Android devices.

---

# 16. Scene Pooling Strategy

Some scenes are created frequently.

Instead of constantly creating and destroying them, they should be reused through object pooling.

---

## Candidate Scenes

Recommended for pooling:

```text id="pool_candidates"
Notification

Resource Popup

Particle Effects

Battle Effects

Selection Highlight

Damage Indicator (Future)
```

Pooling reduces memory allocations and garbage collection overhead.

---

## Pool Lifecycle

```text id="pool_lifecycle"
Create Pool

↓

Acquire Scene

↓

Activate

↓

Use

↓

Deactivate

↓

Return to Pool
```

Scenes remain available for future reuse.

---

## Pool Rules

Pooled scenes should:

* Reset internal state
* Hide themselves
* Disconnect temporary signals
* Return to the pool automatically

They should never retain data from previous usage.

---

## Non-Pooled Scenes

The following scenes should not be pooled.

* Gameplay.tscn
* MainMenu.tscn
* Loading.tscn
* Settings.tscn

These scenes are instantiated infrequently.

---

## Pool Manager (Future)

Future versions may introduce a dedicated PoolManager responsible for:

* Pool creation
* Scene reuse
* Pool statistics
* Memory optimization

Version 1 may manage pools directly within UIManager where appropriate.

---

## Performance Targets

Scene Loading

< 1 second

Popup Creation

< 50 ms

Notification Display

< 16 ms

Memory Increase During Match

Stable and predictable

Target Frame Rate

60 FPS

---

## Design Principle

Scenes should be lightweight, reusable, and disposable.

The player should never notice when scenes are loaded, reused, or released.

Efficient scene management contributes directly to smooth gameplay, low battery usage, and consistent performance across a wide range of Android devices.

---

**End of Part 5**

**Next Sections (Final Part):**

* 17. Scene Reusability Guidelines
* 18. Scene Validation Checklist
* 19. Acceptance Criteria
* 20. Codex Implementation Notes
* 21. Future Expansion
* 22. Design Principle & Conclusion
# 17. Scene Reusability Guidelines

One of the primary goals of Project Velir is to maximize scene reuse.

Reusable scenes reduce development time, improve consistency, simplify maintenance, and allow future content to be added with minimal effort.

Every scene should be designed with reuse in mind.

---

## Reusability Principles

Every reusable scene should be:

* Self-contained
* Independent
* Configurable
* Lightweight
* Data-driven

A scene should never assume a specific board layout, kingdom, or game mode.

---

## Configurable Scenes

Scenes should receive data from Resources or Managers.

Example

```text id="scene_config"
Tile.tscn

↓

TileData

↓

Configure Appearance

↓

Ready
```

The same Tile scene should represent:

* Trade Tile
* Battle Tile
* Ancient Tile
* Kingdom Tile
* Neutral Tile

without changing its implementation.

---

## Reusable Components

Examples of reusable scenes include:

```text id="reusable_components"
Tile.tscn

Player.tscn

Notification.tscn

Popup.tscn

Button.tscn

KingdomBanner.tscn

ResourceIcon.tscn
```

Reusable components should avoid project-specific assumptions.

---

## Customizability

Reusable scenes should expose configurable properties.

Example

Notification Scene

Configurable:

* Icon
* Text
* Duration
* Animation
* Sound Effect

The implementation remains identical.

---

## Reuse Rules

Every reusable scene should satisfy:

✓ No hardcoded values

✓ No direct manager ownership

✓ No fixed board position

✓ No duplicated functionality

---

# 18. Scene Validation Checklist

Before any scene is committed to the repository, it should pass the following validation checks.

---

## Architecture

✓ One Responsibility

✓ Proper Owner

✓ Correct Parent

✓ Correct Scene Category

---

## Performance

✓ Minimal Nodes

✓ Minimal Draw Calls

✓ Efficient Animations

✓ No unnecessary allocations

---

## Communication

✓ Uses Signals

✓ Does not manipulate gameplay directly

✓ Uses public manager interfaces only

---

## Memory

✓ Cleans itself

✓ Disconnects signals

✓ Frees temporary resources

✓ Leaves no orphan nodes

---

## UI

✓ Scales correctly

✓ Mobile friendly

✓ Supports different resolutions

✓ Respects Safe Areas

---

## Maintainability

✓ Clear node names

✓ Clear script names

✓ Proper folder location

✓ Documentation updated

---

## Validation Matrix

| Requirement           | Status |
| --------------------- | ------ |
| Single Responsibility | ✓      |
| Manager Controlled    | ✓      |
| Reusable              | ✓      |
| Data Driven           | ✓      |
| Memory Safe           | ✓      |
| Performance Ready     | ✓      |
| Mobile Compatible     | ✓      |

Every new scene should satisfy all requirements before merging.

---

# 19. Acceptance Criteria

The Scene Hierarchy Specification is considered complete when:

✓ Every root scene is documented.

✓ Every gameplay scene has a defined owner.

✓ Every reusable scene has a documented purpose.

✓ Scene hierarchy diagrams are complete.

✓ Scene loading order is defined.

✓ Scene lifecycle is documented.

✓ Memory management rules are established.

✓ Scene pooling strategy is documented.

✓ Scene validation checklist is complete.

Future gameplay systems should integrate into the existing hierarchy without restructuring the project.

---

# 20. Codex Implementation Notes

Codex should treat this document as the authoritative guide for creating Godot scenes.

Before creating a new scene, verify:

* Correct parent folder
* Correct owner
* Correct base node type
* Correct hierarchy
* Correct naming convention

Implementation Rules

* One scene, one responsibility.
* No gameplay logic inside scenes.
* Managers control behaviour.
* Scenes present information.
* Reusable components should be preferred over duplicated scenes.
* Scene hierarchies should remain shallow whenever practical.

Every new `.tscn` file should conform to the architecture described in this document.

---

# 21. Future Expansion

The Scene Hierarchy has been designed to accommodate future additions without major restructuring.

Potential future scenes include:

## Gameplay

* Diplomacy Screen
* Naval Battle Scene
* Province Management
* Campaign Map
* Story Events

---

## User Interface

* Multiplayer Lobby
* Leaderboards
* Achievement Screen
* Daily Rewards
* Profile Screen

---

## Visual Content

* Seasonal Boards
* Dynamic Weather
* Day/Night Cycle
* Animated Backgrounds

---

## Accessibility

* High Contrast Theme
* Large Text Mode
* Color-Blind Theme
* Simplified HUD

Each future feature should integrate by adding new scenes rather than modifying the existing hierarchy.

---

# 22. Design Principle & Conclusion

The Scene Hierarchy is the physical structure of Project Velir.

Managers define behaviour.

Resources define configuration.

Scenes define presentation.

Maintaining a strict separation between these responsibilities allows the project to remain modular, scalable, and easy to understand.

A developer opening the project should immediately recognize:

* Where every feature belongs.
* Which manager controls it.
* Which scene presents it.
* Which resources configure it.

This document provides the foundation for building a maintainable Godot project that can grow from an MVP into a feature-rich strategy game without requiring architectural redesign.

It serves as the definitive reference for all scene creation throughout the lifetime of Project Velir.

---

## End of Document

**Document ID:** PV-022

**Category:** Engineering Design Document (EDD)

**Document Name:** Scene Hierarchy Specification

**Version:** 1.0

**Status:** Complete
