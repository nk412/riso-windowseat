# Nautilus pompilius: the whole shell as a still life

**Request:** "Make a riso still of a nautilus shell."

**Principle:** `prints/cabinet` already has a nautilus, shown in section. This print shows the
whole shell from outside instead. It stands on its venter on a dark ledge, lit from the upper
left, against a blue wall with a pool of light behind it. It is a still life, with a cast shadow
that runs across the ledge and climbs the wall. There is no text.

## References

**No photo was inspected.** The proxy blocks Wikimedia. The anatomy comes from standard
descriptions:

- whorl expansion of about 3.1 per turn;
- an involute coil, with the umbilicus closed by a callus;
- brown flame stripes that fork and lean back toward the venter, and fade out over the last part
  of the body whorl;
- a hyponomic sinus in the growth lines at the venter;
- a nacreous interior;
- a black film on the previous whorl where the aperture overlaps it.

## Construction

- **The tube.** The shell is one logarithmic spiral tube: `a(θ) = e^{kθ}`, with k = ln 3.1 / 2π.
  - The cross-section is an ellipse: centre 1.0·a, radial half-axis 0.62·a, lateral half-axis
    0.57·a.
  - Because of these proportions, each whorl envelops the one before it without any special
    casing.
  - The model runs 4.2 whorls.
  - The umbilical callus is a low dome.
- **Buffers.** The shell is splatted into per-pixel buffers: θ, v, normal and depth.
- **Inside or outside.** A normal that faces away from the viewer marks the inside of the shell,
  seen through the aperture, and that is where nacre prints.
- **View.** Roll −38°, yaw −20° (which opens the mouth toward the viewer), pitch 6°. The shell is
  auto-fitted to 700 px wide.

### Marks, as functions of the buffers

- **Growth lines.** Lines of constant `θ + 0.07 sin(1.2|v|) − 0.28 e^{−(|v|/0.55)²}`, which
  gives the sinuous flank and the ventral sinus. Their weight follows shade, they drop out in the
  gloss, and they thin where they crowd together.
- **Flames.** 21 per whorl.
  - They lean back toward the venter and are warped by fbm noise, with a zigzag near the
    umbilicus.
  - Each flame has its own weight, and heavy flames split in two toward the venter.
  - They fade out over the last ~70° before the aperture and toward the venter.
  - Colour is orange and pink with indigo, which prints rust-brown.
- **Gloss.** A Blinn highlight (exponent 70) clears every ink to paper.
- **Nacre.** Pink, blue and yellow bands whose phase depends on angle, darkening deeper into the
  tube.
- **Black film.** Indigo, orange and pink overprinted on the previous whorl inside the aperture.

### Shadow

- **On the ledge:** a light ray (KD 0.36, KX 0.8) maps each ledge pixel back onto the shell
  silhouette, with a penumbra that grows with height. A contact shadow sits under the point
  where the shell touches.
- **On the wall:** the same ray carried past the back edge of the ledge.

## Inks and size

- Inks: yellow, orange, pink, blue and indigo. The shell is near-paper cream. Its shade is warm
  orange with blue reflected light, and indigo appears only in the core shadow.
- The ground is blue with indigo. The lip of the ledge is a lighter blue line.
- Native size is 2160², pitch 6.8 device px.

## Inspected

- The 1000 px view.
- 1:1 crops of the umbilicus, the aperture edge and the black film.
- `verify.mjs` passes in Chromium, and `still.mjs` repeats byte-identically.
- **Firefox is not verified.** It could not be installed here.

## Remaining weaknesses

- The callus reads as a flat disc with a crisp edge. A ring of the inner whorl shows around it,
  which is closer to an open umbilicus than to the closed one of *N. pompilius*.
- The tube is a plain ellipse. A real aperture is taller, with a hood and a flared outer lip.
- The flames are stylised, and they don't continue onto the venter of the body whorl.
- Nacre banding is decorative, not a model of thin-film interference.
- The ledge is a single flat plane with no texture.
