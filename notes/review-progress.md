# Review progress and questions I have to review
## 03, 04, 05 Nov 2020 (next 07, 09, 11, 14, 17, 22, 29)
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

## 05 Nov 2020 (next 06, 07, 09, 11, 13, 16, 20, 25, 02 Dec)
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