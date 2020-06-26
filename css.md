# CSS

## Selectors
### Pseudo classes
|Pseudo class|Notes|Level|
|------------|-----|:---:|
|`:not(...)`|- can use: `:not(:last-child)` `:not(p):not(#id)` `:not([attribute])` `:not(.class)`<br>- cannot use: `:not(:not())` `:not(.class-one.class-two)` `:not(::after)`<br>`:not(a span + span ~ span)` (any combined selector)|:deciduous_tree:|
|`:nth-last-child`|from last|:deciduous_tree:|
|`:nth-child(2)`|if the 2nd element is ul, choses, otherwise no|:deciduous_tree:|
|`:only-child`|only one child|:deciduous_tree:|
|`:first-of-type`|with type in mind|:deciduous_tree:|
|`:last-of-type`|with type in mind|:deciduous_tree:|
|`:nth-of-type(2)`||:deciduous_tree:|
|`:nth-last-of-type(2)`||:deciduous_tree:|
|`:only-of-type`|only one of type inside a parent|
|`:empty`|no element or text inside|:deciduous_tree:|
|`:enabled`||:blossom:|
|`:disabled`||:blossom:|
|`:read-write`||:deciduous_tree:|
|`:read-only`||:deciduous_tree:|
|`:required`||:deciduous_tree:|
|`:optional`||:deciduous_tree:|
|`:checked`||:blossom:|
|`:valid`||:deciduous_tree:|
|`:invalid`||:deciduous_tree:|
|`:in-range`||:seedling:|
|`:out-of-range`||:seedling:|

### Pseudo elements
|Pseudo element|Notes|Level|
|--------------|-----|:---:|
|`::first-line`||:seedling:|
|`::first-letter`||:seedling:|
|`::before`||:blossom:|
|`::after`||:blossom:|

### Attribute
|Attribute selector|Notes|Level|
|------------------|-----|:---:|
|`[type="text"]`|exact|:deciduous_tree:|
|`[foo^="bar"]`|starts with 'bar'|:deciduous_tree:|
|`[foo$="bar"]`|ends with 'bar' (good for docs .jpg)|:deciduous_tree:|
|`[foo*="bar"]`|contains 'bar'|:deciduous_tree:|
|`[foo~="bar"]`|'bar' is a separate word|:deciduous_tree:|
|`[foo\|="bar"]`|prefix 'bar', the value has to be either alone or followed by '-'|:deciduous_tree:|

## Measure Units

|Unit|Usage and notes|Level|
|----|---------------|:---:|
|`em`|depends on element's font-size|:deciduous_tree:|

Colors
Variables
Functions
Media Queries
Feature Queries

## Box Model

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`width`|- block full width<br>- phrasing width = content<br>- input's width by default = `[size]` attribute, doesn't grow into full parent's width|:blossom:|
|`max-width`|counts of parent|:blossom:|
|`height`||:blossom:|
|`margin`|- phrasing only hor margins<br>- vertical margins collapse to the more value (parent 40px, child 60px = 60px after collapse)<br>- vertical margins drop out of parent if parent doesn't have paddings or borders and it's margin is < child's margin<br>- horizontal margins do not collapse|:blossom:|
|`padding`|- phrasing only hor paddings|:blossom:|
|`display`|`none` removes element + makes una11y|:blossom:|
|`visibility`|`hidden` hides the element, but the place is still there, makes una11y|

Positioning
Flexbox
Grid
Centering
Floats and Shapes for Floats

## Tables

<details>
<summary>Tables in CSS</summary>

```CSS
table {
  /* to avoid double border*/
  border-collapse: collapse;
  /* when border-collapse != collapse */
  /* between table and cells */
  border-spacing: 10px 1rem;
}

caption {
  caption-side: top;
  caption-side: bottom;
}

tr {
  /* for <tr> we can add only background properties, has almost no self styling */
  background-color: #ffffff;
}

td {
  /* aligns text inside the cell vertically */
  vertical-align: middle;
}
```

```CSS
/* css tables, don't know when could be useful */
.table {
  display: table;
  display: inline-table;
}

.tr {
  display: table-row;
}

.td {
  display: table-cell;
}

.caption {
  display: table-caption;
}

.thead {
  display: table-header-group;
}

.tbody {
  display: table-row-group;
}

.tfoot {
  display: table-footer-group;
}

/* like a <col> tag - empty, used for styling a column one - 1st, two - second ... */
.col {
  display: table-column;
}

/* like a <colgroup> and child <col> tags, empty, styles for every child column */
.colgroup {
  display: table-column-group;
}
```

</details>

## Typography

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`font-weight`|`bolder`, `lighter` from current or inherited|:blossom:|
|`font-size`|- `px`, `small`, `xx-small` absolute;<br>- `em`, `larger`, `smaller` relative to parent;<br>- `rem` relative to `<html>`|:blossom:|
|`line-height`|`px`, (`%`, coefficient - from font-size)|:blossom:|
|`font-family`|`sans-serif`, `monospace`, `serif`, `cursive`, `fantasy`|:blossom:|
|`text-align`|`start`, `end`, `left`, `right`, `center`, `justify`|:blossom:|
|`font-style`|`normal`, `italic`, `oblique` ('pseudo-italic' made by browser)<br>`vertical-rl`, `vertical-lr`, |:deciduous_tree:|
|`text-transform`|`none`, `uppercase`, `lowercase`, `capitalize`|:blossom:|
|`writing-mode`|`horizontal-tb`|:seedling:|
|`vertical-align`|`baseline`, `top`, `middle`, `bottom`, `%`, `px`<br>for inline element regarding the line<br>used on element, not container<br>`px` or `%` of `line-height`<br>`0%` = `0px` = `baseline` (almost)<br>`px` like `%`, counts > or < side|:deciduous_tree:|
|`color`|`#fff(fff)(ff)`, `rgb(a)`, `hsl(a)`|:blossom:|
|`white-space`|`normal`, `nowrap`<br>`pre`, `pre-wrap` = `<pre>` (pre-wrap to new line if overflow)<br>`break-spaces` = `pre-wrap`, but doesn't touch reserved space<br>`pre-line` = `normal`, but breaks lines on line-break symbol|:seedling:|
|`overflow-wrap`|`normal`, `break-word`|:seedling:|
|`letter-spacing`|`px`, `em`, `rem`, `pt`|:blossom:|
|`text-indent`|+- `%`, `px`, `em`, `pt` indent of the 1st line of the text block (of width)|:seedling:|
|`word-spacing`|`em`, `rem`, `%`, `ch` between words +-, could be used also for inline-blocks and images|:deciduous_tree:|
|`direction`|`ltr`, `rtl` changes columns order, scrollbar position|:seedling:|
|`unicode-bidi`|- `normal` according to used symbols<br>- `embed` according to set direction<br>- `bidi-override` overrides according direction|:seedling:|
|`text-overflow`|- applies only if: 1. one-line block; 2. - overflow is initiated<br>- `clip` default cuts on container size<br>- `ellipsis` - adds `...` in the end|:deciduous_tree:|
|`text-decoration`|`underline`|:deciduous_tree:|
|`text-decoration-line`|`underline`, `line-through`, `overline`, `none`|:deciduous_tree:|
|`text-decoration-style`|`solid`, `double`, `dotted`, `dashed`, `wavy`|:deciduous_tree:|
|`text-decoration-color`|`#fff(fff)(ff)`, `rgb(a)`, `hsl(a)`|:deciduous_tree:|
|`text-shadow`|`1px 1px 1px #000000` x y r-blur (0 default) color (text color default), multiple available|:deciduous_tree:|

## Columns

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`column-count`|int, separates block into equal columns of text|:seedling:|
|`column-width`|min width, if column-count is undefined, browser separates into max available width|:seedling:|
|`column-gap`|`1em` default|:seedling:|

Lists
Forms
Backgrounds
Gradients

## Borders

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`border-style`|- `groove` looks like carved into the page<br>- `ridge` opposite to `groove`|:seedling:|

## Outlines

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`outline`|- `1px solid #000`<br>- can't use only for some sides<br>- styles like a border|:deciduous_tree:|
|`outline-offset`|+- outline position|:deciduous_tree:|
|`outline-style`|- `groove` looks like carved into the page<br>- `ridge` opposite to `groove`|:seedling:|

Shadows
Transforms
Transitions
Animations

Overflow
Opacity
Filter
Cursor
Counters
Single Element Shapes
Inline-Block
Clipping and Masking
Fragmentation
CSSOM
Stacking Context
Block Formatting Contexts
Object Fit and Placement