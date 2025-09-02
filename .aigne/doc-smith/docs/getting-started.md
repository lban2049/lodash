# Getting Started

This guide provides concise instructions for installing and using Lodash in various environments to help you get started quickly. Lodash is a powerful JavaScript utility library that simplifies programming by providing helper functions for tasks involving arrays, numbers, objects, strings, and more.

## In Browsers

To use Lodash directly in a browser, you can include it via a CDN. We offer several builds to suit different needs.

Add the following to your HTML file:

```html
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

### Builds

You can choose different builds based on your project's requirements. The core build is smaller and includes the most commonly used utility functions.

| Build | Size (gzipped) | Description |
|---|---|---|
| [Core build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js) | ~4 kB | Includes the core, most commonly used Lodash functions. |
| [Full build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js) | ~24 kB | Includes all Lodash functions. |

For more CDN options, visit [jsDelivr](https://www.jsdelivr.com/projects/lodash).

### Quick Example

After including the script, the `_` variable is exposed as the Lodash global. You can use it to call all Lodash functions.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Lodash Example</title>
  <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
</head>
<body>
  <script>
    const users = [
      { 'user': 'barney',  'active': false },
      { 'user': 'fred',    'active': false },
      { 'user': 'pebbles', 'active': true }
    ];

    // Use _.filter to find users where 'active' is true
    const activeUsers = _.filter(users, { 'active': true });
    console.log(activeUsers);
    // => [{ 'user': 'pebbles', 'active': true }]

    // Use _.chunk to split the array into chunks of a specified size
    const chunks = _.chunk(['a', 'b', 'c', 'd'], 2);
    console.log(chunks);
    // => [['a', 'b'], ['c', 'd']]
  </script>
</body>
</html>
```

## Node.js & Bundlers (Webpack/Rollup)

For Node.js projects or front-end projects using bundlers, it's recommended to install Lodash using npm or another package manager.

### Installation

Install Lodash using npm:
```shell
npm i --save lodash
```

### Usage

After installation, you can import the full library, specific builds, or individual functions as needed.

**1. Import the full build**

Load the full Lodash library.
```javascript
const _ = require('lodash');

const result = _.chunk(['a', 'b', 'c', 'd'], 2);
console.log(result);
// => [['a', 'b'], ['c', 'd']]
```

**2. Import the core build**

If you only need core functionality, you can import the smaller core build.
```javascript
const _ = require('lodash/core');
```

**3. Cherry-picking methods**

To optimize your final bundle size, it's highly recommended to cherry-pick the methods you need. This ensures only the code you use is included.

```javascript
const at = require('lodash/at');
const curryN = require('lodash/fp/curryN');

const object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

const result = at(object, ['a[0].b.c', 'a[1]']);
console.log(result);
// => [3, 4]
```

### Other Module Formats

Lodash also offers several module formats to suit different development needs:

- **`lodash-es`**: An ES module build for easy Tree Shaking.
- **`babel-plugin-lodash`** & **`lodash-webpack-plugin`**: Used with Babel and Webpack to automatically transform Lodash calls into cherry-picked imports, greatly optimizing bundle size.
- **`lodash/fp`**: A functional programming version that provides immutable, auto-curried, iteratee-first, data-last methods.
- **`lodash-amd`**: For use with AMD module loaders.

## Next Steps

Now that you know how to include and use Lodash in your projects, we recommend you browse the [API Reference](./api.md) to explore all the powerful functions it offers.