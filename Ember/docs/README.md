# ember_db - Ember Inochi2D reference database

The source of truth for later cutting, redrawing, meshing and parameter work. Nothing is rigged, exported or cut, and no art was edited.

## Files
- `parts.csv`: one row per future PNG part (88 parts: 40 cut, 41 extend, 7 redraw). Column `keep_first_pass` (yes/later, placed after `mesh`): 52 yes. yes ONLY for parts that move on their own (own node/param/physics) or that uncover a hole when a first-pass move happens; each row's notes end with the reason.
- `tree.txt`: the node skeleton, with the part ids that hang on each node and the SimplePhysics candidates.
- `params.csv`: the parameters this body needs, with the allowed and forbidden deformations for each.
- `overlap.md`: the hidden-surface plan for every extend/redraw part, the measured armpit numbers per side, the HEAD TURNS BLOCKED statement, and a ranked list of hole risks.
- `validation.txt`: output of the last validation run.
- `rules.md`: hard rules for later sessions.

## Sources
| Role | Path | Size |
|---|---|---|
| Jacket-on T-stance, MASTER (coat authority) | /workspace/ember-puppet-art/body/qa/still_closed.png (byte-identical to Nick's attachment 2d348a72...png) | 971x1620 |
| Jacket-off T-stance, MASTER (body/shirt authority) | /workspace/ember-puppet-art/body/qa/still_shirt.png (byte-identical to attachment 99c289b8...png) | 971x1620 |
| Jacket-on arms-down, REFERENCE ONLY (sleeve folds and hands; FULL body) | /home/box/agent-data/agents/c46d3140-db71-4275-8518-90b54565a67b/attachments/ff11fa07de1959af1875b3e49f89ee5206038f2084df35132cb5db49ce9b0381.png | 971x1620 |
| Locked head | /workspace/ember-puppet-art/body/layers_v7/head_approved.png (SHA-256 4c66a971...) | 2048x3072 |
| Rejected | still_orange.png | never use |

Not used: `body/qa/rest_target_v4.png` (1840x2880) is a half-body plate, and a full-body arms-down original exists, so it isn't needed. `body/layers_v12/qa/pose_arms_down_grey.png` is a rigid-rotation pose test built from the T-stance layers, not original art. Evidence only (consulted, nothing copied): `body/layers_v12/layer_manifest.json`, `body/rigmap_v2/layer_plan.md`, `body/rig_v2/STATUS.md`, `/workspace/inochi-study/rigging-knowledge.md`.

## Revision 2 (Nick's review, 2026-10-08)
- Added the `keep_first_pass` column. Revision 3 (first-pass export): face_base, bangs, hair_side_L/R, ear_L/R and neck were set to yes, so there were 48 yes rows. Under-jacket pass (same day): hip, jacket_belt, thigh_R and thigh_L were set to yes for the open-jacket stack, so there are now 52 yes rows (no new rows were added). hood_wrap and hair_back stay later, and head turns stay BLOCKED. The PNGs are in `png_first_pass/` (see `png_first_pass/manifest.json`). First-pass moves are BodyAngleX/Y, ArmL/R, the JacketOpen hinge range 0-0.5 and body physics. Head-subtree parts are `later` because head turns are blocked and the face rig already exists.
- `jacket_body` is now `extend`: cut from the jacket-on T-stance plus a 20 px rim. The unseen side/back is the new `jacket_back_unseen` row (redraw, later).
- Added `fingertips_R` and `fingertips_L` (redraw, parent Hand_R/Hand_L), because the T-stance canvas crops the fingers at x=0/x=970. The arms-down attachment is a shape reference only.
- `hood` is split into `hood_visible` (cut) and `hood_wrap` (redraw; DO NOT cut/draw until a back or three-quarter view exists).
- **HeadAngleX, HeadAngleY and HeadTilt stay BLOCKED until hood_wrap and hair_back are drawn.** This is stated in overlap.md, params.csv and tree.txt.
- The armpit ranges are replaced with measured px per side (overlap.md, "Armpit numbers").

## Decisions from looking at the art
- **Side convention:** `_L`/`_R` = Ember's own sides. Prior assets used viewer sides, so v12 `_L` = db `_R`.
- **Fingers:** one hand part per hand (palm plus the four fingers, which are drawn fused, about 25x8 px each, with no gaps), plus a separate thumb per hand (drawn with a clear gap), plus the redrawn `fingertips_*` for the canvas-cropped ends. The same decision applies to both hands.
- **Buckle:** a flat side-release clip locked on the belt. It can't shift, so it stays inside `jacket_belt` with no buckle row.
- **Bust:** BustYaw/BustPitch are NOT included. The chest is painted as part of the continuous turtleneck torso, with seam lines running across it and no separate drawn mass or occluding edge. Upper-body turn is handled by BodyAngleX/Y on the Chest node. A bust part would be an invented redraw.
- **Loose strands:** 5 (strand_center, strand_crown_R/L, strand_wisp_R/L), all inside head_approved and cut only.
- **Earring:** Ember's left ear only.
- **hair_feather_tips** is split into `hair_feather_tips_R` and `hair_feather_tips_L` (left/right rule).
- **Pants** are split as `hip` plus `thigh_*` plus `shin_*`. There is no single pants PNG.
- **Swinging pieces:** jacket_hem_R/L, jacket_liner_R/L, zipper_pull_L, hood, d_ring_R/L, strap_end_R/L, pouch_tab_R (limited-swing retainer), thigh straps (limited), earring_L, and the hair groups.

## Validation (run when written)
See `validation.txt`.

## First-pass PNG export (revision 3)
- `png_first_pass/` holds 52 PNGs named `<id>.png`, plus 3 rig-pass fixes (`thigh_R_v2.png`, `torso_jacket_off_v2.png`, `jacket_body_v2.png`). The manifest `file` field names the copy the rig uses. The originals are unchanged.
  - The first 48 are the accepted closed-jacket set.
  - Four were added in the under-jacket pass: hip.png, jacket_belt.png, thigh_R.png and thigh_L.png. All four are from still_shirt.png.
- All PNGs use Ember's own L/R, with v12 viewer-side names flipped. All are 1019x1668 RGBA with binary alpha, registered to the masters at offset (24,24).
- `png_first_pass/manifest.json` records id, file, canvas, offset, bbox, pivot estimate, z_order, source, cut_or_redraw, merged later parts and notes. The under-jacket method is under `notes.under_jacket_pass`.
- Z order of the under-jacket parts: thigh 11 < hip 11.5 < jacket_belt 12. They sit above torso_jacket_off (10) and below harness_tuck, the D-rings and every coat part.
- Legs pass (2026-10-09): shin_R/L and boot_R/L are now `yes`, and the new ankle_R/L rows were added, so parts.csv has 90 rows. All six PNGs are cut from still_closed.png with binary alpha and 16 px of hidden surface each, using export_legs.py. They are rigged in rig_first_pass/ember_body_first_pass.inx under Thigh > Knee > Shin > Ankle > Foot, with params LegL and LegR. See overlap.md, 'Lower legs'.
- `png_first_pass/qa/` holds the internal QA:
  - rest recomposites and compares
  - magenta pose renders
  - contact_sheet.png
  - open_jacket_preview.png and open_jacket_preview_magenta.png
  - open_jacket_holes.json and qa_report.json
- Builders in `_ember_db_build/`: export_first_pass.py (the 48; do not rerun, the 48 are frozen), export_under_jacket.py, qa_first_pass.py and open_jacket_preview.py.
