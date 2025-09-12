# Getting Started

Welcome to Lodash! This guide will get you up and running quickly. Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, and strings.

We'll cover how to install and use Lodash in both browser and Node.js environments.

## Installation

You can add Lodash to your project in several ways, depending on your environment.

### In a Browser

For direct use in a browser, you can use a `<script>` tag. You can download the full build or link to a CDN.

```html HTML Setup icon=logos:html-5
<script src="lodash.js"></script>
```

You can find various CDN options, including minified and core builds, on [jsDelivr](https://www.jsdelivr.com/projects/lodash).

**Example using a CDN:**
```html Using a CDN icon=logos:html-5
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

### In Node.js (Using npm)

The recommended way to install Lodash for a Node.js project is through npm.

```shell Install with npm icon=logos:npm
$ npm i --save lodash
```

Once installed, you can require it in your project:

```javascript Basic Usage icon=logos:nodejs
// Load the full build.
const _ = require('lodash');

const anArray = [1, 2, 3, 4, 5, 6];
const chunkedArray = _.chunk(anArray, 2);

console.log(chunkedArray);
// => [[1, 2], [3, 4], [5, 6]]
```

## Module Formats

Lodash is highly modular, allowing you to load only the parts you need to keep your project's bundle size small. Here are the common ways to use it:

*   **Full Build**: Loads the entire library. Ideal for quick prototyping or when many functions are needed.
    ```javascript icon=logos:javascript
    const _ = require('lodash');
    ```

*   **Core Build**: A smaller build that includes essential and commonly used functions.
    ```javascript icon=logos:javascript
    const _ = require('lodash/core');
    ```

*   **Cherry-pick Methods**: Import individual functions to minimize your bundle size. This is the best approach for production web applications.
    ```javascript icon=logos:javascript
    const at = require('lodash/at');
    const curryN = require('lodash/fp/curryN');
    ```

*   **FP Module**: For a functional programming approach with immutable, auto-curried, iteratee-first, and data-last methods.
    ```javascript icon=logos:javascript
    const fp = require('lodash/fp');
    ```

For a more detailed comparison of the available builds and how to create your own, please see our guide on [Build Differences](./guides-build-differences.md).

## What's Next?

Now that you have Lodash installed, here are some next steps to continue your journey:

<x-cards>
  <x-card data-title="API Reference" data-icon="lucide:book-open" data-href="/api">
    Explore the full list of Lodash functions, organized by category with detailed examples for each.
  </x-card>
  <x-card data-title="Functional Programming Guide" data-icon="lucide:function-square" data-href="/fp-guide">
    Learn about the FP variant of Lodash, which provides powerful tools for functional programming patterns.
  </x-card>
</x-cards>