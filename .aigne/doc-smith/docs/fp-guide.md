# A Guide to Functional Programming

The Lodash FP module (`lodash/fp`) provides a functional programming version of Lodash. It follows the core principles of immutability, auto-currying, iteratee-first, and data-last, which makes function composition and code reuse more concise and powerful.

Unlike standard Lodash methods, the methods in the FP version are carefully designed to support a more declarative programming paradigm. You can find more information on the [FP Guide](https://github.com/lodash/lodash/wiki/FP-Guide) wiki page.

## Core Principles

The design of Lodash FP is based on four core principles that work together to provide powerful functional programming capabilities for JavaScript.

<x-cards data-columns="2">
  <x-card data-title="Data-Last" data-icon="lucide:align-end-vertical">
    The collection or data object is always passed as the last argument. This makes it easy to create new functions that wait for data to be passed in before executing.
  </x-card>
  <x-card data-title="Auto-Curried" data-icon="lucide:git-fork">
    All methods are auto-curried, which means you can pass partial arguments and get back a new function that waits for the rest of the arguments.
  </x-card>
  <x-card data-title="Immutability" data-icon="lucide:shield-check">
    FP methods do not modify input data. Any operation that would cause side effects (like `fill` or `assign`) returns a new instance, leaving the original data unchanged.
  </x-card>
  <x-card data-title="Iteratee-First" data-icon="lucide:list-filter">
    The function that processes the collection (the iteratee) is passed as the first argument. This complements the data-last principle, facilitating function creation and composition.
  </x-card>
</x-cards>

### Data Flow Comparison

To better visualize the difference between standard Lodash and Lodash FP, the diagram below illustrates the data flow for the `map` function in both modes.

```d2
direction: down

"Standard Lodash Data Flow": {
  direction: right
  data: "Collection\n[1, 2, 3]"
  iteratee: "Iteratee\nn => n * 2"
  map_func: "_.map(collection, iteratee)"
  result: "Result\n[2, 4, 6]"
  
  data -> map_func
  iteratee -> map_func
  map_func -> result
}

"Lodash FP Data Flow (Point-free style)": {
  direction: right
  iteratee_fp: "Iteratee\nn => n * 2"
  curried_func: "fp.map(iteratee)"
  data_fp: "Collection\n[1, 2, 3]"
  apply_data: "curriedMapFn([1, 2, 3])"
  result_fp: "Result\n[2, 4, 6]"

  iteratee_fp -> curried_func: "Returns a new function `curriedMapFn`"
  curried_func -> apply_data
  data_fp -> apply_data
  apply_data -> result_fp
}
```

## Method Conversions

To achieve a functional style, the FP module converts standard Lodash methods. This mainly involves argument reordering and providing aliases.

### Argument Order

Most methods that accept a collection or object as an argument have been rearranged to place the data argument last. This is crucial for currying and function composition.

| Standard Lodash | Lodash FP | Argument Rearrangement Explanation |
|---|---|---|
| `_.filter(collection, predicate)` | `fp.filter(predicate)(collection)` | `predicate` comes first, `collection` comes last. |
| `_.get(object, path, defaultValue)` | `fp.get(path)(object)` or `fp.getOr(defaultValue, path)(object)` | `path` comes first, `object` comes last. `getOr` is a separate variant. |
| `_.isMatchWith(object, source, customizer)` | `fp.isMatchWith(customizer, source)(object)` | `customizer` and `source` come first, `object` comes last. |
| `_.reduce(collection, iteratee, accumulator)` | `fp.reduce(iteratee, accumulator)(collection)` | `iteratee` and `accumulator` come first, `collection` comes last. |
| `_.set(object, path, value)` | `fp.set(path, value)(object)` | `path` and `value` come first, `object` comes last. |

### Method Aliases

To accommodate developers familiar with other functional libraries like Ramda, `lodash/fp` provides aliases for many common methods.

| Lodash FP Alias | Original Lodash Method | Description |
|---|---|---|
| `pipe` | `flow` | Composes functions from left to right. |
| `compose` | `flowRight` | Composes functions from right to left. |
| `prop` | `get` | Gets the value of a property on an object. |
| `assoc` | `set` | Sets the value of a property on an object (immutable). |
| `contains` | `includes` | Checks if a collection includes a certain value. |
| `all` | `every` | Checks if all elements in the collection satisfy the predicate. |
| `any` | `some` | Checks if any element in the collection satisfies the predicate. |
| `__` | `placeholder` | A placeholder for partial application. |
| `T` | `stubTrue` | A function that returns `true`. |
| `F` | `stubFalse` | A function that returns `false`. |

## Partial Application with Placeholders

When you need to pre-fill data in a non-initial argument position, you can use the placeholder `fp.placeholder` (or its alias `__`). This is very useful for creating functions that require a specific argument order.

For example, the signature of `fp.subtract` is `fp.subtract(subtrahend)(minuend)`, which calculates `minuend - subtrahend`.

```javascript
const fp = require('lodash/fp');

// Create a function that subtracts a number from 10
// Equivalent to creating a function x => 10 - x
const subtractFrom10 = fp.subtract(fp.__, 10);

const result = subtractFrom10(4);
console.log(result);
// => 6
```

In this example, the placeholder `__` occupies the position of the first argument (`subtrahend`), allowing us to provide the second argument, `10` (`minuend`), first.

## Advanced Customization: The `convert` Function

If you need finer control over the behavior of the FP module, you can use the `convert` function. It allows you to create a custom instance of Lodash FP and configure its behavior, such as disabling auto-currying or immutability.

```javascript
const _ = require('lodash');
const fp = require('lodash/fp');

// Create a version of Lodash FP with auto-currying disabled
const nonCurriedFp = fp.convert({ 'curry': false });

const iteratee = x => x * 2;
const collection = [1, 2, 3];

// Since currying is disabled, the following call will throw an error
// nonCurriedFp.map(iteratee)(collection);

// You must provide all arguments at once, like a standard Lodash function
const result = nonCurriedFp.map(iteratee, collection);
console.log(result);
// => [2, 4, 6]
```

The `convert` function accepts a configuration object that you can use to enable or disable the following features:

| Option | Default | Description |
|---|---|---|
| `cap` | `true` | Whether to cap the number of arguments for iteratees. |
| `curry` | `true` | Whether to enable auto-currying. |
| `fixed` | `true` | Whether to fix the number of function arguments to support currying. |
| `immutable` | `true` | Whether to enforce immutability by wrapping methods with side effects. |
| `rearg` | `true` | Whether to reorder arguments to achieve a data-last style. |

With this guide, you should have a solid understanding of the core concepts and usage of Lodash FP. To see all available functions, continue to the [API Reference](./api.md).
