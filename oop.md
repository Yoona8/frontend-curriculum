# OOP

- [To content](#readme.md)

## General info
<details>
<summary>Notes</summary>

- programming methodology, based mostly on representing a program as a set of objects, which are instances of some class
- consists of interfaces and relations
- abstract thinking
</details>

## Classes
- a group of objects or scenes, which have similar signs
- good class
  - describes one entity
  - solves only one task
  - is not a collection of functions for everything
  - uses correctly when needed (ex. when we need several objects with similar behavior and interface, but the state is different)
- good methods
  - one method = one action
  - if method is not called from the outside, make it private

## Interface
- describes an object's structure, it's properties and methods (+ arguments and return values), does not describe the realization, only data types.
```
Math.abs: function(number): number;
Math.random: function(): number;
Array.map: function(function(*, number, Array): *): Array;
```
- interface is important to minimize errors and for proper usage
```JavaScript
[1, 2, 3].map(parseInt); // 1, NaN,  NaN
parseInt: function(number, number): number;
```

## OOP principles
<details>
<summary>Encapsulation</summary>

- in capsula, interfaces, closed realization details

</details>

<details>
<summary>Inheritance</summary>

- one of the ways to use methods and properties from parents in their children
- But Gotchas!
  - do not create long prototypes chains
  - parent max abstract (banana + jungle)
  - if wrong abstract => multiple inheritance problem, works not in all languages
- Inheritance alternatives
  - Composition (react)
  - Delegation
  - Mixins
  - Interfaces (not in JS)
```JavaScript
class GuitarPlayer extends Man {
  constructor(firstName) {
    super(firstName);

    this.guitarCount = 6;
  }
}

// if we're not adding new properties, not necessary to call the constructor
class GuitarPlayer extends Man {
  // reuse parent properties inside the child class
  // this.jump(); also works
  doubleJump() {
    super.jump();
    super.jump();
  }
}
```

</details>

<details>
<summary>Polymorphism</summary>

- (many forms) an ability to use the same identifier (name) for solving alike problems (but different upon realization)
- one interface and many ways or one signature and several interfaces
- overload
```JavaScript
parseInt(42, 10); // float (number)
parseInt('42', 10); // string
parseInt({ name: 'Max', value: 42 }, 10); // NaN
```
- overrides in depths of the prototype chain
- what if w/o polymorphism?
  - naming problem
  - more complex working with code
```JavaScript
class GuitarPlayer extends Man {
  // to override parent method
  jump() {
    console.log('Mega jump!');
  }

  doubleJump() {
    // to use parent method
    super.jump();
    // to use own overridden method
    this.jump();
  }
}
```
- polymorph class almost = interface in TS
```JavaScript
// adding an abstract class
class AbstractMan {
  constructor(firstName) {
    if (new.target === AbstractMan) {
      throw new Error('...');
    }

    this.name = firstName;
  }

  walk() {
    // for the methods needed to be implemented
    throw new Error('...');
  }

  jump() {}
}

const man = new AbstractMan('Tom'); // error
```

</details>

## Data-binding