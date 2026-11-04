# Design brief

## Established requirements

| Area | Requirement |
| --- | --- |
| Player count | 1–4 networked players; two-player development target |
| Perspectives | Independent first-person gunner views on separate devices |
| Aiming | Reticle-based aiming |
| Movement | Limited arena scrolling, preserving the original arcade feel |
| Excluded control models | Conventional FPS movement, side-scrolling characters, third-person mech movement, shared screen |
| Presentation | 16-bit/32-bit-inspired pixel graphics with modern animation and effects |
| Boss families | Mechanical, alien, biomechanical, kaiju |
| Boss systems | Destructible components, independent weapon systems, multiple combat phases |
| Cooperation | Different viewing angles and shared boss damage |
| Platforms | PC, mobile, console ambitions; delivery order beyond initial PC work remains open |

## First boss: Iron Gladiator

The Iron Gladiator is the agreed first milestone boss. Its detailed appearance, component layout, attacks, and phase triggers have not yet been approved.

Candidate design questions, not established features:

- Which components can each gunner see and hit?
- Which destroyed parts disable an attack, reveal a vulnerability, or change a phase?
- What useful cooperative interaction requires the two viewpoints?
- How do players defend or evade within the limited-scroll model?
- What happens when a gunner is defeated, joins late, or disconnects?

## Three weapons

Three weapons are required for the slice. Names, damage, ammunition, cooldowns, firing behavior, and balance are undecided.

Weapon selection must create meaningful choices without requiring conventional FPS movement.

## Viewing angles and art

Both gunners must fight the same boss. Different angles must agree on component identity, exposure, obstruction, and destruction.

The rendering approach is undecided. Candidates include angle-specific sprites with shared gameplay geometry, or 3D geometry rendered into a pixel-style presentation. No candidate has been selected.

## Scope boundary

One boss and one arena are sufficient to prove the first milestone. That does not remove other boss families or the eventual four-player and platform ambitions.
