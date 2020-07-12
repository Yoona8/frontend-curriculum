# OOP

- [To content](#readme.md)

- методология программирования, основанная преимущественно на представлении программы в виде совокупности объектов, каждый из которых является экземпляром определенного класса
- код в виде объектов (интерфейсы) и взаимосвязи между ними
- мышление абстракциями
- высокий порог входа

## Классы
- группа предметов или явлений, обладающих общими признаками.

## Интерфейс
- описание структуры объекта, его свойств и методов, а также аргументов этих методов и их возвращаемых значений. Не описывает реализацию, только типы данных.
```
Math.abs: function(number): number;
Math.random: function(): number;
Array.map: function(function(*, number, Array): *): Array;
```
- интерфейс важен, чтобы избежать ошибок, использовать методы по назначению
```JavaScript
[1, 2, 3].map(parseInt); // 1, NaN,  NaN
parseInt: function(number, number): number;
```

## Принципы ООП
<details>
<summary>Encapsulation</summary>

- in capsula, интерфейсы, сокрытие деталей реализации

</details>

<details>
<summary>Inheritance</summary>

- один из способов исп. методы и свойства одних obj (parent) в других (child)
- But Gotchas!
  - не создавать long prototypes chains
  - parent max abstract (banana + jungle)
  - if wrong abstract => проблема множественного наследования, которое работает не во всех языках
- Альтернативы наследованию
  - Composition (react)
  - Delegation
  - Mixins
  - Interfaces (not in JS)

</details>
- Polymorphism
- Inheritance and polymorphism
- Data-binding