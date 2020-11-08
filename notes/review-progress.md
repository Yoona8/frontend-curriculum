# Review progress and questions I have to review
## 03, ..., 08 Nov 2020 (10, 12, 15, 18, 23, 30)
### JavaScript

<details>
<summary>What is the type of null?</summary>

```JavaScript
// 2 - null
console.log(typeof null); // => object
```

</details>

<details>
<summary>What system JS uses to work with numbers?</summary>

- JS works with binary numbers and converts into decimal

</details>

<details>
<summary>How does BigInt work and when do we use it?</summary>

- only integer, decimal => error
```JavaScript
// can't mix with numbers
10n - 5; // => error
// but can use like this
10n - 5n; // => 5n
parseInt(10n) - 5; // => 5
10n - BigInt(5); // => 5n
// omits decimal
5n / 2n; // => 2n (not 2.5n)
```

</details>

<details>
<summary>How to check if a string contains some text?</summary>

```JavaScript
const playerName = 'Harry Potter';

// case sensitive
console.log(playerName.includes('rr')); // => true
console.log(playerName.includes('h')); // => false
```

</details>

<details>
<summary>What is an iterable (and examples)?</summary>

- objects that implement the 'iterable' protocol (have an `@@iterator` method (ex: `Symbol.iterator`))
- basically objects where you can use `for ... of` loop
- Array, NodeList, String, Map, Set, etc.

</details>

<details>
<summary>How to create an array?</summary>

```JavaScript
// before ES6
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

## 05, ..., 07 Nov 2020 (next 09, 11, 13, 16, 20, 25, 02 Dec)
### JavaScript
<details>
<summary>How are the numbers stored?</summary>

- every number is a float
- numbers are stored as 64 Bit Floating Points (some issues and limits)

</details>

<details>
<summary>What are the maximum and minimum numbers?</summary>

```JavaScript
// max numbers
Number.MAX_SAFE_INTEGER; // 2^53 - 1
Number.MIN_SAFE_INTEGER; // -(2^53 - 1)
// floats
Number.MAX_VALUE;
// > or < calculations won't work, only display
// if we do such calculations, no errors
// but strange results because of binary system
```

</details>

<details>
<summary>What are the strange number cases and why do they occur?</summary>

- because JS works with binary and converts into decimal, there are some strange cases
```JavaScript
0.2 + 0.4 === 0.6; // => false (0.6000...1)
// something similar to 1/3 happens (0.33333(3))
(1).toString(2); // => 1
(5).toString(2); // => 101
(1/5).toString(2); // => 0.001100110011...
(0.2).toString(2); // => 0.001100110011...
0.2; // => 0.2
0.2.toFixed(20); // => 0.2000...1110
```

</details>

<details>
<summary>What are the characteristics of an array?</summary>

- store data of any kind and length
- has many special methods
- order is guaranteed
- duplicates are allowed
- index-based access

</details>

<details>
<summary>What are the characteristics of a set?</summary>

- store data of any kind and length
- has own special methods
- order is not guaranteed
- duplicates are not allowed
- no index-based access

</details>

<details>
<summary>What are the characteristics of a map?</summary>

- store key-value data of any kind and length
- any key values are allowed
- has own special methods
- order is guaranteed
- duplicate keys are not allowed
- key-based access

</details>

<details>
<summary>How to delete or add an element from (to) an array at the start or the end?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// add/remove to the end/last of the array
const newNumbersLength = numbers.push(7, 9);
const newNumbersLength2 = numbers.push(...numbers);
const removedItem = numbers.pop();
// add/remove first, slower than push and pop
const newNumbersLength3 = numbers.unshift(9, 12, 15);
const newNumbersLength4 = numbers.unshift(...numbers);
const removedItem2 = numbers.shift();
```

</details>

<details>
<summary>How to delete or add an element from (to) an array at any position?</summary>

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

## 06, ..., 08 Nov 2020 (next 10, 12, 15, 19, 24, 30, 07 Dec)
### JavaScript
<details>
<summary>How to make an array of a string?</summary>

```JavaScript
const text = 'One two three';
const words = text.split(' '); // => ['One', 'two', 'three']
const words2 = Array.from(text); // => ['O', ..., ' ', 't', ...]
```

</details>

<details>
<summary>How to copy an array or a part of it?</summary>

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

<details>
<summary>How to find an item or an index in an array?</summary>

```JavaScript
const numbers = [1, 2, 5];
// first element in the array
const number = numbers.find(number => number > 1); // => 2
// index of the first element or -1
const numberIndex = numbers.findIndex(number => number > 1); // => 1
```

</details>

<details>
<summary>How and why to create a stack using an array (LIFO)?</summary>

- for tasks, when we have to store previous item (history, browser history, games)
- also available to 'go forward' the history (have to store the removed action back to the stack)
```JavaScript
const questions = [{
  question: 'Which class has a different teacher every year?',
  answers: [{
    answer: 'Defence against the dark arts',
    isCorrect: true
  }, {
    answer: 'Potions',
    isCorrect: false
  }]
}, {
  question: 'What animal represents Hufflepuff house?',
  answers: [{
    answer: 'The Burrow',
    isCorrect: true
  }, {
    answer: 'The Fox',
    isCorrect: false
  }]
}];

const history = [];

const changeQuestion = (newQuestion) => {
  const oldQuestion = questions[0].question;

  questions[0].question = newQuestion;
  
  // store the action (function) and add to the history array
  // works because of closures
  history.push(() => questions[0].question = oldQuestion);
};

console.log(questions[0].question);
changeQuestion('What was the original question?');
console.log(questions[0].question);
changeQuestion('Who is Harry Potter?');
console.log(questions[0].question);

// to get back the stored value
history.pop()();
console.log(questions[0].question);
history.pop()();
console.log(questions[0].question);
```

</details>

<details>
<summary>How and why to create a queue using an array (FIFO)?</summary>

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

## 08 Nov 2020 (next 09, 10, 12, 14, 17, 21, 26, 02, 09 Dec)
### JavaScript
<details>
<summary>How to create the set and add items?</summary>

```JavaScript
const data = new Set();
// add items
data.add(1);

// based on array or any other iterable
const data = new Set([1, 4, 8]);
```

</details>

<details>
<summary>How to check if the item is in the set?</summary>

```JavaScript
const isElementInData = data2.has(1); // => true
```

</details>

<details>
<summary>How to delete the item and what if there is no such item?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// delete not existed item does nothing
data.delete(1);
```

</details>

<details>
<summary>Is set an iterable and how to iterate?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// iterable
for (const item of data) {
  console.log(item);
}
```

</details>

<details>
<summary>What are the entries of the set?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
const entries = data.entries();

for (const entry of entries) {
  console.log(entry); // => [1, 1] => [4, 4] => [8, 8]
}
```

</details>

<details>
<summary>What is a WeakSet and how is it different from a Set?</summary>

- less methods available
- have to store objects, not primitives
- that's because JS clears those objects (releases to garbage collection) if you don't work with the certain piece of data anymore
```JavaScript
let user = {name: 'Harry'};
const users = new WeakSet();

users.add(user);

// do some operations with user
// still need the set, but not the user
// JS garbage collector will remove the object
// but if we use the Set(), the object (reference type) will not be removed
// from the Set
user = null;
```

</details>
