# Overview

Welcome to the official documentation for Lodash v4.17.21. Lodash is a modern JavaScript utility library delivering modularity, performance, and extras. It makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, and strings.

Lodash’s modular methods are great for:
*   Iterating arrays, objects, & strings
*   Manipulating & testing values
*   Creating composite functions

This documentation is designed to help you find the information you need quickly and efficiently, whether you're a new user or an experienced developer.

## Core Concepts

Lodash is built on a foundation of several key principles that make it a powerful tool for any JavaScript project.

```d2
direction: down

Your-Application: {
  shape: rectangle
  label: "Your Application"
}

Lodash-Ecosystem: {
  shape: package
  label: "Lodash Ecosystem"
  grid-columns: 1

  Lodash-Library: {
    label: "Lodash Library (v4.17.21)"
    grid-columns: 2

    Core-Modules: {
      label: "Standard Modules"
      grid-columns: 3
      Array: {}
      Object: {}
      String: {}
      Function: {}
      Util: {}
      "...": {}
    }

    FP-Variant: {
      label: "FP Variant (lodash/fp)"
      "Immutable, Auto-curried,\nIteratee-first, Data-last"
    }
  }

  Build-Tools: {
    label: "Build & Optimization Tools"
    grid-columns: 3
    lodash-cli: {}
    babel-plugin-lodash: {}
    lodash-webpack-plugin: {}
  }
}

Your-Application -> Lodash-Ecosystem.Lodash-Library: "Imports & Uses"
Lodash-Ecosystem.Build-Tools -> Lodash-Ecosystem.Lodash-Library: "Generates Custom Builds"

```

<x-cards data-columns="2">
  <x-card data-title="Modularity &amp; Performance" data-icon="lucide:boxes">
    Lodash is available in various builds. You can load the full library, the core build, or even cherry-pick individual methods to keep your project's bundle size minimal. This modular approach ensures you only include the code you need.
  </x-card>
  <x-card data-title="Functional Programming" data-icon="lucide:function-square">
    For developers who prefer a functional programming style, the `lodash/fp` module provides an immutable, auto-curried, iteratee-first, data-last version of Lodash methods.
  </x-card>
</x-cards>

## How to Use These Docs

This documentation is organized into several key sections to help you get the most out of Lodash. Whether you're looking for installation instructions, detailed API specifications, or advanced guides, you'll find it here.

<x-cards data-columns="2">
  <x-card data-title="Getting Started" data-icon="lucide:rocket" data-href="/getting-started">
    New to Lodash? This is the place to start. Find quick, copy-paste ready instructions for installing and using Lodash in your project.
  </x-card>
  <x-card data-title="API Reference" data-icon="lucide:book-open" data-href="/api">
    The complete reference for every Lodash method, organized by data type. If you know what you're looking for, this is the fastest way to find it.
  </x-card>
  <x-card data-title="Functional Programming Guide" data-icon="lucide:workflow" data-href="/fp-guide">
    Dive deep into the functional programming capabilities of Lodash, including concepts like auto-currying and immutability.
  </x-card>
  <x-card data-title="Guides" data-icon="lucide:compass" data-href="/guides">
    Explore advanced topics, such as creating custom builds, performance benchmarks, and understanding the differences between module formats.
  </x-card>
</x-cards>

## Community & Contributing

Lodash is an open-source project maintained by a dedicated community. We welcome contributions and discussions. 

*   **Chat:** Join the conversation on [Gitter](https://gitter.im/lodash/lodash).
*   **Contribute:** Read our [Contributing Guide](https://github.com/lodash/lodash/blob/master/.github/CONTRIBUTING.md) to get started.
*   **Follow:** Stay up-to-date by following us on [Twitter](https://twitter.com/bestiejs).

## What's Next?

Ready to dive in? Head over to our [Getting Started](./getting-started.md) guide for a quick installation and your first function call.