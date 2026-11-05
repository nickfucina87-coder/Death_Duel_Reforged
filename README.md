# Death Duel Reforged

**Owners:** Nick ([nickfucina87-coder](https://github.com/nickfucina87-coder)) and Mike ([Doomious](https://github.com/Doomious))

A multiplayer spiritual successor to the 1992 Sega Genesis game **Death Duel**, preserving its first-person reticle aiming and limited arena scrolling.

**Status: repository setup and design documentation. Nick’s Ember Inochi2D look pack is in [Ember/](Ember/). No game implementation is included. Engine selection is open.**

## The game

- 1–4 networked players, with **two players as the initial development target**.
- Independent first-person gunner views on separate devices.
- Reticle aiming and limited arena scrolling; no conventional FPS movement, side-scrolling characters, or shared-screen play.
- 16-bit/32-bit-inspired pixel graphics with modern animation and effects.
- Mechanical, alien, biomechanical, and kaiju bosses.
- Destructible boss components, independent weapon systems, and multiple phases.
- Different viewing angles with shared boss damage and cooperative opportunities.
- Long-term ambitions for PC, mobile, and consoles; these are not completed or promised ports.

## First development milestone

A playable two-player networked vertical slice with the **Iron Gladiator**, limited-scroll aiming, three weapons, destructible components, and synchronized combat.

This milestone is a target, not an existing build.

## Start here

| Document | Purpose |
| --- | --- |
| [Design brief](docs/DESIGN_BRIEF.md) | Established requirements and open design questions |
| [Technical baseline](docs/TECHNICAL_BASELINE.md) | Actual repository findings, technical risks, and decisions still needed |
| [First milestone](docs/FIRST_MILESTONE.md) | Smallest meaningful implementation sequence and acceptance checks |
| [Project status](docs/STATUS.md) | Created, verified, and unfinished work |
| [Contributor rules](AGENTS.md) | Guardrails for humans and development agents |
| [Connect your tools](docs/CONNECT_YOUR_TOOLS.md) | Use this repository in ChatGPT, Cursor, and Claude |
| [Ember look pack](Ember/) | Inochi2D face, hair, jacket, body layers, and puppet files for Claude |

## Before anyone writes game code

Read the documents, inspect the current repository, and agree on the engine and combat geometry. Do not silently select an engine or replace the established arcade movement model.

The current authorized work is **GitHub organization and documentation**. Game implementation requires a new instruction from the owner.
