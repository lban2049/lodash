# Getting Started

This guide provides concise, copy-paste ready instructions to get you up and running with Lodash in your project. Whether you're working in a web browser or a Node.js environment, you can start using Lodash's powerful utility functions in just a few steps.

## In a Browser

The simplest way to start using Lodash in a browser is to include it via a `<script>` tag. You can download a copy directly or use a Content Delivery Network (CDN) to serve the file.

```html title="index.html"
<script src="lodash.js"></script>
```

For convenience, you can use a popular CDN like jsDelivr to include Lodash without having to host the file yourself:

```html title="index.html"
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

Once included, the Lodash library will be available via the global `_` variable.

```javascript Example Usage icon=logos:javascript
const array = [1, 2, 3, 4];
const chunkedArray = _.chunk(array, 2);

console.log(chunkedArray);
// => [[1, 2], [3, 4]]
```

<x-card data-title="Find CDN Copies" data-icon="lucide:package-check" data-href="https://www.jsdelivr.com/projects/lodash" data-cta="View CDNs">
  Explore different versions and builds of Lodash available on the jsDelivr CDN.
</x-card>

## Using Node.js and npm

For server-side applications or projects using a module bundler (like Webpack, Rollup, or Browserify), you can install Lodash as a dependency using npm.

### Installation

Run the following command in your project's terminal:

```shell Installation Command icon=logos:npm
npm i --save lodash
```

### Basic Usage

Once installed, you can require the full library in your Node.js files.

```javascript icon=logos:nodejs
// Load the full build.
const _ = require('lodash');

const users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

const activeUser = _.find(users, { 'active': true });

console.log(activeUser);
// => { user: 'pebbles', active: true }
```

### Modular Imports

Lodash is highly modular, allowing you to load only the parts you need to keep your application's bundle size small. This is great for performance, especially in front-end applications.

Here are a few ways to load modules:

**Core Build**

Load a smaller, core build with the most essential functions.

```javascript Core Build
const _ = require('lodash/core');
```

**Functional Programming (FP) Build**

For a functional programming style with immutable, auto-curried, and data-last methods.

```javascript FP Build
const fp = require('lodash/fp');
```

**Cherry-pick Methods**

For maximum bundle size optimization, you can import individual methods. This is the recommended approach for modern web development.

```javascript Cherry-picking
const at = require('lodash/at');
const curryN = require('lodash/fp/curryN');

const object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
const values = at(object, ['a[0].b.c', 'a[1]']);

console.log(values);
// => [3, 4]
```

## Next Steps

Now that you have Lodash installed, you're ready to explore its powerful features. Dive into the complete [API Reference](./api.md) to see the full list of available methods and find the perfect utility for your needs.