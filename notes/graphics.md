# Graphics
- [SVG](#svg)
- [WebP](#webp)

## SVG
<details>
<summary>Basics</summary>

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

<details>
<summary>Shapes</summary>

|Tag|Parameters|Notes|Level|
|---|----------|-----|:---:|
|`<rect>`|`width="50%" height="100" x="20" y="50%"`||:seedling:|
|`<polygon>`|`points="70.5 90.41 136.48"`|points = coords of peaks x, y (px only)|:seedling:|
|`<circle>`|`r="50" cx="100" cy="50%"|- `r` = radius `px` or `%`<br>- `cx` and `cy` = center coords (0 0 by default) `px` or `%`|:seedling:|
|`<ellipse>`|`rx="50" ry="40%" cx="50" cy="50%"||:seedling:|
|`<line>`|- `x1="220" y1="10%" x2="300" y2="15%"`<br>- `stroke="blue" stroke-width="5"`|`stroke-width` = 1 by default|:seedling:|
|`<polyline>`|`points="10,135 100,10 55,135"`|stroke doesn't close (unlike to `<polygon>`)|:seedling:|

</details>

<details>
<summary>Attribute and CSS styling</summary>

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

<details>
<summary>Optimization</summary>

- use fewer nodes
- fewer handlers
- integer numbers
- not too big grid
- Compressing smaller raw data would probably produce smaller compressed data.
- Fewer distinct characters means less entropy. Less entropy is better compression.
- More frequently found characters are compressed with less number of bits. Getting rid of less common characters and making the more common chars to be even more common would most probably improve the compression.
- Long runs of duplicated code are compressed with a few bits. DRY is not always the best option. Sometimes you’d like to repeat yourself to get better results.
- Sometimes more raw data will produce smaller compressed data. Removing entropy will allow the compressor to better remove what is redundant.

</details>

<details>
<summary>Sprites</summary>

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

<details>
<summary>SVG as a placeholder for images</summary>

- nothing - just add sizes for browser not to re-render
- placeholder static - ex. a person svg for a person avatar
- solid color or gradient most suitable colors for the image
- svg simple shapes (vary 10-100), could be heavy
- svg simple shapes + blur filter more light and smooth
- svg silhouettes even with 2 colors look nice

</details>

<details>
<summary>Learn more</summary>

- [Optimizing SVG for Web Use](https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-1-67e8f2d4035)
- [An Overview of SVG Sprite Creation Techniques](https://24ways.org/2014/an-overview-of-svg-sprite-creation-techniques/)
- [How to use SVG as a Placeholder, and Other Image Loading Techniques](https://medium.freecodecamp.org/using-svg-as-placeholders-more-image-loading-techniques-bed1b810ab2c)
- [SVG, Minification and Gzip](https://blog.usejournal.com/of-svg-minification-and-gzip-21cd26a5d007)
- [Making the Switch Away from Icon Fonts to SVG: Converting Font Icons to SVG](https://www.sarasoueidan.com/blog/icon-fonts-to-svg/)
- [SVG by Sara Soueidan](https://www.sarasoueidan.com/tags/svg/)

</details>

## WebP
<details>
<summary>Learn more</summery>

- [ ] [Why and how to use WebP images today](https://bitsofco.de/why-and-how-to-use-webp-images-today/)

</details>

## Resources
<details>
<summary>Photos</summary>

- [Free images](https://unsplash.com/)
- [Free photos and videos](https://www.pexels.com/)

</details>

<details>
<summary>Vectors (illustrations, blobs)</summary>

- [Free illustrations](https://undraw.co/illustrations)
- [Blob generator](https://blobs.app/)

</details>

<details>
<summary>Icons</summary>

- [Free icons (credit)](https://icons8.com/)

</details>