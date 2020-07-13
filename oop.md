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

</details>
- Polymorphism
- Inheritance and polymorphism
- Data-binding