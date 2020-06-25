# Frontend Curriculum

## HTML

Main root
Metadata
Sectioning root
Content sectioning

<details>
<summary>Text content</summary>

|Element|Usage and notes                                     |Level|
|-------|----------------------------------------------------|-----|
|`<ol>` |`start`, `reversed` bool attributes change the order|

</details>

<details>
<summary>Inline text semantics</summary>

|Element|Usage and notes                                     |Level|
|-------|----------------------------------------------------|-----|
|`<q>`  |`cite="https://..."` can cite the e-address also    |

</details>

Images and multimedia
Embedded content
Scripts
Tables
Forms
Interactive elements
Web components

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
<summary>Text HTML and CSS</summary>

```HTML

<!-- ISO for computers, text for humans -->
<ins datetime="ISO string format">Today</ins> 
<del datetime="ISO string format">Today</del> 
<time datetime="ISO string format">Today</time> 
```

</details>

## CSS

<details>
<summary>CSS basics</summary>

- `max-width` counts of parent
- `em` depends on element's font-size

</details>

<details>
<summary>Text HTML and CSS</summary>



|Value        |Usage                     |Description              |
|-------------|--------------------------|-------------------------|
|`font-weight`|`bold`                    |                         |
|             |`400`, `500`, `700`       |                         |
|             |`bolder`, `lighter`       |from current or inherited|
|`font-size`  |`14px`, `2em`, `3rem`

```CSS
/* text styling */
.element {
  /* px, small, xx-small - absolute */
  /* em, larger, smaller - from parent */
  /* rem - from <html> */
  font-size: 14px;
  /* px, (%, coefficient - from font-size) */
  line-height: normal; /* default */
  /* monospace, serif, cursive, fantasy */
  font-family: "PT Sans", "Arial", sans-serif;
  /* end, left, right, center, justify */
  text-align: start;
  /* vertical-rl, vertical-lr */
  /* italic, oblique ('pseudo-italic' made by browser) */
  font-style: normal; /* default */
  /* uppercase, lowercase, capitalize */
  text-transform: none;
  writing-mode: horizontal-tb; /* default */
  /* top, middle, bottom, %, px */
  /* for inline element regarding the line */
  /* used on element, not container */
  /* px or % of line-height */
  /* 0% = 0px = baseline (almost) */
  /* px like %, counts > or < side */
  vertical-align: baseline; /* default */
  /* #fff(fff)(ff), rgb(a), hsl(a) */
  color: #ffffff;
  /* nowrap */
  /* pre, pre-wrap = <pre> (pre-wrap to new line if overflow) */
  /* break-spaces = pre-wrap, but doesn't touch reserved space */
  /* pre-line = normal, but breaks lines on line-break symbol */
  white-space: normal; /* default */
  /* break-word */
  overflow-wrap: normal;
  /* em, rem, pt */
  letter-spacing: 2px;

  /* indent of the 1st line of the text block (of width) */
  /* +- px, em, pt */
  text-indent: 10%;

  text-decoration: underline;
  /* line-through, overline, none */
  text-decoration-line: underline;
  /* double, dotted, dashed, wavy */
  text-decoration-style: solid;
  /* #fff(fff)(ff), rgb(a), hsl(a) */
  text-decoration-color: #ffffff;

  /* x y r-blur (0 default) color (text color default) */
  /* could be several */
  text-shadow: 1px 1px 1px #000000;
}
```

```CSS
/* columns */
.element {
  /* int, separates block into equal columns of text */
  column-count: 2;
  /* min width, if column-count is undefined, browser separates into max available width */
  column-width: 200px;
  column-gap: 1em; /* default */
}
```

```CSS
/* text directions */
.element {
  /* rtl also available, changes columns order, scrollbar position */
  direction: ltr;
  /* normal - according to used symbols */
  /* embed - according to set direction */
  /* bidi-override - overrides according direction */
  unicode-bidi: normal;
  /* clip - cuts on container size */
  /* ellipsis - adds ... in the end */
  /* applies only if: 1 - one-line block; 2 - overflow is initiated */
  text-overflow: clip;
  /* em, rem, %, ch between words +-, could be used also for inline-blocks and images */
  word-spacing: 20px;
}
```

</details>

<details>
<summary>Embedded content tags</summary>

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

```HTML
<figure>
  <figcaption>1st or last in parent</figcaption>
</figure>
```

```HTML
<!-- preload metadata - служебная дата (length, 1 slide) -->
<!-- preload auto - whole video -->
<!-- poster - img when not yet loaded -->
<video 
  width="500" height="300"
  src="#"
  controls
  autoplay
  poster="#"
  preload="none/metadata/auto"
>
  <!-- diff available, first loads first which could be played -->
  <!-- type can also contain codec, browser could do it, but not always the right way -->
  <source src="video.mp4" type="video/mp4"></source>
  <source src="#" type="MPEG-4/H.264"></source>
  <source src="#" type="OGG/Theora"></source>
  <source src="#" type="WebM"></source>
</video>
```

```HTML
<!-- almost like video -->
<audio controls preload="" src="#" autoplay>
  <source src="#" type="MP3"></source>
  <source src="#" type="OGG"></source>
</audio>
```

</details>

<details>
<summary>Tables in HTML and CSS</summary>

- by default `<table>` shrinks to content

```HTML
<table>
  <!-- should be the first child -->
  <caption>Header</caption>
  <tr>
    <!-- colspan for horizontal expanding -->
    <!-- moves right cell, have to delete in html -->
    <td colspan="2">Name 1</td>
    <!-- rowspan for vertical expanding -->
    <!-- moves lower cell in it's own row to right -->
    <td rowspan="2">Value 1</td>
    <td>Count 1</td>
  </tr>
  <tr>
    <td>Name 1</td>
    <td>Value 1</td>
    <td>Count 1</td>
  </tr>
</table>
```

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

<details>
<summary>Forms</summary>

- `autofocus` only one attribute for the whole page
- `pattern` regexp, if incorrect - validation error
- `readonly` can't change but can select and copy, <b>posts to the server</b>
- `disabled` can't change, focus, select or copy, <b>doesn't post to the server</b>

```HTML
<!-- name will also get posted to server -->
<button type="submit" name="some-name"></button>

<!-- rows - strings -->
<!-- cols - symbols -->
<textarea rows="10" cols="100"></textarea>

<!-- good for support needs -->
<input type="hidden">

<!-- for working with files enctype required -->
<form enctype="multipart/form-data">
  <!-- name is required -->
  <input type="file" name="avatar">
</form>

<!-- image input = submit + sends the click coordinates on the image -->
<input type="image" src="#" alt="Some description">

<!-- dates inputs -->
<!-- if browser doesn't support, shows text field -->
<input type="date"> <!-- with locale -->
<input type="time"> <!-- with locale -->
<input type="datetime"> <!-- with time zone -->
<input type="datetime-local"> <!-- w/o time zone -->
<input type="week"> <!-- N of week, year -->
<input type="month"> <!-- month + year -->

<!-- number input -->
<!-- doesn't have min/maxlength -->
<!-- step is applied by clicking arrows, out of step - validation error -->
<!-- number keyboard on mobile -->
<input type="number" min="0" max="100" step="10">

<!-- search almost like text, in some browsers has a cross -->
<input type="search">

<!-- still has no multiple handles -->
<input type="range" min="0" max="100" step="10">

<!-- good with patterns -->
<!-- tel keyboard on mobile -->
<input type="tel">

<!-- validation for correct urls, emails -->
<!-- proper keyboard on mobile -->
<input type="email">
<input type="url">

<!-- opens special pallette with colors -->
<!-- if browser doesn't support = text field -->
<input type="color">

<!-- allow/block browser autocomplete option -->
<input autocomplete="on">
<input autocomplete="off">

<!-- data lists with inputs (like select on type) -->
<!-- connected viw list of input and id of datalist -->
<!-- if inputs type != text, shows only correct items -->
<input type="text" list="browsers" name="browsers">
<datalist id="browsers">
  <option>Google Chrome</option>
  <option>Mozilla Firefox</option>
  <option>Edge</option>
  <option>Opera</option>
</datalist>

<!-- value accessible from js vie element.value -->
<output name="some-name">{default}</output>

<!-- disabled for all the fields inside -->
<fieldset disabled>
  <!-- first child -->
  <legend>Title</legend>
</fieldset>

<!-- multiple - ctrl/cmd to choose with -->
<!-- multiple + size to change height -->
<select multiple size="10">
  <!-- selected to choose value, could be several -->
  <!-- value ? value : text content goes to server -->
  <option selected>Option 1</option>
  <option selected value="option2">Option 2</option>
  <option>Option 3</option>
  <!-- could have group children -->
  <!-- could be used with multiple select -->
  <optgroup label="Group 1">
    <option selected>Option in a group 1</option>
    <option>Option in a group 2</option>
  </optgroup>
</select>
```

</details>

<details>
<summary>Selectors</summary>

```CSS
/* pseudo classes */

/* :not can use */
.element:not(:last-child) {}
.element:not(p):not(#id) {}
.element:not([attribute]) {}
.element:not(.class) {}
/* :not cannot use */
.element:not(:not()) {}
.element:not(.class-one.class-two) {}
.element:not(::after) {}
.element:not(a span + span ~ span) {} /* any combined selector */

/* from last */
.element:nth-last-child {}
/* if the 2nd element is ul, choses, otherwise no */
ul:nth-child(2) {}

/* with type in mind */
.element:first-of-type {}
.element:last-of-type {}
/* 2nd of type */
.element:nth-of-type(2) {}
.element:nth-last-of-type(2) {}

/* no element or text inside */
.element:empty {}

/* only one child */
.element:only-child {}

/* only one p inside a parent */
p:only-of-type {}
```

```HTML
<body>
  <div></div> <!-- ul:first-child = nothing-->
  <ul></ul> <!-- ul:first-of-type ul:nth-child(2) -->
  <ul></ul> <!-- ul:last-of-type ul:nth-of-type(2) -->
</body>
```

```CSS
/* pseudo elements */
.element::first-line {}
.element::first-letter {}

/* mostly used */
.element::before {}
.element::after {}
```

```CSS
/* attribute selectors */
/* exact */
[type="text"] {}
/* starts with 'bar' */
[foo^="bar"] {}
/* ends with 'bar' (good for docs .jpg) */
[foo$="bar"] {}
/* contains 'bar' */
[foo*="bar"] {}
/* 'bar' is a separate word */
[foo~="bar"]
/* prefix 'bar', the value has to be either alone or followed by '-' */
[foo|="bar"]
```

```CSS
/* state selectors */
.element:enabled {}
.element:disabled {}
.element:read-write {}
.element:read-only {}
.element:required {}
.element:optional {}
.element:checked {}
.element:valid {}
.element:invalid {}
.element:in-range {}
.element:out-of-range {}
```

</details>

<details>
<summary>Block model</summary>

- block (full width, new line width/height, paddings, margins)
  - vertical margins collapse to the more value (parent 40px, child 60px = 60px after collapse)
  - vertical margins drop out of parent if parent doesn't have paddings or borders and it's margin is < child's margin
  - horizontal margins do not collapse
- phrasing (width = content, only horizontal paddings, margins)
- input's width by default = `[size]` attribute, doesn't grow into full parent's width
- `display: none;` removes element + makes una11y
- `visibility: hidden;` hides the element, but the place is still there, makes una11y

</details>

<details>
<summary>Floats</summary>

- basically used to float elements with text
- `float: left/right/none;`
- adds sizes to phrasing elements too
- shrinks to content
- drops out of flow (partially)
  - block elements after float stop reacting oon float, go up like with `position: absolute;`
  - inline elements float around the empty side of float element
  - if all blocks are floats, parent shrinks to 0 height
- floats see each other, drop to the next line, but sometimes 'chains' and positions below one of the random floats (awkward behavior)
- `clear: left/right/both/none;` forbids floating, if after float - sees it (clearfix pattern)

</details>

<details>
<summary>Flexbox</summary>

```CSS
.element {
  /* positive int */
  /* free space according to coefficient */
  /* flex-grow + min-width (no min-width = elem could drop out of parent if other elem-s have flex-shrink: 0) */
  flex-grow: 0;
  /* positive int number */
  /* free shrink according to coefficient */
  /* not to shrink = 0 */
  /* only content shrinks (not paddings or borders) */
  /* flex-shrink + multiline flex (only 1 element > container width) */
  flex-shrink: 1;
  /* combined property, has problems in some browsers */
  /* flex-grow flex-shrink flex-basis */
  /* 0 1 auto */
  flex: initial;
  /* 1 1 auto */
  flex: auto;
  /* 0 0 auto */
  flex: none;
  /* 1 0 0% */
  flex: 1 0;
  /* 1 1 0% */
  flex: 1;
  /* min and max sizes apply after all the above (in the very end) */
}
```

</details>

<details>
<summary>Grid</summary>

- children become parent's grid elements
- elements position on the 2d grid between lines
- grids could be layered (default - order in HTML)
- `z-index` changes layering

```CSS
.parent-element {
  display: grid;
}

/* starts from 4 vertical and 3 horizontal lines */
/* if end is undefined, ends on next line */
.child-element {
  grid-column-start: 4;
  grid-row-start: 3;
}

.child-element {
  grid-column-start: 3;
  grid-column-end: 5;
  grid-row-start: 2;
  grid-row-end: 4;
  /* the same, but shorter */
  grid-column: 3 / 5;
  grid-row: 2 / 4;
  /* when used without 2nd param, will behave like -start properties */
  grid-column: 3;
  grid-row: 2;
}
```

</details>

<details>
<summary>Positioning</summary>

```CSS
.element {
  /* when extends browser's borders */
  position: absolute;
  /* by default coords = auto */
  /* no scroll */
  top: -5px;
  left: -5px;
  /* with scroll */
  bottom: -5px;
  right: -5px;
}
```

</details>

<details>
<summary>Backgrounds</summary>

- when multiple - 1st is upper

```CSS
.element {
  /* #fff(fff)(ff) rgb(a) hsl(a) */
  background-color: #ffffff;
  /* image layers on color */
  background-image: url('bg.jpg');
  /* repeat-x(y) no-repeat */
  /* round - repeated parts shrink or grow */
  /* space - adds space between */
  /* could be different by x or y */
  background-repeat: repeat;
  /* x y */
  /* left center right top bottom */
  /* 50% 50px +- */
  /* right 30px top 20px - from any block corner */
  background-position: 50% 100%;
  /* fixed - adds very simple effect */
  background-attachment: scroll;
  /* 100px, 100% 50% */
  /* contain - reserves proportions, max sizes with full fill possible, could not cover the whole container */
  /* cover - reserves proportions, min possible sizes to cover the whole container, */
  /* if block and img proportions are different, img cuts */
  background-size: auto auto;
  /* padding-box (-borders) */
  /* border-box (+padding+borders) */
  /* content-box (-padding-borders) */
  background-origin: padding-box;
  /* border-box doesn't cut */
  /* padding-box cuts till borders */
  /* content-box cuts with paddings */
  background-clip: border-box;
  /* complex property order */
  background: [bc] [bi] [br] [bp] [ba];
}
```

</details>

Borders and outlines
Shadows
Gradients
Transformations
Transitions
Animations

## A11y

## JavaScript

<details>
<summary>ECMAScript</summary>

Global changes:
- new strategy of spec updating
- problem concepts
  - hoisting
  - `var` rewriting
  - scope (var with no block-scope)
- new opportunities
  - `let`, `const` - hoisting, scope, rewriting solved
  - template strings
  - function default params
  - arrow functions
  - destructuring
- better objects

</details>

<details>
<summary>Constants and variables</summary>

```JavaScript
// constants - code agreements
// protected values, hardcoded (default configs, physical consts, coefficients)
// distinguished by it's appearance
// any constant declares as a const
// is immutable
const Earth = {
  RADIUS: 6.371,
  GRAVITATION: 6.67408
};
const DEFAULT_NAMES = ['Michael', 'Anna', 'Chris'];
const LIGHT_SPEED = 255792458;

// consts
// not any const = constant
// declares a variable with immutable link
const element = document.querySelector('p');
const arr = [1, 2, 3, 4];
```

</details>

Data structures
Numbers
Strings
Iterables
Objects
Constructors and prototypes
Classes
Operators

<details>
<summary>Functions</summary>

```JavaScript
// default params
// Earlier
var doSomething = function (caption, amount, isChecked) {
  if (typeof isChecked === 'undefined') {
    isChecked = false;
  }
};

// ES2015
const doSomething = (caption, amount, isChecked = false) => {
  // some code here
};
```

- doesn't have it's own scope (only lexical) - when global, `this === window`
- doesn't have `arguments` object
- can't rewrite `this` (`bind` and `call` won't work)
  - can't be used as a constructor, no `new` keyword
  - can't be method of an object or prototype

```JavaScript
// arrow functions
// only 1 param?
const doSomething = param => console.log(param);

// only 1 line?
// = return left * right;
const doSomething = (left, right) => left * right;

// return object?
const getWizard = (name, level) => ({
  name,
  level
});
```

</details>

Control structures
Modules
DOM

<details>
<summary>Events</summary>

- difference between `change` and `input`
  - `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
  - `input` works with every value change

</details>

<details>
<summary>Other</summary>

- cycle is more optimal than a recursion (call stack overflow), any recursion could be rewritten into a cycle

</details>

<details>
<summary>Async JavaScript (promises and callbacks, async/await)</summary>

  - <details>
    <summary>Sync data loading</summary>

    ```JavaScript
    const getResponse = (url) => {
      const xhr = new XMLHttpRequest();
      xhr.open('GET', url, false);
      xhr.send();
      // we can do it like that, because it's a sync request
      // return will happen after we get the response
      return xhr.response;
    };
    const data = getResponse('https://data.com/users');
    ```

    </details>
  
  - Async ES5 (callbacks)
  - Async ES6 (promises) 

</details>

Http requests
Browser storage
Meta-programming
Performance and optimizations
Security
Deploying
Testing
Debugging
Browser support
Tools and workflow
Libraries
Frameworks

## OOP

Inheritance and polymorphism
Data-binding

## Procedural programming

## Functional programming

## Data structures and Algorithms

## TypeScript

## Angular

<details>
<summary>Setup with Angular CLI</summary>

- install node + npm
- install angular CLI
- global style files could be added to `angular.json`
```bash
# create a project
ng new <project-name>

# run the app
ng serve

# create a component
ng g c <component-name or path + name>

# create a directive
ng g d <directive-name>
```

</details>

<details>
<summary>How the app is being built?</summary>

- don't import with .ts extensions, webpack adds it
```TypeScript
// main.ts
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```
```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
  // should be known components when Angular analyses index.html
  bootstrap: [AppComponent]
})
export class AppModule {}
```
```TypeScript
// app/app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: '...'
})
export class AppComponent {}
```
```HTML
<!-- index.html -->
<!doctype html>
<html>
<head></head>
<body>
  <app-root></app-root>
</html>
```

</details>

<details>
<summary>Components</summary>

- `declarations: [NameComponent]` add to module
- `<app-name></app-name>` or `<p appDir></p>` or `<p class="class"></p>` add to view
- data-binding - communication between business logic and view
- updates dynamically at runtime
- event-binding - reaction to events
- two-way binding - needs a FormsModule

```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';

@NgModule({
  imports: [FormsModule]
})
export class AppModule {}
```

```TypeScript
// app/components/name/name.component.ts
import { Component } from '@angular/core';

@Component({
  // required, must be a unique string
  selector: 'app-name', // tag, mostly for components
  selector: '[appDir]', // attribute, mostly for directives
  selector: '.class', // can also use a class as a selector
  // required, only one of
  template: '<p>Some text</p>',
  templateUrl: './name.component.html',
  // optional, only one of
  styles: '',
  styleUrls: ['./name.component.css'] // scss / less also possible
})
export class NameComponent {
  title: string = 'Hello from name component!';
  name: string = 'Max';

  onButtonClick(evt: Event) {
    console.log(evt.target);
  }
}
```
```HTML
<!-- app/components/name/name.component.html -->

<!-- data-binding -->
<!-- no multiline expressions -->
<!-- resolved to a string -->
<!-- updated dynamically -->
<!-- string interpolation -->
<p>{{ title }}</p> <!-- Hello from name component! -->
<!-- property binding -->
<p [innerText]="title"></p>
<!-- DON'T! improper usage -->
<p [innerText]="{{ title }}"></p>

<!-- event-binding -->
<!-- $event - browser event of type Event -->
<button type="button" (click)="onButtonClick($event)">Click</button>

<!-- two-way binding -->
<!-- triggers input data and updates BL -->
<!-- when BL is updated programmatically, updates the input -->
<input type="text" [(ngModel)]="name">
<p>{{ name }}</p>
```

</details>

Directives
Models
Services
Routing
Pipes
Forms (Template Driven)
Forms (Reactive)

<details>
<summary>Modules</summary>

- bundles different pieces into one package
- custom modules mostly for big projects
- gives Angular info on which features to use
```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';

@NgModule({
  // components, directives, pipes
  declarations: [],
  // modules
  imports: [],
  // root needed on start component
  bootstrap: [],
  // services, interceptors
  providers: []
})
export class AppModule {}
```

</details>

Observables
Http
Authentication
Offline
Testing

<details>
<summary>Debugging</summary>

- find an error in the console
- using sourcemaps and breakpoints in browser
  - `sources` => `webpack` => `.` => `src`
- using `debugger;`
- using chrome extension Augury (access from dev tools)

</details>

Deploy
Animation
Universal

## React

## Canvas API

## WebGL and animations

## Graphics

<details>
<summary>SVG</summary>

- optimization
  - use fewer nodes
  - fewer handlers
  - integer numbers
  - not too big grid
- sprites
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

## Serverless

## Firebase

<details>
<summary>Basic setup</summary>

- firebase.google.com
- console.firebase.com
- add project, default settings
- navigate to database => realtime database => create database
- choose start in test mode (when your auth functional is not ready yet)
- URL in the head is where to send a request
- to simulate errors change some rules to false (database => rules)

</details>

<details>
<summary>Authentication</summary>

- database => rules
- set the rule you need to `auth != null`
- authentication => set up sign-in method
- choose email/password => enable only top switch
- users tab - all the users
- find docs on Auth REST API

</details>

## Web components

## Chrome Dev Tools

<details>
<summary>Shortcuts and tips</summary>

- Shortcuts (menu => shortcuts)
  - `ctrl + F` search (by any word)
  - `ctrl + shift + F` search across all sources
  - `tab` `tab + shift` step forward / back when adding changes
  - `H` hide chosen element of the html (adds `visibility: hidden;`)
  - `F2` to be able to edit html
  - `+` in styles will create a selector for the element
  - `shift + click` on color will change it's output
- `document.body.contentEditable = true;`
- can change sizes in the block with metrics
- in the device emulation can pick pixel density
- settings => coverage lets to see all the rules, which are not applied to the page

</details>

## Webpack

<details>
<summary>Basic config</summary>

- install npm first
- for working with styles import css file into js file, where we use the styles, by default webpack's css loader adds `<link rel="stylesheet">`

```bash
# for webpack usage
$ npm i -DE webpack
$ npm i -DE webpack-cli

# optional, if dev server needed
$ npm i -DE webpack-dev-server
```

```JavaScript
// webpack.config.js
// for the proper path configs for different OS
const path = require('path');

module.exports = {
  // build mode
  mode: 'development',
  // application entry point
  entry: './src/main.js',
  // settings for the output file
  output: {
    filename: 'bundle.js',
    // __dirname is a root directory of out app
    path: path.join(__dirname, 'public')
  },
  devtool: 'source-maps',
  devServer: {
    // where to look for a build
    contentBase: path.join(__dirname, 'public'),
    // detects changes in js files and reloads a page
    watchContentBase: true
  },
  module: {
    rules: [{
      // what files to look for (.scss, .css here)
      test: /\.s?css/,
      // style-loader handles the importing of the files (injects css into DOM as link tag by default)
      // css-loader handles the css code (resolves the css file)
      // order matters (which loader to use)
      use: ['style-loader', 'css-loader']
    }]
  }
};
```

```JavaScript
// component.js
import "./src/style.css";
```

</details>