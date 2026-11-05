# Ember - hard rules for later sessions

1. Master pose is T-stance. Masters: jacket-on `/workspace/ember-puppet-art/body/qa/still_closed.png (971x1620)` (coat authority) and jacket-off `/workspace/ember-puppet-art/body/qa/still_shirt.png (971x1620)` (body/shirt/torso-under-coat authority). The arms-down image `/home/box/agent-data/agents/c46d3140-db71-4275-8518-90b54565a67b/attachments/ff11fa07de1959af1875b3e49f89ee5206038f2084df35132cb5db49ce9b0381.png (971x1620; arms-down REF ONLY)` is reference only, for resting sleeve folds and hands. Never cut pixels from it.
2. One PNG per part, with real transparency. No baked checkerboard, no glow fringe, no feathered edges (a 1 px anti-alias is allowed).
3. Left and right stay separate files. Side convention: `_L`/`_R` = EMBER'S own left/right (character's). Ember's right is on the viewer's LEFT (x<485). Older assets (layers_v12, rigmap_v2, rig_v1) used VIEWER sides, so their `_L` is this database's `_R`.
4. Pivot art stays on the child: elbow cloth on the forearm parts (arm_lower_*, jacket_sleeve_lower_*), shoulder cap on the upper-arm parts (arm_upper_*, jacket_sleeve_*), knee cloth on the shin.
5. Rigid limbs rotate. Mesh only where the drawing must bend: waist, sleeve fold, hair tips, coat hem, mouth, eyes (plus the neck rows and hood/collar strip already listed in parts.csv).
6. Do not auto-mesh long thin parts (straps, strands, liner, collar rim, strap ends). Use a manual strip with a spine row.
7. Do not key face parameters (MouthOpen, EyeBlink, EyeGaze, brow/face keys) on body nodes. Face params live only in the Head subtree.
8. head_approved is LOCKED: `/workspace/ember-puppet-art/body/layers_v7/head_approved.png (2048x3072; head_approved LOCKED)` (SHA-256 4c66a971a951bf69f3795d544e20ffe11be7d3af763f8e2a4edb98373eab77d5; identical copies in layers_v4, layers_v6, layers_v7b and rig_v1/head/head_approved_copy.png). The copy at body/layers_v5/head_approved.png has a DIFFERENT hash (03d944fc...), so never use it. Face parts are cut only from head_approved and never redrawn, repainted, rescaled or altered. Its below-chin pixels (collar emblem, hood, zipper, hands from a half-body plate) are not body sources. The face rig already lives in Ember's live file.
9. still_orange.png is REJECTED. Never use it.
10. No PNG export, cutting or redraw until this database is approved. Do not touch ember.inx, the Raspberry Pi or Nick's PC from database work.
11. The harness (belt, chest straps, thigh straps, pouches, D-rings, tucks) stays independent. The jacket moves UNDER it, and harness parts are never bound into jacket deformation.
12. Hair is never parented to or bound by an arm. Hair under a raised arm is real strands that taper into the armpit shadow.
13. One zipper per side. Opening the jacket shows still_shirt underneath, never a cloned zipper or liner.
14. Body physics anchors are keyed to the body parameters, so physics follows the body (to verify against the official docs).
