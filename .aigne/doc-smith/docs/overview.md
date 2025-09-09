# Overview

Welcome to the official documentation for Lodash v4.17.21. Lodash is a modern JavaScript utility library delivering modularity, performance, and extras. It makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, and strings.

Lodash is released under the [MIT license](https://raw.githubusercontent.com/lodash/lodash/4.17.21/LICENSE) and is designed for modern, high-performance environments.

## Why Use Lodash?

Lodash's modular methods provide a consistent, high-performance, and customizable approach to common programming tasks. Its core strengths lie in:

*   **Iterating Collections**: Simplify complex iterations over arrays, objects, and strings with powerful and concise helper functions.
*   **Manipulating Data**: Streamline the manipulation and testing of values, from simple data transformations to complex object manipulations.
*   **Creating Functions**: Build powerful, reusable logic with utilities for creating composite, curried, and debounced functions.

## Exploring the Documentation

This documentation is designed to help you find what you need quickly. Here are the main sections:

<x-cards data-columns="2">
  <x-card data-title="API Reference" data-icon="lucide:book-open" data-href="/api">
    A comprehensive, searchable reference for all Lodash methods, organized by data type for quick look-up.
  </x-card>
  <x-card data-title="Functional Programming Guide" data-icon="lucide:function-square" data-href="/fp-guide">
    Learn about the FP-variant of Lodash, which promotes immutability with auto-curried, iteratee-first, data-last methods.
  </x-card>
  <x-card data-title="Guides" data-icon="lucide:compass" data-href="/guides">
    Explore technical guides for advanced use cases, including performance optimization and using different library builds.
  </x-card>
  <x-card data-title="Contributing & Community" data-icon="lucide:users" data-href="/contributing">
    Find out how to contribute to the project and connect with the community through our discussion channels.
  </x-card>
</x-cards>

## Quick Start

Get up and running with Lodash in minutes. For detailed instructions for browsers, Node.js, and bundlers, please see the [Getting Started](./getting-started.md) guide.

### Installation

To add Lodash to your project, install it via npm:

```shell npm install
$ npm i --save lodash
```

### Basic Usage

Once installed, you can import and use Lodash methods in your code:

```javascript Usage Example icon=logos:javascript
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

---

Ready to begin? Head over to the [Getting Started](./getting-started.md) section to integrate Lodash into your project.