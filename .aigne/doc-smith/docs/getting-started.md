# Getting Started

Welcome to Lodash! This guide will get you up and running with the library in your project. Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, and strings.

For a complete list of all available functions, please see the [API Reference](./api.md).

## Installation

Lodash is available as a [UMD](https://github.com/umdjs/umd) module, which allows it to be used in various environments. You can add it to your project using a script tag in the browser or by installing it from a package manager like npm.

### In a Browser

To use Lodash directly in a browser, you can include it via a `<script>` tag. Download the full build from the official site or link to a CDN copy.

```html
<script src="lodash.js"></script>
```

You can find various CDN options on [jsdelivr](https://www.jsdelivr.com/projects/lodash).

### Using npm

For Node.js applications or projects using a bundler like webpack or Rollup, the recommended way to install Lodash is through npm.

```shell
$ npm i --save lodash
```

## Basic Usage

Once installed, you can require Lodash in your Node.js files or import it in your modern JavaScript projects.

### In Node.js

Here are the common ways to load Lodash in a Node.js environment:

```javascript
// Load the full build.
var _ = require('lodash');

// Load the core build (a smaller subset of functions).
var _ = require('lodash/core');

// Load the FP build for functional programming with immutable, auto-curried methods.
var fp = require('lodash/fp');
```

### Cherry-picking Methods

To keep your bundle size small, you can import individual methods. This is especially useful for front-end projects.

```javascript
// Cherry-pick a specific method.
var at = require('lodash/at');

// Cherry-pick a method from the FP build.
var curryN = require('lodash/fp/curryN');
```

### Your First Function Call

Let's try a simple example. We'll use the `_.chunk` method, which splits an array into groups of a specified size.

```javascript
const _ = require('lodash');

const data = ['a', 'b', 'c', 'd', 'e'];

const chunks = _.chunk(data, 2);

console.log(chunks);
// => [['a', 'b'], ['c', 'd'], ['e']]
```

This demonstrates how Lodash can simplify common data manipulation tasks with clear and concise code.

## Next Steps

Now that you have Lodash installed, you're ready to explore its powerful features. Dive into the [API Reference](./api.md) to discover all the functions available to you.