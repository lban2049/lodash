# Build Differences

Lodash is a versatile library available in various builds and module formats, allowing you to choose the best option for your project's specific needs, whether you're optimizing for bundle size, working in different JavaScript environments, or using a functional programming style.

This guide explains the primary builds, available module formats, and how to create custom builds for maximum efficiency.

## Primary Builds

Lodash offers two main builds that you can download directly or access via a CDN. The choice between them depends on the number of methods you require and your bundle size constraints.

| Build | Gzipped Size (approx.) | Description |
|---|---|---|
| **Full Build** | ~24 kB | The complete Lodash library. Includes all available methods and is the most common choice for general-purpose use. |
| **Core Build** | ~4 kB | A lightweight version containing a subset of popular and essential Lodash methods. Ideal for projects where a minimal footprint is critical. |

## Module Formats & Usage

Lodash can be integrated into your project in several ways, depending on your environment.

### In the Browser

For direct use in a browser, you can include the full build via a `<script>` tag. This will create a global `_` variable.

```html HTML icon=logos:html-5
<script src="lodash.js"></script>
```

CDN copies are also available via services like [jsDelivr](https://www.jsdelivr.com/projects/lodash).

### In Node.js (CommonJS)

When using Node.js, you can install Lodash via npm and `require` the builds you need.

```shell Shell icon=mdi:bash
$ npm i --save lodash
```

```javascript Node.js Usage icon=logos:nodejs
// Load the full build.
var _ = require('lodash');

// Load the core build for a smaller footprint.
var _ = require('lodash/core');

// Load the FP build for functional programming.
var fp = require('lodash/fp');
```

### With Modern Bundlers (ES Modules)

For applications using bundlers like webpack, Rollup, or Vite, you can significantly reduce your final bundle size by importing only the methods you need. This is often referred to as "cherry-picking".

This approach works best with packages like `lodash-es` that provide ES Modules, enabling effective tree-shaking.

```javascript Cherry-picking Methods icon=logos:javascript
// Cherry-pick methods for smaller bundles.
import at from 'lodash/at';
import curryN from 'lodash/fp/curryN';
```

To automate this process, you can use tools like [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash) and [lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin).

## Specialized Builds

Beyond the primary builds, Lodash offers specialized versions for different programming paradigms and use cases.

### Functional Programming (FP)

The `lodash/fp` build provides methods that are immutable, auto-curried, and follow an iteratee-first, data-last argument order. This style is preferred by developers practicing functional programming.

```javascript Loading the FP Build icon=logos:javascript
var fp = require('lodash/fp');
```

### Per-Method Packages

For ultimate control over bundle size, every Lodash method is available as its own individual npm package. This is ideal for small projects or libraries where you only need one or two helper functions.

Example packages include `lodash.at`, `lodash.curry`, etc. You can find all of them under the [`lodash-modularized` keyword on npm](https://www.npmjs.com/browse/keyword/lodash-modularized).

### Other Module Formats

Lodash is also available for other module systems:
- **`lodash-amd`**: For projects using Asynchronous Module Definition (AMD).

## Creating Custom Builds

You can generate your own custom builds of Lodash using `lodash-cli`. This allows you to create a file containing only the specific methods your project uses.

```shell Creating Builds with lodash-cli icon=mdi:bash
# Generate a full build
$ lodash -o ./dist/lodash.js

# Generate a core build
$ lodash core -o ./dist/lodash.core.js
```