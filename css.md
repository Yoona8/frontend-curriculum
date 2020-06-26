# CSS

Selectors

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
|`max-width`|counts of parent|:blossom:|

Positioning
Flexbox
Grid
Centering
Floats and Shapes for Floats
Tables

## Typography

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`font-weight`|`bolder`, `lighter` from current or inherited|:blossom:|
|`font-size`|`px`, `small`, `xx-small` - absolute;<br>`em`, `larger`, `smaller` - from parent;<br>`rem` - from `<html>`|:blossom:|
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

## Notes