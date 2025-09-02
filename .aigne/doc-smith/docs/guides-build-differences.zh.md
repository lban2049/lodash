# Build Differences

Lodash is available in a variety of builds and module formats to accommodate different development environments and performance needs. Selecting the appropriate build can significantly optimize your application's bundle size and load time. This guide explains the differences between the available builds and helps you choose the one that best fits your project.

## Core vs. Full Builds

Lodash offers two primary pre-compiled builds: a lightweight **Core** build and a comprehensive **Full** build.

| Feature | Full Build | Core Build |
|---|---|---|
| **Description** | Includes all Lodash functions for a wide range of utilities. | A lightweight version containing a subset of the most common functions, suitable for environments where bundle size is critical. |
| **Gzipped Size** | ~24 kB | ~4 kB |
| **Node.js Import** | `require('lodash')` | `require('lodash/core')` |
| **Use Case** | Ideal for Node.js applications or projects where bundle size is not a primary concern. | Recommended for front-end applications, mobile web, or any scenario where initial load performance is a priority. |

You can download these builds directly or use a CDN:

- **Core Build**: [lodash.core.js](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js)
- **Full Build**: [lodash.js](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js)
- **CDN Options**: [jsdelivr](https://www.jsdelivr.com/projects/lodash)

## Module Formats and Optimization

To integrate with modern JavaScript tooling, Lodash supports several module formats that enable optimizations like tree-shaking.

### UMD (Universal Module Definition)

The standard `lodash` package uses the UMD format, making it compatible with various environments.

**In a browser:**
```html
<script src="lodash.js"></script>
```

**In Node.js:**
```javascript
// Load the full build.
var _ = require('lodash');

// Load the core build.
var _ = require('lodash/core');
```

### Cherry-picking Methods

For front-end projects, the most effective optimization is to import only the methods you need. This allows bundlers like webpack or Rollup to perform tree-shaking and exclude unused code from the final bundle.

```javascript
// Cherry-pick methods for smaller bundles.
var at = require('lodash/at');
var curryN = require('lodash/fp/curryN');
```

### ES Modules

For projects using ES modules, the `lodash-es` package is recommended. It provides native ES module exports, which allows for more efficient tree-shaking with modern build tools. To further automate this process, you can use [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash) and [lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin).

### Functional Programming (FP) Build

Lodash also provides a build for functional programming. This version features immutable, auto-curried, iteratee-first, and data-last methods.

```javascript
// Load the FP build.
var fp = require('lodash/fp');
```
For a deeper dive into this paradigm, see the [Functional Programming Guide](./fp-guide.md).

## How to Choose

Use this chart to determine the best build for your needs:

```d2
direction: down

start: "Start: Choose Lodash Build"

env_check: "What is your environment?"

start -> env_check

subgraph "Browser" {
  direction: down
  bundle_sensitive: "Is bundle size critical?"
  use_core: "Use Core Build (lodash.core.js) or Cherry-pick methods."
  use_full: "Use Full Build (lodash.js)."

  bundle_sensitive -> use_core: "Yes"
  bundle_sensitive -> use_full: "No"
}

subgraph "Node.js" {
  direction: down
  use_full_node: "Use the full 'lodash' package."
}

subgraph "Modern Bundler (webpack, Vite)" {
  direction: down
  use_es: "Use 'lodash-es' or Cherry-pick methods for optimal tree-shaking."
}

env_check -> bundle_sensitive: "Browser"
env_check -> use_full_node: "Node.js"
env_check -> use_es: "Modern Bundler"

fp_check: "Do you prefer a functional programming style?"

use_core --> fp_check
use_full --> fp_check
use_full_node --> fp_check
use_es --> fp_check

end: "Selection Complete"

use_fp: "Use the 'lodash/fp' variant."

fp_check -> use_fp: "Yes"
fp_check -> end: "No"
use_fp -> end
```

## Custom Builds

For full control, you can create a custom build using `lodash-cli` to include only the specific methods your project requires. The build process can be initiated through npm scripts defined in `package.json`.

**Generate Standard Builds**

This command will generate the main and FP distribution files in the `./dist/` directory.
```shell
$ npm run build
```

**Use lodash-cli Directly**

Alternatively, you can use the `lodash-cli` to generate specific builds.

```shell
# Create a full build
$ lodash -o ./dist/lodash.js

# Create the core build
$ lodash core -o ./dist/lodash.core.js
```

By understanding these build differences, you can make an informed choice that balances functionality with performance. To further optimize your code, consider reading our guide on [Performance](./guides-performance.md).