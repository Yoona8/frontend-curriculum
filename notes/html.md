# HTML

## Metadata content

## Flow content
<details>
<summary>Lists</summary>

```HTML
<!-- start to set the start point -->
<!-- reversed - bool, changes the order -->
<ol start="10" reversed>
  <li></li>
</ol>
```

</details>

<details>
<summary>Presentation</summary>

```HTML
<figure>
  <figcaption>1st or last element inside the figure</figcaption>
</figure>
```

</details>

<details>
<summary>Tables</summary>

```HTML
<!-- by default shrinks to content -->
<table>
  <caption>Always the 1st child</caption>
  <tr>
    <!-- for horizontal expanding, moves right cell, have to delete in html -->
    <td colspan="2"></td>
    <!-- for vertical expanding, moves lower cell in it's own row to right -->
    <td rowspan="2"></td>
  </tr>
</table>
```

</details>

## Sectioning content

## Heading content

## Phrasing content
<details>
<summary>Text semantics</summary>

```HTML
<!-- can cite the e-address also -->
<q cite="https://google.com">Google</q>

<!-- phrasing if contain only phrasing content -->
<ins datetime="2020-09-08">today</ins>
<del datetime="2020-09-07T14:14">yesterday at 14:14</del>

<!-- phrasing always -->
<time datetime="2020-09-06">2 days ago</time>
```

</details>

<details>
<summary>Learn more</summary>

- [Datetime attribute valid values](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/time)

</details>

## Embedded content

## Interactive content

## Palpable content

## Form-associated content

## Script-supporting elements

## Transparent content model

## Images and multimedia, embedded content
<details>
<summary>Images</summary>

```HTML
<!-- alt is added to only one img of a group, others are "" description -->
<img width="20" height="20" src="star.svg" alt="Rating of 5 stars">
<img width="20" height="20" src="star.svg" alt="">
<img width="20" height="20" src="star.svg" alt="">
<img width="20" height="20" src="star.svg" alt="">
<img width="20" height="20" src="star.svg" alt="">

<!-- for complex images (graphs or alike) with long descriptions -->
<!-- use short and long descriptions -->
<img src="#" alt="Short description" longdesc="#long-desc">
<p id="long-desc">Long description here.</p>
<!--or-->
<img src="#" alt="Short description" aria-labelledby="#long-desc">
<p id="long-desc">Long description here.</p>
<!-- or use figure -->
<figure>
  <img src="#" alt="Short description">
  <figcaption>Long description here.</figcaption>
</figure>
```

</details>

<details>
<summary>Image maps</summary>

- for super strange cases like block-schemes etc
```HTML
<map name="map">
  <!-- defines a hot-spot region on a map, only used within a <map> -->
  <area shape="circle" coords="75,75,75" href="left.html">
</map>
<img usemap="#map" src="#" alt="Map">
```

</details>

<details>
<summary>Video and audio</summary>

```HTML
<!-- preload metadata service data (length, 1 slide) -->
<!-- preload auto - whole video -->
<!-- poster img when not yet loaded -->
<video 
  preload="none/metadata/auto"
  poster="#"
  controls
  autoplay
>
  <!-- first loads first if could be played -->
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
  <source src="" type="MPEG-4/H.264">
  <source src="" type="OGG/Theora">
</video>

<!-- almost like a video -->
<audio controls autoplay>
  <!-- first loads first if could be played -->
  <source src="" type="mp3">
  <source src="" type="ogg">
</audio>
```

</details>

<details>
<summary>Learn more</summary>

- [Video tag on MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)

</details>

## Scripts

## Forms
|Element|Usage and notes|Level|
|-------|---------------|:---:|
|`<form>`|`enctype="multipart/form-data"` required for working with files|:deciduous_tree:|
|`<fieldset>`|`disabled` for all the fields inside|:deciduous_tree:|
|`<legend>`|first child of `<fieldset>`|:deciduous_tree:|
|`<button>`|`name` will also get posted to server|:blossom:|
|`<select>`|- `multiple` - ctrl/cmd to choose with<br>- `multiple` + `size` to change height|:deciduous_tree:|
|`<optgroup>`|- could have group children<br>- could be used with multiple select|:deciduous_tree:|
|`<option>`|- `selected` to choose value, could be several<br>- `value` ? value : text content goes to server|:deciduous_tree:|
|`<textarea>`|- `rows="10"` strings<br>- `cols="100"` symbols|:blossom:|
|`<datalist>`|- connected via `list` of `<input>` and `id` of `<datalist>`<br>- if inputs type != `text`, shows only correct items|:seedling:|
|`<output>`|- has `name` attribute<br>- value accessible from js via `element.value`|:seedling:|

<details>
<summary>Examples</summary>

```HTML
<input type="text" list="browsers" name="browsers">
<datalist id="browsers">
  <option>Google Chrome</option>
  <option>Mozilla Firefox</option>
  <option>Edge</option>
  <option>Opera</option>
</datalist>
```

</details>

|Attribute|Usage and notes|Level|
|---------|---------------|:---:|
|`autofocus`|only one attribute for the whole page|:blossom:|
|`pattern`|regexp, if incorrect - validation error|:deciduous_tree:|
|`readonly`|can't change but can select and copy, **posts to the server**|:blossom:|
|`disabled`|can't change, focus, select or copy, **doesn't post to the server**|:blossom:|
|`autocomplete`|`on` `off` allow/block browser autocomplete option|:blossom:|

|Input type|Usage and notes|Level|
|----------|---------------|:---:|
|`hidden`|good for support needs|:deciduous_tree:|
|`file`|- `name` is required<br>- `enctype` on `<form>`is required|:seedling:|
|`image`|- almost = submit + sends the click coordinates on the image<br>- has `alt` and `src` attributes|:seedling:|
|`date`|- for all date types if browser doesn't support, shows text field<br>- with locale|:seedling:|
|`time`|with locale|:seedling:|
|`datetime`|with time zone|:seedling:|
|`datetime-local`|w/o time zone|:seedling:|
|`week`|N of week, year|:seedling:|
|`month`|month + year|:seedling:|
|`number`|- doesn't have min/maxlength<br>- `step="10"` is applied by clicking arrows, out of step = validation error<br>- number keyboard on mobile<br>- has `min="0"` `max="100"` attributes|:deciduous_tree:|
|`search`|almost like text, in some browsers has a cross|:blossom:|
|`range`|- has `min="0"` `max="100"` `step="10"` attributes<br>- still has no multiple handles|:deciduous_tree:|
|`tel`|- good with patterns<br>- tel keyboard on mobile|:blossom:|
|`email`|- native validation for correct urls, emails<br>- proper keyboard on mobile|:deciduous_tree:|
|`url`|same to `email`|:deciduous_tree:|
|`color`|- opens special pallette with colors<br>- if browser doesn't support = text field|:seedling:|

Interactive elements
Web components

## Notes

<details>
<summary>HTML basic structure</summary>

```HTML
<!doctype html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- optional: start -->
  <meta name="keywords" content="...">
  <meta name="description" content="...">
  <!-- optional: end -->
  <title>Title</title>
  <link href="#" rel="stylesheet">
</head>
<body>
</body>
```

</details>

<details>
<summary>Using a group of images</summary>

```HTML
<!-- alt added to only one img of a group, others are "" description -->
<img src="./star.png" alt="4 out of 5 stars">
<img src="./star.png" alt="">
<img src="./star.png" alt="">
<img src="./star.png" alt="">
<img src="./star.png" alt="">

<!-- there are also image maps (for super strange cases like block-schemes etc) -->
<!-- consider using tags below -->
<map>
<area>
```

</details>

- `target="_blank" rel="noopener"` to avoid fishing