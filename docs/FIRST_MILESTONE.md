# First milestone: two gunners vs. Iron Gladiator

**Target:** a playable two-player networked vertical slice.  
**Current status:** planned; no game implementation committed.

## Smallest viable sequence

1. **Agree on the technical foundation.** Select the engine, rendering/hitbox representation, fixed viewpoints, bounded scrolling, and authority model.
2. **Prove one shared target.** Two clients on separate devices see one stationary component from different viewpoints. Validate reticle projection and occlusion before adding boss complexity.
3. **Prove synchronized destruction.** Shared component health, one authoritative destruction result, and correct late-join state.
4. **Build the Iron Gladiator encounter.** One arena, the approved component layout, independent attack systems, multiple phases, player damage, victory/defeat, and restart.
5. **Add the three approved weapons.** Distinct roles and authoritative firing/resource rules.
6. **Validate the full loop.** Two-PC playtest, latency checks, disconnect/rejoin, and art/readability review.

Placeholder art is acceptable for technical proof. It must be labeled as placeholder work; it does not establish final boss art or the finished pixel-art treatment.

## Acceptance checklist

- [ ] Owner approves engine and architecture.
- [ ] Two players connect from separate devices.
- [ ] Each receives an independent first-person gunner perspective.
- [ ] Reticle aiming and limited arena scrolling work without conventional FPS movement.
- [ ] Both views correspond to the same Iron Gladiator and components.
- [ ] Visible and obstructed components resolve correctly from both angles.
- [ ] Three distinct weapons operate with authoritative validation.
- [ ] Destruction changes the boss's combat behavior.
- [ ] Multiple phases synchronize between players.
- [ ] Shared damage and match outcome agree.
- [ ] Victory, defeat, and restart produce consistent state.
- [ ] A late joiner receives the current component/phase state.
- [ ] Disconnect behavior is defined and tested.
- [ ] Tested latency conditions and remaining limitations are recorded.
- [ ] Pixel presentation is readable and retains the intended arcade feel.

## Beyond this milestone

Four-player expansion, additional boss families, polished art/audio, internet session discovery, and mobile/console delivery remain future work. The initial slice should preserve the ability to pursue them without claiming they are delivered.
