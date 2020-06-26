# HTML

Main root
Metadata
Sectioning root
Content sectioning

## Text content

|Element|Usage and notes|Level|
|-------|---------------|:---:|
|`<ol>`|`start`, `reversed` bool change the order|:blossom:|
|`<figure>`||:deciduous_tree:|
|`<figcaption>`|1st or last in parent `<figure>`|:deciduous_tree:|

## Inline text semantics

|Element|Usage and notes|Level|
|-------|---------------|:---:|
|`<q>`|`cite="https://..."` can cite the e-address also|:blossom:|
|`<ins>`|`datetime="ISO"` and `today` or any other text in tag|:deciduous_tree:|
|`<del>`|`datetime` and content same to `<ins>`|:deciduous_tree:|
|`<time>`|`datetime` and content same to `<ins>`|:deciduous_tree:|

## Images and multimedia, embedded content

|Element|Usage and notes|Level|
|-------|---------------|:---:|
|`<img>`|`alt` added to only one img of a group, others are "" description|:blossom:|
|`<map>`|image maps (for super strange cases like block-schemes etc)|:seedling:|
|`<area>`|defines a hot-spot region on a map, only used within a `<map>`|:seedling:|
|`<video>`|- `preload="none/metadata"` metadata service data (length, 1 slide)<br>- `preload="auto"` whole video<br>- `poster="#"` img when not yet loaded<br> - `controls`, `autoplay` boolean attributes<br>- source types: `video/mp4`, `MPEG-4/H.264`, `OGG/Theora`, `WebM`|:seedling:|
|`<audio>`|- almost like a video<br>- `controls`, `autoplay` boolean attributes<br>- source types: `MP3`, `OGG`|:seedling:|
|`<source>`|- set `src="video.mp4"`, `type="video/mp4"` diff available, first loads first which could be played|:seedling:|

```HTML
<audio controls preload="" src="#" autoplay>
  <source src="#" type="MP3"></source>
  <source src="#" type="OGG"></source>
</audio>
```

Scripts
Tables
Forms
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