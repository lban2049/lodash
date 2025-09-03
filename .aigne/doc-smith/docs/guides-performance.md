# Performance

Performance is a core design principle of Lodash. The library is highly optimized for common use cases, but real-world performance can vary based on data structures, environment, and specific usage patterns. To provide transparency and a tool for analysis, Lodash includes a comprehensive benchmark suite.

This guide explains how to run the performance benchmarks and interpret their results, enabling you to make informed decisions and leverage the library's internal optimizations effectively.

## The Lodash Benchmark Suite

The performance suite, located in the `perf` directory of the source code, uses [Benchmark.js](http://benchmarkjs.com/) to execute a series of tests. It compares the performance of the specified Lodash build against other utility libraries, such as Underscore.js, across a wide array of functions.

Key features of the suite include:

- **Comprehensive Coverage**: Benchmarks cover a wide range of functions, including array and object iteration, function composition, cloning, and deep equality checks.
- **Side-by-Side Comparison**: Directly compares Lodash against another library in the same environment to produce reliable relative performance data.
- **Configurable Builds**: The browser-based runner allows you to select different library builds (e.g., production minified vs. development) to test.

## Running the Benchmarks

You can run the performance suite directly in your browser by following these steps:

1.  **Clone the Repository**: First, clone the Lodash source code from GitHub.
    ```bash
    git clone https://github.com/lodash/lodash.git
    ```

2.  **Navigate to the Directory**: Change into the performance test directory.
    ```bash
    cd lodash/perf
    ```

3.  **Open the HTML Runner**: Open the `index.html` file in your web browser. The suite will start automatically.

4.  **View the Results**: Open your browser's developer console to see the benchmark results as they are completed. The UI at the top of the page allows you to select different builds of Lodash and the library it's being compared against.

## Benchmark Process Overview

The diagram below illustrates the workflow of the browser-based performance test suite.

```d2
direction: down

"index.html": {
  label: "Browser loads index.html"
  shape: document
}

"perf-ui.js": {
  label: "perf-ui.js"
  shape: rectangle
}

"perf.js": {
  label: "perf.js Test Runner"
  shape: package
}

"Benchmark.js": {
  label: "Benchmark.js Engine"
  shape: hexagon
}

"console": {
  label: "Developer Console Output"
  shape: rectangle
}

"index.html" -> "perf-ui.js": "Loads"
"index.html" -> "perf.js": "Loads"
"perf.js" -> "Benchmark.js": "Configures and runs suites"
"Benchmark.js" -> "perf.js": "Executes tests and triggers event handlers"
"perf.js" -> "console": "Logs formatted results"
```

## Interpreting the Results

For each test suite, the runner logs the performance of both libraries in operations per second (Hz). A higher number indicates better performance. It concludes by identifying the faster library for that specific test.

A typical output for a single function test looks like this:

```text
`_.filter` iterating an array:
lodash x 4,371,037 ops/sec ±1.24% (89 runs sampled)
underscore x 2,143,876 ops/sec ±1.51% (87 runs sampled)
lodash is 103.88% faster.
```

After all suites have run, a final summary is printed. This summary uses the geometric mean of all test results to provide a balanced overall comparison of the two libraries.

```text
lodash is 74.31% (1.74x) faster than underscore.
```

## Writing Performant Code

The benchmark suite itself is an excellent resource for understanding how to write high-performance code with Lodash. By examining the `perf/perf.js` file, you can see how various functions are tested under different conditions.

For performance-critical applications, consider using the benchmark suite to test your specific use cases. You can modify the existing tests or add new ones to measure how different Lodash functions perform with your data, helping you identify and eliminate bottlenecks.

---

By understanding and utilizing the Lodash performance suite, you can validate performance claims and optimize your own code. For another key optimization strategy, see our guide on [Build Differences](./guides-build-differences.md) to learn how to create smaller, custom builds for your projects.