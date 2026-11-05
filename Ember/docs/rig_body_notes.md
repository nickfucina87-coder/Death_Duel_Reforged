# Body rig notes (not the live puppet)

Nothing here is installed. `ember.inx` is not edited. No file was copied to a PC or a Pi.

Chest size is the golden rest. Do not redraw it larger. A slight size change is an Inochi warp on the chest MeshGroup later, because that warp also drives the jiggle.

## Show or hide, do not twist one mesh

A different arm angle is a separate part. It is shown or hidden. It is not the rest mesh rotated into that pose. Rotating one mesh shrinks the limb and chops the joint.

Upper arm and forearm each aim on their own. The forearm is already painted up under the upper sleeve, so the elbow has cloth to bend. Counts in the current files: left elbow overlap 59273 pixels, right 58997. Jacket cloth under the sleeves: left 365022, right 364095.

T-stance and Da Vinci stance are not drawn as their own parts yet. The stance sheet shows the current rest arms and says so. It does not twist them.

Easing between poses is a runtime curve. It is not extra paintings and it is not a mesh spin.

## Deform regions, kept separate

- Chest: `layers_fulljacket/skin_suit_chest.png` (the v7 chest, not scaled)
- Stomach: `layers_fulljacket/skin_suit_stomach.png`
- Hips: `layers_fulljacket/skin_suit_hips.png`
- Outer jacket: `tech_jacket_L.png`, `tech_jacket_R.png`, and the four `tech_sleeve_*` parts
- Orange zipper jacket and the belt and straps are extracts of painted pixels only

The neck of the gray suit is the collar at the top of the chest, under the chin of `head_approved.png`. That head file is not edited. Bare neck skin is not a separate drawing.
