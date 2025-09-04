# Functional Programming Guide

The `lodash/fp` module provides an immutable, auto-curried, iteratee-first, data-last version of Lodash methods. This guide explains the core principles of the FP-style variant and how it differs from the standard Lodash build.

To get started, simply import the `fp` module:

```js
// Load the FP build for immutable auto-curried iteratee-first data-last methods.
var fp = require('lodash/fp');
```

## Core Principles

The FP module is built on several key functional programming principles that facilitate creating modular, reusable, and side-effect-free code.

### 1. Immutability

Unlike many standard Lodash methods, functions in the `lodash/fp` module are immutable. They do not modify the input data. Instead, they return a new, modified instance. This applies to methods that would typically mutate arrays or objects.

For example, methods like `assign`, `pull`, and `set` are wrapped to first clone the input data before performing the operation, ensuring the original data structure remains unchanged.

Below are examples of standard Lodash methods that are wrapped for immutability in the FP module:

| Category | Methods Made Immutable |
| --- | --- |
| **Array** | `fill`, `pull`, `pullAll`, `pullAllBy`, `pullAllWith`, `pullAt`, `remove`, `reverse` |
| **Object** | `assign`, `assignAll`, `assignIn`, `defaults`, `defaultsDeep`, `merge`, `mergeAll` |
| **Setters** | `set`, `setWith`, `unset`, `update`, `updateWith` |

### 2. Auto-Currying

All methods in the FP module with an arity greater than 1 are auto-curried. This allows you to create new functions by partially applying arguments. This feature is central to building up complex operations from simpler functions.

```js
const fp = require('lodash/fp');

// Create a specialized function by providing the iteratee.
const getNames = fp.map(fp.get('name'));

const users = [{ name: 'Alice' }, { name: 'Bob' }];

// Apply the data to the specialized function.
getNames(users);
// => ['Alice', 'Bob']
```

You can also use the placeholder `fp.placeholder` (aliased as `__`) to defer providing an argument.

```js
const g = fp.get(__, { 'a': 1 });

g('a');
// => 1
```

### 3. Data-Last and Argument Reordering

To facilitate currying and function composition, all methods are data-last. This means the data structure being operated on (like an array or object) is provided as the final argument. This is achieved by reordering the original Lodash method arguments.

Common reordering patterns include:
- **2-argument functions**: `(a, b)` becomes `(b, a)`.
- **3-argument functions**: `(a, b, c)` becomes `(c, a, b)`.

This makes it easy to create pipelines of operations using composition functions like `fp.flow`.

**Standard Lodash (Data-First)**
```js
const _ = require('lodash');
_.map(['a', 'b', 'c'], _.toUpper);
// => ['A', 'B', 'C']
```

**Lodash FP (Data-Last)**
```js
const fp = require('lodash/fp');
fp.map(fp.toUpper)(['a', 'b', 'c']);
// => ['A', 'B', 'C']
```

### 4. Iteratee-First

Iteratee functions (callbacks) are always the first argument. This consistent signature, combined with data-last, is what makes composing functions straightforward.

```js
const fp = require('lodash/fp');

const getFirstAndDouble = fp.flow(
  fp.map(x => x * 2),
  fp.first
);

getFirstAndDouble([1, 2, 3]);
// => 2
```

## Aliases for Interoperability

To provide a familiar experience for developers coming from other functional libraries like Ramda, `lodash/fp` includes several common aliases.

| Alias | Lodash FP Method | Description |
| --- | --- | --- |
| `__` | `placeholder` | The curry placeholder for partial application. |
| `pipe` | `flow` | Left-to-right function composition. |
| `compose` | `flowRight` | Right-to-left function composition. |
| `prop` | `get` | Retrieves a property value from an object. |
| `path` | `get` | Retrieves a nested property value from an object. |
| `equals` | `isEqual` | Performs a deep equality comparison. |
| `always` | `constant` | Creates a function that returns a constant value. |
| `T` | `stubTrue` | A function that always returns `true`. |
| `F` | `stubFalse` | A function that always returns `false`. |
| `any` | `some` | Checks if any element in a collection passes a test. |
| `all` | `every` | Checks if all elements in a collection pass a test. |

## Custom Conversion

The FP module is generated using a `convert` function that can be used to create custom Lodash variants with specific behaviors. This is an advanced feature that allows fine-grained control over the generated functions.

Each FP method has a `.convert()` method attached, which accepts an options object.

```js
const fp = require('lodash/fp');

// Create a mutable, data-first, but still curried version of `set`
const mutableCurriedSet = fp.set.convert({
  'immutable': false,
  'rearg': false
});
```

Available conversion options include:
- `cap` (boolean): Specify capping iteratee arguments. Defaults to `true`.
- `curry` (boolean): Specify currying. Defaults to `true`.
- `fixed` (boolean): Specify fixed arity. Defaults to `true`.
- `immutable` (boolean): Specify immutable operations. Defaults to `true`.
- `rearg` (boolean): Specify rearranging arguments. Defaults to `true`.

---

For a complete list of available functions and their signatures, please see the [API Reference](./api.md).