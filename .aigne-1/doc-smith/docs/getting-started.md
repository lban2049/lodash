# Getting Started

To begin using Lodash, integrate it into your project. This guide provides steps for installation via package managers, setup in different JavaScript environments, and a quick example to get you started.

## Download Lodash

You can download specific builds of Lodash directly or use a CDN:

*   [Core build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js) (~4 kB gzipped, optimized for size)
*   [Full build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js) (~24 kB gzipped, includes all features)
*   [CDN copies](https://www.jsdelivr.com/projects/lodash) (for quick browser integration)

Review the [build differences](https://github.com/lodash/lodash/wiki/build-differences) to select the right version for your project.

## Installation Methods

Lodash supports various installation methods to suit your development environment.

### In a Browser

Include the Lodash library directly in your HTML using a `<script>` tag:

```html
<script src="lodash.js"></script>
```

### Using npm

If you are using Node Package Manager (npm), you can install Lodash as a dependency for your project. First, ensure npm is up to date, then install Lodash:

```shell
$ npm i -g npm
$ npm i --save lodash
```

This command installs the full Lodash build and saves it as a dependency in your `package.json`.

### In Node.js

After installing via npm, you can require Lodash modules in your Node.js application. You have several options depending on your needs:

*   **Load the full build:** Imports all Lodash methods.

    ```js
    var _ = require('lodash');
    ```

*   **Load the core build:** Imports a smaller, more focused set of utility methods.

    ```js
    var _ = require('lodash/core');
    ```

*   **Load the FP build:** For functional programming paradigms with immutable, auto-curried, iteratee-first, and data-last methods.

    ```js
    var fp = require('lodash/fp');
    ```

*   **Load method categories:** Import only specific categories of methods to reduce bundle size.

    ```js
    var array = require('lodash/array');
    var object = require('lodash/fp/object');
    ```

*   **Cherry-pick individual methods:** For the smallest possible browserify/rollup/webpack bundles, import only the methods you need.

    ```js
    var at = require('lodash/at');
    var curryN = require('lodash/fp/curryN');
    ```

**Note:** If you are using Node.js versions older than 6 for REPL (Read-Eval-Print Loop), install `n_` for optimal Lodash usage:

```shell
$ npm i -g n_
```

## Why Use Lodash?

Lodash streamlines JavaScript development by simplifying common operations on arrays, numbers, objects, and strings. Its modular methods are particularly effective for:

*   Iterating over arrays, objects, and strings.
*   Manipulating and testing values.
*   Creating composite functions.

## "Hello World" with Lodash

Let's write a simple Node.js example to see Lodash in action. This example uses the `_.camelCase` method to convert a string.

```javascript
const _ = require('lodash');

const greeting = "hello world lodash";
const camelCasedGreeting = _.camelCase(greeting);

console.log(camelCasedGreeting);
```

**Example Output:**

```
helloWorldLodash
```

This shows how a simple string transformation is handled by Lodash, making common tasks more concise and readable.

---

Now that you have Lodash installed and understand its basic benefits, proceed to the [Core Concepts](./core-concepts.md) section to delve deeper into its modular design and various distribution formats.