# Iron Gladiator — giant mech proof-of-concept asset list

Status: production planning document, not delivered artwork or implemented gameplay.
Working name: Iron Gladiator, preserving the existing repository name. The owner's recollection of Iron Gauntlet/Iron Giant is not treated as a rename.
Scope: one giant mechanical boss, one arena, two-PC proof; retain 1–4-player support as the design target. Engine and rendering pipeline remain open.

## Requirements carried forward

- Original giant mech inspired by the spirit of Sega Genesis Death Duel: first-person gunner cockpit, reticle aiming, limited scrolling, separate networked devices.
- Consistent 16-bit/32-bit-inspired pixel presentation, with more precise aiming and clear feedback.
- One shared boss. Opposing players see front versus rear when its facing aligns with their stations; adjacent stations see corresponding side/three-quarter views.
- Boss turns and changes aggro. Destruction and exposed weak points agree across all perspectives.
- More participating players make the boss physically larger and more dangerous. Exact dimensions and balance remain to be tested.
- No game code or engine choice is established by this asset plan.

Everything below that specifies appearance, counts, attacks, sizes, or weapon roles is a proposed production baseline, not a previously approved feature.

## 1. Proposed mech identity and component inventory

Industrial arena siege mech: broad armored torso, heavy legs, recessed sensor head, cannon on its anatomical right, missile assembly on its anatomical left, rear reactor. Gunmetal armor, worn ochre markings, orange heat, distinct cyan reactor. Strong silhouettes; avoid decorative detail that disappears at gameplay resolution. All artwork must be original.

| Stable ID | Asset / separation | States or purpose |
| --- | --- | --- |
| IG-01 | Pelvis / internal chassis | Shared structural base; intact and wrecked |
| IG-02 | Chest armor plate | Intact, damaged, detached; protects core |
| IG-03 | Front core beneath plate | Closed/protected, exposed, hit, overload |
| IG-04 | Sensor head | Scan, target acquisition, damaged |
| IG-05 | Anatomical right upper arm | Independent attachment and motion |
| IG-06 | Right forearm cannon | Idle, charge, fire, recoil, disabled, detached |
| IG-07 | Anatomical left upper arm | Independent attachment and motion |
| IG-08 | Left missile assembly | Closed, open, launch, empty, disabled, detached |
| IG-09 | Rear reactor housing | Intact, damaged, breached |
| IG-10 | Rear radiator shutters and inner vent | Separate shutters; closed, open, venting, destroyed |
| IG-11/12 | Left/right thigh assemblies | Separate legs for weight shifts |
| IG-13/14 | Left/right shin assemblies | Intact, damaged; gait remains readable |
| IG-15/16 | Left/right feet | Planted, lifted, impact |
| IG-17 | Cables, pistons, joint caps | Separate only where animation requires it |
| IG-18 | Wreck / debris kit | Chest plate, cannon, launcher, armor fragments |

These are source components, not a promise of 18 final sprite sheets. Export structure depends on the chosen rendering method. The reactor housing and vent are separate so the vent can animate without replacing the whole back.

Anatomical left/right never changes with viewer position. Do not mirror asymmetric weapons.

## 2. Directional coverage and references

Build one coherent turnaround from one source design. Independent front/back image generations cannot establish consistent production geometry.

Required reference deliverables: front, rear, anatomical left, anatomical right, top, three-quarter construction view, exploded component layout, palette/material sheet. Orthographic construction views support assembly; gameplay exports use the actual gunner camera projection and elevation.

Proposed directional export baseline: 16 azimuth samples at 22.5-degree intervals. DIR00 shows the front; DIR04 shows anatomical right; DIR08 shows rear; DIR12 shows anatomical left. Intermediates cover all three-quarter views. These are sampled views, not continuous 360-degree animation.

| Viewer relationship | Direction sample relationship |
| --- | --- |
| Same camera elevation, opposite stations | Eight samples apart, modulo 16 |
| Same camera elevation, adjacent quadrant stations | Four samples apart, modulo 16 |
| Boss turns | Every client recalculates from the same authoritative pose |
| Torso twists separately | Render both shared torso and chassis transforms; whole-body yaw alone is insufficient |

Station layout proposal: P1 NE, P2 SW for the opposing two-player proof; P3 NW, P4 SE for four-player coverage.

The runtime must derive each view from station position and actual boss facing, not permanently assign “front art” to P1. At arbitrary angles, directional sampling approximates the pose; validate visible hit regions near sample transitions. If this is too coarse, increase samples or use pixel-rendered geometry before polishing art.

All directions share dimensions, pivots, ground baseline, attachment coordinates, lighting convention, and animation frame timing. No view-specific armor or weapon swaps. Top references are construction aids, not top-down gameplay assets.

## 3. Animation inventory

Frame counts below are budgeting proposals per direction where the action is visible. Hidden parts need not receive useless exports.

| Clip / state | Suggested frames | Purpose |
| --- | --- | --- |
| Idle / mechanical breathing | 6 | Weight and operating machinery |
| Aggro acquisition / wind-up | 4 | Readable target change |
| Turning / foot planting | 8 | Turn motion with weight transfer; yaw comes from shared state |
| Cannon charge | 4 | Dodge/cover warning |
| Cannon fire / recoil | 4 | Shot timing and feedback |
| Missile bay open / close | 4 each | Exposes launch mechanism |
| Missile launch | 4 | Salvo timing |
| Rear vent open / close | 4 each | Cooperative vulnerability window |
| Stagger | 4 | Confirmed heavy impact |
| Overload | 6 | Final phase warning |
| Collapse | 10 | Shared defeat event |
| Wreck idle | 1 | Persistent encounter end state |

Budget example only: one 6-frame full-body clip at 16 directions is 96 images before packing. This is why directional proof precedes full animation production.

Use modular damage layers or component visibility so losing the cannon does not require every possible combination of full-body damage sheets. Depth order changes by view: rear components cannot simply be drawn on top of front armor. Directional exports need correct occlusion/masks, or geometry must provide it.

## 4. Cooperative encounter and aggro assets

Proposed first interaction: player A draws frontal cannon attention; player B attacks the rear radiator during its vent window. When attention switches, the boss turns, the exposed angle changes for both players, and station-specific danger indicators update.

Required presentation assets:
- Sensor tracking motion and target-acquisition light.
- Directional attack warning plus distinct target-lock sound.
- Cockpit indicator: TARGETING YOU / TARGETING ALLY, backed by shared target state.
- Rear shutter motion, heat plume, exposed vent glow, confirmed weak-point hit effect.
- Cannon-disabled and launcher-disabled silhouettes visible wherever those components are exposed.
- Short universal warning for attacks that threaten multiple stations.

Aggro design proposal: damage builds threat; a deliberate challenge/ping can create a temporary threat burst. Add target commitment and a switch margin to prevent constant spinning. Exact threat values, duration, cooldown, and any taunt control remain tuning work. Do not implement instant permanent taunt-lock.

Asset cues must follow real targeting and attack commitment. Looking toward a player alone does not prove an attack targets them.

## 5. Giant scale and player-count variants

Proposed test sizes, not final canon:

| Participating players | Height | Presentation / encounter proposal |
| --- | --- | --- |
| 1 | 40 m | Base configuration |
| 2 | 50 m | Larger silhouette; alternating station pressure |
| 3 | 60 m | Additional salvo pressure |
| 4 | 70 m | Maximum scale; coordinated attack windows |

One source mech supports all sizes. Camera distance, ground contact, cover, muzzle positions, shot geometry, weak-point visibility, and source pixel resolution must be checked at each size. Do not merely enlarge a PNG independently of its hit geometry. Do not move the camera back enough to cancel all perceived growth.

Support scale cues: fixed-size buildings, loading cranes, catwalks, antennae, containers, dust and footfall impacts. Establish the largest intended screen footprint before final raster export.

For early proof, apply player-count changes at encounter start/restart. Later mid-fight joins require an explicit synchronized growth transition; growth VFX are deferred assets until join behavior is chosen. A player being defeated must not immediately shrink the boss.

## 6. Arena and parallax kit

Proposed arena: circular industrial test yard with stations around its perimeter.

| Kit | Required assets |
| --- | --- |
| Shared layout reference | Top plan with boss center, four station positions, cover and sightlines |
| Background | Distant skyline, middle-distance cranes/gantries, arena wall |
| Ground | Yard floor, boss contact shadow, footfall/debris overlays |
| Near layer | Station railing / structural framing |
| Cover | Three silhouettes: low concrete barrier, tall steel shield, machinery block; intact and destroyed states |
| Scale landmarks | Building facade, crane, catwalk, container |
| Atmosphere | Sparse smoke, heat vent plume, dust |
| Station dressing | Four layout-consistent camera views |

A world landmark occupies one shared location and appears only where that camera can see it. Opposite views are not mirrored copies. Parallax follows bounded camera motion; it must not imply full player locomotion. Cover visibility, destruction, and shot blocking must agree with gameplay.

## 7. Player weapon and combat effects kit

Three provisional weapon roles preserve the existing three-weapon target; names/balance are open.

| Role | Visual assets | Audio |
| --- | --- | --- |
| Rapid cannon | Muzzle flash, tracer, shell ejection, reload/heat state | Fire loop, tail, reload, overheat |
| Precision cannon | Charge, narrow shot, recoil, armor penetration impact | Charge, shot, confirmed impact |
| Rocket launcher | Launch flash, rocket, smoke trail, blast | Launch, flight, detonation |

Shared VFX: armor ricochet, ordinary impact, weak-point impact, sparks, component break, explosion, smoke, cockpit damage, footfall dust.
Shared audio: servos, turning feet, cannon charge/fire, missile bay/launch, vent opening, reactor warning, stagger, component loss, collapse, arena ambience, victory/defeat.

Aim proposal: direct responsive reticle, adjustable sensitivity, clear impact location and separate confirmed hit feedback. Use the shared visible surface/occlusion for hits; no random spread on the precision weapon. Any latency treatment remains a technical decision. Pretty muzzle effects must not determine hit outcomes.

## 8. Rudimentary but functional UI kit

- Cockpit frame and readable pixel font; clear central aiming window.
- Reticle states: ready, firing, reload/unavailable; hit marker only after confirmed hit.
- Hull/armor gauge, ammunition, heat, reload progress, selected weapon.
- Boss health, component condition, current target, station direction.
- Ally hull/down/disconnected status and teammate labels.
- Main menu, host/join, two-player ready lobby, weapon selection, encounter start.
- Victory, defeat, restart, connection lost/reconnecting.
- Controller/touch variants remain future platform assets; PC proof comes first.

Indicators must reflect actual game state. Color should be reinforced by shape, icon, or text. Avoid ornamental meters with no gameplay meaning.

## 9. Export and delivery rules

Proposed visual baseline: 640x360 internal frame, integer-scaled presentation, nearest-neighbor pixel treatment, controlled palette and crisp silhouettes. Validate readability before fixing final sheet dimensions; avoid mixing unrelated pixel scales.

- Transparent PNGs for sprites/effects; no baked checkerboard or labels.
- Preserve editable source, palette, rig if used, and export settings.
- Separate labeled reference boards from clean production exports.
- Naming example: IG_CannonR_DIR04_Fire_F03.png.
- Manifest fields: asset ID, component ID, direction, clip, frame, frame duration, pivot, attachment points, bounds, source version, license/provenance.
- Keep gameplay colliders and shot tests aligned with presentation, including removed parts.
- A sprite source workflow and a geometry render workflow are both possible. Do not commission both complete pipelines; validate one first.

## 10. Production order and acceptance

1. Make one coherent mech reference turnaround and component diagram.
2. Prove front/rear and both side views in neutral pose.
3. Add diagonal views and turning; validate 16-direction sampling.
4. Prove chest protection, rear vent exposure, and cannon removal across opposing views.
5. Add aggro cues and one cannon attack.
6. Add remaining clips, three weapons, arena layers, HUD and audio.
7. Test all four proposed sizes and then expand polished assets.

Visual checks: no left/right swaps; same pose and frame time across views; plausible occlusion; detached parts remain absent; rear vent cannot be hit through front armor; foreground cover blocks correctly; weak points remain readable at the largest scale.

Gameplay/network checks remain unfinished: two-PC shared damage, turning and aggro; component destruction; resource/HUD agreement; restart; disconnect/rejoin; timing under latency.

Created: this asset specification.
Verified: existing repository instructions and design brief inspected; naming and movement requirements preserved.
Not delivered: reference renders, sprites, models, animations, audio, engine project, gameplay or multiplayer tests.
