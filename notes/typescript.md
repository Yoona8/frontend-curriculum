# TypeScript

## Types
<details>
<summary>Assigning types</summary>

```TypeScript
const addNumbers = (a: number, b: number) => {
  return a + b;
};

const users: { name: string, greet: () => void }[] = [];
const harry = { 
  name: 'Harry',
  age: 27,
  greet() {
    console.log(this.name);
  }
};

// no error here (checks if it has at least the announced fields)
// may contain other properties or methods
users.push(harry);

// defining a type
type User = { name: string, greet: () => void };
const user: User = {
  name: 'Ron',
  age: 27,
  greet() {
    console.log(this.name);
  }
};

// literal types
const printHarry = (name: 'Harry') => {
  console.log(name);
};

// union types
const printName = (name: string, mode: 'console' | 'alert') {
  switch (mode) {
    case 'console':
      console.log(name);
      break;
    case 'alert':
      alert(name);
      break;
  }
}

// better with enums
// stored as numbers under the hood { 'CONSOLE': 0, 'ALERT': 1 }
enum Mode { CONSOLE, ALERT };

const printName2 = (name: string, mode: Mode) {
  switch (mode) {
    case Mode.CONSOLE:
      console.log(name);
      break;
    case Mode.ALERT:
      alert(name);
      break;
  }
}
```

</details>

<details>
<summary>Casting</summary>

```TypeScript
// both syntax work in a same way
const input = document.querySelector('input') as HTMLInputElement;
const input = <HTMLInputElement>document.querySelector('input');
```

</details>

<details>
<summary>Generic types</summary>

- types working with other types together (ex: array of something, promise resolving to some other type)
```TypeScript
// basic assignment
const numbers: Array<number> = [];
// syntactic sugar
const values: number[] = [];

const dataPromise: Promise<User> = fetch('');

// creating a generic type
// wherever we call the function
// tell what type we pass as an argument
function log<T>(value: T) {
  console.log(value);
  return value;
}

log<string>('Hello!').split();
```

</details>

<details>
<summary>Learn more</summary>

- [Types: Generics and Augmentation will Make You a TypeScript Wizard](https://medium.com/iqoqo-engineering/two-advanced-techniques-to-make-you-a-typescript-wizard-df42e00b1cf8)

</details>

## Classes and Interfaces
<details>
<summary>How to create a class?</summary>

```TypeScript
class Player {
  // have to add fields in TS
  name: string;
  age: number;
  // can set the private fields
  private level: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

// shorter form of creating a class
// exactly the same as the first one
class Player {
  private level: number;

  constructor(public name: string, public age: number) {}
}
```

</details>

<details>
<summary>Why and hot to use an interface?</summary>

- it's similar to a class but when you don't need to create an instance
- can be used as a type (alternative to the `type`)
- the difference to `type` is that can be used by classes (TS feature)
```TypeScript
interface User {
  name: string;
  age: number;
  greet(): void;
}

// forces to have the fields defined in the interface
class Player implements User {
  constructor(
    public name: string,
    public age: number,
  ) {}

  greet() {}
}
```

</details>

## Other features
<details>
<summary>How to ignore the null case?</summary>

```TypeScript
// mostly for strict configuration
// potentially there can be no button (TS error in strict mode)
const submitButtonElement = document.querySelector('button');
// can add the check
if (submitButtonElement) {
  // do something
}

// or just use !
const submitButtonElement2 = document.querySelector('button')!;
```

</details>

<details>
<summary>Learn more</summary>

- [TS official](https://www.typescriptlang.org/)

</details>