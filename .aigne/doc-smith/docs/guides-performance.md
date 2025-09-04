# Performance

Lodash is engineered for high performance, with its functions carefully optimized for speed across various JavaScript environments. To validate and showcase these optimizations, the library includes a comprehensive benchmark suite that measures the performance of its functions against other popular utility libraries, such as Underscore.js.

This guide provides an overview of the performance testing setup and explains how you can run the benchmarks and interpret the results.

## The Benchmark Suite

The performance suite is built using [Benchmark.js](https://benchmarkjs.com/), a robust library for creating accurate and reliable performance tests. It comprises numerous test cases, each targeting a specific Lodash function under different scenarios, such as iterating over arrays versus objects or handling various data sizes.

The suite is designed to run in multiple JavaScript environments, including modern browsers and server-side runtimes like Node.js, ensuring that performance is consistent across platforms.

### How Benchmarking Works

The following diagram illustrates the workflow of the performance testing process. A runner script executes a series of test suites defined in `perf.js`. These suites use `Benchmark.js` to compare the performance of Lodash against a specified alternative library (e.g., Underscore), ultimately generating a detailed performance report.

```d2
direction: down

"Benchmark-Runner": {
  shape: package
  label: "Benchmark Runner"
  grid-columns: 2

  "Browser-Test": {
    label: "Browser\n(perf/index.html)"
    shape: rectangle
  }

  "CLI-Test": {
    label: "Node.js\n(perf/perf.js)"
    shape: rectangle
  }
}

"Benchmark-js": {
  label: "Benchmark.js"
  shape: hexagon
}

"Libraries-to-Compare": {
  shape: package
  label: "Libraries to Compare"
  grid-columns: 2

  "Lodash": { 
    shape: document
  }
  "Underscore": {
    shape: document
  }
}

"Results": {
  label: "Performance Report\n(ops/sec, % faster)"
  shape: document
}

"Benchmark-Runner" -> "Benchmark-js": "Uses"
"Benchmark-js" -> "Libraries-to-Compare": "Tests"
"Benchmark-js" -> "Results": "Outputs"
```

## Running the Benchmarks

You can run the performance suite yourself to see the results on your own machine.

### In the Browser

To run the benchmarks in a browser, open the `perf/index.html` file from a local server. This page provides a user interface where you can select different builds of Lodash and the library you wish to compare it against. The results are logged to the Firebug Lite console embedded on the page.

### From the Command Line

To run the tests in a Node.js environment, execute the `perf/perf.js` script from your terminal. The script will load Lodash and the comparison library, run all benchmark suites, and print the results directly to the console.

```bash
node perf/perf.js
```

## Interpreting the Results

The output for each test shows the number of **operations per second (ops/sec)**, where a higher number indicates better performance. The script also reports the percentage difference, making it easy to see which function is faster.

After all individual suites complete, a final summary is displayed. This summary uses the **geometric mean** of all test scores to provide a reliable overall comparison, concluding which library is faster on average and by what percentage.

An example of the output for a single suite might look like this:

```text
`_.assign`:
lodash x 45,932,749 ops/sec ±0.79% (96 runs sampled)
underscore x 38,198,391 ops/sec ±0.83% (98 runs sampled)
lodash is 20% faster.
```

The final report provides a high-level summary:

```text
lodash is 42% (1.42x) faster than underscore.
```

## Key Areas of Optimization

The benchmark suite covers a wide range of Lodash's functionality. The following table highlights some of the key areas that are rigorously tested for performance.

| Category | Example Functions Benchmarked |
|---|---|
| **Chaining** | `_(...).map(...).filter(...).value()` |
| **Object Manipulation** | `assign`, `clone`, `isEqual`, `defaults`, `omit`, `pick` |
| **Collection Iteration** | `each`, `map`, `filter`, `reduce`, `every`, `some`, `find` |
| **Function Utilities** | `bind`, `bindAll`, `partial`, `flowRight`, `wrap` |
| **Array Operations** | `difference`, `intersection`, `union`, `uniq`, `flatten`, `zip` |
| **Type Checking** | `isArguments`, `isDate`, `isFunction`, `isObject`, etc. |
| **Utilities** | `template`, `times`, `shuffle`, `sortBy` |

---

Lodash's commitment to performance is demonstrated by its comprehensive and transparent benchmarking process. For further performance gains in production, especially regarding bundle size, consider creating a custom build tailored to your specific needs. You can find more information in our [Build Differences](./guides-build-differences.md) guide.