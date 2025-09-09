# Performance

Lodash is engineered for high performance, featuring highly optimized functions for common operations. This guide provides an overview of the performance testing suite included with Lodash, enabling you to run benchmarks and understand the performance characteristics of different functions.

## Running the Performance Suite

The Lodash repository includes a comprehensive performance suite built with [Benchmark.js](http://benchmarkjs.com/). You can run these tests to compare the performance of Lodash against other libraries like Underscore.js on your own hardware.

### Browser-Based Testing

For a user-friendly way to run the benchmarks, you can use the HTML runner:

1.  **Clone the Lodash repository** and navigate to the project root.
2.  Open the `perf/index.html` file in your web browser.
3.  Use the dropdown menus in the toolbar to select the specific Lodash build and the other library you wish to compare.
4.  The benchmarks will run automatically, and the results will be logged in your browser's developer console.

This interface allows for easy, on-the-fly comparisons between different library versions and builds.

```html perf/index.html icon=mdi:language-html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>lodash Performance Suite</title>
    <style>
      /* ... styles ... */
    </style>
  </head>
  <body>
    <div id="perf-toolbar"></div>
    <script src="../lodash.js"></script>
    <script src="../node_modules/platform/platform.js"></script>
    <script src="../node_modules/benchmark/benchmark.js"></script>
    <script src="../vendor/firebug-lite/src/firebug-lite-debug.js"></script>
    <script src="./asset/perf-ui.js"></script>
    <script>
      // ... script to load builds and run tests ...
    </script>
  </body>
</html>
```

### Command-Line Testing

You can also run the performance suite from your terminal using Node.js. This is useful for automated testing or scripting.

1.  **Navigate to the `perf/` directory** within the Lodash project.
2.  Run the script, passing the path to the Lodash file you want to test as an argument:

```bash Run Benchmark icon=mdi:console
node perf.js ../lodash.js
```

The script will execute all benchmark suites and print a summary of the results to the console, including a final geometric mean comparison against the other library (Underscore.js by default).

## Understanding the Benchmarks

The performance suite is composed of numerous tests, each targeting a specific Lodash function or a common usage pattern. These tests are defined in `perf/perf.js`.

Key areas covered by the benchmarks include:

| Category | Functions Tested (Examples) |
| :--- | :--- |
| **Chaining** | `_(...).map(...).filter(...).value()` |
| **Object Manipulation** | `assign`, `clone`, `defaults`, `omit`, `pick` |
| **Array Operations** | `compact`, `difference`, `flatten`, `intersection`, `union`, `uniq` |
| **Collection Iteration** | `each`, `every`, `filter`, `find`, `map`, `reduce`, `some` |
| **Equality & Type Checking** | `isEqual`, `isArguments`, `isDate`, `isFunction` |
| **Function Utilities** | `bind`, `bindAll`, `partial`, `flowRight` |
| **Utilities** | `template`, `shuffle`, `sortBy`, `sortedIndex` |

Each suite compares Lodash's implementation against a baseline, providing clear metrics on which is faster and by what percentage for a given operation. The results are adjusted for the margin of error to provide more reliable statistics.

```javascript Benchmark Suite Example icon=logos:javascript
// Example from perf/perf.js

suites.push(
  Benchmark.Suite('`_.filter` iterating an array')
    .add(buildName, '\n      lodash.filter(numbers, function(num) {\n        return num % 2;\n      })')
    .add(otherName, '\n      _.filter(numbers, function(num) {\n        return num % 2;\n      })')
);
```

## Performance Insights

While raw performance can vary by environment, the benchmark suite highlights several of Lodash's strengths:

*   **Lazy Evaluation in Chains**: For complex chains of array methods (`map`, `filter`, `take`, etc.), Lodash's lazy evaluation can be significantly more performant than native array methods. It minimizes the number of iterations and avoids creating intermediate arrays, processing each element through the entire chain before moving to the next.

*   **Optimized Iteration**: Lodash contains highly optimized internal loops for iterating over arrays and objects, which can provide a performance boost for functions like `_.each`, `_.map`, and `_.filter` in certain JavaScript environments.

*   **Robust Deep Equality**: The `_.isEqual` function is heavily benchmarked against a wide variety of data structures (primitives, objects, nested arrays). This reflects a focus on providing a correct and performant deep comparison utility.

By running the performance suite, you can gain confidence in the library's optimizations and make informed decisions when writing performance-critical code.

---

For more advanced customization, including creating builds with only the functions you need, see the guide on [Build Differences](./guides-build-differences.md).