# PV-018 — Testing & Quality Assurance Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** QA Lead / Technical Director

**Related Documents**

* PV-001 AI Constitution
* PV-004 Core Gameplay Loop
* PV-006 Board System Specification
* PV-012 AI System Specification
* PV-017 Technical Architecture Specification

**Last Updated:** June 2026

---

# 1. Purpose

This document defines the testing strategy, quality assurance process, and release criteria for Project Velir.

Testing is not a final development phase. Every feature should be tested immediately after implementation.

The objective is to ensure that gameplay remains stable, fair, enjoyable, and performant across supported Android devices.

---

# 2. QA Philosophy

Project Velir follows five testing principles.

### Test Early

Every feature should be tested immediately after implementation.

---

### Test Continuously

Testing occurs throughout development rather than only before release.

---

### Test Real Gameplay

Automated testing should be complemented by real gameplay sessions.

---

### Prevent Regression

New features must never break existing systems.

---

### Data Before Opinion

Balancing decisions should be based on gameplay statistics rather than assumptions.

---

# 3. Testing Pyramid

Project Velir follows a layered testing strategy.

```text id="testing_pyramid"
        Playtesting
              ▲
      Integration Tests
              ▲
         Unit Tests
```

Every layer supports the next.

---

# 4. Testing Categories

Version 1 includes:

* Unit Testing
* Integration Testing
* Gameplay Testing
* Performance Testing
* UI Testing
* AI Testing
* Save/Load Testing
* Regression Testing

Each category has dedicated acceptance criteria.

---

# 5. Unit Testing

Every manager should be tested independently.

Examples:

### DiceManager

Tests:

* Dice values between 1–6
* Equal probability
* No invalid values

---

### EconomyManager

Tests:

* Gold increases correctly
* Gold decreases correctly
* Negative Gold prevented

---

### BattleManager

Tests:

* Battle formula
* Tie rule
* Reward application

---

# 6. Integration Testing

Verify systems communicate correctly.

Examples:

* Dice → Movement
* Movement → Tile
* Tile → Event
* Event → Economy
* Economy → UI

Signals should trigger expected behavior.

---

# 7. Gameplay Testing

Complete matches should verify:

* Match duration
* Resource balance
* AI competitiveness
* Battle frequency
* Player engagement

Target Match Length:

15–20 minutes

---

# 8. Performance Testing

Supported Target Device

Mid-range Android phone

Performance goals:

| Metric        | Target      |
| ------------- | ----------- |
| FPS           | 60          |
| RAM Usage     | < 500 MB    |
| Load Time     | < 5 seconds |
| Autosave      | < 250 ms    |
| Battery Usage | Moderate    |

Gameplay should remain smooth throughout long sessions.

---

# 9. User Interface Testing

Verify:

* Responsive layouts
* Correct scaling
* Touch targets
* Font readability
* Popup behavior
* Orientation locking

All supported Android resolutions should be tested.

---

# 10. AI Testing

AI should:

* Complete turns.
* Use resources intelligently.
* Enter Velir Aram strategically.
* Avoid impossible actions.
* Respect kingdom personalities.

AI should never become stuck.

---

# 11. Save & Load Testing

Verify:

* Autosave
* Manual Save
* Match restoration
* Event restoration
* AI restoration
* Board restoration
* Economy restoration

Loading should restore the exact gameplay state.

---

# 12. Balance Testing

Collect gameplay metrics.

Examples:

* Win Rate
* Average Gold
* Average Army
* Battle Frequency
* Event Frequency
* Prestige Gain
* Match Duration

These statistics guide balancing decisions.

---

# 13. Regression Testing

Before every release:

Verify:

* Existing gameplay
* Previous bug fixes
* Save compatibility
* UI behavior
* Performance

Regression testing is mandatory.

---

# 14. Bug Classification

| Priority | Description              |
| -------- | ------------------------ |
| Critical | Crash or corrupted save  |
| High     | Gameplay-breaking bug    |
| Medium   | Incorrect mechanics      |
| Low      | Minor UI or visual issue |
| Cosmetic | Art or animation issue   |

Critical bugs block release.

---

# 15. Bug Report Format

Every reported issue should include:

* Bug ID
* Build Version
* Device
* Description
* Reproduction Steps
* Expected Result
* Actual Result
* Screenshot or Video
* Severity

Consistent reports improve debugging efficiency.

---

# 16. Test Environment

Required devices:

* Low-end Android
* Mid-range Android
* High-end Android
* Tablet (Future)

Testing should cover different screen sizes and Android versions.

---

# 17. Automation Strategy

Future automated tests include:

* Dice probability validation
* Save file validation
* Battle calculations
* Resource calculations
* Event selection
* AI simulations

Automation should reduce repetitive manual testing.

---

# 18. Acceptance Criteria

A feature is complete only if:

✔ Compiles successfully

✔ Passes unit tests

✔ Passes integration tests

✔ Passes gameplay testing

✔ Meets performance targets

✔ Has documentation

✔ Has no Critical bugs

---

# 19. Release Checklist

Before public release:

* All Critical bugs fixed.
* High-priority bugs reviewed.
* Performance verified.
* Save compatibility confirmed.
* AI tested.
* UI tested.
* Audio tested.
* Documentation updated.

No release should bypass this checklist.

---

# 20. Codex Implementation Notes

Codex should generate:

* Testable managers
* Small functions
* Predictable outputs
* Clear logging
* Assertions where appropriate

Gameplay systems should expose interfaces suitable for automated testing.

---

# 21. Future Expansion

Future QA improvements may include:

* Continuous Integration (CI)
* Automated Android builds
* Crash analytics
* Performance telemetry
* Multiplayer testing
* Cloud testing
* AI simulation tournaments
* Automated balancing reports

These systems should integrate without changing the core QA workflow.

---

# 22. Design Principle

Quality is achieved through continuous verification, not final inspection.

Every feature should be considered incomplete until it has been thoroughly tested under realistic gameplay conditions.

Stable gameplay builds player trust, and player trust is one of Project Velir's greatest assets.

---

**Document ID:** PV-018

**Version:** 1.0

**Status:** Complete
