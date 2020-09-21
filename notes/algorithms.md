# Data structures and Algorithms

## Data Structures (JS implementation)
<details>
<summary>Lists</summary>

- elements can be repeated
- order matters
- numbered lists
- access via key `list[0]`

</details>

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