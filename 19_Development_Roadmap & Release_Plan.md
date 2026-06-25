# PV-019 — Development Roadmap & Release Plan

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Project Director

**Related Documents**

* PV-000 Project Vision
* PV-001 AI Constitution
* PV-002 Master Game Specification
* PV-017 Technical Architecture Specification
* PV-018 Testing & QA Specification

**Last Updated:** June 2026

---

# 1. Purpose

This document defines the complete development roadmap for Project Velir.

It establishes the development milestones, release phases, deliverables, quality gates, and long-term vision for transforming Project Velir from an idea into a commercially released strategy game.

Every milestone should result in a playable build.

---

# 2. Development Philosophy

Project Velir follows an **AI-First Iterative Development Model**.

Every development phase must satisfy four rules:

* Always produce a playable build.
* Keep the project modular.
* Test every completed feature.
* Document everything before implementation.

Documentation always precedes coding.

---

# 3. Development Timeline

```text id="development_timeline"
Planning

↓

Documentation

↓

Prototype

↓

Core Gameplay

↓

Feature Complete

↓

Closed Testing

↓

Open Beta

↓

Google Play Release

↓

Post Launch Updates
```

---

# 4. Version Roadmap

| Version | Goal            | Status     |
| ------- | --------------- | ---------- |
| 0.1     | Documentation   | ✅ Complete |
| 0.2     | Board Prototype | Planned    |
| 0.3     | Core Gameplay   | Planned    |
| 0.4     | AI Integration  | Planned    |
| 0.5     | MVP Complete    | Planned    |
| 1.0     | Public Launch   | Planned    |

---

# 5. Phase 1 — Foundation

Objectives

* Git Repository
* Documentation
* Project Structure
* Godot Setup
* Coding Standards

Deliverables

* Repository
* Documentation
* Architecture

Completion Criteria

* Documentation approved.
* Repository organized.
* AI Constitution finalized.

---

# 6. Phase 2 — Prototype

Objectives

* Board System
* Dice
* Turn System
* Movement
* Basic UI

Deliverable

First playable prototype.

Players should be able to complete an entire match without battles or events.

---

# 7. Phase 3 — Core Gameplay

Objectives

* Resources
* Tile System
* Battles
* Economy
* Events
* Velir Aram

Deliverable

Complete gameplay loop.

Players should experience the intended strategy mechanics.

---

# 8. Phase 4 — AI Integration

Objectives

* AI Kingdoms
* Difficulty Levels
* Kingdom Personalities
* Resource Management
* Strategic Decision Making

Deliverable

Single-player mode becomes fully playable.

---

# 9. Phase 5 — Polish

Objectives

* Animations
* Audio
* UI Improvements
* Visual Effects
* Accessibility
* Performance Optimization

Deliverable

Feature-complete MVP.

---

# 10. Phase 6 — Closed Alpha

Testing Focus

* Stability
* AI Balance
* Match Length
* User Experience
* Bug Reports

Participants

Small invited testing group.

Feedback drives balancing.

---

# 11. Phase 7 — Closed Beta

Objectives

* Larger player base
* Device compatibility
* Gameplay balancing
* Performance testing

Target

100–500 testers.

---

# 12. Version 1.0 Release

Launch Platform

Google Play Store

Release Goals

* Stable gameplay
* Complete documentation
* High-quality visuals
* Balanced AI
* Reliable Save System

The MVP should feel complete despite future planned content.

---

# 13. Post Launch Roadmap

Version 1.1

* New Event Cards
* Balance Updates
* Bug Fixes

---

Version 1.2

* Additional Relics
* More Ancient Sites
* Improved AI

---

Version 1.5

* Commander Expansion
* Cosmetic Content
* Seasonal Boards

---

Version 2.0

Major Update

Features

* Online Multiplayer
* Ranked Matches
* Friends System
* Matchmaking
* Leaderboards

---

# 14. Long-Term Vision

Future milestones may include:

* Campaign Mode
* Story Expansion
* Steam Release
* iOS Release
* Tablet Optimization
* Cross-platform Multiplayer
* Clan System
* Tournament Mode
* Mod Support

---

# 15. Development Workflow

Every feature follows the same workflow.

```text id="workflow"
Design

↓

Documentation

↓

Implementation

↓

Testing

↓

Review

↓

Merge

↓

Release
```

No feature skips any stage.

---

# 16. Git Workflow

Main Branches

```text id="git_workflow"
main

↓

develop

↓

feature/*
```

Examples

```
feature/board-system

feature/battle-system

feature/ui

feature/ai

feature/events
```

Every feature should be developed independently before merging.

---

# 17. Release Criteria

A milestone is complete only when:

* Documentation approved.
* Code reviewed.
* Tests passed.
* Android build successful.
* Performance targets achieved.
* No Critical bugs remain.

---

# 18. Codex Workflow

Codex should follow this order.

1. Read Documentation
2. Build Manager
3. Write Tests
4. Generate Resources
5. Verify Build
6. Commit Changes

Codex should never implement undocumented features.

---

# 19. Success Metrics

Project success is measured by:

Technical

* Stable 60 FPS
* Fast loading
* Minimal crashes

Gameplay

* Average match 15–20 minutes
* Balanced kingdom win rates
* High replayability

Player Experience

* Easy onboarding
* Positive reviews
* Strong retention

---

# 20. Risk Assessment

| Risk                | Mitigation                   |
| ------------------- | ---------------------------- |
| Feature Creep       | Strict MVP scope             |
| AI Complexity       | Modular AI system            |
| Poor Balance        | Frequent playtesting         |
| Performance Issues  | Continuous profiling         |
| Documentation Drift | Documentation-first workflow |

Risks should be addressed early rather than after implementation.

---

# 21. Future Team Structure

As Project Velir grows, recommended roles include:

* Game Director
* Gameplay Programmer
* AI Engineer
* UI/UX Designer
* Environment Artist
* Character Artist
* Audio Designer
* QA Engineer
* Community Manager

Initially, many of these roles may be fulfilled by AI-assisted development.

---

# 22. Design Principle

Project Velir should evolve through disciplined, incremental development.

Every version should be enjoyable to play, easier to maintain than the last, and provide a stronger foundation for future expansion.

A successful roadmap is not measured by the number of completed features, but by consistently delivering polished, well-tested gameplay.

---

**Document ID:** PV-019

**Version:** 1.0

**Status:** Complete
