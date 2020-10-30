# Data structures and Algorithms
Programming = Algorithms + Data Structures

## Algorithms
<details>
<summary>General info</summary>

- a sequence of steps
- finite, ordered, predictable
- linear - step by step
- logical - on condition
- recursive - iterations of the same action till the certain condition is met
  - every recursive algorithm has a condition
  - must have a closing condition
  - iteration - repetition
  - recursion - self-repetition (everywhere: programming, linguistics, maths, nature)

</details>

## Performance and The "Big O" notation
<details>
<summary>General info</summary>

- for comparing different algorithms
- how long does an operation take?
- expressed in a generalized form (not in time units but in mathematical terms)
- time complexity
<img width="500" src="../images/big-o.png" alt="Big O notation">

</details>

<details>
<summary>Constant Time Complexity</summary>

- `O(1)`
```JavaScript
// Constant Time Complexity => O(1)
function getEvenOrOdd(number) {
  return number % 2 ? 'Odd' : 'Even';
}
```

</details>

<details>
<summary>Linear Time Complexity</summary>

- `O(n)`
```JavaScript
// T = 1 + 1 + 1 + 2 + [0 - 2] + 1
// initial stage and result are the same T (constants)
// T = 3 (init) + 2 + [0 - 2] + 1 (return)
// number of elements might be different (n)
// since the initiation of the current min depends on the array
// c2 - constant time of executions inside the for loop
// T = 2 + n * c2 + 1
// the dependance on number of values matters
// T = n => Linear Time Complexity => O(n)
// best case: [1] => O(1)
// worst case: [7, 6] => O(n)
// average case: [?, ?, ?] => O(n) => matters the most
function getMin(numbers) { // [4, 5, -2]
  if (!numbers.length) { // 1 execution
    throw new Error('Should be not an empty array');
  }

  let currentMin = numbers[0]; // 1 execution

  for (let i = 1; i < numbers.length; i++) { // 1 execution
    if (numbers[i] < currentMin) { // 2 executions
      currentMin = numbers[i]; // 0 - 2 executions
    }
  }

  return currentMin; // 1 execution
}
```

</details>

<details>
<summary>Quadratic Time Complexity</summary>

- `O(n^2)`
```JavaScript
// compare to the other algorithm
// T = n * (n - 1) => Quadratic Time Complexity => O(n^2)
// best case: [1, 2, 3] => O(n^2)-
// worst case: [4, 3, 1] => O(n^2)+
// average case: [?, ?, ?] => O(n^2) => matters the most
function getMinSorting(numbers) { // [3, 5, 10]
  if (!numbers.length) { // 1 execution
    throw new Error('Should be not an empty array');
  }

  for (let i = 0; i < numbers.length; i++) { // 1 execution
    let outerNumber = numbers[i]; // n executions

    for (let j = i + 1; j < numbers.length; j++) {
      let innerNumber = numbers[j]; // (n - 1) executions

      if (outerNumber > innerNumber) {
        numbers[i] = innerNumber;
        numbers[j] = outerNumber;

        outerNumber = numbers[i];
        innerNumber = numbers[j];
      }
    }
  }

  return numbers[0]; // 1 execution
}
```

</details>

<details>
<summary>Logarithmic Time Complexity</summary>

- `O(log n)`
- ex: binary search

</details>

<details>
<summary>Learn more</summary>

- [ ] [How you can change the world by learning Data Structures and Algorithms](https://adrianmejia.com/how-you-can-change-the-world-learning-data-structures-algorithms-free-online-course-tutorial/)
- [ ] [8 time complexities that every programmer should know](https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course/)

</details>

## Data Structures (Lists)
<details>
<summary>General info</summary>

- elements can be repeated
- order matters
- numbered lists
- access via key `list[0]`

</details>

<details>
<summary>Time Complexity</summary>

```JavaScript
const numbers = [1, 3, 17];

// Constant Time Complexity O(1)
// [1, 3, 17] => [1, 3, 17, _]
// indexes are not affected
numbers.push(34);

// Linear Time Complexity O(n)
// [1, 3, 17] => [_, 1, 3, 17]
// indexes are reassigned for every position
numbers.unshift(51);

const currentNumber = numbers[1]; // O(1)
const num = number.find(num => num === 3); // best: O(1), worst, av: O(n)
```

</details>

## Data Structures
<details>
<summary>Sets</summary>

- order doesn't matter
- unique elements `set.add('item');`
- has no keys
- access via value `set.has('item');`

</details>

<details>
<summary>Dictionaries</summary>

- associative array
- no order, has keys
- unique keys
```JavaScript
const filterValueToScale = {
  'smallest': 0.25,
  'small': 0.5,
  'normal': 1,
  'big': 1.5
};

// if you need to iterate, use Map
const pairs = new Map([
  ['Ron', 'Hermione'],
  ['Harry', 'Ginny']
]);
for (const pair of pairs) {
  console.log(pair); // ['Ron', 'Hermione']
}
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Data Structures in JavaScript: Arrays, HashMaps, and Lists](https://adrianmejia.com/data-structures-time-complexity-for-beginners-arrays-hashmaps-linked-lists-stacks-queues-tutorial/)
- [ ] [JavaScript Algorithms and Data Structures](https://github.com/trekhleb/javascript-algorithms)

</details>