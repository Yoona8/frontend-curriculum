# Review progress and questions I have to review
## 12, ..., 25 Feb 2021 (04, 11, 18 Mar)
### JavaScript
<details>
<summary>What are local and session storages and what is the difference?</summary>

- simple key-value store
- local storage lives till either user or browser (when ran out of space) clears it
- session storage lives in the browser while you don't close the tab

</details>

<details>
<summary>What are local and session storages good for?</summary>

- manage user preferences or basic user data
- simple, easy to use, but bad for complex data

</details>

<details>
<summary>How are local and session storages being cleared?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to work with the local storage?</summary>

```JavaScript
// local storage works sync
const userId = '775';
const user = {
  name: 'Harry',
  age: 33
};

// JS converts data into a string
localStorage.setItem('userId', userId);
localStorage.setItem('user', user); // => [object Object]
localStorage.setItem('user', JSON.stringify(user));

// to get item
localStorage.getItem('user');
```

</details>

<details>
<summary>How to work with the session storage?</summary>

```JavaScript
// session storage works sync

// JS converts data into a string
sessionStorage.setItem('userId', userId);
sessionStorage.setItem('user', JSON.stringify(user));

// to get item
sessionStorage.getItem('user');
```

</details>

## 13, ..., 27 Feb 2021 (06, 13, 20 Mar)
### JavaScript
<details>
<summary>What are cookies and the difference from local/session storage?</summary>

- cookie stored to server
- simple key-value store with some config options
- not as easy to use
- the advantage is that you can set it to expire or send to a server
- available only if your app is served on a running server

</details>

<details>
<summary>What are cookies good for?</summary>

- manage user preferences or basic user data
- bad for complex data

</details>

<details>
<summary>How to clear the cookies?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to use cookies?</summary>

```JavaScript
// cookies work sync
const userId = 'fd3928';
const user = {
  name: 'Harry',
  age: 33
};
// data stored as a string
// under the hood uses a setter
// so adds new cookie, not overrides
document.cookie = `userId=${userId}; max-age=360`; // => seconds
document.cookie = `user=${JSON.stringify(user)}; expires=date`; // => date

// to get info
// returns all the cookies stored in one string
document.cookie;
```

</details>

## 14, ..., 28 Feb 2021 (07, 14, 21 Mar)
### JavaScript
<details>
<summary>What is IndexedDB?</summary>

- client-side database

</details>

<details>
<summary>What is IndexedDB good for?</summary>

- manage complex data your app needs
- not as easy to use, great for complex (non-critical) data, good performance (good for usage like google sheets)

</details>

<details>
<summary>How to clean the IndexedDB?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to use IndexedDB?</summary>

```JavaScript
// indexedDB works sync
// pass name and version
// creates or opens an existed DB
const dbRequest = indexedDB.open('Name', 1);
let db;

// to be able to change the data from a button too
dbRequest.onsuccess = function(evt) {
  // access to the created database
  db = evt.target.result;
};

// for better browser support not .addEventListener, but:
// this event runs when the db is created or the version is upgraded
dbRequest.onupgradeneeded = function(evt) {
  db = evt.target.result;
  const objStore = db.createObjectStore('products', {keyPath: 'id'});

  // oncomplete triggers when createObjectStore is finished
  objStore.transaction.oncomplete = function(evt) {
    // connecting to the data base
    // name of the store + mode (readonly, readwrite, etc)
    const productsStore = db.transaction('products', 'readwrite')
      .objectStore('products');
    // adding a new item, has to have the property from keyPath
    productsStore.add({
      id: 'pr1',
      name: 'Product 1',
      price: 1.22,
      tags: ['Vegetarian', 'No-Sugar']
    });
  };
};

dbRequest.onerror = function() {};

addButton.addEventListener('click', () => {
  if (!db) {
    return;
  }

  const productsStore = db.transaction('products', 'readwrite')
    .objectStore('products');

  productsStore.add({
    id: 'pr2',
    name: 'Product 2',
    price: 1.42,
    tags: ['Vegetarian', 'No-Sugar']
  });
});

// to retrieve the data
getButton.addEventListener('click', () => {
  const productsStore = db.transaction('products', 'readwrite')
    .objectStore('products');

  const request = productsStore.get('pr1');

  request.onsuccess = function() {
    console.log(request.result);
  };
});
```

</details>

## 23, ..., 01 Mar 2021 (05, 12, 19, 26 Mar)
### Angular
<details>
<summary>What are the core ideas behind Angular?</summary>

- components - building blocks to compose the application
- templates - cleanly separate the application's logic from its presentation
- dependency injection - allows to declare the dependencies without caring about their instantiation, write more testable and flexible code

</details>

<details>
<summary>How to build the application?</summary>

```bash
# build for production
ng build --prod
```

</details>

<details>
<summary>How to build and serve the application?</summary>

```bash
# run the app in dev mode
ng serve
```

</details>

<details>
<summary>How to generate or modify files?</summary>

```bash
# create a component
ng g c <component-name or path + name>

# create a directive
ng g d <directive-name>

# generate one more application
ng generate application <application-name>

# generate a library
ng generate library <library-name>
```

</details>

<details>
<summary>How to run unit tests?</summary>

```bash
ng test
```

</details>

<details>
<summary>How to build, serve and run e2e tests?</summary>

```bash
ng e2e
```

</details>

<details>
<summary>What is a component?</summary>

- a TypeScript class with `@Component()` decorator, HTML template and styles

</details>

<details>
<summary>How to create a basic component?</summary>

```TypeScript
// app/app.module.ts
import { NgModule } from '@angular/core';
import { NameComponent } from './components/name/name.component';

@NgModule({
  declarations: [NameComponent]
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
export class NameComponent {}
```
```HTML
<!-- app/components/name/name.component.html -->
<app-name></app-name>
<p appDir></p>
<p class="class"></p>
```

</details>

<details>
<summary>How is data binding implemented in Angular?</summary>

```TypeScript
// app/components/name/name.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  templateUrl: './name.component.html',
  styleUrls: ['./name.component.css']
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
<!-- data-binding - communication between business logic and view -->
<!-- no multiline expressions -->
<!-- resolved to a string -->
<!-- updated dynamically at runtime -->
<!-- string interpolation -->
<p>{{ title }}</p> <!-- Hello from name component! -->
<!-- property binding -->
<p [innerText]="title"></p>
<!-- DON'T! improper usage -->
<p [innerText]="{{ title }}"></p>

<!-- event-binding - reaction to events -->
<!-- $event - browser event of type Event -->
<button type="button" (click)="onButtonClick($event)">Click</button>

<!-- two-way binding -->
<!-- triggers input data and updates BL -->
<!-- when BL is updated programmatically, updates the input -->
<!-- but have to import FormsModule on module level -->
<input type="text" [(ngModel)]="name">
<p>{{ name }}</p>
```

</details>

<details>
<summary>How to bind to a custom property (component interaction parent to child)?</summary>

```TypeScript
// app/components/child/child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent {
  // to allow access from the outside
  // (by default props are accessible
  // only from the inside of the component)
  // if object = same object (reference type)
  @Input() user: object;
  @Input('fieldLabel') label: string;
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<app-child [user]="{ name: 'Lala' }" fieldLabel="E-mail"></app-child>
```

</details>

## 26, ..., 02 Mar 2021 (04, 08, 15, 22, 29 Mar)
### JavaScript
<details>
<summary>When do you need to use meta-programming?</summary>

- advanced concepts used mostly when you create libraries

</details>

<details>
<summary>What are Symbols and how to use them?</summary>

- primitive values
- used as keys in objects
- built-in symbols and creatable symbols
- uniqueness is guaranteed
```JavaScript
const userId = Symbol(); // => Symbol()
const playerId = Symbol('id'); // => Symbol(id)

const player = {
  [playerId]: 1, // can't access this property out of library
  name: 'Harry',
  level: 11
};

// can use inside the library
player[playerId] = 2;

console.log(playerId === Symbol('id')); // => false

// built-in symbol
const user = {
  name: 'Ron',
  level: 9,
  [Symbol.toStringTag]: 'User'
};

console.log(user.toString()); // => [object User]
```

</details>

## 01, ..., 02 Mar 2021 (03, 05, 07, 11, 18, 25, 01 Apr)
### JavaScript
<details>
<summary>What are Iterators and how to use them?</summary>

- create your own iterable values
- iterables use it internally
- iterator is an object which has `next()` method
```JavaScript
const player = {
  currentFriend: 0,
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
  next() {
    if (this.currentFriend >= this.friends.length) {
      return {value: this.currentFriend, done: true};
    }

    const result = {
      value: this.friends[this.currentFriend],
      done: false
    };

    this.currentFriend++;
    return result;
  }
};

console.log(player.next());
console.log(player.next());
console.log(player.next());
console.log(player.next());

// still can't use for loop, but while is ok
let friend = player.next();

while(!friend.done) {
  console.log(friend.value);
  friend = player.next();
}
```

</details>

## 02 Mar 2021 (03, 04, 06, 08, 12, 19, 26, 02 Apr)
### JavaScript
<details>
<summary>What is API?</summary>

- API (Application Public Interface)
  - a set of available properties and methods to solve a particular task
  - frequent implementation - objects

</details>

<details>
<summary>What are statements?</summary>

- syntax constructs and commands that perform actions
- can be separated with `;`
- usually written on separate lines
```JavaScript
console.log('Hello!');
```

</details>

## 03 Mar 2021 (04, 05, 07, 09, 13, 20, 27, 03 Apr)
- next time start JS with Numbers section