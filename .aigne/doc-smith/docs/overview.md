# Overview

Lodash is a modern JavaScript utility library that provides modularity, performance, and extra features. It simplifies common programming tasks by taking the hassle out of working with arrays, numbers, objects, and strings. This documentation covers Lodash v4.17.21, which is released under the MIT license and supports modern environments, including Node.js v4.0.0 and higher.

## Why Lodash?

Lodash’s modular methods are great for:

*   **Iterating** arrays, objects, and strings
*   **Manipulating** and testing values
*   **Creating** composite functions

It provides a comprehensive toolset that helps you write more concise and maintainable code.

## Core Features

Lodash is designed with the professional developer in mind, offering several key architectural benefits.

```d2
direction: down

"Lodash Library": {
  shape: package
  grid-columns: 1

  "Core Philosophy": {
    shape: rectangle
    "Simplicity": "Make JavaScript easier"
    "Consistency": "Reliable utility functions"
  }

  "Key Modules": {
    shape: rectangle
    grid-columns: 2
    "Standard Build": "Full-featured UMD module"
    "Core Build": "Lightweight subset for basic needs"
    "FP Module": "Functional programming variant"
    "Per-Method Packages": "Maximum modularity"
  }

  "Key Modules" -> "Core Philosophy": "Guided by"
}
```

### Modularity and Custom Builds

Lodash is available in various builds and module formats, enabling you to keep your project's bundle size to a minimum. You can cherry-pick individual methods, use ES modules (`lodash-es`), or leverage plugins like `babel-plugin-lodash` and `lodash-webpack-plugin` for optimized builds.

For more details, see the [Build Differences](./guides-build-differences.md) guide.

### Functional Programming Variant

For developers who prefer a functional programming style, Lodash offers a dedicated `lodash/fp` module. It provides immutable, auto-curried, iteratee-first, and data-last methods that make it easier to compose functions and build functional pipelines.

To learn more, read the [FP Guide](./fp-guide.md).

## Navigating the Documentation

This site is structured to help you find the information you need efficiently. Here’s a guide to the main sections:

<x-cards data-columns="2">
  <x-card data-title="Getting Started" data-href="/getting-started" data-icon="lucide:play-circle">
    Concise, copy-paste ready instructions for installing and using Lodash in your project.
  </x-card>
  <x-card data-title="API Reference" data-href="/api" data-icon="lucide:book-open">
    A comprehensive, searchable reference for every Lodash method, organized by data type.
  </x-card>
  <x-card data-title="Guides" data-href="/guides" data-icon="lucide:compass">
    Technical guides for advanced use cases, including performance optimization and custom builds.
  </x-card>
  <x-card data-title="Contributing & Community" data-href="/contributing" data-icon="lucide:users">
    Information on how to contribute and connect with the Lodash community.
  </x-card>
</x-cards>


## Community and Support

Join the discussion and connect with other Lodash users through our community channels. For information on how to get involved, report issues, or contribute to the project, please visit the [Contributing & Community](./contributing.md) section.