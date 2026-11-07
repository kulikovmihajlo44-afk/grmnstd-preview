# konsole3d

Live ASCII 3D objects for the web, in one file with no dependencies. It powers the Berlin landmarks on
[germanstudy.tech](https://www.germanstudy.tech), the site of the Deutsch-Klub at Constructor University.

**Live demo:** https://kulikovmihajlo44-afk.github.io/grmnstd-preview/

To run it locally, open `index.html` through any local web server (images do not load from `file://`).

## How it works

- Every bright pixel of a line drawing becomes a 3D point on a front and a back face, so the object has depth when it turns.
- Each frame the points are rotated and projected onto a grid of sub-cells, 2 × 3 per character.
- Each character cell gets the glyph whose shape best matches its sub-cells: columns become `|`, cornices `_ = -`, diagonals `/ \`.
  This keeps the drawing crisp instead of noisy.
- Objects scan in line by line when they first appear, sway gently and can be dragged to any angle.
- Only objects on screen are drawn. With reduced motion, each object is drawn once and stands still.

## Usage

```html
<pre class="ascii" data-src="drawing.png"></pre>
<pre class="ascii" data-shape="ring"></pre>
<script src="ascii3d.js"></script>
```

Give the `<pre>` a size, a monospace font, `line-height: 1` and `white-space: pre`. See `index.html`.

| Attribute | What it does | Default |
|---|---|---|
| `data-src` | Image to turn into an object. Bright pixels on a dark or transparent background | — |
| `data-shape` | Built-in model: `ring`, `kugel` (globe), `wuerfel` (cube), `fernsehturm` (Berlin TV tower) | — |
| `data-size` | Font size in px | 9 |
| `data-res` | Sample width of the image | 200 |
| `data-speed` | Rotation or sway speed, radians per second | 0.35 |
| `data-yaw`, `data-pitch` | Starting angles | 0, 0.1 |
| `data-floor` | `"1"` adds a dotted ring plaza under the object | off |
| `data-fps` | Frame rate cap | 30 (20 on small screens) |
| `data-shade` | `"1"` draws a greyscale photo cut-out as a lit relief | off |
| `data-fit` | `"x,y"`: how much of the box the object may fill | `0.38,0.84` |
| `data-anchor` | `"top"` pins the object to the top of the box | centre |

JavaScript: `window.DKAscii.mount(el)` mounts a new element, and `DKAscii.define(name, parts)` adds a model.

## License

MIT, see [LICENSE](LICENSE).
