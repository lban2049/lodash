# Performance

Lodash is engineered with performance as a core principle. To validate and maintain our high standards, the library includes a comprehensive benchmark suite. This suite allows for transparent, repeatable performance testing against other popular utility libraries, such as Underscore.js, ensuring that Lodash functions are optimized for real-world scenarios.

This guide provides an overview of our performance testing framework, shows you how to run the benchmarks yourself, and explains how to interpret the results.

## The Benchmark Suite

Our performance tests are built using [Benchmark.js](http://benchmarkjs.com/), the industry standard for reliable JavaScript benchmarking. The suite is designed to run in various environments, including modern browsers and Node.js.

Each test case compares a Lodash function directly against its counterpart in a competing library, measuring operations per second (Hz). This provides clear data on which implementation is faster and by how much.

## How to Run the Benchmarks

You can easily run the entire performance suite in either a browser or a Node.js environment.

### In the Browser

The most straightforward way to run the benchmarks is by opening the `perf/index.html` file from the Lodash project in your web browser. This page provides a user interface to select and compare different library builds.

1.  **Open the File**: Navigate to `perf/index.html` in your local clone of the repository and open it in a browser.
2.  **Select Builds**: Use the dropdown menus at the top to choose the Lodash build and the other library (e.g., Underscore) you wish to compare.
3.  **View Results**: The benchmarks will run automatically, and the results will be logged to the Firebug Lite console embedded in the page.

The HTML file dynamically loads the necessary scripts to create the test environment:

```html perf/index.html icon=mdi:language-html5
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>lodash Performance Suite</title>
  </head>
  <body>
    <div id="perf-toolbar"></div>
    <!-- Core libraries -->
    <script src="../lodash.js"></script>
    <script src="../node_modules/benchmark/benchmark.js"></script>
    <script src="../vendor/firebug-lite/src/firebug-lite-debug.js"></script>
    <script src="./asset/perf-ui.js"></script>

    <!-- Dynamically load selected builds -->
    <script>
      document.write('<script src="' + ui.buildPath + '"><\/script>');
    </script>
    <script>
      var lodash = _.noConflict();
    </script>
    <script>
      document.write('<script src="' + ui.otherPath + '"><\/script>');
    </script>

    <!-- Run the benchmark suite -->
    <script src="perf.js"></script>
    <script>
      window.onload = function() { setTimeout(run, 15); };
    </script>
  </body>
</html>
```

### In Node.js

To run the benchmarks from the command line, use the `perf/perf.js` script with Node.js.

```bash Terminal icon=mdi:console
# Run the benchmarks against the default lodash.js build
node perf/perf.js

# Specify a custom build to test
node perf/perf.js ../dist/lodash.min.js
```

The script will execute all test suites and print the results directly to your terminal.

## Understanding the Output

For each test suite, the script logs the performance of both Lodash and the comparison library in operations per second. It concludes with a summary indicating which is faster and by what percentage.

```text Sample Suite Output
`_.assign`:
lodash x 4,717,677 ops/sec ±1.24% (89 runs sampled)
underscore x 2,048,429 ops/sec ±1.15% (91 runs sampled)
lodash is 130% faster.
```

After all individual tests are complete, the script calculates the geometric mean of all results to provide a final, overall performance comparison between the two libraries.

```text Final Summary Output
lodash is 54% (1.54x) faster than underscore.
```

## Test Environment Setup

To ensure fair and consistent comparisons, all benchmarks share a common setup that prepares a variety of data structures. This setup is defined once and applied to every test case.

The prepared data includes arrays of numbers, objects, nested arrays, and other common structures that Lodash functions operate on.

```javascript Benchmark Setup icon=logos:javascript
// A simplified view of the setup code from perf.js
var limit = 50,
    object = {},
    objects = Array(limit),
    numbers = Array(limit),
    nestedNumbers = [1, [2], [3, [[4]]]];

for (var index = 0; index < limit; index++) {
  numbers[index] = index;
  object["key" + index] = index;
  objects[index] = { "num": index };
}

// ...and many more data variables for specific function tests.
```

## Example Test Suites

The benchmark file defines dozens of suites, each targeting a specific function. The structure is simple and declarative.

Here is an example of a test suite for `_.clone` operating on an array:

```javascript `_.clone` Benchmark Suite icon=logos:javascript
suites.push(
  Benchmark.Suite('`_.clone` with an array')
    .add(buildName, 'lodash.clone(numbers)')
    .add(otherName, '_.clone(numbers)')
);
```

This example tests a chained method call, which is a common pattern in Lodash:

```javascript Chaining Benchmark Suite icon=logos:javascript
suites.push(
  Benchmark.Suite('`_(...).map(...).filter(...).take(...).value()`')
    .add(buildName, {
      'fn': 'lodashChaining.map(square).filter(even).take(100).value()',
      'teardown': 'function chaining(){}'
    })
    .add(otherName, {
      'fn': '_chaining.map(square).filter(even).take(100).value()',
      'teardown': 'function chaining(){}'
    })
);
```

---

By providing a transparent and comprehensive benchmarking suite, we ensure that Lodash not only offers a rich set of utilities but also delivers the performance modern web applications require. If you are looking to further optimize your application, consider creating [custom builds](./guides-build-differences.md) to minimize your bundle size.