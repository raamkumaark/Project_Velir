---

Document ID: PV-025

Category: Engineering Design Document (EDD)

Document Name: Godot Project Structure

Project: Project Velir

Version: 1.0

Status: Draft

Owner: Technical Director

Related Documents

* PV-021 Class Diagram & Object Model
* PV-022 Scene Hierarchy
* PV-023 Signal Architecture
* PV-024 Data Model

Last Updated: June 2026

---

# 1. Purpose

> "A well-organized project is easier to build, easier to debug, and easier to expand."

---

## Overview

This document defines the complete directory structure, file organization, naming conventions, and engineering standards for the Godot implementation of Project Velir.

It specifies:

* Folder hierarchy
* Script organization
* Scene organization
* Asset organization
* Resource organization
* Autoload structure
* Git repository layout
* Development workflow

This document serves as the definitive reference for organizing every file in the project.

---

## Objectives

The Project Structure has six primary objectives.

### Consistency

Every file should have one logical location.

Developers should never wonder where a file belongs.

---

### Scalability

The project should comfortably support:

* Hundreds of scripts
* Hundreds of scenes
* Thousands of assets

without requiring structural reorganization.

---

### Maintainability

A new developer should understand the project structure within minutes.

Folders should describe purpose rather than implementation.

---

### Collaboration

A predictable directory layout reduces merge conflicts and simplifies teamwork.

Every contributor should follow the same organizational rules.

---

### AI Readability

Codex should immediately understand:

* Where to create files
* Where to modify files
* Where dependencies exist
* Where assets belong

---

### Long-Term Growth

The folder structure should remain suitable from Version 1 through future expansions including multiplayer, campaigns, downloadable content, and mod support.

---

## Scope

This document defines:

* Repository layout
* Godot project folders
* Asset folders
* Script folders
* Documentation folders
* Build folders
* Naming standards

It does not define gameplay systems.

---

## Audience

This specification is intended for:

* Gameplay Engineers
* Technical Artists
* UI Engineers
* AI Coding Assistants
* Future Contributors

---

# 2. Project Organization Philosophy

Project Velir follows a feature-oriented organization rather than a type-oriented organization wherever practical.

The project should be organized around gameplay domains instead of arbitrary file types.

---

## Principle 1

### Predictability

Every developer should immediately know where a file belongs.

Example

BattleManager

↓

scripts/managers/

BattlePopup

↓

scenes/ui/popups/

BattleConfig

↓

resources/config/

---

## Principle 2

### Separation of Responsibilities

Different file categories should never be mixed.

Examples

Scripts

↓

scripts/

Scenes

↓

scenes/

Textures

↓

assets/textures/

Resources

↓

resources/

Documentation

↓

docs/

---

## Principle 3

### One Responsibility Per Folder

Folders should have clear purposes.

Good

```text
scripts/

managers/

resources/

audio/

```

Avoid

```text
misc/

temp/

new/

test2/

```

Folder names should communicate intent.

---

## Principle 4

### Minimal Nesting

Prefer shallow directory trees.

Target

Maximum depth:

4–5 levels

Deep nesting slows navigation and increases maintenance costs.

---

## Principle 5

### Stable Paths

Frequently used files should rarely change location.

Stable paths reduce merge conflicts and simplify automated tooling.

---

## Principle 6

### Documentation First

Every major folder should include documentation describing its purpose.

Large gameplay systems should reference the relevant engineering document.

---

## Organization Rules

Every folder should satisfy:

✓ Clear Purpose

✓ Predictable Contents

✓ Logical Ownership

✓ Minimal Nesting

✓ Scalable Layout

---

# 3. High-Level Folder Architecture

Project Velir follows a layered repository structure.

---

## Repository Layout

```text
Project_Velir/

├── assets/
├── audio/
├── docs/
├── resources/
├── scenes/
├── scripts/
├── shaders/
├── tests/
├── tools/
├── .github/
├── .gitignore
├── icon.svg
├── project.godot
└── README.md
```

Every top-level folder has a single responsibility.

---

## Folder Responsibilities

### assets/

Stores:

* Textures
* Sprites
* Icons
* UI Graphics
* Illustrations

---

### audio/

Stores:

* Music
* Sound Effects
* Ambient Audio
* Voice (Future)

---

### docs/

Stores:

* Game Design Documents
* Engineering Documents
* Codex Specifications
* Architecture

No implementation files belong here.

---

### resources/

Stores:

* `.tres`
* `.res`
* Gameplay Configuration
* Localization
* Themes

---

### scenes/

Stores every reusable Godot scene.

Examples

* Gameplay
* Board
* Player
* HUD
* Popups

---

### scripts/

Stores all GDScript source code.

Managers, gameplay logic, utilities, and UI controllers belong here.

---

### shaders/

Stores custom GPU shaders.

Version 1 is expected to use only lightweight mobile-compatible shaders.

---

### tests/

Stores automated tests and debugging tools.

No production gameplay assets belong here.

---

### tools/

Stores editor scripts, import utilities, generation tools, and developer utilities.

These tools are never included in gameplay builds.

---

## Repository Principles

The repository should remain understandable without opening Godot.

A developer browsing the project in GitHub should immediately understand the purpose of every major folder.

---

## Design Principle

The repository structure is the physical foundation of Project Velir.

A clean, predictable organization improves development speed, reduces maintenance costs, simplifies onboarding, and enables AI coding assistants such as Codex to generate new files in the correct locations with minimal ambiguity.

---

**End of Part 1**

**Next Sections (Part 2):**

* 4. Root Directory Structure
* 5. Asset Organization
* 6. Script Organization
# 4. Root Directory Structure

The root directory is the highest level of the repository.

Every top-level folder should have one clearly defined responsibility.

No gameplay implementation should exist directly inside the project root except essential Godot project files.

---

## Complete Root Structure

```text
Project_Velir/
│
├── assets/
├── audio/
├── docs/
├── resources/
├── scenes/
├── scripts/
├── shaders/
├── tests/
├── tools/
├── addons/
├── exports/
├── build/
├── .github/
├── .vscode/
├── .gitignore
├── README.md
├── LICENSE
├── project.godot
├── icon.svg
└── export_presets.cfg
```

This structure should remain stable throughout the project's lifecycle.

---

## Root Folder Responsibilities

### assets/

Contains all visual assets.

Examples

* UI Graphics
* Sprites
* Icons
* Backgrounds
* Logos

---

### audio/

Contains all audio files.

Examples

* Music
* Ambient Tracks
* Sound Effects
* Voice Overs (Future)

---

### docs/

Contains all project documentation.

Examples

* Game Design Documents
* Engineering Documents
* Development Guides
* Codex Specifications

---

### resources/

Contains Godot Resource files.

Examples

* TileData
* KingdomData
* AI Profiles
* Themes

---

### scenes/

Contains every reusable `.tscn`.

---

### scripts/

Contains every `.gd` source file.

---

### tests/

Contains automated testing.

---

### tools/

Contains editor utilities.

---

### build/

Temporary build output.

Never commit build artifacts.

---

### exports/

Contains exported Android APKs and future desktop builds.

Git should ignore exported binaries unless releasing official builds.

---

### addons/

Contains third-party Godot plugins.

Examples

* Dialogue System
* Debug Console
* Localization Plugin

Never modify third-party addon code directly.

---

## Root File Rules

The root directory should contain only:

* Project configuration
* Repository configuration
* Documentation
* Build configuration

Gameplay implementation belongs inside dedicated folders.

---

# 5. Asset Organization

Assets represent all non-code visual content.

The asset library should remain highly organized to simplify production.

---

## Asset Directory

```text
assets/
│
├── backgrounds/
├── boards/
├── characters/
├── effects/
├── icons/
├── illustrations/
├── kingdoms/
├── logos/
├── particles/
├── portraits/
├── sprites/
├── textures/
├── tiles/
└── ui/
```

Every asset belongs to exactly one category.

---

## UI Assets

```text
assets/ui/

├── buttons/

├── panels/

├── icons/

├── hud/

├── popups/

└── themes/
```

Avoid mixing gameplay graphics with UI graphics.

---

## Tile Assets

```text
assets/tiles/

├── battle/

├── trade/

├── village/

├── temple/

├── fort/

├── ancient/
```

Adding new tile types should only require adding new artwork.

---

## Character Assets

```text
assets/characters/

├── chola/

├── chera/

├── pandya/

├── pallava/

└── neutral/
```

Each kingdom receives its own asset directory.

---

## Naming Convention

Preferred

```text
tile_trade.png

battle_popup.png

kingdom_banner_chola.png
```

Avoid

```text
image1.png

new.png

test.png

icon_final2.png
```

Asset names should clearly communicate purpose.

---

## Asset Rules

Assets should satisfy:

✓ Lowercase

✓ Snake Case

✓ Descriptive

✓ Categorized

✓ Version Controlled

---

# 6. Script Organization

The script architecture mirrors the software architecture defined in PV-021.

Scripts should be grouped by responsibility rather than by implementation order.

---

## Script Directory

```text
scripts/
│
├── ai/
├── autoload/
├── managers/
├── gameplay/
├── runtime/
├── resources/
├── ui/
├── utilities/
├── debug/
└── tests/
```

Each folder represents one engineering domain.

---

## Managers

```text
scripts/managers/

GameManager.gd

TurnManager.gd

PlayerManager.gd

BoardManager.gd

DiceManager.gd

BattleManager.gd

EconomyManager.gd

EventManager.gd

VelirAramManager.gd

AIManager.gd

SaveManager.gd

UIManager.gd

AudioManager.gd
```

Managers coordinate gameplay.

---

## Gameplay

Contains gameplay logic.

```text
scripts/gameplay/

board/

battle/

economy/

events/

movement/

turns/
```

Gameplay code remains independent of presentation.

---

## Runtime

Contains runtime objects.

```text
scripts/runtime/

PlayerRuntime.gd

TileRuntime.gd

BattleRuntime.gd

EventRuntime.gd

GameRuntime.gd
```

Runtime classes store mutable gameplay state.

---

## Resources

Contains custom Resource classes.

```text
scripts/resources/

KingdomData.gd

TileData.gd

BoardData.gd

EventData.gd

BattleConfig.gd

AIProfile.gd
```

These scripts extend `Resource`.

---

## Utilities

Contains reusable helper classes.

Examples

```text
RandomHelper.gd

PathFinder.gd

SerializationHelper.gd

MathHelper.gd

ValidationHelper.gd
```

Utilities should contain no gameplay ownership.

---

## Debug

Contains development-only utilities.

Examples

* FPS Counter
* Debug Console
* Cheat Menu
* Signal Inspector

These scripts should not affect production gameplay.

---

## Script Rules

Every script should satisfy:

✓ One Responsibility

✓ Proper Folder

✓ Clear Name

✓ Minimal Dependencies

✓ Documented Purpose

---

## Design Principle

The repository should reflect the software architecture.

A developer should be able to locate any script, asset, or scene by following consistent naming conventions and folder organization rather than relying on search.

A well-organized repository reduces onboarding time, simplifies code reviews, minimizes merge conflicts, and enables AI coding assistants to generate new files in the correct locations with confidence.

---

**End of Part 2**

**Next Sections (Part 3):**

* 7. Scene Organization
* 8. Resource Organization
* 9. Autoload Organization
# 7. Scene Organization

The `scenes/` directory contains every reusable Godot scene (`.tscn`) used in Project Velir.

Every scene should represent a single responsibility and follow the architecture defined in **PV-022 – Scene Hierarchy Specification**.

Scenes should never contain gameplay logic beyond presentation and input forwarding.

---

## Scene Directory

```text
scenes/
│
├── boot/
├── gameplay/
├── loading/
├── main_menu/
├── ui/
├── board/
├── player/
├── tiles/
├── battle/
├── events/
├── velir_aram/
├── camera/
├── effects/
├── common/
└── debug/
```

---

## Gameplay Scenes

```text
scenes/gameplay/

Gameplay.tscn

Victory.tscn

Defeat.tscn
```

Gameplay.tscn is the root gameplay scene.

---

## Board Scenes

```text
scenes/board/

Board.tscn

BoardBackground.tscn

MovementPath.tscn

RegionOverlay.tscn
```

Owned by BoardManager.

---

## Tile Scenes

```text
scenes/tiles/

Tile.tscn

BattleTile.tscn

TradeTile.tscn

VillageTile.tscn

TempleTile.tscn

AncientTile.tscn

NeutralTile.tscn
```

These inherit from the same visual structure while being configured through TileData resources.

---

## Player Scenes

```text
scenes/player/

Player.tscn

KingdomBanner.tscn

CommanderPortrait.tscn

SelectionRing.tscn
```

Player scenes should remain lightweight.

---

## UI Scenes

```text
scenes/ui/

HUD.tscn

ResourceBar.tscn

TurnPanel.tscn

Notification.tscn

PauseMenu.tscn

SettingsMenu.tscn
```

---

## Popup Scenes

```text
scenes/ui/popups/

BattlePopup.tscn

EventPopup.tscn

RewardPopup.tscn

ConfirmationPopup.tscn

VictoryPopup.tscn
```

Every popup is reusable.

---

## Common Components

```text
scenes/common/

AnimatedButton.tscn

Panel.tscn

Tooltip.tscn

Divider.tscn

IconLabel.tscn
```

These components should be reused throughout the project.

---

## Scene Rules

Every scene should satisfy:

✓ One Responsibility

✓ Reusable

✓ Minimal Node Count

✓ Manager Controlled

✓ Mobile Optimized

---

# 8. Resource Organization

Resources define gameplay configuration.

Every `.tres` or `.res` file should be stored inside the `resources/` directory.

Resources should never contain runtime state.

---

## Resource Directory

```text
resources/
│
├── kingdoms/
├── boards/
├── tiles/
├── battles/
├── economy/
├── events/
├── ai/
├── audio/
├── ui/
├── localization/
└── themes/
```

---

## Kingdom Resources

```text
resources/kingdoms/

Chola.tres

Chera.tres

Pandya.tres

Pallava.tres
```

Each kingdom has its own configuration.

---

## Tile Resources

```text
resources/tiles/

BattleTile.tres

TradeTile.tres

TempleTile.tres

VillageTile.tres

FortTile.tres

AncientTile.tres
```

Tile resources define gameplay properties.

---

## Event Resources

```text
resources/events/

TradeEvents/

BattleEvents/

AncientEvents/

KingdomEvents/

RandomEvents/
```

Each event exists independently.

---

## AI Resources

```text
resources/ai/

Easy.tres

Normal.tres

Hard.tres

Legendary.tres
```

Changing AI difficulty should require only swapping profiles.

---

## UI Resources

```text
resources/ui/

HUDTheme.tres

ButtonTheme.tres

PopupTheme.tres
```

Version 1 uses a single default theme.

Future versions may support multiple UI themes.

---

## Resource Rules

Resources should satisfy:

✓ Immutable

✓ Data Driven

✓ Human Readable

✓ Version Controlled

✓ Independent

---

# 9. Autoload Organization

Autoloads provide globally accessible services.

Project Velir intentionally limits Autoload usage.

Too many Autoloads create hidden dependencies.

---

## Recommended Autoloads

```text
scripts/autoload/

GameManager.gd

SettingsManager.gd

LocalizationManager.gd

DebugManager.gd (Debug Only)
```

Version 1 should keep the number of Autoloads small.

---

## GameManager

Responsibilities

* Application State
* Match Lifecycle
* Scene Switching
* Global Initialization

GameManager is the primary Autoload.

---

## SettingsManager

Stores:

* Audio Settings
* Graphics Settings
* Accessibility
* Language

Settings persist between sessions.

---

## LocalizationManager

Future implementation.

Responsibilities

* Language Loading
* Translation Lookup
* Runtime Language Switching

---

## DebugManager

Available only in Debug builds.

Provides:

* Debug Console
* Performance Metrics
* Cheat Commands
* Logging

Should never be included in production exports.

---

## Autoload Rules

Autoloads must satisfy:

✓ Global Responsibility

✓ Minimal Dependencies

✓ No Gameplay Logic

✓ Small Public API

✓ Stable Interface

---

## Autoload Communication

Preferred

```text
GameManager

↓

Signal

↓

Managers

↓

Gameplay
```

Avoid

```text
GameManager

↓

Controls Everything
```

Autoloads should coordinate, not dominate.

---

## Folder Relationship Diagram

```text
Project_Velir
│
├── assets/
├── audio/
├── docs/
├── resources/
├── scenes/
├── scripts/
│
│   ├── managers/
│   ├── gameplay/
│   ├── runtime/
│   ├── resources/
│   ├── ui/
│   ├── autoload/
│   └── utilities/
│
└── shaders/
```

The folder hierarchy should closely mirror the software architecture.

---

## Design Principle

Scenes, Resources, and Autoloads form the operational backbone of the Godot project.

Scenes define presentation, Resources define configuration, and Autoloads provide essential application-wide services.

Keeping these responsibilities clearly separated ensures that Project Velir remains modular, maintainable, and scalable while making navigation intuitive for both human developers and AI coding assistants.

---

**End of Part 3**

**Next Sections (Part 4):**

* 10. Naming Conventions
* 11. File Standards
* 12. Code Organization
# 10. Naming Conventions

Consistent naming conventions improve readability, reduce ambiguity, simplify navigation, and enable AI-assisted development tools to generate predictable code.

Every file, folder, class, scene, resource, and asset in Project Velir should follow these standards.

---

## General Principles

Names should be:

* Descriptive
* Predictable
* Consistent
* Easy to search
* Easy to pronounce

Avoid abbreviations unless they are universally understood.

---

## Folder Naming

Folders use:

```text id="folder_naming"
lowercase

snake_case
```

Examples

```text id="folder_examples"
scripts/

resources/

battle_system/

user_interface/

audio/

particle_effects/
```

Avoid

```text id="folder_bad"
NewFolder/

Temp/

misc/

Folder1/
```

---

## Script Naming

Scripts use:

```text id="script_naming"
PascalCase.gd
```

Examples

```text id="script_examples"
GameManager.gd

BattleManager.gd

PlayerRuntime.gd

EconomyConfig.gd

TileData.gd
```

---

## Scene Naming

Scenes also use:

```text id="scene_naming"
PascalCase.tscn
```

Examples

```text id="scene_examples"
Gameplay.tscn

Board.tscn

Player.tscn

BattlePopup.tscn

RewardPopup.tscn
```

---

## Resource Naming

Resources follow PascalCase.

Examples

```text id="resource_examples"
Chola.tres

BattleTile.tres

HardAI.tres

EconomyConfig.tres
```

---

## Asset Naming

Assets use:

```text id="asset_naming"
lowercase_snake_case
```

Examples

```text id="asset_examples"
battle_tile.png

gold_icon.png

kingdom_banner_chola.png

main_menu_background.png
```

---

## Audio Naming

Examples

```text id="audio_examples"
battle_theme.ogg

dice_roll.wav

gold_gain.wav

button_click.wav
```

---

## Animation Naming

Examples

```text id="animation_examples"
idle

move

attack

victory

fade_in

fade_out
```

Animation names should remain short and descriptive.

---

## Variable Naming

Variables use:

```text id="variable_naming"
snake_case
```

Example

```gdscript id="variable_examples"
current_gold

player_position

battle_result

turn_number
```

---

## Constant Naming

Constants use:

```text id="constant_naming"
UPPER_SNAKE_CASE
```

Example

```gdscript id="constant_examples"
MAX_PLAYERS

DEFAULT_GOLD

BOARD_TILE_COUNT
```

---

## Function Naming

Functions use:

```text id="function_naming"
snake_case()
```

Examples

```gdscript id="function_examples"
move_player()

calculate_reward()

load_board()

save_game()
```

---

## Signal Naming

Signals use:

```text id="signal_naming"
snake_case
```

Examples

```text id="signal_examples"
player_moved

battle_finished

gold_updated

save_completed
```

Signals describe completed events.

---

## Naming Rules

Every name should satisfy:

✓ Descriptive

✓ Consistent

✓ Searchable

✓ Stable

✓ Self-explanatory

---

# 11. File Standards

Every file within Project Velir should follow common engineering standards.

Consistency improves maintainability and simplifies AI-assisted development.

---

## Script Header

Every script should begin with a documentation header.

Example

```gdscript id="script_header"
##==================================================
## Project Velir
## PlayerManager
## Owner: Gameplay Systems
## Responsibility:
## Manages all player runtime objects.
##==================================================
```

---

## File Length

Recommended limits

| File Type      | Recommended Maximum |
| -------------- | ------------------: |
| Manager        |           600 lines |
| Runtime Class  |           300 lines |
| Utility        |           250 lines |
| UI Script      |           250 lines |
| Resource Class |           200 lines |

Files exceeding these recommendations should be reviewed for refactoring.

---

## One Class Per File

Every script should define one primary class.

Correct

```text id="one_class"
PlayerManager.gd

↓

PlayerManager
```

Avoid multiple unrelated classes within the same file.

---

## One Responsibility

Each file should solve one problem.

Example

BattleManager

Responsible only for battle coordination.

Not

Battle + Economy + UI

---

## Documentation

Every public method should include a short description.

Example

```gdscript id="method_docs"
## Moves the active player to the destination tile.
func move_player():
```

---

## Comment Guidelines

Comments should explain:

* Why
* Design decisions
* Assumptions

Avoid comments that merely repeat the code.

---

## File Standards Checklist

✓ One Responsibility

✓ One Primary Class

✓ Documentation Header

✓ Public API Documented

✓ Consistent Formatting

---

# 12. Code Organization

Project Velir follows a structured coding style.

Code organization should remain consistent across every system.

---

## Standard Script Layout

Every script should follow this order.

```gdscript id="script_layout"
class_name

extends

constants

signals

enums

export variables

private variables

onready variables

public methods

private methods
```

This ordering should remain consistent.

---

## Public vs Private Methods

Public methods appear first.

Private helper methods follow.

Example

```gdscript id="public_private"
initialize()

move_player()

save_state()

_reset_turn()

_validate_move()

_update_statistics()
```

Private methods begin with an underscore.

---

## Signals

Signals should appear near the top of the file.

Example

```gdscript id="signal_layout"
signal player_moved

signal battle_finished

signal gold_updated
```

---

## Enums

Enums should be grouped together.

Example

```gdscript id="enum_example"
enum PlayerState {
    WAITING,
    ACTIVE,
    MOVING,
    BATTLING
}
```

---

## Regions

Large scripts may use region comments.

Example

```text id="regions"
Initialization

Gameplay

Utilities

Debug

Save / Load
```

Regions improve navigation in larger files.

---

## Dependencies

Imports and dependencies should remain minimal.

Managers communicate primarily through:

* Signals
* Public Interfaces
* Dependency Injection

Avoid hidden dependencies.

---

## Code Style

Preferred

* Short methods
* Clear variable names
* Early returns
* Small classes
* Composition over inheritance

Avoid

* Deep nesting
* Long switch statements
* Large God Objects
* Circular dependencies

---

## Organization Checklist

Every script should satisfy:

✓ Consistent Layout

✓ Small Functions

✓ Clear Sections

✓ Minimal Dependencies

✓ Readable Formatting

✓ Testable Structure

---

## Design Principle

Naming conventions, file standards, and code organization define the engineering culture of Project Velir.

A consistent codebase is easier to understand, easier to maintain, and easier for AI coding assistants such as Codex to extend safely.

By enforcing these standards from the beginning, Project Velir minimizes technical debt, improves collaboration, and creates a repository that remains organized even as it grows to hundreds of scripts, scenes, resources, and assets.

---

**End of Part 4**

**Next Sections (Part 5):**

* 13. Build Pipeline
* 14. Git Strategy
* 15. Development Workflow
* 16. Continuous Integration Strategy
# 13. Build Pipeline

The Build Pipeline defines how Project Velir progresses from source code to a playable release.

A consistent build process ensures repeatable, reliable, and verifiable releases across all supported platforms.

Version 1 targets **Android** as the primary platform while maintaining compatibility with desktop development environments.

---

## Build Philosophy

Every build should be:

* Reproducible
* Automated where practical
* Versioned
* Tested
* Traceable

Developers should be able to generate identical builds from the same source revision.

---

## Build Stages

```text id="build_pipeline"
Source Code

↓

Compile Scripts

↓

Import Assets

↓

Validate Resources

↓

Execute Tests

↓

Generate Build

↓

Package APK

↓

Release
```

Each stage must complete successfully before the next begins.

---

## Build Types

Project Velir supports multiple build configurations.

### Development Build

Purpose

* Daily development
* Debugging
* Internal testing

Features

* Debug Console
* Performance Overlay
* Cheat Commands
* Verbose Logging

---

### Testing Build

Purpose

* QA
* Playtesting
* Performance Evaluation

Features

* Gameplay Logs
* Error Reporting
* Performance Metrics

Debug cheats remain disabled.

---

### Release Build

Purpose

Public distribution.

Characteristics

✓ Optimized

✓ Debug tools removed

✓ Logging minimized

✓ Production settings enabled

---

## Build Configuration

Every build should include:

```text id="build_configuration"
Version Number

Build Number

Git Commit Hash

Build Date

Platform
```

This information assists with debugging and issue tracking.

---

## Build Output

```text id="build_output"
exports/

├── android/

│     ProjectVelir_v1.0.apk

│

├── windows/

├── linux/

└── macos/
```

Version 1 officially exports only Android builds.

---

## Build Rules

Every release build should satisfy:

✓ Compiles Successfully

✓ No Critical Errors

✓ No Missing Resources

✓ Version Updated

✓ Release Notes Prepared

---

# 14. Git Strategy

Git is the authoritative source of Project Velir.

Every change should be tracked through version control.

The repository should always remain in a buildable state.

---

## Branch Structure

```text id="git_branches"
main

↓

develop

↓

feature/*
```

Examples

```text id="feature_branches"
feature/battle-system

feature/ui-redesign

feature/ai-improvements

feature/velir-aram
```

---

## Main Branch

Purpose

Production-ready code.

Only tested and reviewed changes should be merged into `main`.

---

## Develop Branch

Purpose

Integration branch.

New gameplay systems should merge into `develop` before reaching `main`.

---

## Feature Branches

Every major feature receives its own branch.

Examples

```text id="feature_example"
feature/events

feature/save-system

feature/audio

feature-board
```

Feature branches should remain focused on a single gameplay domain.

---

## Commit Messages

Preferred format

```text id="commit_examples"
feat: implement BattleManager

fix: resolve player movement bug

refactor: simplify BoardManager

docs: update PV-023 signal architecture

test: add economy manager tests
```

Avoid

```text id="bad_commit"
update

fix

changes

final

new code
```

Commit messages should clearly describe the change.

---

## Pull Requests

Every Pull Request should include:

* Summary
* Related Document ID
* Testing Status
* Screenshots (UI Changes)
* Reviewer

---

## Repository Rules

The repository should always satisfy:

✓ Builds Successfully

✓ Passes Tests

✓ No Broken References

✓ Documentation Updated

---

# 15. Development Workflow

Project Velir follows a documentation-first development process.

Engineering documentation precedes implementation.

Implementation precedes testing.

Testing precedes release.

---

## Workflow Diagram

```text id="workflow"
Requirement

↓

Engineering Document

↓

Implementation

↓

Unit Testing

↓

Integration Testing

↓

Playtesting

↓

Release
```

Skipping workflow stages is discouraged.

---

## Feature Development

Every new feature follows:

```text id="feature_workflow"
Document

↓

Architecture Review

↓

Implementation

↓

Testing

↓

Code Review

↓

Merge
```

This process maintains architectural consistency.

---

## Daily Development Cycle

Recommended workflow

```text id="daily_workflow"
Pull Latest Code

↓

Create Feature Branch

↓

Implement Feature

↓

Run Tests

↓

Commit

↓

Push

↓

Create Pull Request
```

---

## Code Review Checklist

Every review should verify:

✓ Architecture

✓ Naming

✓ Documentation

✓ Signal Usage

✓ Performance

✓ Mobile Compatibility

✓ Test Coverage

---

## Testing Strategy

Before merging:

Run

* Unit Tests
* Integration Tests
* Gameplay Tests
* Performance Tests
* Regression Tests

Critical gameplay systems should never bypass testing.

---

# 16. Continuous Integration Strategy

Although Version 1 may begin with manual builds, the project should be structured to support Continuous Integration (CI) from the beginning.

Automated validation improves reliability and reduces integration issues.

---

## CI Pipeline

```text id="ci_pipeline"
Push Code

↓

GitHub Actions

↓

Run Validation

↓

Run Tests

↓

Verify Build

↓

Report Status
```

Every commit should be validated automatically whenever practical.

---

## Automated Checks

Recommended automated tasks:

✓ GDScript syntax validation

✓ Resource integrity checks

✓ Scene loading verification

✓ Documentation linting

✓ Unit tests

✓ Build generation

---

## Build Artifacts

CI should archive:

* APK
* Build Logs
* Test Results
* Coverage Reports

Artifacts assist debugging and release verification.

---

## Release Tags

Official releases should follow Semantic Versioning.

Example

```text id="release_tags"
v1.0.0

v1.0.1

v1.1.0

v2.0.0
```

---

## CI Goals

The CI pipeline should ensure:

✓ Every commit compiles

✓ Every release is reproducible

✓ Documentation remains synchronized

✓ Broken changes are detected early

---

## Design Principle

The Build Pipeline, Git Strategy, Development Workflow, and Continuous Integration process establish the operational engineering practices of Project Velir.

A disciplined workflow ensures that development remains predictable, collaborative, and scalable. By treating documentation, implementation, testing, and version control as equally important parts of the engineering process, Project Velir creates a professional development environment that supports long-term maintenance and AI-assisted development.

---

**End of Part 5**

**Next Sections (Final Part):**

* 17. Repository Validation Rules
* 18. Acceptance Criteria
* 19. Codex Implementation Notes
* 20. Future Expansion
* 21. Engineering Best Practices
* 22. Design Principle & Conclusion
# 17. Repository Validation Rules

Repository validation ensures that Project Velir remains organized, buildable, and maintainable throughout its development lifecycle.

Every contribution should satisfy the validation requirements before being merged into the main development branch.

Repository validation protects the project against broken references, inconsistent organization, missing assets, and architectural drift.

---

## Validation Philosophy

Every change should pass four levels of validation.

```text id="repository_validation_flow"
Repository

↓

Folder Structure

↓

File Structure

↓

Implementation

↓

Build Verification
```

Each level verifies a different aspect of project quality.

---

## Folder Validation

Verify:

✓ Correct folder hierarchy

✓ No misplaced files

✓ No duplicate folders

✓ No temporary directories

✓ No unused folders

Example

Correct

```text id="folder_validation_good"
scripts/managers/

resources/events/

scenes/ui/popups/
```

Incorrect

```text id="folder_validation_bad"
scripts/new/

resources/temp/

misc/
```

---

## File Validation

Every file should satisfy:

✓ Correct naming

✓ Correct extension

✓ Proper location

✓ Documentation updated

✓ Referenced correctly

Example

```text id="file_validation"
BoardManager.gd

↓

scripts/managers/
```

Not

```text id="file_validation_bad"
scripts/random/
```

---

## Scene Validation

Every scene should verify:

✓ No missing scripts

✓ No missing textures

✓ No missing resources

✓ Correct node hierarchy

✓ No broken references

Scenes should load without editor warnings.

---

## Resource Validation

Verify:

✓ Resource IDs

✓ Valid references

✓ Existing assets

✓ Correct configuration

✓ Version compatibility

Invalid Resources should fail validation immediately.

---

## Script Validation

Every script should satisfy:

✓ No syntax errors

✓ Proper formatting

✓ One responsibility

✓ Minimal dependencies

✓ Documentation header

---

## Repository Checklist

Before merging:

✓ Repository builds

✓ Tests pass

✓ Documentation updated

✓ Assets validated

✓ No merge conflicts

---

# 18. Acceptance Criteria

The Godot Project Structure document is considered complete when:

✓ Root repository structure is defined.

✓ Folder hierarchy is documented.

✓ Scene organization is complete.

✓ Resource organization is complete.

✓ Script organization is complete.

✓ Naming conventions are documented.

✓ File standards are established.

✓ Git workflow is defined.

✓ Build pipeline is documented.

✓ Repository validation rules are established.

Future contributors should be able to organize new files without introducing ambiguity.

---

# 19. Codex Implementation Notes

Codex should treat this document as the authoritative reference for repository organization.

Before creating any new file:

Verify

* Correct folder
* Correct filename
* Correct naming convention
* Correct dependency location
* Correct ownership

---

## Repository Rules

Codex should never:

* Create duplicate folder structures.
* Introduce temporary directories.
* Place scripts inside scene folders.
* Place Resources inside assets folders.
* Place gameplay logic inside UI folders.

---

## File Creation Rules

When creating a new Manager

```text id="manager_creation"
scripts/managers/

↓

ManagerName.gd
```

When creating a Scene

```text id="scene_creation"
scenes/

↓

Feature/

↓

FeatureScene.tscn
```

When creating a Resource

```text id="resource_creation"
resources/

↓

Feature/

↓

FeatureData.tres
```

When creating Artwork

```text id="asset_creation"
assets/

↓

Category/

↓

asset_name.png
```

Codex should always preserve repository consistency.

---

# 20. Future Expansion

The repository structure has been designed to accommodate future growth without requiring major reorganization.

---

## Future Gameplay Modules

```text id="future_modules"
scripts/

diplomacy/

campaign/

multiplayer/

naval/

quests/
```

---

## Future Scene Modules

```text id="future_scenes"
scenes/

diplomacy/

campaign/

multiplayer/

cinematics/
```

---

## Future Resource Modules

```text id="future_resources"
resources/

campaign/

quests/

modding/

dlc/
```

---

## Future Asset Modules

```text id="future_assets"
assets/

cinematics/

dlc/

seasonal/

skins/
```

---

## Future Build Targets

Version 1

✓ Android

Future

✓ Windows

✓ Linux

✓ macOS

✓ Steam

✓ Nintendo Switch (Long-term)

The repository should support these platforms without structural redesign.

---

# 21. Engineering Best Practices

Every contributor should follow these engineering principles.

---

## Repository Hygiene

Keep the repository clean.

Remove:

* Temporary files
* Duplicate assets
* Obsolete resources
* Dead scripts

---

## Documentation

Documentation should evolve alongside implementation.

Every significant architectural change should update the corresponding engineering document before or alongside the code change.

---

## Reuse Before Creation

Before adding a new:

* Scene
* Resource
* Script
* Asset

verify that an existing reusable component cannot satisfy the requirement.

---

## Keep Systems Modular

Prefer:

Small independent modules

Instead of:

Large tightly coupled systems

---

## Performance Awareness

Organize assets and scripts to minimize:

* Loading time
* Memory usage
* Build size
* Search complexity

---

## AI-Friendly Repository

The repository should remain predictable.

A coding assistant should be able to determine:

* Where new files belong
* Which existing files to modify
* Which systems are affected

without ambiguity.

---

# 22. Design Principle & Conclusion

The repository structure is the physical representation of the software architecture.

A disciplined project layout is not merely a matter of organization; it directly influences development speed, maintainability, onboarding, debugging, and long-term scalability.

By enforcing:

* Consistent folder organization
* Predictable naming conventions
* Clear ownership
* Standardized workflows
* Documentation-first development
* Validation before integration

Project Velir establishes a professional engineering environment capable of supporting years of development and future expansion.

The repository is designed so that both human developers and AI coding assistants can navigate it confidently, understand it quickly, and extend it safely without introducing architectural inconsistencies.

This document, together with:

* **PV-021 – Class Diagram & Object Model**
* **PV-022 – Scene Hierarchy Specification**
* **PV-023 – Signal Architecture**
* **PV-024 – Data Model**

forms the complete foundation of the engineering architecture for Project Velir.

---

# End of Document

**Document ID:** PV-025

**Category:** Engineering Design Document (EDD)

**Document Name:** Godot Project Structure

**Version:** 1.0

**Status:** Complete
