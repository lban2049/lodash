# Build Differences

Lodash provides a variety of builds and module formats tailored to different environments and project requirements. Choosing the right build is key to optimizing your application's performance and bundle size. This guide explains the available options and how to create customized builds.

## Official Builds

Lodash offers two primary pre-compiled builds: a comprehensive **Full build** and a lightweight **Core build**. These are ideal for quick setup in browsers or environments where a single file is preferred.

| Build | Gzipped Size | Description |
| :--- | :--- | :--- |
| [Full build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js) | ~24 kB | Includes the complete set of Lodash methods. Best for server-side applications or when bundle size is not a critical constraint. |
| [Core build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js) | ~4 kB | A minimal build containing a subset of popular, core Lodash utilities. Ideal for projects where every kilobyte matters. |

For more CDN options, you can visit [jsDelivr](https://www.jsdelivr.com/projects/lodash).

## Module Formats

For modern development workflows, Lodash is available in several module formats that offer greater flexibility and optimization opportunities.

<x-cards data-columns="2">
  <x-card data-title="UMD (lodash)" data-icon="mdi:npm">
    The standard package on npm. It uses the UMD format, making it compatible with browsers via a `<script>` tag and Node.js using `require('lodash')`.
  </x-card>
  <x-card data-title="ES Modules (lodash-es)" data-icon="logos:esmodules">
    Provides ES modules, allowing modern bundlers like Webpack or Rollup to perform tree-shaking and include only the code you use.
  </x-card>
  <x-card data-title="Functional (lodash/fp)" data-icon="material-symbols:function">
    A functional programming variant with immutable, auto-curried, iteratee-first, and data-last methods. See the [FP Guide](./fp-guide.md) for details.
  </x-card>
  <x-card data-title="Per-Method Packages" data-icon="ph:package-duotone">
    Each Lodash method is published as a separate package (e.g., `lodash.at`). This offers the most granular control for minimal bundle sizes.
  </x-card>
</x-cards>

## Optimizing Bundle Size

Beyond choosing the right build, you can further reduce your bundle size using several techniques.

### Cherry-picking Methods

Instead of importing the entire library, you can import only the specific methods you need. This is the most direct way to help bundlers eliminate unused code.

```javascript Cherry-picking in Node.js icon=logos:nodejs-icon
// Load only the 'at' method
var at = require('lodash/at');

// Load only the 'curryN' method from the FP build
var curryN = require('lodash/fp/curryN');
```

### Using Build Tools and Plugins

For larger projects, manually cherry-picking can be tedious. The ecosystem provides plugins that automate this process.

- **[babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash)**: A Babel plugin that transforms your Lodash imports to be cherry-picked, so you can write `import { at } from 'lodash'` and get an optimized result.
- **[lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin)**: A Webpack plugin that works with `babel-plugin-lodash` to further optimize builds by replacing method calls with more specific or smaller alternatives.

### Generating Custom Builds

You can generate your own custom builds directly from the source using `lodash-cli`. This gives you full control over the included modules.

```shell Generating Builds with lodash-cli icon=mdi:console
# Generate the standard full build
$ lodash -o ./dist/lodash.js

# Generate the core build
$ lodash core -o ./dist/lodash.core.js
```