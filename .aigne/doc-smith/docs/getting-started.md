# Getting Started

Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, and strings. Get up and running in minutes with these instructions.

## Installation

You can add Lodash to your project using a script tag in the browser or by installing it from a package manager like npm.

### In the Browser

To get started in a browser, include the Lodash script on your page. You can host the file yourself or use a CDN.

```html
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

This will make the Lodash library available under the global `_` variable.

<x-cards>
  <x-card data-title="Full Build" data-icon="lucide:box" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js">
    Includes all Lodash methods for comprehensive functionality (~24 kB gzipped).
  </x-card>
  <x-card data-title="Core Build" data-icon="lucide:box-select" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js">
    A lighter version with essential methods for smaller projects (~4 kB gzipped).
  </x-card>
</x-cards>

For more CDN options, visit [jsDelivr](https://www.jsdelivr.com/projects/lodash).

### Using npm

For Node.js applications or projects using a build tool like Webpack or Rollup, install Lodash via npm:

```shell
$ npm i --save lodash
```

## Basic Usage

Once installed, you can start using Lodash functions immediately.

### In Node.js

Require the full library and call a method:

```javascript
// Load the full build.
var _ = require('lodash');

var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

// Find the first active user
var activeUser = _.find(users, function(o) { return o.active; });

console.log(activeUser);
// => { 'user': 'pebbles', 'active': true }
```

### In the Browser

With the script tag included, the `_` variable is available globally:

```html
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
<script>
  var users = [
    { 'user': 'barney',  'active': false },
    { 'user': 'fred',    'active': false },
    { 'user': 'pebbles', 'active': true }
  ];

  var activeUser = _.find(users, { 'active': true });

  console.log(activeUser);
  // => { 'user': 'pebbles', 'active': true }
</script>
```

## Modular Loading for Smaller Bundles

To optimize your application's bundle size, you can import individual methods instead of the entire library. This is especially useful for front-end projects where file size is critical.

### Cherry-pick Methods

You can require methods one by one:

```javascript
// Load only the 'at' method.
var at = require('lodash/at');

var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

### Functional Programming (FP) Build

For a functional programming style with immutable, auto-curried, iteratee-first, and data-last methods, use the FP build.

```javascript
// Load the FP build.
var fp = require('lodash/fp');

var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false }
];

// The FP style is data-last.
var getActiveUsers = fp.filter({ 'active': true });

getActiveUsers(users);
// => [{ 'user': 'barney', 'age': 36, 'active': true }]
```

For a complete guide on this paradigm, see the [Functional Programming Guide](./fp-guide.md).

---

Now that you have Lodash installed and understand the basics, you can explore the complete list of functions in our [API Reference](./api.md).