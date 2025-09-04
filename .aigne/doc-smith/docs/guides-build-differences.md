# Build Differences

Lodash provides a variety of builds and module formats to accommodate different project requirements, environments, and bundle size constraints. Understanding these differences allows you to select the most efficient build for your needs.

## Available Builds

Lodash offers two primary pre-compiled builds: a full build with all methods and a lightweight core build.

| Build | Gzipped Size (Approx.) | Description |
|---|---|---|
| **Full Build** | ~24 kB | Includes the complete Lodash library. Ideal for environments where bundle size is not the primary concern, such as Node.js backends. |
| **Core Build** | ~4 kB | A lightweight subset of Lodash's most essential functions, suitable for projects where minimizing the JavaScript payload is critical. |

Both builds are available for download directly or through various CDNs.

*   [Download Core build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js)
*   [Download Full build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js)
*   [View CDN copies](https://www.jsdelivr.com/projects/lodash)

## Module Formats & Usage

Lodash can be integrated into your project in several ways, depending on your module system and optimization strategy.

### UMD (Universal Module Definition)

For direct use in browsers, you can include the UMD build via a `<script>` tag. This is a simple way to get started without a build process.

```html
<script src="lodash.js"></script>
```

### CommonJS (Node.js)

In Node.js environments, you can require Lodash using the standard CommonJS syntax.

```javascript
// Load the full build.
var _ = require('lodash');

// Load the core build.
var _ = require('lodash/core');
```

### Functional Programming (FP) Build

For developers using a functional programming style, Lodash provides a dedicated FP build. These methods are immutable, auto-curried, and have iteratee-first, data-last signatures.

```javascript
// Load the FP build
var fp = require('lodash/fp');
```

### Per-Method Packages (Cherry-Picking)

To achieve the smallest possible bundle size, you can import individual methods. This approach is highly effective when used with bundlers like Webpack, Rollup, or Browserify, as it ensures only the code you use is included in the final output.

```javascript
// Cherry-pick a standard method
var at = require('lodash/at');

// Cherry-pick an FP method
var curryN = require('lodash/fp/curryN');
```

### ES Modules & Build Tools

For modern JavaScript projects, several packages facilitate tree-shaking and automated optimization:

*   **`lodash-es`**: An ES module version of Lodash, ideal for use with bundlers that support tree-shaking.
*   **`babel-plugin-lodash`**: A Babel plugin that automatically transforms your code to use per-method imports, simplifying the cherry-picking process.
*   **`lodash-webpack-plugin`**: A Webpack plugin that further optimizes Lodash builds by replacing method implementations with smaller, more specific versions.

## Creating Custom Builds

You can generate custom builds tailored to your specific needs using `lodash-cli`. This allows you to create a build containing only the methods you require.

The following commands demonstrate how to generate the standard full and core builds:

```shell
# Generate the full build from source
$ lodash -o ./dist/lodash.js

# Generate the core build
$ lodash core -o ./dist/lodash.core.js
```

--- 

By choosing the appropriate build and module format, you can optimize your project's performance and bundle size. For more in-depth optimization techniques, refer to the [Performance](./guides-performance.md) guide.