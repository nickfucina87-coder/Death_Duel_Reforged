# Ember - overlap / hidden-surface plan

Every part marked `extend` or `redraw` in parts.csv, with what covers it, what the other sources contain, and what must be invented. Database only - nothing has been painted or exported.

Sources:
- Jacket-on T-stance (MASTER, coat authority): `/workspace/ember-puppet-art/body/qa/still_closed.png (971x1620)`
- Jacket-off T-stance (MASTER, body/shirt/torso-under-coat authority): `/workspace/ember-puppet-art/body/qa/still_shirt.png (971x1620)`
- Jacket-on arms-down (REFERENCE ONLY, resting sleeve folds and hands; full body, separate render so pixels are not aligned to the masters): `/home/box/agent-data/agents/c46d3140-db71-4275-8518-90b54565a67b/attachments/ff11fa07de1959af1875b3e49f89ee5206038f2084df35132cb5db49ce9b0381.png (971x1620; arms-down REF ONLY)`
- Locked head: `/workspace/ember-puppet-art/body/layers_v7/head_approved.png (2048x3072; head_approved LOCKED)` (cut only, never altered).
- Evidence for px extents: `/workspace/ember-puppet-art/body/layers_v12/layer_manifest.json` (prior attempt; it used VIEWER sides, mapped here to Ember's sides).
- Rejected, never used: `still_orange.png`.

Rule of thumb: `extend` = paint 10-20 px of hidden surface past every overlap edge (more where a listed motion range needs it). `redraw` = the piece does not exist in any source.

Side convention: _L/_R = Ember's own left/right; Ember's right is the viewer's left (x<485).

> **HEAD TURNS BLOCKED:** HeadAngleX, HeadAngleY and HeadTilt head turns stay BLOCKED until hood_wrap and hair_back are drawn. hood_wrap must not be cut or drawn until a back or three-quarter view exists.

## Armpit numbers (ArmL / ArmR range), per side

Range: Arm -1 = raised 30 deg, 0 = T-stance, +1 = arms down 75 deg. Pivots: Ember's right shoulder (348,405), Ember's left shoulder (622,405) (v12 manifest, viewer sides mapped to Ember's).
How measured: the v12 arm masks (shirt chain = upper_arm+elbow_overlap+forearm+wrist_cuff+palm; jacket chain = sleeve_upper+sleeve_elbow+sleeve_fore+cuff + shirt chain) were rigidly rotated about the shoulder pivot to +75 deg and -30 deg. Reveal = pixels the arm covered at rest, no longer covered after rotation, inside the row-wise body hull on that side of centre x=485 (shirt hull from v12 torso+neck alpha; jacket hull from v12 side+front+back_mass alpha), minus pixels still covered by chest straps/rear hair (net). Caps: a half-disc on the body side of the pivot with radius = half the arm root thickness measured 15 px out from the pivot, minus the existing arm pixels. Rigid rotation over-states the reveal compared with mesh deform, so these are upper bounds. Paint = measured box + 10 px margin. Script: /workspace/ember-puppet-art/_ember_db_build/measure_armpit.py; raw output armpit_measure.json.

| Side | Piece | Part id | Must match (color + line) | Arms down +75 | Raised -30 | Paint (union) | Max depth |
|---|---|---|---|---|---|---|---|
| Ember's right (viewer-left) | (a) shirt/turtleneck side under the arm | torso_jacket_off | still_shirt.png | 48x85 (x301-348 y365-449, 1490 px) | 44x85 (x305-348 y365-449, 659 px) | **48x85 (x301-348 y365-449, 1960 px)** | 27 px |
| Ember's right (viewer-left) | (b) jacket sleeve underside/shoulder cap | jacket_sleeve_R | still_closed.png; fold shape from arms-down ff11fa07...png | - | - | **42x84 (x348-389 y370-453, 2804 px)** (half-disc r=42.0 px, root 84 px thick) | 42 px |
| Ember's right (viewer-left) | (b') shirt upper-arm cap | arm_upper_R | still_shirt.png | - | - | **32x63 (x348-379 y374-436, 1594 px)** (half-disc r=31.5 px, root 63 px thick) | 31 px |
| Ember's right (viewer-left) | (c) jacket side panel under the arm | jacket_side_R | still_closed.png | 53x106 (x297-349 y358-463, 1139 px) | 42x106 (x308-349 y358-463, 194 px) | **53x106 (x297-349 y358-463, 1266 px)**; 2042 px if hair/strap swing away | 22 px |
| Ember's left (viewer-right) | (a) shirt/turtleneck side under the arm | torso_jacket_off | still_shirt.png | 46x74 (x622-667 y370-443, 1021 px) | 33x91 (x622-654 y370-460, 546 px) | **46x91 (x622-667 y370-460, 1536 px)** | 27 px |
| Ember's left (viewer-right) | (b) jacket sleeve underside/shoulder cap | jacket_sleeve_L | still_closed.png; fold shape from arms-down ff11fa07...png | - | - | **42x84 (x581-622 y371-454, 2805 px)** (half-disc r=42.0 px, root 84 px thick) | 42 px |
| Ember's left (viewer-right) | (b') shirt upper-arm cap | arm_upper_L | still_shirt.png | - | - | **36x71 (x587-622 y374-444, 2020 px)** (half-disc r=35.5 px, root 71 px thick) | 35 px |
| Ember's left (viewer-right) | (c) jacket side panel under the arm | jacket_side_L | still_closed.png | 52x56 (x622-673 y366-421, 931 px) | 30x108 (x622-651 y366-473, 408 px) | **52x108 (x622-673 y366-473, 1329 px)**; 1745 px if hair/strap swing away | 29 px |

## hair_back (redraw)
- Covered: Behind face_base/neck/hood in head_approved (locked) and still_closed (jacket-on T-stance); only a 5-25 px rim of back hair shows around the head silhouette.
- Other sources: still_shirt (jacket-off T-stance): same rim only. arms-down ref ff11fa07 (jacket-on, full body): same rim only. No source shows the back of the head.
- Invent: The whole back-hair mass from crown to nape behind the face and neck, painted in the existing silver->orange gradient and strand direction.
- Extent: Fill the full head silhouette plus 15-20 px beyond the visible rim on all sides (needed for HeadAngleX +/-1 and HeadTilt).

## hair_back_long (extend)
- Covered: In still_closed (jacket-on T-stance) the rear hair runs behind the jacket sleeves/sides and hood; behind each arm about 42 px of hair is missing (v12 max 42 px).
- Other sources: still_shirt (jacket-off T-stance) has the jacket-off layout (falls in front of the arms) - different shape, use only for strand texture. arms-down ref ff11fa07 (jacket-on, full body): arms cover the same zone.
- Invent: Real strands continuous behind each sleeve root, tapering up into the armpit shadow (no hard horizontal edge, no streaks, no grey-green patch).
- Extent: 10-20 px past every edge covered by sleeves/sides; up to ~42 px behind the sleeve roots so ArmL/ArmR -1 (raised) shows strands.

## hair_feather_tips_R (extend)
- Covered: Tip roots hidden under hair_side_R/hair_back_long in still_closed (jacket-on T-stance); tips lie against the sleeve top/side panel (x270-335 y330-520).
- Other sources: still_shirt (jacket-off T-stance): tips present but in the jacket-off layout. arms-down ref ff11fa07 (jacket-on, full body): tips present, arms down - compare drape only.
- Invent: Root overlap where the tip clump joins the main lock so physics lag never opens a gap.
- Extent: 10-20 px of root under the lock.

## hair_feather_tips_L (extend)
- Covered: Tip roots hidden under hair_side_L/hair_back_long in still_closed (jacket-on T-stance); tips lie against the sleeve top/side panel (x635-690 y330-520).
- Other sources: still_shirt (jacket-off T-stance): tips present but in the jacket-off layout. arms-down ref ff11fa07 (jacket-on, full body): tips present, arms down - compare drape only.
- Invent: Root overlap where the tip clump joins the main lock so physics lag never opens a gap.
- Extent: 10-20 px of root under the lock.

## neck (extend)
- Covered: Upper neck under the chin/jaw of face_base (head_approved (locked)); sides under jacket_collar/hood in still_closed (jacket-on T-stance).
- Other sources: still_shirt (jacket-off T-stance): turtleneck and collar emblem fully visible below the chin; jaw shadow region missing in all sources.
- Invent: Turtleneck/neck surface 15-20 px up under the jaw; ONE emblem only (no duplicate triangle).
- Extent: 15-20 px up under jaw (v12 max 34 px), 10-15 px under collar/hood at sides.

## torso_jacket_off (extend)
- Covered: In still_closed (jacket-on T-stance) the shirt torso is under the jacket fronts/sides; in still_shirt (jacket-off T-stance) it is still under hair tips, chest harness straps, shoulder caps and belt.
- Other sources: still_shirt (jacket-off T-stance) supplies almost the whole torso. still_closed (jacket-on T-stance) only shows the centre strip between the jacket fronts.
- Invent: Shirt cloth and the cyan seam lines continued under the straps (9-12 px), hair tips, shoulder caps and belt top.
- Extent: 10-20 px under each overlap; up to ~92 px under shoulder-cap/hair (v12 max).

## hip (extend)
- Covered: Under jacket_belt, torso hem and jacket hems in still_closed (jacket-on T-stance); under the belt in still_shirt (jacket-off T-stance).
- Other sources: still_shirt (jacket-off T-stance) shows the pants seat around the belt; still_closed (jacket-on T-stance) hides the sides under the jacket hems.
- Invent: Pants waistband and pelvis cloth under the belt and torso hem; crotch area behind thigh tops.
- Extent: 10-20 px under the belt/torso hem; v12 needed up to 88 px under belt+hem.

## arm_upper_R (extend)
- Covered: Shoulder cap and armpit sit under the torso edge/hair in still_shirt (jacket-off T-stance); in still_closed (jacket-on T-stance) the whole shirt arm is under jacket_sleeve_R.
- Other sources: still_shirt (jacket-off T-stance) has the visible shirt upper arm only. arms-down ref ff11fa07 (jacket-on, full body): jacket on, so no shirt arm. No source shows the armpit.
- Invent: Rounded shoulder cap and armpit cloth continuing into the torso edge (cloned along the arm axis from real sleeve pixels).
- Extent: Shirt upper-arm cap (on this part, match still_shirt.png): 32x63 px (x348-379 y374-436, 1594 px), half-disc r=31.5 px. Torso side under this arm: see the Armpit numbers section.

## arm_lower_R (extend)
- Covered: Elbow end hides under arm_upper_R; wrist end under wrist_cuff_R (still_shirt (jacket-off T-stance)).
- Other sources: still_shirt (jacket-off T-stance) only (forearm). still_closed (jacket-on T-stance): covered by jacket sleeve.
- Invent: Rounded elbow overlap cloth on the forearm (pivot art on child) and sleeve under the tech cuff.
- Extent: Elbow cap ~20 px into the upper arm; ~40 px under the cuff (v12 max ~43 px).

## hand_R (extend)
- Covered: Wrist root under wrist_cuff_R; thumb root under the thumb; fingertips clipped by the canvas edge in both T-stance masters.
- Other sources: still_shirt (jacket-off T-stance)/still_closed (jacket-on T-stance): same pixels (identical hands). arms-down ref ff11fa07 (jacket-on, full body): full hand with uncut fingertips, arms down - shape reference only.
- Invent: Wrist skin under the cuff; palm under the thumb root. Cropped finger ends are the separate fingertips part.
- Extent: 10-20 px under the cuff; ~6 px under the thumb root.

## thumb_R (extend)
- Covered: Thumb root sits ~6 px under hand_R (still_shirt (jacket-off T-stance)/still_closed (jacket-on T-stance)).
- Other sources: Same in both masters; arms-down ref ff11fa07 (jacket-on, full body) shows a resting thumb for shape.
- Invent: Thumb root skin under the palm edge.
- Extent: ~6-10 px.

## fingertips_R (redraw)
- Covered: Not covered - cropped: the fused fingers run off the T-stance canvas at x=0 in both still_closed (jacket-on T-stance) and still_shirt (jacket-off T-stance).
- Other sources: still_shirt (jacket-off T-stance)/still_closed (jacket-on T-stance): identical cropped hands. arms-down ref ff11fa07 (jacket-on, full body): full uncropped fingertips with arms down - SHAPE REFERENCE ONLY (separate render, not pixel-aligned).
- Invent: Rounded finger ends and the rest of the orange nails for the fused finger block, matching still_shirt.png skin and line; ~4 px overlap onto hand_R. Pad the canvas >=16 px on that side first.
- Extent: Crop at x=0: the finger block is 3 px tall at the edge column (y450-452) and tapers from 11 px at x=7, so ~3 px of finger tip plus the nail end is missing; invent ~3-6 px long x 3-11 px tall (paint box ~8x12 px incl. 4 px overlap).

## arm_upper_L (extend)
- Covered: Shoulder cap and armpit sit under the torso edge/hair in still_shirt (jacket-off T-stance); in still_closed (jacket-on T-stance) the whole shirt arm is under jacket_sleeve_L.
- Other sources: still_shirt (jacket-off T-stance) has the visible shirt upper arm only. arms-down ref ff11fa07 (jacket-on, full body): jacket on, so no shirt arm. No source shows the armpit.
- Invent: Rounded shoulder cap and armpit cloth continuing into the torso edge (cloned along the arm axis from real sleeve pixels).
- Extent: Shirt upper-arm cap (on this part, match still_shirt.png): 36x71 px (x587-622 y374-444, 2020 px), half-disc r=35.5 px. Torso side under this arm: see the Armpit numbers section.

## arm_lower_L (extend)
- Covered: Elbow end hides under arm_upper_L; wrist end under wrist_cuff_L (still_shirt (jacket-off T-stance)).
- Other sources: still_shirt (jacket-off T-stance) only (forearm). still_closed (jacket-on T-stance): covered by jacket sleeve.
- Invent: Rounded elbow overlap cloth on the forearm (pivot art on child) and sleeve under the tech cuff.
- Extent: Elbow cap ~20 px into the upper arm; ~40 px under the cuff (v12 max ~43 px).

## hand_L (extend)
- Covered: Wrist root under wrist_cuff_L; thumb root under the thumb; fingertips clipped by the canvas edge in both T-stance masters.
- Other sources: still_shirt (jacket-off T-stance)/still_closed (jacket-on T-stance): same pixels (identical hands). arms-down ref ff11fa07 (jacket-on, full body): full hand with uncut fingertips, arms down - shape reference only.
- Invent: Wrist skin under the cuff; palm under the thumb root. Cropped finger ends are the separate fingertips part.
- Extent: 10-20 px under the cuff; ~6 px under the thumb root.

## thumb_L (extend)
- Covered: Thumb root sits ~6 px under hand_L (still_shirt (jacket-off T-stance)/still_closed (jacket-on T-stance)).
- Other sources: Same in both masters; arms-down ref ff11fa07 (jacket-on, full body) shows a resting thumb for shape.
- Invent: Thumb root skin under the palm edge.
- Extent: ~6-10 px.

## fingertips_L (redraw)
- Covered: Not covered - cropped: the fused fingers run off the T-stance canvas at x=970 in both still_closed (jacket-on T-stance) and still_shirt (jacket-off T-stance).
- Other sources: still_shirt (jacket-off T-stance)/still_closed (jacket-on T-stance): identical cropped hands. arms-down ref ff11fa07 (jacket-on, full body): full uncropped fingertips with arms down - SHAPE REFERENCE ONLY (separate render, not pixel-aligned).
- Invent: Rounded finger ends and the rest of the orange nails for the fused finger block, matching still_shirt.png skin and line; ~4 px overlap onto hand_L. Pad the canvas >=16 px on that side first.
- Extent: Crop at x=970: the finger block is 8 px tall at the edge column (y448-455), blunter than the right, so ~6-8 px is missing; invent ~6-8 px long x 8-11 px tall (paint box ~12x12 px incl. 4 px overlap).

## jacket_body (extend)
- Covered: cut from jacket-on T-stance + extend. In still_closed (jacket-on T-stance) only 261 px of the back shell show at rest (x319-486 y802-838, back hem below the front hems); the rest sits behind jacket_front/side/hem panels and the shirt body.
- Other sources: still_shirt (jacket-off T-stance): no jacket. arms-down ref ff11fa07 (jacket-on, full body): same front view, arms down; no extra back pixels.
- Invent: Only the extend rim: back-shell cloth continuing 20 px behind the outer edges of the front/side/hem panels, so JacketHinge (15-18 px opening), hem physics and BodyAngleX never show a gap. The unseen side/back is jacket_back_unseen.
- Extent: Visible 261 px; extend rim 14753 px within x285-672 y301-804 (20 px band behind panel outer edges, measured from the v12 owner map + back_mass alpha).

## jacket_back_unseen (redraw)
- Covered: Behind the shirt body (torso/hip) and more than 20 px behind the jacket panels in still_closed (jacket-on T-stance).
- Other sources: None: still_shirt (jacket-off T-stance) has no jacket, arms-down ref ff11fa07 (jacket-on, full body) is a front view. No source shows the jacket's side/back.
- Invent: The full jacket side/back shell: plain jacket cloth + liner tone matching still_closed.png color and line weight.
- Extent: 24488 px within x289-667 y301-822 (379x522): 12829 px behind the shirt body + 11659 px deeper than 20 px behind panels. Not exposed by any first-pass move; keep_first_pass later.

## jacket_collar (extend)
- Covered: Rim runs under hair_side_L/R and the chin in still_closed (jacket-on T-stance).
- Other sources: head_approved (locked) also bakes collar/hood pixels below the chin - NOT a source. still_shirt (jacket-off T-stance): no collar. arms-down ref ff11fa07 (jacket-on, full body): similar rim at rest.
- Invent: Smooth collar rim and orange liner under the hair, cut on a cloth edge (not the jagged hair outline).
- Extent: 10-20 px under hair and chin.

## hood_wrap (redraw)
- Covered: The hood's U behind head_approved, hair_back and hair_side_L/R in still_closed (jacket-on T-stance); only hood_visible (8268 px, x289-670 y207-374) shows at rest.
- Other sources: still_shirt (jacket-off T-stance): none. arms-down ref ff11fa07 (jacket-on, full body): a little more hood at the shoulders, still front view (fold reference only). head_approved (locked) has hood pixels around the neck - excluded, never a source.
- Invent: The whole hidden hood wrap (inside and back of the hood). DO NOT cut/draw until a back or three-quarter view exists.
- Extent: 30832 px within x290-665 y200-392 (376x193); v12 max depth 86 px. HEAD TURNS (HeadAngleX/HeadAngleY/HeadTilt) STAY BLOCKED until hood_wrap and hair_back are drawn.

## jacket_front_R (extend)
- Covered: Panel edges under hair tips, jacket_strap_R and the sleeve root in still_closed (jacket-on T-stance); shoulder top under the hinge overlap (380,345).
- Other sources: still_shirt (jacket-off T-stance): none (no jacket). arms-down ref ff11fa07 (jacket-on, full body): same panel, arms down; similar edges.
- Invent: Panel cloth under the strap (strap runs over it), under hair tips and 10-20 px past the shoulder hinge so opening never shows a seam.
- Extent: 10-20 px under straps/hair; ~32 px under sleeve root (v12 max 32 px).

## jacket_interior_R (redraw)
- Covered: Not visible in any source; revealed when jacket_front_R swings on JacketOpen.
- Other sources: still_closed (jacket-on T-stance): only the liner facing edge; still_shirt (jacket-off T-stance)/arms-down ref ff11fa07 (jacket-on, full body): none.
- Invent: The whole inside face of the front panel (lining tone, seam at the liner facing).
- Extent: Full panel footprint (~140x480 px).

## jacket_liner_R (extend)
- Covered: Inner edge under jacket_front_R in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): liner facing visible at rest similarly; still_shirt (jacket-off T-stance): none.
- Invent: Liner facing continuing under the panel edge.
- Extent: 10-20 px.

## jacket_side_R (extend)
- Covered: Upper part under jacket_sleeve_R root, hair tips and jacket_front_R in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): arms down, so the side panel there is covered by the arm - no help. still_shirt (jacket-off T-stance): none.
- Invent: Shoulder-cap underpaint and side cloth under the sleeve root and hair tips.
- Extent: Side panel under the arm (match still_closed.png): 53x106 px (x297-349 y358-463, 1266 px) net of hair/strap cover; 2042 px if hair/straps swing away; max depth 22 px. See the Armpit numbers section.

## jacket_sleeve_R (extend)
- Covered: Shoulder cap/armpit under the side panel and hair in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): resting fold shapes at the shoulder and upper arm (shape only; separate render, pixels not aligned). still_shirt (jacket-off T-stance): none.
- Invent: Shoulder cap and armpit cloth (pivot art on child) plus resting fold lines referenced from the arms-down image.
- Extent: Jacket sleeve cap/underside (on this part, match still_closed.png; fold shape from the arms-down attachment): 42x84 px (x348-389 y370-453, 2804 px), half-disc r=42.0 px. See the Armpit numbers section.

## jacket_sleeve_lower_R (extend)
- Covered: Elbow cloth under jacket_sleeve_R; wrist end under jacket_cuff_R (still_closed (jacket-on T-stance)).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): elbow folds at rest (shape only). still_shirt (jacket-off T-stance): none.
- Invent: Rounded elbow overlap cloth (no hinge corner, no slivers) and cloth under the cuff.
- Extent: ~20 px into the upper sleeve; v12 max 73 px incl. under-cuff.

## jacket_cuff_R (extend)
- Covered: Under wrist_cuff_R in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): cuff at rest (shape only). still_shirt (jacket-off T-stance): none.
- Invent: Cuff cloth under the tech band.
- Extent: 10-20 px; v12 max ~38 px.

## jacket_hem_R (extend)
- Covered: Underside behind jacket_front_R in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): hem at rest (similar). still_shirt (jacket-off T-stance): none.
- Invent: Hem underside and orange edge so physics fold never shows the gap.
- Extent: 10-15 px (v12 max 13 px).

## jacket_front_L (extend)
- Covered: Panel edges under hair tips, jacket_strap_L and the sleeve root in still_closed (jacket-on T-stance); shoulder top under the hinge overlap (590,345).
- Other sources: still_shirt (jacket-off T-stance): none (no jacket). arms-down ref ff11fa07 (jacket-on, full body): same panel, arms down; similar edges.
- Invent: Panel cloth under the strap (strap runs over it), under hair tips and 10-20 px past the shoulder hinge so opening never shows a seam.
- Extent: 10-20 px under straps/hair; ~32 px under sleeve root (v12 max 32 px).

## jacket_interior_L (redraw)
- Covered: Not visible in any source; revealed when jacket_front_L swings on JacketOpen.
- Other sources: still_closed (jacket-on T-stance): only the liner facing edge; still_shirt (jacket-off T-stance)/arms-down ref ff11fa07 (jacket-on, full body): none.
- Invent: The whole inside face of the front panel (lining tone, seam at the liner facing).
- Extent: Full panel footprint (~140x480 px).

## jacket_liner_L (extend)
- Covered: Inner edge under jacket_front_L in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): liner facing visible at rest similarly; still_shirt (jacket-off T-stance): none.
- Invent: Liner facing continuing under the panel edge.
- Extent: 10-20 px.

## jacket_side_L (extend)
- Covered: Upper part under jacket_sleeve_L root, hair tips and jacket_front_L in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): arms down, so the side panel there is covered by the arm - no help. still_shirt (jacket-off T-stance): none.
- Invent: Shoulder-cap underpaint and side cloth under the sleeve root and hair tips.
- Extent: Side panel under the arm (match still_closed.png): 52x108 px (x622-673 y366-473, 1329 px) net of hair/strap cover; 1745 px if hair/straps swing away; max depth 29 px. See the Armpit numbers section.

## jacket_sleeve_L (extend)
- Covered: Shoulder cap/armpit under the side panel and hair in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): resting fold shapes at the shoulder and upper arm (shape only; separate render, pixels not aligned). still_shirt (jacket-off T-stance): none.
- Invent: Shoulder cap and armpit cloth (pivot art on child) plus resting fold lines referenced from the arms-down image.
- Extent: Jacket sleeve cap/underside (on this part, match still_closed.png; fold shape from the arms-down attachment): 42x84 px (x581-622 y371-454, 2805 px), half-disc r=42.0 px. See the Armpit numbers section.

## jacket_sleeve_lower_L (extend)
- Covered: Elbow cloth under jacket_sleeve_L; wrist end under jacket_cuff_L (still_closed (jacket-on T-stance)).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): elbow folds at rest (shape only). still_shirt (jacket-off T-stance): none.
- Invent: Rounded elbow overlap cloth (no hinge corner, no slivers) and cloth under the cuff.
- Extent: ~20 px into the upper sleeve; v12 max 73 px incl. under-cuff.

## jacket_cuff_L (extend)
- Covered: Under wrist_cuff_L in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): cuff at rest (shape only). still_shirt (jacket-off T-stance): none.
- Invent: Cuff cloth under the tech band.
- Extent: 10-20 px; v12 max ~38 px.

## jacket_hem_L (extend)
- Covered: Underside behind jacket_front_L in still_closed (jacket-on T-stance).
- Other sources: arms-down ref ff11fa07 (jacket-on, full body): hem at rest (similar). still_shirt (jacket-off T-stance): none.
- Invent: Hem underside and orange edge so physics fold never shows the gap.
- Extent: 10-15 px (v12 max 13 px).

## harness_strap_shirt_R (extend)
- Covered: Short stretch under hair tips in still_shirt (jacket-off T-stance).
- Other sources: still_closed (jacket-on T-stance): strap follows a different path over the jacket - not usable.
- Invent: Webbing continued under the hair.
- Extent: 9-12 px (v12).

## harness_tuck_R (extend)
- Covered: Belt/strap stretch drawn under jacket_front_R/jacket_hem_R in still_closed (jacket-on T-stance).
- Other sources: still_shirt (jacket-off T-stance): fully visible - copy from it, aligned to the still_closed strap path.
- Invent: Only alignment joins at the hem edge.
- Extent: 10-20 px at each join.

## harness_strap_shirt_L (extend)
- Covered: Short stretch under hair tips in still_shirt (jacket-off T-stance).
- Other sources: still_closed (jacket-on T-stance): strap follows a different path over the jacket - not usable.
- Invent: Webbing continued under the hair.
- Extent: 9-12 px (v12).

## harness_tuck_L (extend)
- Covered: Belt/strap stretch drawn under jacket_front_L/jacket_hem_L in still_closed (jacket-on T-stance).
- Other sources: still_shirt (jacket-off T-stance): fully visible - copy from it, aligned to the still_closed strap path.
- Invent: Only alignment joins at the hem edge.
- Extent: 10-20 px at each join.

## thigh_strap_L_outer (extend)
- Covered: Top under pouch_L / inner strap (still_closed (jacket-on T-stance) and still_shirt (jacket-off T-stance)).
- Other sources: Both masters agree.
- Invent: Strap webbing under the pouch.
- Extent: ~11 px (v12).

## thigh_R (extend)
- Covered: Top under hip and jacket_hem_R in still_closed (jacket-on T-stance); under pouch/straps in both.
- Other sources: still_shirt (jacket-off T-stance) shows the thigh top without jacket hems.
- Invent: Thigh cloth under the hip and under pouch/straps.
- Extent: 10-20 px under each overlap; v12 max ~140 px (top under pelvis).

## shin_R (extend)
- Covered: Knee end under thigh_R in both masters.
- Other sources: Both masters agree.
- Invent: Knee overlap cloth (pivot art on child) and shin cloth up under the knee.
- Extent: ~20 px of knee cap; v12 max 74 px.

## boot_R (extend)
- Covered: Boot top under the pant cuff in both masters.
- Other sources: Both masters agree.
- Invent: Boot shaft under the cuff.
- Extent: 10-20 px; v12 max ~60 px.

## thigh_L (extend)
- Covered: Top under hip and jacket_hem_L in still_closed (jacket-on T-stance); under pouch/straps in both.
- Other sources: still_shirt (jacket-off T-stance) shows the thigh top without jacket hems.
- Invent: Thigh cloth under the hip and under pouch/straps.
- Extent: 10-20 px under each overlap; v12 max ~140 px (top under pelvis).

## shin_L (extend)
- Covered: Knee end under thigh_L in both masters.
- Other sources: Both masters agree.
- Invent: Knee overlap cloth (pivot art on child) and shin cloth up under the knee.
- Extent: ~20 px of knee cap; v12 max 74 px.

## boot_L (extend)
- Covered: Boot top under the pant cuff in both masters.
- Other sources: Both masters agree.
- Invent: Boot shaft under the cuff.
- Extent: 10-20 px; v12 max ~60 px.

## Ranked: overlaps most likely to leave a hole

1. **hood_wrap + hair_back + neck under the locked head (HeadAngleX/HeadAngleY/HeadTilt)** - head_approved cannot be edited, hood_wrap is 30832 px with no source view and the back of the head is drawn nowhere - the v1 ragged hood/neck defect. Head turns are BLOCKED until hood_wrap and hair_back exist.
2. **Armpit stack: torso_jacket_off + arm_upper + jacket_sleeve cap + jacket_side, both sides (ArmL/ArmR)** - no source shows the armpit; the measured reveal is ~46-53 x 85-108 px per side and four layers matched to two different masters must agree there.
3. **fingertips_R/L (ArmL/ArmR)** - the masters crop the fingertips at x=0/x=970; the tips are invented from a non-aligned reference and a flat cut shows the moment an arm rotates.
4. **jacket_body rim + jacket_interior_R/L (JacketOpen hinge)** - the 20 px rim (14753 px) and both interiors are invented and appear right next to real still_closed/still_shirt pixels.

## Lower legs (legs pass, 2026-10-09)
Source: still_closed.png only. Cuts (master y): thigh hem | shin | 1267 | ankle | 1307 | boot. Z: boot 10.55 < ankle 10.7 < shin 10.85 < thigh 11.
### shin_R / shin_L
- Hidden: top 16 px under the thigh_* hem (per column, from the thigh PNG bottom edge). Pixels are real still_closed pant pixels, because the still shows the pant there.
- Knee: shin rotates -20 deg (R) / +20 deg (L) at Knee (379,1110) / (585.5,1110). Shin rows above y1114 keep the thigh's angle through a manual knee-strip deform (6 px rows), blended out by y1150, so the hidden top never peeks out.
### ankle_R / ankle_L (new)
- This part is the pant cuff band, the orange tab and the dark ankle ring between the bunched hem and the boot tongue (y1267-1306).
- Hidden: top 16 px under the shin hem, cloned from still_closed cuff rows mirrored about y1267. Ankle counter-rotation (about 13 deg) at the ankle is at most about 10 px vertical at the cuff edge, which is inside the 16 px.
### boot_R / boot_L
- Hidden: top 16 px under ankle_*, cloned from still_closed boot-collar rows mirrored about y1307. The boot shares the Ankle transform with ankle_*, so this seam never opens.
### Thigh top
- thigh_* top rows (above y840) keep the rest angle under LegL/LegR, blending to the full thigh rotation by y930. This keeps the crotch and hip closed. Without it, a crotch sliver of 12-17 px opened at LegL=LegR=1.
### Hole QA (magenta, enclosed px vs v6)
- rest: 0 new. LegL=LegR=1: 0 new. BodyAngleX +1 / -1: 0 new vs v6.
- The 694 px enclosed at rest are pre-existing hair gaps and strap gaps, identical in v6. See rig_first_pass/qa/legs_holes.json.
