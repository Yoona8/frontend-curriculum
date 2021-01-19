# Review progress and questions I have to review
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

## 25, ..., 19 Jan 2020 (26 Jan)
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

## 29, ..., 16 Jan 2020 (23, 30 Jan)
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

## 30, ..., 17 Jan 2020 (24, 31 Jan)
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

## 04, ..., 16 Jan 2020 (22, 29, 05 Feb)
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

## 08, ..., 16 Jan 2020 (20, 26, 02, 09 Feb)
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

## 09, ..., 17 Jan 2020 (21, 27, 03, 10 Feb)
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

## 14, ..., 18 Jan 2020 (20, 23, 27, 02, 09, 16 Feb)
### JavaScript
<details>
<summary>What is sync data loading?</summary>

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
<summary>What is the event loop and how it works?</summary>

- JS is single threaded
- browser is multi threaded
- all kind of async tasks (like timers, event listeners, etc) are going to browser (message queue)
- micro - promises (run first), macro - timeouts (run second)
- when the call stack is empty, event loop goes through message queue and executes the functions from there

</details>

<details>
<summary>What is async?</summary>

- async - run the operation without blocking the main script process

</details>
  
<details>
<summary>How was async implemented in ES5 and what are the issues?</summary>

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

<details>
<summary>How is async implemented in ES6?</summary>

- promise is a way to work with an async function as if it's sync 
- different states of a promise object
<img src="../images/promise.jpg" alt="promises" width="400">

```JavaScript
const getResponse = (url) => new Promise(
  (resolve, reject) => {
    // Object => Pending...
    // neither then() or catch() executes at this moment
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    // Object => Fulfilled
    // then() executes
    xhr.onload = () => resolve(xhr.response);
    // Object => Rejected
    // catch() executes
    xhr.onerror = () => reject(xhr.status);
    xhr.send();
  }
);

getResponse('data.json')
  // callback on success
  // could work with several promises
  // returns new Promise()
  .then(
    (data) => console.log(data),
    // but better to use catch
    (error) => console.warning(error)
  );

getResponse('data.json')
  // if there is anywhere in then chain throw new Error
  // it's going to be caught in catch
  .then((data) => console.log(data))
  // catches all the errors before
  // the blocks before are skipped but
  // doesn't stop the chain (if there are some then after)
  .catch((error) => console.warning(error))
  // if there are no more then() blocks left
  // promise enters the final mode: settled
  // once settled, you can use the special block finally()
  // to do some cleanup work
  // this block is reached anyways (resolve or reject before)
  // optional, executes always
  // will not return a promise in the end (like then() and catch())
  .finally(cb);

// you can work with promises chaining then
// every then returns a promise, where we can also call then
Promise.resolve('a') // 'a'
  .then((val) => val.concat('b')) // 'ab'
  // when we have another then() or catch()
  // the promise re-enters pending mode
  .then((val) => val.concat('c')) // 'abc'
  .then((val) => val.concat('d')); // 'abcd'
```

</details>

## 19 Jan 2020 (20, 21, 22, 24, 27, 31, 06, 13, 20 Feb)
### JavaScript
<details>
<summary>What is Promise.race?</summary>

```JavaScript
Promise.race([getPromise1(), getPromise2()])
  .then(dataFromTheFastest => {});
// the other promise is not canceled!
// just ignored (the http request will still be sent)
```

</details>

<details>
<summary>What is the difference between Promise.all and Promise.allSettled?</summary>

- when you need an array of requests at the same time 
  - `Promise.all(<Array.Promise>)`
    - executed when all the promises are resolved
    - if one with error, drops, can't access the data
    - returns an array
  - `Promise.allSettled(<Array.Promise>)`
    - waits till all the promises are completed (success/error)
    - can access the data even when some promises complete with an error
    - poor browser support
- `Promise.then` could return
  - just value/array - goes to the next promise
  - object Promise
  - array of values / promises - can turn into something else

</details>

<details>
<summary>What is async await?</summary>

- uses promises under the hood
- can be used only with functions
```JavaScript
// can't use like that
await setTimer(1000);
// but can wrap into IIFE
(async function() {
  await setTimer(1000);
})();
```
- when `async` is added, function automatically returns a promise
- wraps everything inside into a promise
```JavaScript
const setTimer = async () => {
  // waits till the promise is resolved and goes to the next line
  const data = await getData();
  const otherData = await getOtherData();
  // won't get executed till the await block resolved
  // as if wrapping into then() block
  console.log('Done!');
  // returns promise
};

async function setTimer() {
  // to handle errors can use try ... catch
  try {
    // if anything here yields an error,
    // the block fails into the catch
    // if error is in the 1st line, 2nd won't be executed
    const data = await getData();
    const otherData = await getOtherData();
  } catch (error) {
    console.log(error);
  }
  // this code will be executed anyways
  console.log('Done!');
  // returns promise
}

// creates a wrapping promise
function setTimer() {
  return new Promise((resolve, reject) => {
    // all the code here
  });
}
```
- `await` wraps everything into a `then()` block
- not good for cases when we need to run some code and not wait for promise to resolve or reject

</details>

## 20 Jan 2020 (21, 22, 23, 25, 28, 01, 07, 14, 21 Feb)