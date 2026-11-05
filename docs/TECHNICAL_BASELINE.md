# Technical baseline

## Repository inspection

Inspected repository: nickfucina87-coder/Death_Duel_Reforged  
Branch: main  
Starting commit: 272e5d2551613b8b77cbe3c60a4bbd595d458564

The initial inspection found only README.md with the project name. During setup, commit 413aaece0059545a1d77ba63d01377fbbec05bbf expanded that README with owner information and an early-setup status. This setup preserves that owner information. No engine project, code, or assets were present in either inspected tree.

| Item | Actual finding |
| --- | --- |
| Engine | No engine project present; selection open |
| Architecture | No gameplay architecture present |
| Code | No game source present |
| Assets | `Ember/` Inochi2D look pack (reference art and puppet files). No gameplay asset pipeline |
| Functionality | No implemented or verified game functionality |
| Existing decisions | User's design brief; preserved in DESIGN_BRIEF.md |

The README and root contents were fetched directly from GitHub. No claim is made about unpublished files on either developer's PC.

`Ember/` was added after that inspection. It is Nick’s Inochi2D look pack for Claude. It does not add an engine, game source, or implemented gameplay.

## Decisions required before implementation

1. Select an engine with the owner, considering both developers' experience, networking, pixel presentation, and longer-term platform ambitions.
2. Define fixed gunner station geometry and exactly what limited scrolling changes.
3. Choose a shared representation for boss components and shot occlusion.
4. Choose authority, transport, session lifecycle, and initial hosting model.
5. Define the Iron Gladiator's minimum component/phase layout and three weapon roles.
6. Record the approved decisions before implementing them.

## Recommended architecture — proposal only

One authority should own boss health, component destruction, attack timing, phase transitions, and match outcome. Clients should submit shot intent rather than declare damage.

A shot should be reconstructed using the assigned gunner station, bounded view/scroll input, reticle coordinates, and validated timing. Each component needs a stable ID shared by every view.

The authority should resolve the nearest valid hit with occlusion, then distribute confirmed combat results. Presentation effects must not independently determine damage.

This is an architectural recommendation, not an implemented system or an approved engine-specific design.

## Principal risks

| Risk | Why it matters | Proposed proof |
| --- | --- | --- |
| Different-angle hit detection | A visible weak point may be obstructed in shared geometry | Fire at the same component from both stations, including blocked cases |
| Sprite/geometry mismatch | Artwork can imply a hittable region outside its collider | Compare reticle impacts and component outlines at every supported angle |
| Latency and moving poses | A shot may reach the host after the boss moves | Define a timing policy; test delayed shots against recorded poses |
| Destruction ordering | A delayed shot may bypass armor that was present when fired | Test component destruction and late shots in both orders |
| Duplicate/out-of-order messages | Damage or transitions may apply twice | Repeat/reorder commands and confirm one authoritative result |
| Session lifecycle | Late joiners can receive stale or incomplete boss state | Join after damage, destruction, and phase changes; reconnect |
| Scaling to four | Extra stations may require art and visibility redesign | Reserve stable player/component IDs and revisit visibility before expansion |
| Cross-platform ambitions | Input, performance, transport, and deployment differ | Treat each platform as a separate validation gate |

## Multiplayer verification standard

Separate simulation checks, local multi-process network checks, two physical PC tests, and internet tests. Passing one does not establish the others.

Record engine version, build/commit, test setup, observed result, and known limitations. No multiplayer test has been run on a game build in this repository.
