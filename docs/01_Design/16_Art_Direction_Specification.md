# PV-016 — Art Direction Specification

**Project:** Project Velir
**Version:** 1.0
**Status:** Draft
**Owner:** Art Director

**Related Documents**

* PV-002 Master Game Specification
* PV-006 Board System Specification
* PV-007 Kingdom System Specification
* PV-008 Velir Aram System Specification
* PV-013 UI System Specification

**Last Updated:** June 2026

---

# 1. Purpose

This document establishes the complete visual identity of Project Velir.

It defines the artistic direction, visual language, color systems, architecture, environments, icons, animations, and asset standards to ensure every visual element belongs to the same world.

Every asset should immediately communicate:

> **Ancient Tamil Civilization. Strategy. Royal Power. Mystery.**

---

# 2. Art Vision

Project Velir is **not** a medieval European fantasy game.

It is a stylized strategy game inspired by ancient Tamilakam during the Sangam and Early Classical periods.

The visual style should feel:

* Ancient
* Royal
* Warm
* Elegant
* Historical
* Timeless

Players should instantly recognize that they are playing a game rooted in South Indian heritage.

---

# 3. Art Style

Project Velir adopts **Stylized Historical Realism**.

Characteristics:

* Clean readable shapes
* Moderate detail
* Strong silhouettes
* Rich textures
* Warm lighting
* High contrast for gameplay clarity

Avoid:

* Hyper realism
* Cartoon exaggeration
* Low-detail flat graphics
* Medieval fantasy tropes

---

# 4. Visual Inspiration

Primary inspiration includes:

* Sangam Literature
* Brihadeeswara Temple
* Shore Temple
* Mahabalipuram Monuments
* Madurai Temple Architecture
* Keeladi Archaeological Site
* Adichanallur Civilization
* Tamil-Brahmi Inscriptions
* Ancient Palm-leaf Manuscripts

These are inspirations rather than direct recreations.

---

# 5. Color Palette

## Global Palette

| Element | Primary Color   |
| ------- | --------------- |
| Stone   | Granite Grey    |
| Sand    | Sandstone Beige |
| Bronze  | Antique Bronze  |
| Gold    | Royal Gold      |
| Water   | Deep Blue       |
| Forest  | Palm Green      |
| Fire    | Ember Orange    |

The palette should remain warm and earthy.

---

# 6. Kingdom Themes

## Chola

Identity

Imperial Expansion

Palette

* Crimson
* Bronze
* Black
* Deep Gold

Architecture

* Massive temples
* Naval symbols
* Tiger motifs

---

## Chera

Identity

Trade & Prosperity

Palette

* Emerald Green
* Copper
* Brown

Architecture

* Ports
* Warehouses
* Spice markets
* Mountain trade routes

---

## Pandya

Identity

Culture & Heritage

Palette

* Sapphire Blue
* Ivory
* Gold

Architecture

* Temple cities
* Sacred ponds
* Cultural centers

---

## Pallava

Identity

Knowledge & Stone

Palette

* Golden Yellow
* Granite
* White

Architecture

* Rock-cut temples
* Stone monuments
* Learning centers

---

# 7. Velir Aram

Velir Aram must visually dominate the board.

Visual features include:

* Massive stone ruins
* Broken pillars
* Ancient carvings
* Sacred pools
* Overgrown vegetation
* Hidden chambers
* Bronze relics

The center should evoke curiosity and mystery.

---

# 8. Board Art

The game board should resemble an engraved royal map carved into stone.

Decorative elements include:

* Lotus patterns
* Kolam-inspired borders
* Palm-leaf motifs
* Temple engravings
* Ancient roads
* Rivers
* Mountain carvings

The board itself tells part of the world's story.

---

# 9. Character Art

Version 1 focuses on:

* Commander portraits
* Kingdom banners
* Tokens
* Statues

Full animated rulers are planned for future releases.

Character design principles:

* Noble appearance
* Traditional attire
* Distinct silhouettes
* Historically inspired ornaments

---

# 10. Iconography

Every gameplay system receives a unique icon.

Examples:

| Gameplay Element | Icon           |
| ---------------- | -------------- |
| Gold             | Ancient Coin   |
| Army             | Sword          |
| Influence        | Lotus          |
| Prestige         | Crown          |
| Temple           | Gopuram        |
| Harbor           | Ship           |
| Event            | Palm Scroll    |
| Battle           | Crossed Spears |
| Relic            | Ancient Seal   |

Icons should remain recognizable at small sizes.

---

# 11. Typography

Primary Font

Historical-inspired serif.

Secondary Font

Modern readable sans-serif.

Rules:

* Large body text
* High readability
* Consistent spacing
* Minimal decorative usage

---

# 12. Asset Categories

Version 1 assets include:

## Environment

* Board
* Tiles
* Ruins
* Trees
* Rivers
* Mountains

---

## UI

* Buttons
* Panels
* Icons
* Frames
* Banners

---

## Gameplay

* Kingdom Tokens
* Dice
* Commander Portraits
* Event Cards
* Relics

---

## Effects

* Resource Popups
* Battle Effects
* Ancient Discoveries
* Victory Effects

---

# 13. Animation Style

Animations should be:

* Smooth
* Purposeful
* Short

Examples:

* Dice Roll
* Token Movement
* Resource Collection
* Popup Fade
* Battle Impact

Target duration:

200–600 ms

---

# 14. Lighting

Lighting should reinforce atmosphere.

Examples:

Kingdom Regions

Warm sunlight

Velir Aram

Cool ambient lighting

Battles

High contrast dramatic lighting

Victory

Golden glow

---

# 15. Particle Effects

Version 1 uses lightweight particles.

Examples:

* Gold Sparkles
* Dust
* Smoke
* Falling Leaves
* Water Ripples
* Torch Flames

Particle systems should not reduce mobile performance.

---

# 16. Asset Naming Convention

Examples

```text
tile_trade_01.png

kingdom_chola_banner.png

commander_pandya.png

icon_gold.png

ui_panel_bronze.png

battle_slash_01.png
```

Consistent naming improves AI-assisted development.

---

# 17. Technical Specifications

Sprites

PNG

Transparent Background

Icons

SVG (Master)

PNG (Export)

Portraits

2048 × 2048

Tiles

512 × 512

Board

4096 × 4096

UI Icons

128 × 128

These values may change during optimization.

---

# 18. Performance Requirements

Target:

* 60 FPS
* Low memory usage
* Efficient texture atlases
* Minimal overdraw

All assets should be optimized for Android.

---

# 19. Testing Checklist

The following must be verified:

* Kingdoms visually distinct.
* Icons readable.
* Fonts readable.
* Board uncluttered.
* Velir Aram visually dominant.
* UI consistent.
* Animations smooth.
* Mobile performance maintained.

---

# 20. Codex Implementation Notes

Art assets should remain completely independent from gameplay logic.

Scenes reference artwork through Resources.

Never hardcode asset paths inside gameplay scripts.

Future asset replacements should not require code modifications.

---

# 21. Future Expansion

Planned visual improvements include:

* Animated commanders
* Seasonal environments
* Dynamic weather
* Day/Night cycle
* Animated water
* Temple festivals
* Cinematic introductions
* Premium board skins
* Cosmetic kingdom themes

The visual identity should evolve while preserving the distinctive Project Velir style.

---

# 22. Design Principle

Every screenshot of Project Velir should be instantly recognizable.

Without reading the title, players should immediately identify:

* Ancient Tamil inspiration
* Strategic gameplay
* Four rival kingdoms
* The mysterious ruins of Velir Aram

The art should celebrate Tamil heritage through elegance, authenticity, and readability rather than overwhelming realism.

---

**Document ID:** PV-016

**Version:** 1.0

**Status:** Complete
