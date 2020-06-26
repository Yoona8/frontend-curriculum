# Frontend Curriculum

## Content
- [HTML](html.md)
- [CSS](css.md)

## Reference

<details>
<summary>Levels</summary>

- :seedling: - to learn
- :deciduous_tree: - common
- :blossom: - good

</details>

## CSS

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