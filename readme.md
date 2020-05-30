# Frontend Curriculum

## HTML CSS

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
<summary>CSS basics</summary>

- `max-width` counts of parent
- `em` depends on element's font-size

</details>

<details>
<summary>Text HTML and CSS</summary>

```HTML
<!-- bool for changing the order -->
<ol start></ol>
<ol reversed></ol>

<!-- cite the address -->
<q cite="https://..."></q>

<!-- ISO for computers, text for humans -->
<ins datetime="ISO string format">Today</ins> 
<del datetime="ISO string format">Today</del> 
<time datetime="ISO string format">Today</time> 
```

</details>

<details>
<summary>Embedded content tags</summary>

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

Tables in HTML and CSS

<details>
<summary>Forms</summary>

```HTML
<!-- name will also get posted to server -->
<button type="submit" name="some-name"></button>

<!-- rows - strings -->
<!-- cols - symbols -->
<textarea rows="10" cols="100"></textarea>
```

</details>

Selectors
Block model
Floats
Flexbox
Grid
Positioning
Backgrounds
Borders and outlines
Shadows
Gradients
Transformations
Transitions
Animations

## JavaScript

ECMAScript
Constants and variables
Data structures
Numbers
Strings
Iterables
Objects
Constructors and prototypes
Classes
Operators
Functions
Control structures
Modules
DOM
Events

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

// app/app.module.ts
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
  // should be known components when Angular analyses index.html
  bootstrap: [AppComponent]
})
export class AppModule {}

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

## React

## Canvas API

## WebGL and animations

## Graphics

SVG

## Serverless

## Firebase

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
