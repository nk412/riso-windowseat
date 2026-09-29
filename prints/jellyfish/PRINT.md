# Chrysaora fuscescens: an engraved natural-history plate

**Request:** "A new riso still of a jellyfish. Highly detailed. No text. Style it like old
botanical illustrations."

**Principle:** a 19th-century hand-coloured specimen plate. There is one large figure and one
small secondary view on aged paper inside a pressed plate mark. Form is engraved line in indigo;
colour is a wash laid over it, and the slight misregistration that comes with that is expected.
There is **no lettering**: no figure numbers and no captions.

## Subject and references

The subject is the Pacific sea nettle. **No photo or plate was inspected.** The proxy blocks
Wikimedia, so the anatomy comes from standard descriptions of *Chrysaora*:

- 16 dark radial stripes on an amber bell;
- 32 marginal lappets. Each octant has 4 lappets, with 3 tentacles in the notches between them
  and 1 rhopalium (a small marginal sense organ) at the octant boundary, giving 24 tentacles and
  8 rhopalia;
- nematocyst warts on the exumbrella (the bell's outer surface);
- 4 long, spiralled, frilled oral arms;
- 4 gonads, visible through the bell.

The style follows Haeckel-era plates from memory, not from an inspected source.

## Construction

### Bell

- **Surface.** The bell is a flattened ellipsoid, R 250 × H 185. Meridian angle runs to 96° at
  the margin and then continues for another 13° into the lappets. The lappet reach is shaped by
  `|sin 16φ|^0.55`, which puts a notch at every m·2π/32.
- **Buffers.** Each figure is rotated, then splatted densely into per-pixel buffers
  (`BUF`): φ, t, normal, Lambert light and depth. There is a front buffer and a back buffer.
  Everything on the bell is then a pixel function of those buffers (`BELL`).
- **Meridian engraving.** 192 meridians, with widths set by shade. The line family halves as the
  meridians converge on the apex, so it doesn't clog.
- **Other line work.** Contour hatching appears in the shade only. Stripe edges, lappet notch
  creases, the ring where the lappets begin, and an outline complete it.
- **Stripes.** They taper from the apex to the margin, with slightly wavering edges.
- **Warts.** Staggered rings in (φ, t), sized in surface pixels.
- **Translucency.** The far wall's stripes and lappet rim are printed faintly from the back
  buffer. Everything behind the bell (arms, gonads, far tentacles) is drawn to a layer and
  merged at 0.32 inside the bell.

### Parts below and behind

- **Oral arms.** Each is a twisted ribbon. Width goes as |cos twist|, so the arm narrows where it
  turns edge-on, and the underside is shaded where cos < 0. The margins are frilled, with curved
  pleat folds at each crest. Arms are drawn far to near, each clearing its own value first.
- **Tentacles.** They start at the notches and leave along the bell surface. Near and far
  tentacles are split by depth. They then turn into the trailing direction, with waves of
  varied frequency.
- **Fig. 2.** The same bell, seen from above (τ = 90°) at 0.34 scale.

### Paper

The stock is aged (`#EFE4CB`), with toning toward the edges, 70 foxing spots, and an embossed
plate mark: a smoother, lighter field inside, a shadowed upper-left edge and a lit lower-right
edge.

## Inks

The inks are yellow, pink, orange and indigo.

- **Bell:** amber from yellow plus a little pink. Stripes are rust: orange with pink, and indigo
  in the shade. Highlights are cleared toward paper.
- **Arms:** pale pink with pinker frilled margins. The undersides are mauve, and the central
  canal is rust.
- **Tentacles:** a solid orange line broken up by pink.
- **Line:** all line work is indigo, which is the only dark.
- **Size:** native 2160², pitch 6.8 device px.

## Inspected

- The 1000 px view.
- 1:1 crops of the bell's front margin and lappets, the arms with their frills and pleats, and
  Fig. 2.
- `verify.mjs` passes in Chromium, and `still.mjs` repeats byte-identically.
- **Firefox is not verified.** It could not be installed in this container.

## Remaining weaknesses

- The anatomy is descriptive, not measured from a specimen photo.
- The arms still read partly as twisted strips. Real *Chrysaora* arms are fuller curtains with
  deeper, overlapping ruffles.
- Fig. 2 hides the lappets, because they curl under the margin when seen from above. The top
  view would read better with a slight tilt, or with lappets drawn flat.
- The far rim seen through the dome sits at mid-bell. It is correct for this tilt, but it can
  read as a band.
- Tentacles are simple waves. There are no coils, and no nematocyst banding.
