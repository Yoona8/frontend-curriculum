# Frontend Curriculum

## Content
- [HTML](html.md)
- [CSS](css.md)
- A11y
- [Graphics](graphics.md)
- [JavaScript](javascript.md)

## Reference

<details>
<summary>Levels</summary>

- :seedling: - to learn
- :deciduous_tree: - common
- :blossom: - good

</details>

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