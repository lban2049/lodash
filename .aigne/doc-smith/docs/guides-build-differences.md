# Build Differences

Lodash provides several builds and module formats tailored for different environments and use cases. Selecting the appropriate build is key to optimizing your application's bundle size and performance. This guide details the available options and helps you choose the one that best fits your needs.

For an interactive build tool, see the official [Custom Builds](https://lodash.com/custom-builds) page.

## Main Builds

Lodash offers two primary builds: a comprehensive **Full build** and a lightweight **Core build**. Both are available as UMD modules, making them suitable for direct use in browsers or with module loaders.

| Build | Gzipped Size (approx.) | Description |
|---|---|---|
| **Full Build** | ~24 kB | Contains all Lodash methods. Ideal for general-purpose use in Node.js or when a wide range of utilities is needed. |
| **Core Build** | ~4 kB | A smaller subset of Lodash, including essential utility functions. Best for environments where bundle size is critical. |

### CDN and Download Links

You can directly download or link to these builds via a CDN:

<x-cards data-columns="2">
  <x-card data-title="Full Build" data-icon="lucide:box" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js" data-cta="Download">
    The complete Lodash library with all functions included.
  </x-card>
  <x-card data-title="Core Build" data-icon="lucide:box-select" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js" data-cta="Download">
    A lightweight build with a subset of core utilities.
  </x-card>
</x-cards>

For more CDN options, visit the [jsDelivr project page](https://www.jsdelivr.com/projects/lodash).

## Module Formats and Optimization

Beyond the main builds, Lodash supports various module formats to integrate with modern development workflows and bundlers.

### Per-Method Packages (Cherry-Picking)

For maximum bundle size optimization, you can import individual methods. This approach ensures that only the code you use is included in your final bundle. This is highly effective when using bundlers like Webpack, Rollup, or Parcel.

```javascript
// Load only the 'at' method from the main library.
var at = require('lodash/at');

// Load only the 'curryN' method from the FP build.
var curryN = require('lodash/fp/curryN');

// You can also load entire categories.
var array = require('lodash/array');
```

### ES Modules

For projects using ES module syntax (`import`/`export`), the `lodash-es` package is the recommended choice. It allows for tree-shaking, where unused code is automatically eliminated by your bundler.

To further optimize this process, you can use plugins like:
- [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash)
- [lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin)

### Functional Programming (FP) Build

Lodash provides a dedicated build for functional programming styles. The `lodash/fp` module offers methods with these characteristics:

- **Immutable**: Does not mutate input data.
- **Auto-curried**: Functions can be called with one argument at a time.
- **Iteratee-first**: The function to be applied comes before the data.
- **Data-last**: The data collection is the last argument.

```javascript
// Load the FP build for immutable, auto-curried methods.
var fp = require('lodash/fp');
```

## Creating Custom Builds

You can generate your own custom builds using `lodash-cli`. This allows you to package only the methods you need into a single file.

First, install the CLI tool if you haven't already. Then, use the build scripts available in the project's `package.json` or run `lodash-cli` commands directly.

Here are the commands used to generate the standard distribution files:

```shell
# Generate the full build
$ lodash -o ./dist/lodash.js

# Generate the core build
$ lodash core -o ./dist/lodash.core.js
```

By leveraging these different builds and module formats, you can tailor Lodash to the specific performance and size constraints of your project.