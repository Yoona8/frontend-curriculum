# Review progress and questions I have to review
## 08, ..., 02 Feb 2021 (09 Feb)
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

## 09, ..., 03 Feb 2021 (10 Feb)
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

## 14, ..., 02 Feb 2021 (09, 16 Feb)
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

## 19, ..., 31 Jan 2021 (06, 13, 20 Feb)
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

## 21, ..., 01 Feb 2021 (08, 15, 22 Feb)
### JavaScript
<details>
<summary>What is Http?</summary>

- Data transfer protocol - the way computer uses to exchange the information (there are many different protocols, in the web we use http)
- HTTP - hypertext transfer protocol - client exchanges data with the server
- HTTP request is always text
- request to the server = text
```
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```
- server response = text
```
HTTP/1.1 200 OK
Cache-Control: max-age=604800
Content-Type: text/html
Date: Tue, 24 Oct 2017 11:08:24 GMT
Etag: "359670651+ident"
Expires: Tue, 30 Oct 2017 11:08:24 GMT
Last-Modified: Fri, 09 Aug 2016 23:23:35 GMT
Server: ECS (dcs/53DB)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1270

<!doctype html>
<html>
  <head></head>
  <body></body>
</html>
```

</details>

## 22, ..., 02 Feb 2021 (09, 16, 23 Feb)
### JavaScript
<details>
<summary>How to send the http request with XMLHttpRequest?</summary>

```JavaScript
// can be used on its own
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://google.com');
xhr.send();

// or inside a function
const sendRequest = (method, url) => {
  const xhr = new XMLHttpRequest();

  xhr.open(method, url);
  xhr.responseType = 'json';
  // to add more headers use the method multiple times
  xhr.setRequestHeader('Content-Type', 'application/json');
  
  // to get and use the data have to listen to onload event
  // for XHR .addEventListener is not supported in some browsers
  xhr.onload = function() {
    // check if the status is success
    if (xhr.status >= 200 && xhr.status < 300) {
      // JSON data (mostly, depends on server)
      console.log(xhr.response);
      // either parse JSON.parse(...)
      // or configure responseType (will be parsed automatically)
    } else {
      console.log(xhr.response);
      console.log('Something went wrong.');
    }
  };
  
  // not for sent requests (when we get a response)
  // only for the errors of sending the request
  // like timeout or wasn't sent
  xhr.onerror = function() {
    console.log(xhr.response);
    console.log(xhr.status);
  };
  
  xhr.send();
};

// with using a promise
const sendHttpRequest = (method, url, data) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();

    xhr.setRequestHeader('Content-Type', 'application/json');
    xhr.open(method, url);
    xhr.responseType = 'json';

    xhr.onload = function() {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(xhr.response);
      } else {
        reject(new Error('Something went wrong!'));
      }
    };

    xhr.onerror = function() {
      reject(new Error('Error while sending a request!'));
    };

    xhr.send(JSON.stringify(data));
  });
};

const fetchPosts = () => {
  sendHttpRequest('GET', 'https://...')
    .then(responseData => console.log(responseData))
    .catch(error => console.log(error));
};

const addPosts = async () => {
  try {
    const responseData = await sendHttpRequest(
      'POST',
      'https://...',
      post
    );
  } catch (error) {
    console.log(error);
  } 
};
```

</details>

## 23, ..., 03 Feb 2021 (10, 17, 24 Feb)
### JavaScript
<details>
<summary>How to use fetch API?</summary>

- `fetch` is a wrapper around promise
- function for sending/fetching data (`XMLHttpRequest` under hood)
```JavaScript
// response.json(); returns promise
// resolves when the string will parse json into an object
// if no 2nd param, get request, returns Promise
// resolves into response object
// if fetch => error, but the response is received,
// fetch doesn't count it as a throw new Error (for catching inside catch)
// and returns that response into then
// because the request is fulfilled and response received from server
// 404 / redirect / etc - for fetch those are normal server responses
// so have to add our own status handling
fetch('https://data.com', {
  method: 'POST',
  body: JSON.stringify({
    'date': Date.now(),
    'time': 402,
    'lives': 3
  }),
  headers: {
    'Content-Type': 'application/json'
  }
});

const sendHttpRequest = (method, url, data) => {
  // returns a JSON (unparsed), have to parse
  // with .json() available in fetch API
  return fetch(url, {
    method: method,
    body: JSON.stringify(data)
  })
    .then(response => {
      if (response.status >= 200 && response.status < 300) {
        return response.json();
      } else {
        // if we need the response, error handling could be tricky
        return response.json()
          .then(errorData => {
            console.log(errorData);
            throw new Error('Something went wrong on the server side!');
          });
      }
    })
    .catch(error => {
      console.log(error);
      throw new Error('Something went wrong with the request!');
    });
};
```

</details>

<details>
<summary>What are the good parts for feedback in the UI?</summary>

- When you sync data with a server, don't change control state, change only if the request was successful (returned 200+ codes)
- View => Model => Server => Model => View
- click on favorites - gone on update, if there was an error response from server
- comment doubles if you don't disable the submit button

</details>

## 24, ..., 04 Feb 2021 (11, 18, 25 Feb)
### JavaScript
<details>
<summary>What is the basic implementation of show password case?</summary>

- change type of input from `password` to `text`

</details>

<details>
<summary>What is the purpose of the authorization?</summary>

- restricts the access for different users

</details>

<details>
<summary>What are the ways to identify the user?</summary>

- Identification - tell the site who you are
- Authentication - (authentic - true, genuine) the confirmation that you are who you state you are
- Authorization - check if you are allowed to get access to some parts of the website or webapp

</details>

<details>
<summary>What is the authorization order?</summary>

1. Identification - user enters login and password
2. Authentication - server checks if the login and password are correct and gives a token (access to the web app, often holds the rules and never stores open)
3. Authorization - you give the token to the server and the server decides whether to give you an access or not
  - 200 - success, allowed
  - 401 - unauthorized
  - 403 - not enough rights

</details>

## 25, ..., 05 Feb 2021 (12, 19, 26 Feb)
### JavaScript
<details>
<summary>What are the main problems when working with data?</summary>

- user input - user can enter unsafe data for the view and UI has to be ready for it
- storing and passing data formats could be different to the format needed on the UI, so we need to convert data in our app
  - some ES6 objects (Date, Sets, Maps) could not be converted to JSON, so have to convert into standard data types (primitives, arrays, objects)

</details>

<details>
<summary>What is JSON (and the restrictions)?</summary>

- JavaScript Object Notation
- can't use functions here
- for keys only `" "`
- for values `"string"` (double quotes only), `10`, `true`, `{...}`, `[...]`, `null`

</details>

## 28, ..., 04 Feb 2021 (07, 14, 21, 28 Feb)
### JavaScript
<details>
<summary>How to get the parameters from the link?</summary>

```JavaScript
const url = new Url(location.href);
const queryParams = url.searchParams;
const data = queryParams.get('data');
```

</details>

<details>
<summary>How to convert into a link?</summary>

- `encodeURI('some text');`

</details>

## 29, ..., 05 Feb 2021 (08, 15, 22, 01 Mar)
### JavaScript
<details>
<summary>How to load script files from JS dynamically?</summary>

- basically generate html and add it to the page

</details>

<details>
<summary>What is the location API used for?</summary>

- for the app url and navigation

</details>

<details>
<summary>What is history API used for?</summary>

- works with location
- can use `history.back()` to navigate back (ex different cases with questions like age)

</details>

<details>
<summary>Why do we use the navigator API?</summary>

- don't use for defining browser version
- could be useful when we need
  - geolocation

</details>

## 05 Feb 2021 (06, 07, 09, 11, 15, 22, 01, 08 Mar)