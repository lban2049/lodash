# Functional Programming Guide

The Lodash FP guide provides a functional programming alternative to the standard Lodash library. It promotes a more declarative and composable style of writing code by adhering to key principles: immutability, auto-currying, and data-last argument order.

This module is ideal for developers who prefer a functional approach and want to build complex data processing pipelines with ease.

## Core Principles

The `lodash/fp` module transforms standard Lodash functions to follow a consistent set of functional programming rules.

### 1. Immutability

FP methods are designed to be pure functions that do not modify their input data. Instead of mutating arrays or objects in place, these methods return a new, cloned instance with the changes applied. This prevents side effects and makes your application's state more predictable.

For example, methods that are mutable in standard Lodash, such as `assign`, `defaults`, `merge`, `pull`, and `reverse`, are made immutable in the FP version.

```javascript In Node.js icon=logos:nodejs
// Load the FP module
const fp = require('lodash/fp');

const originalArray = [1, 2, 3, 4];

// 'remove' in fp returns a new array instead of mutating the original
const newArray = fp.remove(n => n % 2 === 0)(originalArray);

console.log(newArray);
// => [1, 3]

console.log(originalArray);
// => [1, 2, 3, 4] (The original array remains unchanged)
```

### 2. Auto-Currying

All methods in `lodash/fp` are automatically curried. This means you can call a function with fewer arguments than it expects, and it will return a new function that waits for the remaining arguments. This is incredibly powerful for creating specialized, reusable functions.

```javascript icon=logos:javascript
const fp = require('lodash/fp');

const users = [
  { 'user': 'barney', 'active': false },
  { 'user': 'fred',   'active': true },
  { 'user': 'pebbles', 'active': true }
];

// Create a specialized function by providing only the iteratee
const findActiveUser = fp.find({ 'active': true });

// Later, apply this function to your data
const firstActiveUser = findActiveUser(users);

console.log(firstActiveUser);
// => { user: 'fred', active: true }
```

You can also use a placeholder (`fp.placeholder` or `__` as an alias) to supply arguments out of order.

```javascript icon=logos:javascript
const fp = require('lodash/fp');

// The placeholder allows us to specify the data argument first
const getOrFred = fp.getOr('fred', fp.__, { 'a': { 'b': 'barney' } });

// Now we can specify the path
const result = getOrFred('a.b');

console.log(result);
// => 'barney'
```

### 3. Iteratee-First, Data-Last

Method arguments are rearranged to always accept the data (like an array or object) as the last argument. The iteratee or configuration arguments come first. This consistent signature makes it trivial to compose functions together into a sequence of operations.

The most common use case is with `fp.flow` (or `fp.pipe`), which creates a pipeline of functions where the output of one becomes the input for the next.

```javascript icon=logos:javascript
const fp = require('lodash/fp');

const users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred', 'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1, 'active': true }
];

// Create a data processing pipeline
const getActiveUserNames = fp.flow(
  fp.filter('active'), // First, filter for active users
  fp.map('user'),      // Then, get their names
  fp.join(', ')       // Finally, join them into a string
);

const activeNames = getActiveUserNames(users);

console.log(activeNames);
// => 'barney, pebbles'
```

## Method Aliases and Remapping

To align with functional programming conventions and for compatibility with libraries like Ramda, many Lodash methods have aliases. This helps developers transition smoothly and use familiar terminology.

Below is a table of common aliases. Note that this is not an exhaustive list.

| Lodash FP Method | Standard Lodash Method | Common Alias(es) |
|---|---|---|
| `forEach` | `forEach` | `each` |
| `toPairs` | `toPairs` | `entries` |
| `assignIn` | `assignIn` | `extend` |
| `head` | `head` | `first` |
| `isMatch` | `isMatch` | `whereEq`, `matches` |
| `get` | `get` | `prop`, `path`, `property` |
| `placeholder` | (FP only) | `__` |
| `stubFalse` | `stubFalse` | `F` |
| `stubTrue` | `stubTrue` | `T` |
| `every` | `every` | `all` |
| `some` | `some` | `any` |
| `constant` | `constant` | `always` |
| `flowRight` | `flowRight` | `compose` |
| `includes` | `includes` | `contains` |
| `flow` | `flow` | `pipe` |
| `flatten` | `flatten` | `unnest` |

## Custom Conversion

Lodash provides a powerful `convert` method that allows you to generate your own FP-style utility object with customized behavior. You can control options like immutability, currying, and argument rearrangement.

```javascript icon=logos:javascript
const _ = require('lodash');
const convert = require('lodash/fp/convert');

// Create a custom FP version of `map` that is not curried
const fp = convert('map', _.map, { 'curry': false });

// This will now work like standard _.map but with re-arranged arguments
fp(x => x * 2, [1, 2, 3]);
// => [2, 4, 6]
```

This is an advanced feature for users who need fine-grained control over their utility functions.
