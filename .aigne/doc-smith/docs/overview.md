# Overview

Lodash is a modern JavaScript utility library that delivers modularity, performance, and customization. It makes JavaScript programming easier by simplifying operations on common data structures like arrays, numbers, objects, and strings. Lodash is released under the MIT license, and its current version is v4.17.21.

### Core Philosophy and Features

Lodash's design philosophy revolves around modularity, consistency, and performance. It provides a large number of optimized helper functions aimed at solving common problems in JavaScript development.

<x-cards data-columns="3">
  <x-card data-title="Collection Iteration" data-icon="lucide:list-tree">
    Provides a unified API to easily iterate over arrays, objects, and strings, handling various data collections.
  </x-card>
  <x-card data-title="Value Manipulation & Testing" data-icon="lucide:clipboard-check">
    Includes a rich set of tools for manipulating and validating various data types, ensuring code robustness.
  </x-card>
  <x-card data-title="Composite Function Creation" data-icon="lucide:function-square">
    Supports functional programming paradigms, making it easy to create composite functions like curried, composed, and deferred functions.
  </x-card>
</x-cards>

### Modular Architecture

Lodash uses a modular architecture, allowing developers to load features on demand, which significantly optimizes the final application size. This structure has also led to a variety of different build versions and usage methods.

```d2
direction: down

"Lodash Core": {
  "Core Utilities (e.g., identity, constant)": {
    shape: package
  }
}

"Feature Modules": {
  grid-columns: 3
  "Arrays (e.g., chunk, drop)": {}
  "Collections (e.g., map, filter)": {}
  "Objects (e.g., get, set)": {}
  "Strings (e.g., camelCase, trim)": {}
  "Functions (e.g., debounce, curry)": {}
  "Others (Math, Lang, etc.)": {}
}

"Build Targets & Formats": {
  grid-columns: 3
  "Full Build (lodash)": {}
  "FP Build (lodash/fp)": {}
  "ES Modules (lodash-es)": {}
  "Per-Method Packages (lodash.map)": {}
  "Plugins (babel-plugin-lodash)": {}
  "CDN": {}
}

"Lodash Core" -> "Feature Modules"
"Feature Modules" -> "Build Targets & Formats"
```

### Available Module Formats

Lodash offers various build versions and module formats to suit different project needs and bundlers. For more details, please refer to the [Build Differences Guide](./guides-build-differences.md).

| Format/Build Version | NPM Package | Description |
|---|---|---|
| Standard Build | `lodash` | Provides the full feature set in UMD format, suitable for Node.js and browser environments. |
| Per-Method Packages | `lodash.map`, `lodash.get`, ... | Publishes each method as a separate package for ultimate on-demand loading, ideal for scenarios with strict bundle size requirements. |
| ES Modules | `lodash-es` | Provides an ES module version, facilitating Tree Shaking with modern bundlers like Webpack and Rollup. |
| Functional Programming (FP) | `lodash/fp` | Provides an immutable, auto-curried, function-first, data-last version for functional programming. |
| AMD Build | `lodash-amd` | A build version specifically for projects using the AMD specification (like RequireJS). |
| Plugins | `babel-plugin-lodash`, `lodash-webpack-plugin` | Automatically optimizes module imports through Babel or Webpack plugins, simplifying the development process. |

### How to Use This Documentation

To help you quickly find the information you need, this documentation is organized by topic:

<x-cards data-columns="2">
  <x-card data-title="Getting Started Guide" data-icon="lucide:rocket" data-href="/getting-started">
    Provides instructions for quickly installing and using Lodash in different environments.
  </x-card>
  <x-card data-title="API Reference" data-icon="lucide:book-open" data-href="/api">
    A complete list of methods organized by data type, including detailed parameter descriptions and examples.
  </x-card>
  <x-card data-title="Functional Programming Guide" data-icon="lucide:function-square" data-href="/fp-guide">
    An in-depth look at Lodash's functional programming features, including immutability, auto-currying, and more.
  </x-card>
  <x-card data-title="Advanced Guides" data-icon="lucide:compass" data-href="/guides">
    Covers advanced topics such as performance optimization and custom builds.
  </x-card>
  <x-card data-title="Security Policy" data-icon="lucide:shield" data-href="/security">
    Learn about the project's security update policy and vulnerability reporting process.
  </x-card>
  <x-card data-title="Community & Contributing" data-icon="lucide:github" data-href="/contributing">
    Join community discussions or contribute code to the project.
  </x-card>
</x-cards>

### Next Steps

Now that you have a basic understanding of Lodash, we recommend you start with the [Getting Started Guide](./getting-started.md) to quickly integrate Lodash into your project.