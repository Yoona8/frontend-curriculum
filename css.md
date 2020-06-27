# CSS

## Content
- [Selectors](#selectors)
  - [Pseudo classes](#pseudo-classes)
  - [Pseudo elements](#pseudo-elements)
  - [Attribute](#attribute)
- [Measure Units](#measure-units)
- Colors
- Variables
- Functions
- Media Queries
- Feature Queries
- [Box Model](#box-model)
- [Positioning](#positioning)
- [Flexbox](#flexbox)
- [Grid](#grid)
- Centering
- [Floats and Shapes for Floats](#floats-and-shapes-for-floats)
- [Tables](#tables)
- [Typography](#typography)
- [Columns](#columns)
- Lists
- Forms
- [Backgrounds](#backgrounds)
- Gradients
- [Borders](#borders)
- [Outlines](#outlines)
- Shadows
- Transforms
- Transitions
- Animations

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

## Positioning
|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`position`||:blossom:|
|`top`|- by default all coords = auto<br>- no scroll when extends browser's borders|:blossom:|
|`left`|no scroll when extends browser's borders|:blossom:|
|`bottom`|with scroll when extends browser's borders|:blossom:|
|`right`|with scroll when extends browser's borders|:blossom:|

## Flexbox
|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`display: flex;`|min and max sizes apply after the basic size is counted (in the very end)|:deciduous_tree:|
|`flex-grow`|- positive int<br>- free space according to coefficient|:deciduous_tree:|
|`flex-shrink`|- positive int number<br>- free shrink according to coefficient<br>- not to shrink = 0<br>- only content shrinks (not paddings or borders)<br>- flex-shrink + multiline flex (only 1 element > container width)|:deciduous_tree:|
|`flex`|- combined property, has problems in some browsers<br>- flex-grow flex-shrink flex-basis<br>- `initial` = 0 1 auto<br>- `auto` = 1 1 auto<br>- `none` = 0 0 auto<br>- `1 0` = 1 0 0%<br>- `1` = 1 1 0%|:seedling:|

## Grid
### Applied to the container
|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`display: grid;`|- children become parents grid elements<br>- elements position on the 2d grid between lines<br>- grids could be layered (default - order in HTML)<br>- `z-index` changes layering|:seedling:|

### Applied to children
|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`grid-column-start: 3;`|starts from 3 vertical line, if end is undefined, ends on next line|:seedling:|
|`grid-column-end: 5;`||:seedling:|
|`grid-column: 3 / 5;`|- start / end<br>- when used without 2nd param, will behave like `-start` property|:seedling:|
|`grid-row-start: 5;`|starts from 5 horizontal line, if end is undefined, ends on next line|:seedling:|
|`grid-row-end: 7;`||:seedling:|
|`grid-row: 5 / 7;`|- start / end<br>- when used without 2nd param, will behave like `-start` property|:seedling:|

Centering

## Floats and Shapes for Floats
|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`float`|- `left/right/none` basically used to float elements with text<br>- adds sizes to phrasing elements too<br>- shrinks to content<br>- drops out of flow (partially)<br>- block elements after float stop reacting oon float, go up like with `position: absolute;`<br>- inline elements float around the empty side of float element<br>- if all blocks are floats, parent shrinks to 0 height<br>- floats see each other, drop to the next line, but sometimes 'chains' and positions below one of the random floats (awkward behavior)|:seedling:|
|`clear`|`left/right/both/none` forbids floating, if after float - sees it (clearfix pattern)|:seedling:|

## Tables
### Styling tables
|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`border-collapse`|`collapse` set on `<table>` to avoid double border|:blossom:|
|`border-spacing: 10px 1rem;`|- set on `<table>`<br>- when `border-collapse` != `collapse`<br>- between table and cells|:seedling:|
|`caption-side`|`top`, `bottom`|:seedling:|
|`background-color`|for `<tr>` we can add only background properties, has almost no self styling|:seedling:|
|`vertical-align`|aligns text inside the cell vertically|:seedling:|

### Make it a table with CSS
|Display value|Usage and notes|Level|
|-------------|---------------|:---:|
|`table`|`<table>`|:seedling:|
|`inline-table`||:seedling:|
|`table-row`|`<tr>`|:seedling:|
|`table-cell`|`<td>`|:seedling:|
|`table-caption`|`<caption>`|:seedling:|
|`table-header-group`|`<thead>`|:seedling:|
|`table-row-group`|`<tbody>`|:seedling:|
|`table-footer-group`|`<tfoot>`|:seedling:|
|`table-column`|like a `<col>` tag - empty, used for styling a column one - 1st, two - second ...|:seedling:|
|`table-column-group`|like a `<colgroup>` and child `<col>` tags, empty, styles for every child column|:seedling:|

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

## Backgrounds
|Property                |Usage and notes|Level|
|------------------------|---------------|:---:|
|`background-color`|`#fff(fff)(ff)` `rgb(a)` `hsl(a)`|:blossom:|
|`background-image`|- `url('bg.jpg')` image layers on color<br>- when multiple - 1st is upper|:blossom:|
|`background-repeat`|- `repeat`, `repeat-x(y)` `no-repeat`<br>- `round` repeated parts shrink or grow<br>- `space` adds space between<br>- could be different by x or y|:deciduous_tree:|
|`background-position`|- x y `left` `center` `right` `top` `bottom`<br>- `50%` `50px` +-<br>- `right 30px top 20px` - from any block corner|:deciduous_tree:|
|`background-attachment`|-`scroll` default<br>`fixed` adds very simple parallax effect|:deciduous_tree:|
|`background-size`|-`auto auto` default<br>- `100px, 100% 50%`<br>- `contain` reserves proportions, max sizes with full fill possible, could not cover the whole container<br>- `cover` reserves proportions, min possible sizes to cover the whole container, if block and img proportions are different, img cuts|:deciduous_tree:|
|`background-origin`|- `padding-box` (-borders) default<br>- `border-box` (+padding+borders)<br>- `content-box` (-padding-borders)|:deciduous_tree:|
|`background-clip`|- `border-box` default doesn't cut<br>- `padding-box` cuts till borders<br>- `content-box` cuts with paddings|:seedling:|
|`background`|complex property order `[bc] [bi] [br] [bp] [ba]`|:deciduous_tree:|

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