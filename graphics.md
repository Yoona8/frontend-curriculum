# Graphics

## 1 - SVG
### 1.1 - Basics
<details>
<summary>Notes</summary>

- all tags should be closed
- `<svg width="100" height="200"></svg>` `px` default or `%`
- `width` / `height` by default = 300 x 150
- have to set sizes, otherwise it'll grow big (width of a viewport)
- viewport space = svg borders
- user space = content borders
- no viewBox: viewport = user
- with viewBox/transform: user coordinates grid moves/scales, start/end coords also change
- inside svg
    - `px` or `%` (% counts of svg sizes)
    - coords x y from top left corner (both % and px)
    - `rx` = `ry` if not specified (corner rounds % or px)

</details>

<details>
<summary>Table</summary>

|Attribute|Notes and usage|Level|
|---------|---------------|:---:|
|`viewBox`|- `x y w h` attribute only, no CSS, `px`<br>- with viewBox content fits and centers<br>- svg with no w/h but with viewBox fills the whole viewport|:seedling:|
|`preserveAspectRatio`|- changes viewBox behavior<br>- `none` doesn't preserve proportions, fills the whole svg (ex. rubber backgrounds)<br>- `xMidYMid` default, another possible `Min` `Max`<br>-- doesn't work w/o viewBox<br>-- second param indicates how the viewport fills: `melt` almost = `background: contain;` full svg and `slice` almost = `background: cover;` fills container|:seedling:|

</details>

### 1.2 - Shapes
<details>
<summary>Table</summary>

|Tag|Parameters|Notes|Level|
|---|----------|-----|:---:|
|`<rect>`|`width="50%" height="100" x="20" y="50%"`||:seedling:|
|`<polygon>`|`points="70.5 90.41 136.48"`|points = coords of peaks x, y (px only)|:seedling:|
|`<circle>`|`r="50" cx="100" cy="50%"|- `r` = radius `px` or `%`<br>- `cx` and `cy` = center coords (0 0 by default) `px` or `%`|:seedling:|
|`<ellipse>`|`rx="50" ry="40%" cx="50" cy="50%"||:seedling:|
|`<line>`|- `x1="220" y1="10%" x2="300" y2="15%"`<br>- `stroke="blue" stroke-width="5"`|`stroke-width` = 1 by default|:seedling:|
|`<polyline>`|`points="10,135 100,10 55,135"`|stroke doesn't close (unlike to `<polygon>`)|:seedling:|

</details>

### 1.3 - Attribute and CSS styling
<details>
<summary>Table</summary>

|Attribute|Property|Notes|Level|
|---------|--------|-----|:---:|
|`fill="gold"`|`fill: gold;`|if not specified = `black`|:deciduous_tree:|
|`fill-opacity="0.1"`|`fill-opacity: 1;`||:seedling:|
|`stroke="orange"`|`stroke: orange;`||:deciduous_tree:|
|`stroke-width="5"`|`stroke-width: 5;`|% also available, counts of SVG size|:deciduous_tree:|
|`stroke-opacity="0.5"`|`stroke-opacity: 1;`||:seedling:|
|`stroke-linecap="butt"`|`stroke-linecap: butt;`|- `butt` default, cuts the edges<br>- `round` rounds the edges<br>- `square` - squares the edges|:seedling:|
|`stroke-linejoin="miter"`|`stroke-linejoin: miter;`|- `miter` default, square<br>- `round`, `bevel` almost = `butt`|:seedling:|
|`stroke-dasharray="15"`|`stroke-dasharray: 50 10;`|- dashed lines<br>- `15` dashes = spaces<br>- `50 10` dash space<br>- `1 2 10 15` dash space dash space<br>- could be not even in circle|:seedling:|
|`stroke-dashoffset="10"`|`stroke-dashoffset: 1;`|move of dasharray +-|:seedling:|
</details>

### 1.4 - Optimization
<details>
<summary>Notes</summary>

- use fewer nodes
- fewer handlers
- integer numbers
- not too big grid

</details>

### 1.5 - Sprites
<details>
<summary>Notes</summary>

- HTML inline sprites `<svg style="display: none;"><symbol></symbol></svg>`
    - minus: doesn't cache in the browser
- SVG sprite file (have to add a fallback)
    - for IE support use svg4everybody
- CSS inline SVG sprite (`svg+xml`)
    - fallback base64, fallback images
    - can't change svg style properties
- using SVG fragment ids and views
    - bugs in safari

</details>