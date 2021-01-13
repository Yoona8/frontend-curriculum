# Review progress and questions I have to review
## 14, ..., 08 Jan 2020 (15 Jan)
### JavaScript
<details>
<summary>How to use destructuring with iterables?</summary>

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
// when we want specific values and an array of the rest
const [first, ...otherNumbers] = numbers;
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
<summary>How to use destructuring with Object?</summary>

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
// creates name and object of remained properties
const {name, ...otherProperties} = cat;

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
<summary>What is better: loop or recursion?</summary>

- in most cases loop is more efficient than a recursion (call stack overflow)
- any recursion could be rewritten into a loop

</details>

<details>
<summary>What are the general loops?</summary>

- `for (let i = 0; i < 5; i++) {}`
- `for (const item of items) {}`
  - almost the same as `for` loop
  - can use `break` and `continue`
  - could be used with every iterable (not only `Array`)
- `for (const key in someObject) {}`
  - requires additional check, otherwise can go through the whole prototype chain
- `while (isEdit) {}` as long as the condition is true
- `do { ... } while (isEdit);` runs at least once

</details>

<details>
<summary>What do `break` and `continue` do?</summary>

- `break;` stops the loop execution
  - if inside the nested loop - stops only the nested one, outer continues
- `continue;` skips only the current iteration and moves to the next

</details>

<details>
<summary>How and why to use a labeled statement?</summary>

- labeled statements could be used with any expression but mostly used with loops
- to break or continue the outer loop from inner
```JavaScript
outerLoop: for (const item of items) {
  console.log('Outer', item);

  innerLoop: for (let i = 0; i < 5; i++) {
    if (i === 2) {
      break outerLoop;
      // or
      continue outerLoop;
    }

    console.log('Inner', i);
  }
}

// could also break from somewhere else in the code
const button = document.querySelector('.button');

button.addEventListener('click', () => {
  break outerLoop;
  // or
  continue outerLoop;
});
```

</details>

<details>
<summary>How to use rest and spread operators?</summary>

- rest collects several values into one iterable structure
- rest must be last parameter in the function (or error)
```JavaScript
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
<summary>What can be used with the `throw` operator?</summary>

- `throw { message: 'some message' };` can throw anything as an error, not only `new Error()`

</details>

## 16, ..., 10 Jan 2020 (17 Jan)
### JavaScript
<details>
<summary>When is it good to use `try catch finally`?</summary>

- use `try {} catch (error) {}` only for the code you can't control (ex: server errors, user input)

</details>

<details>
<summary>In what variations can we use `try catch finally`?</summary>

- `try ... catch` or `try ... finally` but never `catch ... finally`

</details>

<details>
<summary>When does `catch` get executed?</summary>

- if `try` doesn't throw an error, `catch` won't be executed

</details>

<details>
<summary>Why to use and when does `finally` run?</summary>

- when we want to throw the error from inside the `catch` block to send to some statistics etc
- some cleanup work (release data, clear the variables, etc)
- if the error is thrown from `catch`, only finally executes, code after `try ... catch ... finally` block won't be executed
- `finally` always runs

</details>

<details>
<summary>How does `try catch finally` work in details?</summary>

```JavaScript
function doSomething() {
  try {
    console.log(0); // => 0
    throw 'error ocurred';
  } catch(error) {
    // error => 'error ocurred' (what was used with 'throw')
    console.log(1); // => 1
    // this return statement is suspended till finally block completes
    return true;
    // not reachable
    console.log(2);
  } finally {
    console.log(3); // => 3
    // overwrites the return from catch block
    // function returns this value
    return false;
    // not reachable
    console.log(4);
  }
  // the function returns false from finally block
  // not reachable 
  console.log(5);
}

console.log(doSomething()); // => 0, 1, 3, false
```

</details>

## 18, ..., 12 Jan 2020 (19 Jan)
### JavaScript
<details>
<summary>What problems do modules solve?</summary>

- namespace
  - no global scope
  - encapsulation
- dependencies
  - easy to follow on what module depends on
- interface
  - methods and props export, easy to navigate

</details>

<details>
<summary>What methods to write modules were used in ES5 (and what are the downsides)?</summary>

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
<summary>What about `use strict` inside the module?</summary>

- `'use strict;'` by default

</details>

## 19, ..., 13 Jan 2020 (20 Jan)
### JavaScript
<details>
<summary>How to create a module?</summary>

- syntax looks like destructuring but not the same
- better export const or class (if you export let, can't reassign in the other module anyway)
- do not fold `export` and `import` into code blocks `{}`
```JavaScript
// module-name.js
// named - names should be the same (or error, module won't get loaded)
// could import not all the export
// can't export the same variable 2x
// better not to combine inline and group exports
export { name, age };
// or
export const name = 'Max';
export const age = 40;
// renamed
export { name as userName };
// default
// better for classes
// could be hard to debug (imported by any name)
export default name;
export default { name };
export { name as default };
```

</details>

<details>
<summary>How to import a module?</summary>

- syntax looks like destructuring but not the same
- imported variable is not created (the same link to the exported variable)
- do not fold `export` and `import` into code blocks `{}`
- no hoisting, so that's why `import` is always on top
```JavaScript
// other-module.js
// import using the same variable name
import { name } from './module-name.js';
// import all as child (ignores default, insecure, have no control on import)
import * as child from './module-name.js';
// renamed
import { name as userName } from './module-name.js';
// default
import name from './module-name.js';
import { default as name } from './module-name.js';
// import without a variable if we only need to execute the code from module
import './log.js';
```

</details>

<details>
<summary>What if we import an inexistent variable or some error occurs while importing a module or children?</summary>

- `import` of inexistent variable = error, module won't get loaded
- if there is an error while downloading the module or its children => all connected modules won't get loaded

</details>

<details>
<summary>What are the dynamic imports?</summary>

- there are dynamic imports, but browser support is still pretty poor

</details>

<details>
<summary>What if you import the same module for several times?</summary>

- even when you import the same module several times, browser loads only once

</details>

<details>
<summary>What paths can be used in imports?</summary>

- both `''` and `""` available
- path is an immutable constant, can't generate the path
- if 2 same imports => browser downloads only one
- paths abs or rel
  - `https://google.com` url
  - `/utils/helpers.js` abs domain-name
  - `./helpers.js` rel
  - `../helpers.js` rel
- `helpers.js` or `utils/helpers.js` is not supported (reserved for libs from package managers)

</details>

<details>
<summary>What are the module loaders?</summary>

- browsers: ES modules in browsers
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
- static: webpack, rollupJS, parcel, ...

</details>

<details>
<summary>What does the module loader do?</summary>

- orders files
- downloads, stores files
- builds, minifies, packs
- all dependencies are loaded relatively to the 1st loaded module
- browser cashes not only a file, but also the result of executing the module + returned values

</details>

<details>
<summary>What is a proxy module?</summary>

```JavaScript
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

</details>

## 25, ..., 12 Jan 2020 (19, 26 Jan)
### JavaScript
<details>
<summary>What is the `window` object and how do we use it?</summary>

- browser API, contains all the global properties and methods
```JavaScript
// can call both ways
alert('Say something');
window.alert('Say something');
```

</details>

<details>
<summary>What is DOM?</summary>

- a part of `window` object

</details>

<details>
<summary>How does the browser searches through the DOM?</summary>

- browser searches DOM in depths, so that the first tag is being found (otherwise not obvious)

</details>

<details>
<summary>How to select the elements with query methods?</summary>

- if no matching => `null` for single or empty collection
```JavaScript
// any css selector
// returns first matching element in the DOM
document.querySelector('ul li:last-child');
// any css selector
// returns NodeList - static collection (snapshot)
// DOM changes doesn't affect 
// (nodes, not only DOM elements, also text, spaces, etc)
document.querySelectorAll('li');

// all those methods could be called only on document, not on element
document.getElementById('title');
// return HTMLCollection - live collection
document.getElementsByClassName('class');
document.getElementsByTagName('li');
```

</details>

<details>
<summary>How to select parents, children, descendants, ancestors?</summary>

```JavaScript
const element = document.querySelector('ul');

// parent node (any parent node: element, text etc)
// but in many cases works the same
element.parentNode;
// selects document
document.documentElement.parentNode;
// parent html element
element.parentElement;
// returns null
element.documentElement.parentElement;
// ancestor
element.closest('selector');

// child nodes (any: element, text etc)
element.childNodes;
// returns HTMLCollection - live collection (only DOM elements)
element.children;

// first or last child node
element.firstChild;
element.lastChild;
// first or last child html element
element.firstElementChild;
element.lastElementChild;

// siblings
element.previousSibling;
element.previousElementSibling;
element.nextSibling;
element.nextElementSibling;
```

</details>

<details>
<summary>How to select some html elements with special properties?</summary>

```JavaScript
// to select the <html>
document.documentElement;
// to select the <body>
document.body;
// to select the <head>
document.head;
```

</details>

<details>
<summary>How do some attribute changes work (changes UI/value)?</summary>

```JavaScript
const input = document.querySelector('input');

// UI changes but value html attribute stays the same
// classes, ids etc do change the html attribute
input.value = 'Some new text';
// UI stays the same but value attribute changes
input.setAttribute('value', 'Other text');
```

</details>

<details>
<summary>How to work with data attributes?</summary>

```JavaScript
// html attribute data-cat-name="Cat" can be accessed
const catName = element.dataset.catName;
```

</details>

<details>
<summary>How to insert some text to HTML?</summary>

```JavaScript
const element = document.querySelector('section');
// replaces all the content inside the element
element.textContent = 'Some text';
// increments the content
element.textContent++;
// is the same
element.textContent = element.textContent++;
```

</details>

<details>
<summary>How to insert an element to HTML using an HTML string?</summary>

```JavaScript
const element = document.querySelector('section');
// replaces all the content inside the element
element.innerHTML = '<p>Description</p>';
// add html to a specific position
element.insertAdjacentHTML('beforeend', '<p>Description</p>');
```

</details>

## 29, ..., 10 Jan 2020 (16, 23, 30 Jan)
### JavaScript
<details>
<summary>How to create an element?</summary>

```JavaScript
const newElement = document.createElement('p');
newElement.textContent = 'Description';
```

</details>

<details>
<summary>How to add / move the element to the DOM?</summary>

```JavaScript
// all these methods remove the element (if existed)
// and move to the new position
// (need to clone not to be removed)
// append new DOM element or node
// any node, several nodes (IE not supported)
// last inside the element
element.append('Some text', newElement);
// first inside the element
element.prepend(newElement);
// before the element (as sibling) (problems with Safari)
element.before(newElement);
// after the element (as sibling) (problems with Safari)
element.after(newElement);
// replace existing DOM element or node with a new one
element.replaceWith(newElement);

// only one element (older methods, have IE support)
// = append();
element.appendChild(newElement);
// = before();
// if referenceNode === null, newElement is inserted
// at the end of the element's child nodes
const newNode = element.insertBefore(newElement, referenceNode);
const newNode1 = element.insertBefore(newElement, null);
// = replaceWith();
const oldNode = element.replaceChild(newElement, oldElement);

// alternative method (supports IE, Safari)
element.insertAdjacentElement('beforeend', newElement);
```

</details>

## 30, ..., 11 Jan 2020 (17, 24, 31 Jan)
### JavaScript
<details>
<summary>How to clone the DOM Node?</summary>

```JavaScript
// deep? boolean
// better to pass an argument
// (default could be different for some browsers)
const newElement = element.cloneNode(true);
```

</details>

<details>
<summary>How to remove the elements from the DOM?</summary>

```JavaScript
const element = document.querySelector('p');

element.innerHTML = '';
// IE is not supported
element.remove();
// works with IE
element.parentElement.removeChild(element);
```

</details>

<details>
<summary>What happens to the event listeners when the element is removed from the DOM?</summary>

- when the element is deleted (no reference left), all the listeners are also cleaned up - no memory leaks

</details>

## 04, ..., 12 Jan 2020 (16, 22, 29, 05 Feb)
### JavaScript
<details>
<summary>How to work with styles in JS?</summary>

- `style` to get styles but only the inline styles
```JavaScript
const element = document.querySelector('p');

// for CSS properties in several words camelCase is used in JS
element.style.backgroundColor = 'green';
element.style['backgroundColor'] = 'green';
element.style['background-color'] = 'green';
```
- `window.getComputedStyle` to get all styles applied to the element

</details>

<details>
<summary>How to work with the element coordinates relative to the document?</summary>

- always relative to the start of the document, not the viewport (doesn't change upon scrolling)
```JavaScript
// readonly property
const topPosition = element.offsetTop;
```

</details>

<details>
<summary>How to work with the element inner coordinates?</summary>

- inner coordinates of the element do not include the border
- rounds the value to an integer
- the distance from where the margin area ends and the padding and content begins
```JavaScript
// readonly integer property
const innerTop = element.clientTop;
const innerLeft = element.clientLeft;
```

</details>

<details>
<summary>How to work with the element measurements?</summary>

- height of an element's content (including the content not visible on the screen due to overflow)
```JavaScript
// readonly property
const elementFullHeight = element.scrollHeight;
```

</details>

<details>
<summary>How to get the window width and height with and without scroll?</summary>

- in pixels
```JavaScript
// readonly properties
const viewportWidthWithScroll = window.innerWidth;
const viewportHeightWithScroll = window.innerHeight;

// real available window sizes not including the scroll
const viewportWidth = document.documentElement.clientWidth;
const viewportHeight = document.documentElement.clientHeight;
```

</details>

<details>
<summary>How to scroll the content into the viewport?</summary>

```JavaScript
element.scrollIntoView();
```

</details>

<details>
<summary>How to work with templates?</summary>

- `importNode` (learn more)

</details>

## 08, ..., 13 Jan 2020 (16, 20, 26, 02, 09 Feb)
### JavaScript
<details>
<summary>What is the general constructor for the event?</summary>

- made with `Event` constructor

</details>

<details>
<summary>What are the specific event constructors?</summary>

- specific constructors inherited from `Event` (ex `MouseEvent`, `DragEvent`)

</details>

<details>
<summary>To what element can you add the event?</summary>

- can be added to any element (even div)

</details>

<details>
<summary>When are the event listeners removed?</summary>

- event listeners are removed when there is no reference to the element left (either in code or DOM)

</details>

<details>
<summary>How to add the listener (2 ways)?</summary>

- `onclick` attribute or adding via JS `element.onclick = console.log();` overrides previous handler (can't add 2 handlers)
- the best way to add events is `element.addEventListener();`

</details>

<details>
<summary>What is the difference between `change` and `input`?</summary>

- `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
- `input` works with every value change

</details>

<details>
<summary>How to implement the scroll event?</summary>

- useful for infinite loading
```JavaScript
let currentElementNumber = 0;

const onScroll = () => {
  // measure the distance between our viewport (top left corner)
  // and the end of the page (not viewport)
  const distanceToBottom = document.body.getBoundingClientRect().bottom;
  const viewportHeight = document.documentElement.clientHeight;

  // compare to the window height + threshold
  // if we have < 100px to the end of the content,
  // append new data
  if (distanceToBottom < viewportHeight + 100) {
    const newElement = document.createElement('div');

    currentElementNumber++;
    newElement.innerHTML = `<p>Add element ${currentElementNumber}</p>`;
    document.body.append(newElement);
  }
};

window.addEventListener('scroll', onScroll);
```

</details>

## 09, ..., 12 Jan 2020 (14, 17, 21, 27, 03, 10 Feb
### JavaScript
<details>
<summary>What are the event phases?</summary>

- (1) capturing (out - in) => (2) bubbling (in - out)

</details>

<details>
<summary>In what phase does `addEventListener` register the event by default and how to switch the behavior?</summary>

- `addEventListener` by default registers event in a bubbling phase (when we have a listener on button and it's wrapper, first fires button, second wrapper)
- third parameter of `addEventListener(, , true);` switches to the capturing phase (can add to only one listener in a chain)

</details>

<details>
<summary>How to stop the event phases?</summary>

- to prevent propagation
```JavaScript
evt.stopPropagation();
evt.stopImmediatePropagation();
```

</details>

<details>
<summary>What is the event delegation and what are `target` and `currentTarget`?</summary>

- `event.target` is referred to the actual item triggered the event
- `event.currentTarget` always referred to the element, where the listener is added
- `event.target.closest('li');` can also get the item itself

</details>

<details>
<summary>How to trigger DOM events programmatically?</summary>

```JavaScript
// if triggered like that, the event listener added
// is skipped (won't get executed)
// but triggering click event on submit button will work
form.submit();
// works with added listeners
button.click();
```

</details>

<details>
<summary>What is `this` inside the event handler?</summary>

- with arrow functions as handlers `this === window`
- with regular function as handler `this === evt.currentTarget`

</details>

<details>
<summary>How to implement Drag & Drop?</summary>

1. set attribute to `draggable="true"`
2. listen to `dragstart` event (describe the operation and append some data here)
```JavaScript
elementToDrag.addEventListener('dragstart', evt => {
  evt.dataTransfer.setData('text/plain', id);
  evt.dataTransfer.effectAllowed = 'move';
});
```
3. allow to drop into the droppable area (add `preventDefault()` to `dragenter` and `dragover` events)
```JavaScript
// if in drop area we won't prevent default,
// drop event won't be triggered
containerDroppable.addEventListener('dragenter', evt => {
  // can get the data type
  // but not the actual data
  if (evt.dataTransfer.types[0] === 'text/plain') {
    evt.preventDefault();
    // add some visual effect to indicate
    // it's droppable (on dragenter)
    containerDroppable.parentElement.classList.add('droppable');
  }
});

containerDroppable.addEventListener('dragover', evt => {
  if (evt.dataTransfer.types[0] === 'text/plain') {
    evt.preventDefault();
  }
});
```
4. (optional) listen to `dragleave` event (ex. to update some styles)
```JavaScript
containerDroppable.addEventListener('dragleave', evt => {
  // check if only left the element, not just moved
  // to it's children 
  // (w/o this will be triggered when move over the children elements)
  if (evt.relatedTarget.closest('ul') !== containerDroppable) {
    containerDroppable.parentElement.classList.remove('droppable');
  }
});
```
5. listen to `drop` event and update data and UI
```JavaScript
// to react to the drop event need to add a listener
// to the droppable container
containerDroppable.addEventListener('drop', evt => {
  // can get any data we set in dragstart event
  // (now it's available)
  const id = evt.dataTransfer.getData('text/plain');

  // check if the item is in the list and do nothing
  // if not - add item to the list and remove where it was
});
```
6. (optional) listen to `dragend` event and update data and UI (triggered event when the drag was canceled)
```JavaScript
// is added to a draggable element
elementToDrag.addEventListener('dragend', evt => {
  // check if the drag wasn't done
  evt.dataTransfer.dropEffect === 'none';
});
```

</details>

## 13 Jan 2020 (14, 15, 16, 18, 21, 25, 31, 07, 14 Feb