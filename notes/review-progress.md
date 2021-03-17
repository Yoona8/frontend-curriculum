# Review progress and questions I have to review
## 12, ..., 11 Mar 2021 (18 Mar)
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

## 13, ..., 13 Mar 2021 (20 Mar)
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

## 14, ..., 14 Mar 2021 (21 Mar)
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

## 23, ..., 12 Mar 2021 (19, 26 Mar)
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

## 26, ..., 15 Mar 2021 (22, 29 Mar)
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

## 01, ..., 11 Mar 2021 (18, 25, 01 Apr)
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

## 02, ..., 12 Mar 2021 (19, 26, 02 Apr)
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

## 03, ..., 13 Mar 2021 (20, 27, 03 Apr)
### JavaScript
<details>
<summary>How to create an Array?</summary>

```JavaScript
// ES5
// 1
var numbers = new Array(3, 5); // => [3, 5]
var emptyArray = new Array(3); // => [] with length === 3
// 2
var numbers2 = Array(3, 5);
var emptyArray2 = Array(3);
// 3
var letters = ['a', 'r']; // => ['a', 'r']
// 4 clones array and adds values from another array
const newNumbers = numbers.concat([8, 5, 2]);

// ES6+
// 5 makes an array of any iterable (collection, separate values)
const elements = Array.from(document.querySelectorAll('li'));
const letters = Array.from('string');
// 6 of separate values
const values = Array.of(1, 2, 3);
// 7
const items = [...elements, ...values];
```

</details>

<details>
<summary>How to make an Array of a string?</summary>

```JavaScript
const text = 'One two three';
const words = text.split(' '); // => ['One', 'two', 'three']
const symbols1 = Array.from(text); // => ['O', ..., ' ', 't', ...]
const symbols2 = [...text]; // => ['O', ..., ' ', 't', ...]
```

</details>

<details>
<summary>How to make a string of an Array?</summary>

```JavaScript
const words = ['one', 'two', 'three'];
// by default separates with ,
const text = words.join();
const text2 = words.join(' ');
```

</details>

<details>
<summary>How to delete or add an element from (to) an Array at any position?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// start index, delete count, value to add (or more 10, 15)
const removedElements = numbers.splice(1, 0, 10); // => [1, 10, 2, 5]
// removes from the end
const removedElements2 = numbers.splice(-1, 1); // => [1, 2]
// will delete all items starting with the provided index
const removedElements3 = numbers.splice(0);
```

</details>

<details>
<summary>How to sort items in an Array?</summary>

- changes the initial array
```JavaScript
const numbers = [1, 2, 5];
// by default converts to a string and sorts characters
const sortedDefault = numbers.sort();
const sortedNumbers = numbers.sort((a, b) => {
  if (a > b) {
    // or any positive value
    return 1;
  } else if (a === b) {
    return 0;
  } else {
    // or any negative value
    return -1;
  }

  // or
  return a - b;
});
```

</details>

<details>
<summary>How to copy an Array or a part of it?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
// copy an array
const clonedNumbers = numbers.slice();
// copy starting from index till the end
const clonedNumbers2 = numbers.slice(2);
// end item not included
const clonedNumbers3 = numbers.slice(0, 2); // => [1, 2]
// [] if nothing is in between
const emptyNumbers = numbers.slice(3, 2);
const emptyNumbers2 = numbers.slice(-3, -4);
// from the end
const clonedPartOfNumbers = numbers.slice(-3, -1); // => [1, 2]
```

</details>

## 06, ..., 16 Mar 2021 (23, 30, 06 Apr)
### Angular
<details>
<summary>How to intercept input property changes with a setter?</summary>

```TypeScript
// app/components/child/child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent {
  private _fieldLabel = '';
  @Input() 
  get fieldLabel(): string { return this._fieldLabel; };
  set fieldLabel(fieldLabel: string) {
    this._fieldLabel = (fieldLabel && fieldLabel.trim()) || 'Unknown Label';
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<!-- E-mail -->
<app-child fieldLabel="E-mail"></app-child>
<!-- Unknown Label -->
<app-child fieldLabel="  "></app-child>
```

</details>

<details>
<summary>How to intercept input property changes with OnChanges and why?</summary>

- you may prefer this approach to the property setter when watching multiple, interacting input properties
```TypeScript
// app/components/child/child.component.ts
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent implements OnChanges {
  @Input() level: number;
  @Input() power: number;
  changeLog: string[] = [];

  ngOnChanges(changes: SimpleChanges) {
    const log: string[] = [];

    for (const propName in changes) {
      const changedProp = changes[propName];
      const to = JSON.stringify(changedProp.currentValue);

      if (changedProp.isFirstChange()) {
        log.push(`Initial value of ${propName} set to ${to}`)
      } else {
        const from = JSON.stringify(changedProp.previousValue);

        log.push(`${propName} changed from ${from} to ${to}`);
      }
    }

    this.changeLog.push(log.join(', '));
  }
}

// app/components/parent/parent.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './'
})
export class ParentComponent {
  level: number = 1;
  power: number = 0;

  increasePower() {
    this.power++;
  }

  increaseLevel() {
    this.level++;
    this.power = 0;
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<button type="button" (click)="increasePower()">Power Up</button>
<button type="button" (click)="increaseLevel()">Level Up</button>
<app-child [level]="level" [power]="power"></app-child>
```

</details>

<details>
<summary>How to pass data from child to parent (listen to child event)?</summary>

- the child exposes an `EventEmitter` property with which it emits events when something happens
- the parent binds to that event property and reacts to those events
```TypeScript
// app/components/child/child.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h2>{{ name }}</h2>
    <button 
      (click)="checkIn(true)" 
      [disabled]="haveChosen" 
      type="button"
    >Check In</button>
    <button 
      (click)="checkIn(false)" 
      [disabled]="haveChosen" 
      type="button"
    >I'm Out</button>
  `
})
export class ChildComponent implements OnChanges {
  @Input() name: string;
  @Output() checkedIn = new EventEmitter<boolean>();
  haveChosen = false;

  checkIn(isIn: boolean) {
    this.checkedIn.emit(isIn);
    this.haveChosen = true;
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<app-child name="Harry" (checkedIn)="onCheckedIn($event)"></app-child>
```

</details>

<details>
<summary>How to use a local reference (inside one component) and what is the limitation?</summary>

- can be used only in the template, not in the component (.ts file)
- returns an HTML element
```HTML
<!-- simple.component.html -->
<input type="text" #locRef>
<button (click)="onButtonClick(locRef)" type="button">Get the input HTML</button>
<p>{{ locRef.value }}</p>
```

</details>

<details>
<summary>How to interact parent > child via local variable (reference) and what is the limitation?</summary>

- parent component cannot use data binding to read child properties or invoke child methods
- can do both by creating a template reference variable for the child element and then reference that variable within the parent template
- accessible only from the template, not from the parent component itself
```TypeScript
// child.component.ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p>{{ message }}</p>'
})
export class ChildComponent {
  message: string = '';

  start() {
    this.message = 'Start in 10 seconds.';
    // some countdown code
  }

  stop() {
    this.message = 'Stopped!';
    // stop the timer code
  }
}
```
```HTML
<!-- parent.component.html -->
<app-child #childComponent></app-child>
<p>{{ childComponent.message }}</p>
<button (click)="childComponent.start()" type="button">Start</button>
<button (click)="childComponent.stop()" type="button">Stop</button>
```

</details>

## 09, ..., 15 Mar 2021 (19, 26, 02, 09 Apr)
### JavaScript
<details>
<summary>How and why to create a queue using an Array (FIFO)?</summary>

- for tasks to be executed in a row after some async event
- for unique actions can use `Set` instead of `Array`
```JavaScript
const callbacks = [];

const addAsyncListener = (fn) => {
  // check if the callback exists (used before set was created)
  if (!callbacks.find((it) => it === fn)) {
    callbacks.push(fn);
  }
};

const startAsync = () => {
  setTimeout(() => {
    for (const cb of callbacks) {
      callbacks.delete(cb);
      cb();
    }

    console.log('Done');
  }, 500);
};

const log2 = () => console.log(2);

addAsyncListener(() => console.log(1));
addAsyncListener(log2);
addAsyncListener(log2); // won't be added to array
addAsyncListener(() => console.log(3));

console.log('Start!');
startAsync();

addAsyncListener(() => console.log(4));
addAsyncListener(() => console.log(5));

// the log will be: Start! 1 2 3 4 5 Done
```

</details>

## 10, ..., 16 Mar 2021 (20, 27, 03, 10 Apr)
### JavaScript
<details>
<summary>Why a Map, not just an Object?</summary>

- any keys possible
- iterable
- pairs are objects
- better performance (than object) for large quantities of data
- better performance when adding / removing data frequently

</details>

<details>
<summary>How to create a Map and add items?</summary>

```JavaScript
const pairs = new Map();
// add items
pairs.set('John', 'May');
pairs.set('Ichigo', 'Rukiya');

// or with iterable
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
```

</details>

<details>
<summary>How to convert an Object into a Map and back from a Map to an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

const playerMap = new Map(Object.entries(player));
const newPlayer = Object.fromEntries(playerMap.entries());
```

</details>

## 12, ..., 16 Mar 2021 (18, 22, 29, 05, 12 Apr)
### JavaScript
<details>
<summary>What data structures could be used as a key in an Object?</summary>

- strings
- numbers (positive int or floats)
- symbols

</details>

<details>
<summary>Is an Object iterable and how to iterate?</summary>

- not iterable (can use `for ... in` old loop, has some issues, not `for ... of`)

</details>

<details>
<summary>How to create an Object (ES5, ES6 creation of the properties)?</summary>

```JavaScript
// ES5
// simple object
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

// ES6+
// creation with variable
const name = 'Harry';
const user = {
  name,
  level: 1
};
// complex keys (could be useful for dictionaries)
const potter = 'Harry Potter';
const voldemort = 'Tom Riddle';
const antagonist = {
  [potter]: voldemort,
  ['Sirius Black']: 'Bellatrix Lestrange'
};
// new syntax for methods
const character = {
  go() {}
};
```

</details>

<details>
<summary>What if we access the prop/method which doesn't exist in an object?</summary>

```JavaScript
const person = {
  name: 'Ron',
  age: 22,
  level: 3
};

// if no property or method => undefined (not an error)
console.log(person.hobbies);
```

</details>

<details>
<summary>How to deep copy an object?</summary>

- copying deep - recursive with checking typeof function or object
  - lodash has deep copy
  - also there is a hack with `json.parse`, `json.stringify`

</details>

<details>
<summary>How to work with Object Descriptors?</summary>

```JavaScript
const character = {
  name: 'Harry',
  printName: function() {
    console.log(this.name);
  }
};

const descriptors = Object.getOwnPropertyDescriptors(character);
Object.defineProperty(character, 'name', {
  // defaults
  // can delete or define property
  configurable: true,
  // is accessible in for ... in loop
  enumerable: true,
  value: character.name,
  // can rewrite
  writable: true
});

// if writable === false
// no error but won't change, stays the same (Harry)
character.name = 'Ron';

// if configurable === false
// no error but won't delete, stays the same (Harry)
// can't reset configuration also, be careful
delete character.name;

// if enumerable === false
for (const key in character) {
  // will skip the name key, logs only printName
  console.log(key);
}
```

</details>

## 17 Mar 2021 (18, 19, 21, 23, 27, 03, 10, 17 Apr)