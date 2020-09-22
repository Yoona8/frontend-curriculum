# CSS
## Naming
<details>
<summary>Learn more</summary>

- [Слова, часто используемые в CSS-классах](https://github.com/yoksel/common-words)

</details>

## Selectors
<details>
<summary>Pseudo classes</summary>

- pseudo classes are dynamic (if we check the checkbox in the DOM - attribute is not added, `input:checked` will select this input but attribute selector `input[checked]` will not)
```CSS
/* forms */
input:checked {}

/* styles based on language */
:lang(ko) {}
```
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
|`:valid`||:deciduous_tree:|
|`:invalid`||:deciduous_tree:|
|`:in-range`||:seedling:|
|`:out-of-range`||:seedling:|

</details>

<details>
<summary>Pseudo elements</summary>

```CSS
p::first-line {}
p::first-letter {}

p::before {}
p::after {}
```

</details>

<details>
<summary>Attribute</summary>

```CSS
/* exact */
[type="text"] {}
/* starts with 'bar' */
[foo^="bar"] {}
/* ends with 'bar' (good for docs .jpg) */
[foo$="bar"] {}
/* contains 'bar' */
[foo*="bar"] {}
/* 'bar' is a separate word */
[foo~="bar"] {}
/* prefix 'bar', the value has to be either single or followed by '-' */
[foo\|="bar"] {}
```

</details>

<details>
<summary>Learn more</summary>

- [Intriguing CSS Level 4 Selectors](https://webdesign.tutsplus.com/tutorials/intriguing-css-level-4-selectors--cms-29499)
- [Селектор обобщенных родственных элементов](https://habr.com/ru/post/150720/)
- [Article: CSS-селекторы](https://learn.javascript.ru/css-selectors)

</details>

## Measure Units
<details>
<summary>Table</summary>

|Unit|Usage and notes|Level|
|----|---------------|:---:|
|`em`|depends on element's font-size|:deciduous_tree:|

</details>

## Colors
<details>
<summary>Notes</summary>

- `color: currentColor` to reset color to normal text color

</details>

## Variables
## Functions
## Media Queries
## Feature Queries

## Box Model
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`width`|- block full width<br>- phrasing width = content<br>- input's width by default = `[size]` attribute, doesn't grow into full parent's width|:blossom:|
|`max-width`|counts of parent|:blossom:|
|`height`||:blossom:|
|`margin`|- phrasing only hor margins<br>- vertical margins collapse to the more value (parent 40px, child 60px = 60px after collapse)<br>- vertical margins drop out of parent if parent doesn't have paddings or borders and it's margin is < child's margin<br>- horizontal margins do not collapse|:blossom:|
|`padding`|- phrasing only hor paddings|:blossom:|
|`display`|`none` removes element + makes una11y|:blossom:|
|`visibility`|`hidden` hides the element, but the place is still there, makes una11y|

</details>

## Positioning
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`position`||:blossom:|
|`top`|- by default all coords = auto<br>- no scroll when extends browser's borders|:blossom:|
|`left`|no scroll when extends browser's borders|:blossom:|
|`bottom`|with scroll when extends browser's borders|:blossom:|
|`right`|with scroll when extends browser's borders|:blossom:|

</details>

## Layouts
<details>
<summary>Learn more</summary>

- [Relearn CSS layout](https://every-layout.dev/)

</details>

## Flexbox
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`display: flex;`|min and max sizes apply after the basic size is counted (in the very end)|:deciduous_tree:|
|`flex-grow`|- positive int<br>- free space according to coefficient|:deciduous_tree:|
|`flex-shrink`|- positive int number<br>- free shrink according to coefficient<br>- not to shrink = 0<br>- only content shrinks (not paddings or borders)<br>- flex-shrink + multiline flex (only 1 element > container width)|:deciduous_tree:|
|`flex`|- combined property, has problems in some browsers<br>- flex-grow flex-shrink flex-basis<br>- `initial` = 0 1 auto<br>- `auto` = 1 1 auto<br>- `none` = 0 0 auto<br>- `1 0` = 1 0 0%<br>- `1` = 1 1 0%|:seedling:|

</details>

<details>
<summary>Learn more</summary>

- [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Harnessing Flexbox For Today’s Web Apps](https://www.smashingmagazine.com/2015/03/harnessing-flexbox-for-todays-web-apps/)
- [Flexbugs](https://github.com/philipwalton/flexbugs#flexbugs)

</details>

## Grid
<details>
<summary>Applied to the container</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`display: grid;`|- children become parents grid elements<br>- elements position on the 2d grid between lines<br>- grids could be layered (default - order in HTML)<br>- `z-index` changes layering|:seedling:|

</details>

<details>
<summary>Applied to children</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`grid-column-start: 3;`|starts from 3 vertical line, if end is undefined, ends on next line|:seedling:|
|`grid-column-end: 5;`||:seedling:|
|`grid-column: 3 / 5;`|- start / end<br>- when used without 2nd param, will behave like `-start` property|:seedling:|
|`grid-row-start: 5;`|starts from 5 horizontal line, if end is undefined, ends on next line|:seedling:|
|`grid-row-end: 7;`||:seedling:|
|`grid-row: 5 / 7;`|- start / end<br>- when used without 2nd param, will behave like `-start` property|:seedling:|

</details>

<details>
<summary>Learn more</summary>

- [A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid Layout on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [Grid Resources](https://gridbyexample.com/resources/)

</details>

## 13 - Centering
<details>
<summary>Learn more</summary>

- [Centering in CSS: A Complete Guide](https://css-tricks.com/centering-css-complete-guide/)

</details>

## 14 - Floats and Shapes for Floats
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`float`|- `left/right/none` basically used to float elements with text<br>- adds sizes to phrasing elements too<br>- shrinks to content<br>- drops out of flow (partially)<br>- block elements after float stop reacting oon float, go up like with `position: absolute;`<br>- inline elements float around the empty side of float element<br>- if all blocks are floats, parent shrinks to 0 height<br>- floats see each other, drop to the next line, but sometimes 'chains' and positions below one of the random floats (awkward behavior)|:seedling:|
|`clear`|`left/right/both/none` forbids floating, if after float - sees it (clearfix pattern)|:seedling:|

</details>

## 15 - Tables
<details>
<summary>Styling tables</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`border-collapse`|`collapse` set on `<table>` to avoid double border|:blossom:|
|`border-spacing: 10px 1rem;`|- set on `<table>`<br>- when `border-collapse` != `collapse`<br>- between table and cells|:seedling:|
|`caption-side`|`top`, `bottom`|:seedling:|
|`background-color`|for `<tr>` we can add only background properties, has almost no self styling|:seedling:|
|`vertical-align`|aligns text inside the cell vertically|:seedling:|

</details>

<details>
<summary>Make it a table with CSS</summary>

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

</details>

<details>
<summary>Learn more</summary>

- [A Complete Guide to the Table Element](https://css-tricks.com/complete-guide-table-element/)

</details>

## 16 - Typography
<details>
<summary>Table</summary>

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

</details>

## 17 - Columns
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`column-count`|int, separates block into equal columns of text|:seedling:|
|`column-width`|min width, if column-count is undefined, browser separates into max available width|:seedling:|
|`column-gap`|`1em` default|:seedling:|

</details>

## 18 - Lists
## 19 - Forms
<details>
<summary>Snippets</summary>

- [Radio button styles](https://freebiesupply.com/blog/css-radio-buttons/)

</details>

<details>
<summary>Learn more</summary>

- [A Sliding Nightmare: Understanding the Range Input](https://css-tricks.com/sliding-nightmare-understanding-range-input/)

</details>

## 20 - Backgrounds
<details>
<summary>Table</summary>

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Property&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Usage and notes|Level|
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

</details>

## 21 - Gradients
<details>
<summary>Table</summary>

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Function&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Usage and notes|Level|
|--------|---------------|:---:|
|`linear-gradient()`|- `[to top], yellow, green, red, black`<br>- `to bottom` default<br>- `top`, `bottom`, `left`, `right` straight<br>- `right top`, `right bottom` diagonal<br>- `90deg`, `-90deg`<br>- diagonal always to corners, `45deg` not<br>- `red 0%, yellow 100%` adds the color stop, the most colorful point, where other color starts<br>- if for siblings, add same color stop, sharp transition (like stripes)|:deciduous_tree:|
|`repeating-linear-gradient()`|- gradient size (fragment) = last color stop, to see the repetition gradient size should be < element size<br>- if 1st and last colors are the same, the transition will be sharp, equal colors needed<br>- color stop usually px, but % could be used too<br>- can imitate linear-gradient + bg-size + repeat|:deciduous_tree:|

</details>

## 22 - Borders
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`border-style`|- `groove` looks like carved into the page<br>- `ridge` opposite to `groove`|:seedling:|
|`border-radius`|- tl tr br bl<br>- of a circle corner radius<br>- `10px 20px 30px 40px / 5px 15px 25px 35px`|:blossom:|
|`border-top-left-radius`|`30px 15px` hor vert, could be different|:blossom:|
|`border-image`|complex property|:seedling:|
|`border-image-source`|- `url('bg.png')` or gradients also work<br>- by default fills only corners with the whole background-image|:seedling:|
|`border-image-slice`|- `px`, `%` paddings from sides of image to 4 lines<br>- `fill` will fill center too|:seedling:|
|`border-image-repeat`|`stretch` default, can use different to hor and vert<br>- `round` grows evenly<br>- `space` leaves space between|:seedling:|
|`border-image-width`|> border-width = under content|:seedling:|
|`border-image-outset`|almost = `outline-offset`, moves border out of elements borders, evenly grows the image (no neg numbers)|:seedling:|
|||:seedling:|

</details>

## 23 - Outlines
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`outline`|- `1px solid #000`<br>- can't use only for some sides<br>- styles like a border|:deciduous_tree:|
|`outline-offset`|+- outline position|:deciduous_tree:|
|`outline-style`|- `groove` looks like carved into the page<br>- `ridge` opposite to `groove`|:seedling:|

</details>

## 24 - Shadows
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`box-shadow`|- `[inset] x y [blur] [spread] [color]`<br>- `blur` less = more strict<br>- `spread` +more -less than element<br>- `color` default = `color` of the element<br>- if only `spread` with + looks like border<br>- `blur` + `spread` negative = light shadow<br>- `blur` + no `spread` = default shadow<br>- `blur` > `spread` = darker than default<br>- `blur` < `spread` = too dark shadow<br>- multi shadows = upper in the list = upper layering|:deciduous_tree:|

</details>

## 25 - Transforms
<details>
<summary>2D Transforms</summary>

|Property or function|Usage and notes|Level|
|--------|---------------|:---:|
|`transform`|`translate(...) rotate(...)` order matters|:deciduous_tree:|
|`translateX()`<br>`translateY()`<br>`translate(X, [Y])`|if no Y, Y = 0|:deciduous_tree:|
|`scaleX()`<br>`scaleY()`<br>`scale(X, [Y])`|- if no Y, Y = X (base point = 1)<br>- `0` shrinks the element, couldn't see (invisible)<br>- if negative num, element rotates (mirrors)|:seedling:|
|`rotate()`|- `180deg`<br>- by default relatively elements center<br>- rotates with coordinate grid|:deciduous_tree:|
|`skewX()`<br>`skewY()`<br>`skew(X, [Y])`|- if no Y, Y = 0, but `skew()` has bugs<br>- x = +left -right<br>- y = +down -up|:seedling:|
|`transform-origin`|- `X [Y]` if Y is unset, Y = 50%<br>- `50% 50%` default<br>- `px`, `em`, `%`, `left-right`, `top-bottom`<br>- with `rotate` changes the axis<br>- with `scale` to what place shrink<br>- with `scale(0)` to `scale(1)` could be added different effects|:seedling:|

</details>

## 26 - Transitions
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`transition`|`width 1s ease-in 2s` duration, delay complex property|:deciduous_tree:|
|`transition-duration`|`1s`, `300ms` default applied to all properties|:blossom:|
|`transition-property`|`width`, `height`, `opacity` if different duration, order must be the same|:deciduous_tree:|
|`transition-delay`|`1s`, `300ms` delay before start|:blossom:|
|`transition-timing-function`|- `ease` default = `cubic-bezier(0, 0.42, 0, 1, 1)`<br>- `linear` even<br>- `ease-in`, `ease-out`, `ease-in-out`<br>- `cubic-bezier(0, X1, Y1, X2, Y2)` X, Y coords form 0 to 1<br>- `steps(6, end)` int count, keyword for direction<br>- animates like 'dashes'<br>- first/last step executes evenly with start/end of the transition|:deciduous_tree:|

</details>

## Animations
<details>
<summary>Table</summary>

|Property|Usage and notes|Level|
|--------|---------------|:---:|
|`@keyframes <name> {}`|- `0% { width: 100%; }`<br>- start and end steps are either `from ... to` or `0% 100%`, steps inside are in `%`<br>- if no start point, animation runs from basic elements state to 1st existing step<br>- if there is no last step, after last inner step animation runs backwards to initial state<br>- steps could be in any order, but chronological preferred|:deciduous_tree:|
|`animation`|`<name> 1s` one element can have multiple animations|:deciduous_tree:|
|`animation-name`|`name1, name2`|:deciduous_tree:|
|`animation-duration`|`1s`, `300ms`|:deciduous_tree:|
|`animation-iteration-count`|- `0` won't run<br>- positive int = runs count<br>- `infinite`|:deciduous_tree:|
|`animation-direction`|- `normal`, `reverse`<br>- `alternate` when count > 1 odd = `normal`, even = `reverse`<br>- `alternate-reverse`|:deciduous_tree:|
|`animation-delay`|`1s`, `300ms` delay before start|:deciduous_tree:|
|`animation-fill-mode`|- if animation effect visible when ends<br>- `forwards` keeps the final state (even when several runs or `reverse`)<br>- `backwards` keeps state initial or `0%` / `from`<br>- if `delay` + `backwards` = styles `from` / `0%` apply before delay (animation starts)<br>- `both` = `forwards` + `backwards`|:deciduous_tree:|
|`animation-play-state`|- `running` default<br>- `paused` stopped|:deciduous_tree:|
|`animation-timing-function`|- `ease` slow-slow default<br>- `linear` evenly<br>- `ease-in` slow-fast<br>- `ease-out` fast-slow<br>- `ease-in-out` almost like `ease`, but more intensive<br>- `cubic-bezier(...)`<br>- `steps(6, start)`|:deciduous_tree:|

</details>

<details>
<summary>Snippets</summary>

- [Hovers, loaders](https://emilkowalski.github.io/css-effects-snippets/)
- [Different animations](https://animate.style/)

</details>

<details>
<summary>Learn more</summary>

- [Creating smooth CSS animations — even with a heavy DOM](https://medium.com/purpledesign/creating-smooth-css-animations-even-with-a-heavy-dom-212cb80441a9)

</details>

## 28 - Overflow
## 29 - Opacity
## 30 - Filter
## 31 - Cursor
## 32 - Counters
## 33 - Single Element Shapes
## 34 - Inline-Block
## 35 - Clipping and Masking
## 36 - Fragmentation
## 37 - CSSOM
## 38 - Stacking Context
## 39 - Block Formatting Contexts
## 40 - Object Fit and Placement
## Optimization

<details>
<summary>Learn more</summary>

- [CSS triggers](https://csstriggers.com/)

</details>

## Houdini
<details>
<summary>Learn more</summary>

- [Houdini](https://css-houdini.rocks/js-in-css/)

</details>

## Resources
<details>
<summary>Learn more</summary>

- [CSS Reference](https://tympanus.net/codrops/css_reference/)
- [State of CSS 2019](https://2019.stateofcss.com/)
- [Refactoring (the way we talk about) CSS](https://noti.st/rachelandrew/VqOEAa/refactoring-the-way-we-talk-about-css#sNdvV9Y)

</details>

<details>
<summary>Books</summary>

- [Cascading Style Sheets: The Definitive Guide, 2nd Edition](http://shop.oreilly.com/product/9780596005252.do)
- [CSS: The Missing Manual, 4th Edition](http://shop.oreilly.com/product/0636920036357.do)

</details>

