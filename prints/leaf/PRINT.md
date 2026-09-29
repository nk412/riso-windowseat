# Castanea sativa — one leaf as a vintage poster

**Request:** "a riso image of a highly detailed leaf, like a vintage poster."

**Principle:** a botanical specimen drawn at engraving detail, set inside a travel-poster frame: a
flat, graphic ground (a sky ramp, a striped setting sun, mountains, a grove) with a lettered band.
The leaf is the only area of high detail. Everything else is a flat field or a single ramp.

## Subject and references

Sweet chestnut (*Castanea sativa*). I chose it because its venation is the most poster-legible
of the common leaves: straight, parallel secondaries each run into a bristle-tipped tooth, with
ladder-like tertiaries between them.

**No photo was inspected.** The container's proxy refused Wikimedia Commons, so proportions come
from standard botanical descriptions, not measurement:

- oblong-lanceolate blade, about 3.3 : 1;
- widest a little below the middle;
- rounded-cuneate base and acuminate tip;
- about 17 pairs of craspedodromous secondaries at about 40–60°, flatter toward the base;
- coarse, forward-pointing, mucronate teeth;
- percurrent tertiaries and a short petiole.

If a reference becomes available, measure the tooth shape and the secondary angles against it
first.

## Construction (all in `LEAF()`)

| What | How |
|---|---|
| Midrib | Bows 24 px to the lower right. Every point on the blade is `P(s, v)` in midrib coordinates. |
| Envelope | `f(s)` gives the outline; the two halves are slightly asymmetric (165 / 155 px). |
| Teeth | One per secondary. The tip is a doubled Catmull-Rom point, so it forms a cusp. The sinus sits a third of the way toward the next tooth, and the basal flank is long and convex. A nib bristle carries each tooth past the blade. |
| Secondaries | Run from the midrib to the tooth. `s = s0 + Δs·q^1.3`, so each vein leaves the midrib steeply and bends apically near the margin. |
| Basal veins | Two looping basal veins per side. |
| Tertiaries | A ray from every ~7.4 px along a secondary, square to it and turned toward the apex, stops at the first hit on the next secondary, the midrib or the margin. The same rule fills the teeth and the apex. About 12% end free mid-panel. |
| Areoles | Veinlets bridge neighbouring tertiaries; about 22% end free. |
| Light | Upper left. Each panel between secondaries is a bulge: green is removed on the lit flank, indigo is added on the shadow flank, and there is an indigo groove at each vein. The right half is folded slightly away from the light, and the midrib groove casts a short shadow. |
| Autumn | Orange scorch with green removed at the tip. About 40% of tooth tips are browned. Six rust spots, each with a yellow halo where green is carved. An insect hole is cut with reversed winding, so the sun shows through it; it has a brown rim. |

## Plates

The inks are yellow, orange, green, blue and indigo.

- **Veins** are carved from green and indigo, so they print as the solid yellow under the blade.
  Where they cross the orange scorch they turn orange.
- **Blade:** the leaf is yellow at full coverage with green over it, so no ink is foreign to the
  subject. The only dark is an indigo overprint.
- **Poster shadow:** the leaf's shadow is indigo at 0.42, offset (15, 19) and clipped to the sky.
- **Sun:** solid yellow with an orange ramp. Its stripes and halo are carved.
- **Ground:** the sky ramp is blue, with indigo deepening at the top. The mountains are blue and
  green. The grove treeline is blue, indigo and green.
- **Band and lettering:** the band is solid indigo. The title *CASTANEA SATIVA* is carved to
  paper. *SWEET CHESTNUT* and its rules are carved and printed in orange. The lettering is a
  monoline condensed sans drawn as strokes (`GLYPH`), not a font.

## Native size and engine changes

- Size is 2160² (`OUT = 2160`, `K = 2`). Pitch is `3.4 * K` = 6.8 device px, and registration is
  `REG × K × 0.6`, following Cabinet.
- In this copy of the engine, screen dots are centred on pixels (`+0.5`), mid-tones get a fixed
  ±4.5% dither, and coverage ≥ 1 prints solid, so the 1 px tertiaries don't break into dots.
- `?only=<ink>` bakes a single plate.

## Inspected

- The 1000 px view.
- 1:1 crops of: the mid-blade venation and spots, the lower margin with the hole and the shadow
  over the sun stripes, the upper-right margin with its teeth and bristles, and the tip scorch.
- `verify.mjs` passes in Chromium. Firefox could not be installed in this container (the browser
  download was blocked), so the Firefox run is **not done**.
- `still.mjs --engine chromium` repeats byte-identically.

## Remaining weaknesses

- The geometry is not measured from a specimen photo; tooth shape and vein angles are
  descriptive.
- The insect hole reads as a dark spot at viewing size. It only shows as a hole at 1:1.
- Where the poster shadow crosses the sun, indigo over orange goes olive-brown. That is plausible
  as shadow, but muddier than the rest.
- The leaf tip touches the frame rule rather than clearly breaking through it.
- The bristles are hair-thin and only read at 1:1.
- The corrugation is gentle; the blade reads flatter than a real, plicate chestnut leaf.
