# Functional Programming Guide

The `lodash/fp` module provides a more functional approach to programming by offering an immutable, auto-curried, iteratee-first, data-last version of Lodash methods. This guide explains the core concepts and how to leverage them.

To get started, simply import from `lodash/fp`:

```js
// Load the FP build for immutable auto-curried iteratee-first data-last methods.
var fp = require('lodash/fp');
```

## Core Principles

The functional programming variant of Lodash is built on four main principles that enable a different, more declarative style of coding, particularly for data manipulation.

### 1. Immutability

Standard Lodash methods sometimes mutate the input array or object (e.g., `_.pull`, `_.assign`). In the FP version, these methods are wrapped to operate immutably. Instead of modifying the original data structure, they always return a new, updated one.

For example, methods that mutate arrays like `fill`, `pull`, `pullAll`, and `reverse` will return a new array. Similarly, object methods like `assign`, `defaults`, and `merge` will return a new object.

```js
const data = { 'a': 1, 'b': 2 };

// Standard Lodash (mutates 'data')
// _.assign(data, { 'c': 3 });
// console.log(data); // => { 'a': 1, 'b': 2, 'c': 3 }

// Lodash FP (returns a new object)
const result = fp.assign({ 'c': 3 }, data);
console.log(result); // => { 'a': 1, 'b': 2, 'c': 3 }
console.log(data);   // => { 'a': 1, 'b': 2 } (original is unchanged)
```

### 2. Data-Last Method Signatures

Most Lodash methods have a `(data, ...args)` signature. The FP variant rearranges these arguments to be data-last: `(...args, data)`. This is a critical change that facilitates function composition and currying.

| Standard Lodash | Lodash FP |
|---|---|
| `_.map(collection, iteratee)` | `fp.map(iteratee, collection)` |
| `_.filter(collection, predicate)` | `fp.filter(predicate, collection)` |
| `_.get(object, path, defaultValue)` | `fp.get(path, object)` or `fp.getOr(defaultValue, path, object)` |

This convention allows you to create specialized functions by pre-filling the arguments, leaving the data to be supplied later.

### 3. Auto-Currying

All methods in `lodash/fp` are automatically curried. This means you can call a function with fewer arguments than it expects, and it will return a new function that waits for the remaining arguments. This works seamlessly with the data-last approach.

```js
const users = [{ 'name': 'Alice', 'active': true }, { 'name': 'Bob', 'active': false }];

// Create a specialized function by providing the iteratee argument first.
const getNames = fp.map(fp.get('name'));

// Now, apply this function to your data.
const names = getNames(users);
// => ['Alice', 'Bob']
```

You can also use a placeholder, `fp.__`, to supply arguments out of order.

```js
// Create a function that divides any number by 2
const divideBy2 = fp.divide(fp.__, 2);

divideBy2(10); // => 5
```

### 4. Capped Iteratee Arguments

By default, iteratee functions passed to methods like `map` and `filter` receive only one argument: `(value)`. This prevents common errors where, for example, `parseInt` receives the `index` argument and produces unexpected results.

## Function Composition

The primary benefit of these principles is powerful and readable function composition. You can build complex data transformations by chaining simple functions together using `fp.flow` (left-to-right) or `fp.flowRight` (right-to-left).

```js
const users = [
  { 'name': 'ALICE', 'age': 30 },
  { 'name': 'bob', 'age': 25 },
  { 'name': 'CHARLIE', 'age': 35 }
];

const processUsers = fp.flow(
  fp.filter(user => user.age > 28),
  fp.map(fp.get('name')),
  fp.map(fp.lowerCase),
  fp.map(fp.capitalize)
);

const result = processUsers(users);
// => ['Alice', 'Charlie']
```

## Aliases & Remapping

To provide a more consistent FP experience and align with conventions from other libraries like Ramda, `lodash/fp` includes several aliases and remapped methods.

| Lodash FP Alias | Real Lodash Method |
|---|---|
| `pipe` | `flow` |
| `compose` | `flowRight` |
| `prop` | `get` |
| `propEq` | `matchesProperty` |
| `assoc` | `set` |
| `dissoc` | `unset` |
| `any` | `some` |
| `all` | `every` |
| `__` | `placeholder` |
| `equals` | `isEqual` |
| `T` | `stubTrue` |
| `F` | `stubFalse` |

## Custom Conversion

You can create your own FP-style functions or convert an entire library using `fp.convert`. This is an advanced feature that gives you control over the conversion process.

```js
const myLib = {
  add: (a, b) => a + b
};

const fpLib = fp.convert(myLib, {
  'curry': true,
  'rearg': true
});

const add5 = fpLib.add(5);
add5(10); // => 15
```

The `convert` function accepts an options object to control its behavior:

| Option | Default | Description |
|---|---|---|
| `cap` | `true` | Specifies capping iteratee arguments. |
| `curry` | `true` | Specifies currying. |
| `fixed` | `true` | Specifies fixed arity. |
| `immutable` | `true` | Specifies immutable operations. |
| `rearg` | `true` | Specifies rearranging arguments to be data-last. |

---

By embracing these functional principles, `lodash/fp` enables a declarative, powerful, and highly reusable way to manipulate data. For a complete list of functions, please see the [API Reference](./api.md).
