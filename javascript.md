# JavaScript

- [To content](readme.md)

## 1 - ECMAScript
<details>
<summary>Notes</summary>

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

## 2 - Constants and variables
<details>
<summary>Examples</summary>

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

## 3 - Data types and structures
<details>
<summary>Table</summary>

|Name|Notes and usage|Level|
|----|---------------|:---:|
|undefined|`'undefined'`|:deciduous_tree:|
|Boolean|`'boolean'`|:blossom:|
|Number|`'number'`|:blossom:|
|String|`'string'`|:deciduous_tree:|
|BigInt|`'bigint'`|:seedling:|
|Symbol|`'symbol'`|:seedling:|
|null|`'object'`|:deciduous_tree:|
|Object|- `'object'`<br> - `Object`<br>- iterable lists: `Array`, collections<br>- collections: `NodeList`, `HTMLElementsList`, `classList`, `arguments`<br>- iterable dictionaries: `Map`, `WeakMap`<br>- iterable sets: `Set`, `WeakSet`|:deciduous_tree:|
|Function|`'function'`|:blossom:|

</details>

## 4 - Numbers

## 5 - Strings

## 6 - Iterables: Arrays
<details>
<summary>Creation</summary>

```JavaScript
// before ES6
var numbers = new Array();
var letters = [];

// ES6+
// make an array of any iterable (collection, separate values)
const elements = Array.from(document.querySelectorAll('li'));
const values = Array.of(1, 2, 3);
const items = [...elements, ...values];
```

</details>

<details>
<summary>Methods</summary>

|Method|Notes|Level|
|------|-----|:---:|
|`arr.sort()`|changes the initial array|:deciduous_tree:|
|`arr.filter()`|creates a new array|:deciduous_tree:|
|`arr.slice()`|creates a new array|:deciduous_tree:|
|`arr.map()`|creates a new array|:deciduous_tree:|
|`arr.reduce()`|creates a new value|:deciduous_tree:|

</details>

<details>
<summary>Arrays as a stack LIFO</summary>

- for tasks, when we have to store previous item (history, browser history, games)
- store the action (function) and add to the history array
- use `history.pop()();` to get back the stored value
- also available to 'go forward' the history (have to store the removed action back to the stack)

```JavaScript
history.push(() => {
  questions[0].text = oldText;
  return newText;
});
```

</details>

<details>
<summary>Arrays as a queue FIFO</summary>

- for tasks to be executed in a row after some async event
- for unique actions can use `Set` instead of `Array`

```JavaScript
const startAsync = () => {
  setTimeout(() => {
    for (const cb of callbacks) {
      callbacks.delete(cb);
      cb();
    }
  }, 500);
};

// before .find was used to check
// breaks the loop when the 1st item is found
callbacks.find((it) => it === 'some');
```

</details>

## 7 - Objects
<details>
<summary>Dictionaries</summary>

Object
- keys are strings or numbers (other not possible)
- not iterable (can use `for ... in` old cycle has some issues, not `for ... of`)
Map + WeakMap
- any keys possible
- iterable
- pairs are objects

```JavaScript
// object
const filterValueToScale = {
  'smallest': 0.25,
  'small': 0.5,
  'normal': 1,
  'large': 2
};

// map
let pairs = new Map();
pairs.set('John', 'May');
pairs.set('Ichigo', 'Rukiya');
// or with iterable
let pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
// iterating
for (const [first, second] of pairs) {
  console.log(first.name + second.name);
}
```

```JavaScript
// new features for objects in ES6
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
// destructuring
const newAntagonist = {...antagonist};
// new syntax for methods
const character = {
  _level: 1,
  // before
  go: function() {},
  // ES6
  go() {},
  // getters and setters
  // can't use getter/setter + property
  // can't address itself = infinite cycle
  get level() {
    return this._level;
  },
  // always strictly 1 parameter
  set level(value) {
    this._level = value;
  }
};
// addressing the getter or setter
const level = character.level;
character.level = 100;
// it there is only setter, can't access the value
```

</details>

<details>
<summary>Iterating</summary>

```JavaScript
// before ES6
// for ... in
// deprecated
// requires additional check, otherwise can go through the whole prototype chain

// ES6
// for ... of works
const player = {
  name: 'Harry',
  level: 10
};
// [['name', 'Harry'], ['level', 10]]
const playerEntries = Object.entries(player);
// ['Harry', 10]
const playerValues = Object.values(player);
// ['name', 'level']
const playerKeys = Object.keys(player);
```

</details>

<details>
<summary>Delete a property or method</summary>

- `delete player.name;`

</details>

<details>
<summary>Check if property exists</summary>

```JavaScript
// but if the property = undefined, also returns false
player.name !== undefined;
// true even with undefined
'name' in player;
// true even if undefined
player.hasOwnProperty('name');
```

</details>

<details>
<summary>Copy</summary>

```JavaScript
// не избавляет от проблем с вложенностью
// {} - where
// player - what
const newPlayer = Object.assign({}, player);
// for several
const newPlayer = Object.assign({}, player, {options: 'code'});

// также не избавляет от проблем с вложенностью
const newPlayer = {...player};

// копирование с вложенностью - рекурсивно по всем ключам
// с проверкой typeof function or object
// есть в lodash
// hack with json.parse, json.stringify
```

</details>

## 8 - Functions
<details>
<summary>Notes</summary>

- function without `return` statement returns `undefined`

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

## 9 - Scope
- scope where the function runs
- `this` links to current object in a `class`
- depends on how the function is called
- could be changed, also with `apply`, `call`, `bind`
- `bind` creates a new function, the initial function stays the same
- `bind` context can't be changed even with `apply`, `call`
- arrow functions do not have their context
- while the function is not called, it doesn't have any context
- context is being created upon the function call
- `this` assigns only upon the function call
- `use strict` affects `this` value
  - no `use strict` = `window`, with = `undefined`
- in an object (method) `this` = link to the object itself
- doesn't matter how the function is created, matters only how it's called
```JavaScript
const walk = function() {
  console.log(this + 'walk!');
};
const player = {walk};
player.walk(); // this === link to player object
walk(); // TypeError: Cannot read property '...' of undefined
```
- doesn't matter how the function is written, context will be the same `walk = player.walk`
- with closure the result is more obvious
```JavaScript
const guitarPlayer = {
  firstName: 'Michael',
  lastName: 'Lantsov',
  play() {
    console.log(`${guitarPlayer.firstName} ${guitarPlayer.lastName}`);
  }
};

// the result will be the same
const anotherPlayer = {
  play: guitarPlayer.play
};
```
- calling a function with binded context (1st param in those functions is always context, the 2nd parameter differs)
```JavaScript
// arguments separated with ',' will be function params
// perfect when there are not many params
play.call(anotherPlayer, '20.02.1967');
// array, which values will be function params
// good for many params or undefined number of params
play.apply(guitarPlayer, ['20.02.1967']);
```
```JavaScript
const numbers = [1, 3, 100, 5];

// we don't need context here, so pass 'null'
console.log(Math.max.apply(null, numbers));
```
- listener's context is always === the element, to which the listener is applied `document.body` or `evt.currentTarget`
  - can override if create the event handler and execute the method
  ```JavaScript
  item.addEventListener('click', function() {
    cart.print();
  });
  // browser will store the function
  callback = cart.print;
  // and executes the callback
  callback();
  // so just won't work
  ```
- with bind (but careful, `bind` returns a new function, store first in a separate variable to unsubscribe if needed)
```JavaScript
item.addEventListener('click', cart.print.bind(cart));
```
```JavaScript
// custom binder (like the bind works)
const customBind = function(fn, context) {
  return function() {
    return fn.apply(context, arguments);
  };
};
```

## 10 - Constructors and prototypes
<details>
<summary>Notes</summary>

- naming `GuitarPlayer`
- creation of an instance with new
- add a method in prototype
```JavaScript
GuitarPlayer.prototype.play = function() {};
```
- without new => undefined (void = return undefined) will not be created
- ES6 проверка if new inside constructor
```JavaScript
if (!new.target) { throw new Error(); }
```
- проверить принадлежность `instanceof`
- why new if we can return an object?
  - `instanceof` becomes useless
  - inheritance (prototype) won't work
- `new` keyword не вызывает функцию, а берет и на основе полей этой функции (то, что записывается через `this.name = name`) создает объект
  - созданный с `new GuitarPlayer` объект JS наделяет свойством вновь созданный объект, которое содержит информацию, с помощью какой функции-конструктора он создан
- если попробовать сымитировать функцию-конструктор и `return this;`, будет ссылаться на глобальный объект

</details>

## 11 - Classes
<details>
<summary>Notes</summary>

- `class Player {}` better to use instead of `const Singer = class {};`
- `constructor() {}` предопределенный метод класса, помогает создать экземпляр класса, все свойства определяются в нем
- `play() {}` методы записываются в `prototype`, определяются как у объекта
- `constructor` необязателен
- `new` для создания instance (or type error)
- если внутри класса обратиться к несуществующему свойству, получим `undefined`
- есть статические методы (не передаются потомкам (экземплярам))
```JavaScript
static createJuniorPlayer() {
  return new this(5, 2);
}
```
- также статическими могут быть свойства (но плохая поддержка)
- можно использовать getters / setters
- можно и без setter, но нарушим правило ООП, так как проверки будут снаружи
- приватные поля, но пока плохая поддержка `this.#skill = value;`

</details>

<details>
<summary>Difference between class and constructor functions</summary>

- `class` нельзя без `new` (в функции-конструкторе можно сделать имитацию с проверкой `target.new`)
- вывод в консоль (`class` / `f`)
- методы класса не перечисляемые
```JavaScript
for (const prop in player) {
  console.log(prop);
}
```

</details>

## 12 - Expressions and Operators
<details>
<summary>Destructuring: Arrays and alike</summary>

- for iterable structures only (doesn't work on strings!)
- all the elements go in an order, can't address the last one

```JavaScript
const numbers = [1, 2, 3, 4, 5];
// before 
const first = numbers[0];
const third = numbers[2];
// with destructuring
const [first, , third] = numbers;
// when there is no value, can use defaults
const [first, , , , , sixth = 45] = numbers;
// good for swapping the values
let first = 'Harry';
let second = 'Ron';
[first, second] = [second, first];
// can destruct the function result
const [first, , third] = getNumbers();
// or function parameters
const printValues = ([first = 4, , third = 7]) => {
  console.log(`${first} ${third}`);
};
printValues(document.querySelectorAll('li'));
printValues([1, 2]);
printValues([]);
printValues(); // error: undefined is not iterable
```

</details>

<details>
<summary>Destructuring: Objects</summary>

```JavaScript
const cat = {
  name: 'Mini',
  location: 'London',
  color: 'Auburn',
  address: {
    street: 'Some street'
  },
  'home city': 'London'
};
// propOfAnObject: varName = default
const {name: catName, color: catColor = 'White'} = cat;
// with folded objects
const {address: {street: catStreet}} = cat;
// for combined prop use quotes
const {'home city': catCity} = cat;

// great to use for DOM nodes
const elements = document.querySelectorAll('li');
for (let i = 0; i < elements.length; i++) {
  const {textContent: text} = elements[i];
  console.log(text);
}

// can combine [] and {} destructuring
const [, {textContent: text}] = document.querySelectorAll('li');
```

</details>

<details>
<summary>:deciduous_tree: - For ... of loop</summary>

- almost the same to `for` loop
- can use `break` and `continue`
- could be used with every iterable

</details>

<details>
<summary>:deciduous_tree: - Rest and spread operators</summary>

```JavaScript
// rest collects several values into one iterable structure
// before
function doSomething() {
  return Array.from(arguments);
}
// with rest
const doSomething = (...values) => {
  return values;
};
// destructuring + rest = first and an array of others
const [first, ...others] = doSomething();
```

```JavaScript
// spread - any iterable into separate values
// before
const values = [1, 2, 40, 73, 5];
// find max
Math.max.apply(null, values);
// merge arrays
const newValues = [];
newValues.concat(values);

// with spread
// find max
Math.max(...values);
// merge arrays
const newValues = [...values];
const filteredValues = [...values].filter();
```

</details>

<details>
<summary>New and instance of</summary>

- утиная типизация - ненадежно
- add some field to function, which will create an object and compare that key - велосипед
- функции-конструкторы
- more information [constructors and prototypes](#constructors-and-prototypes)

</details>

## 13 - Control structures

## 14 - Modules
<details>
<summary>Tasks to solve</summary>

- Namespace
  - no global scope
  - encapsulation
- Dependencies
  - easy to follow on what modules depends on
- Interface
  - methods and props export, easy to navigate

</details>

<details>
<summary>Before ES6</summary>

- manual configuration
- have to remember dependencies order
- is not clear, what dependencies are used

```JavaScript
// IIFE
'use strict';
// slider.js
(function() {
  window.slider = {
    name: 'Eve'
  };
})();
```

- better module approaches were found (AMD, CommonJS, UMD)

</details>

<details>
<summary>ES6 exports and imports</summary>

- `'use strict;'` by default
- syntax looks like destructuring, but not the same
- imported variable is not created, the same as in export
- better export const or class
- import without variable when just need to execute the code
- do not fold `export` and `import` into code blocks `{}`
- no hoisting, so that's why `import` is always on top
- `import` of unexcited variable = error, module won't be loaded
- there are dynamic imports, but browser support is still pretty low

Import paths:
- both `''` and `""` available
- path is a immutable constant, can't generate the path
- if 2 same imports => browser downloads only one
- paths abs or rel
  - `https://google.com` url
  - `/utils/helpers.js` abs domain-name
  - `./helpers.js` rel
  - `../helpers.js` rel
- `helpers.js` or `utils/helpers.js` is not supported (reserved for libs from package managers)
- If there is an error while downloading the module or its children => all connected modules won't be loaded

Modules loaders ()
- browsers: ES modules in browsers
- static: webpack, rollupJS, parcel, ...
- orders files
- downloads, stores files
- builds, minifies, packs

```JavaScript
// named
// names should be equal or error, module won't get loaded
// could import not all the export
// can't export the same variable 2x
// better not to combine line and group exports
export { name, age };
export const name = 'Max';
import { name } from './module-name.js';
// import all as child (ignores default, insecure, have no control on import)
import * as child from './module-name.js';

// renamed
export { name as userName};
import { name as userName} from './module-name.js';

// default
// better for classes
// could be hard to debug (imported by any name)
export default name;
export default { name };
export { name as default };
import name from './module-name.js';
```

```JavaScript
// proxy
// module-1.js
export { name as nameOne };

// module-2.js
export { name as nameTwo };

// module-3.js
export * from './module-1.js';
export * from './module-2.js';

// module-target.js
import { nameOne, nameTwo } from './module-3.js';
```

- all dependencies load relatively to the 1st loaded module
- browser cashes not only a file, but also the result of executing the module + returned values

```HTML
<!-- adding modules to the page -->
<!-- by default works like defer -->
<script type="module">
  // some code here
</script>
<script src="module-1.js" type="module"></script>
<!-- fallbacks (ignored by browsers, which support modules) -->
<script src="module-1.js" nomodule></script>
```

</details>

## 15 - DOM

## 16 - Events
<details>
<summary>Events</summary>

- difference between `change` and `input`
  - `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
  - `input` works with every value change

</details>

## 17 - Async JavaScript (promises and callbacks, async/await)

<details>
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
  
<details>
<summary>Async ES5 (callbacks)</summary>

- async - run the operation without blocking the main script process
- minuses:
  - complex interface, have to add all possible callbacks, difficult to make optional manipulation for some cases
  - difficult to read the code, recreate the methods sequence is quite hard
  - callback hell - several chained async methods turn into nested sequences of callbacks, too hard to support https://callbackhell.ru/
```JavaScript
const getResponse = (url, onload, onerror) => {
  const xhr = new XMLHttpRequest();
  xhr.open('GET', url, true);
  xhr.onload = () => onload(xhr.response);
  xhr.onerror = () => onerror(xhr.status);
  xhr.send();
};

getResponse('data.json',
  (response) => console.log(response),
  (errorStatus) => console.log(errorStatus)
);
```

</details>
Async ES6 (promises) 

## 17 - Http requests

## 18 - Working with data
<details>
<summary>Issues</summary>

- user input - user can enter unsafe data for the view and UI has to be ready for it
- storing and passing data formats could be different to the format needed on the UI, so we need to convert data in our app
  - some ES6 objects (Date, Sets, Maps) could not be converted to JSON, so have to convert into standard data types (primitives, arrays, objects)

</details>

## 19 - Browser storage

## 20 - Meta-programming

## 21 - Performance and optimizations

## 22 - Security

## 23 - Deploying

## 24 - Testing

## 25 - Debugging

## 26 - Browser support

## 27 - Tools and workflow

## 28 - Libraries

## 29 - Frameworks

## Notes
<details>
<summary>Other</summary>

- cycle is more optimal than a recursion (call stack overflow), any recursion could be rewritten into a cycle

</details>