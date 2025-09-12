# 性能

Lodash 将性能作为其核心设计原则。为验证并维持我们的高标准，该库包含一个全面的基准测试套件。此套件可以针对其他流行的实用工具库（例如 Underscore.js）进行透明、可重复的性能测试，从而确保 Lodash 的函数针对真实场景进行了优化。

本指南将概述我们的性能测试框架，介绍如何自行运行基准测试，并说明如何解读结果。

## 基准测试套件

我们的性能测试使用 [Benchmark.js](http://benchmarkjs.com/) 构建，这是可靠的 JavaScript 基准测试的行业标准。该套件旨在各种环境中运行，包括现代浏览器和 Node.js。

每个测试用例都会将一个 Lodash 函数与其在竞争库中的对应函数直接进行比较，测量每秒操作数 (Hz)。这可以提供清晰的数据，说明哪种实现更快，以及快了多少。

## 如何运行基准测试

您可以在浏览器或 Node.js 环境中轻松运行整个性能测试套件。

### 在浏览器中

运行基准测试最直接的方法是在网页浏览器中打开 Lodash 项目中的 `perf/index.html` 文件。该页面提供了一个用户界面，用于选择和比较不同的库构建版本。

1.  **打开文件**：在您本地克隆的仓库中找到 `perf/index.html` 文件，并在浏览器中打开它。
2.  **选择构建版本**：使用顶部的下拉菜单选择要比较的 Lodash 构建版本和另一个库（例如 Underscore）。
3.  **查看结果**：基准测试将自动运行，结果会记录到页面内嵌的 Firebug Lite 控制台中。

该 HTML 文件会动态加载必要的脚本来创建测试环境：

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

### 在 Node.js 中

要从命令行运行基准测试，请使用 Node.js 运行 `perf/perf.js` 脚本。

```bash Terminal icon=mdi:console
# Run the benchmarks against the default lodash.js build
node perf/perf.js

# Specify a custom build to test
node perf/perf.js ../dist/lodash.min.js
```

该脚本将执行所有测试套件，并将结果直接打印到您的终端。

## 理解输出结果

对于每个测试套件，脚本会记录 Lodash 和对比库的性能（以每秒操作数计）。最后，脚本会给出一个摘要，指出哪个库更快以及快了多少百分比。

```text Sample Suite Output
`_.assign`:
lodash x 4,717,677 ops/sec ±1.24% (89 runs sampled)
underscore x 2,048,429 ops/sec ±1.15% (91 runs sampled)
lodash is 130% faster.
```

所有单个测试完成后，脚本会计算所有结果的几何平均值，以提供两个库之间最终的、全面的性能对比。

```text Final Summary Output
lodash is 54% (1.54x) faster than underscore.
```

## 测试环境设置

为确保比较的公平性和一致性，所有基准测试共享一个通用设置，用于准备各种数据结构。该设置只需定义一次，即可应用于每个测试用例。

准备好的数据包括数字数组、对象、嵌套数组以及 Lodash 函数操作的其他常见结构。

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

## 示例测试套件

基准测试文件定义了数十个套件，每个套件都针对一个特定的函数。其结构简单且具有声明性。

以下是一个针对数组操作的 `_.clone` 测试套件示例：

```javascript `_.clone` Benchmark Suite icon=logos:javascript
suites.push(
  Benchmark.Suite('`_.clone` with an array')
    .add(buildName, 'lodash.clone(numbers)')
    .add(otherName, '_.clone(numbers)')
);
```

此示例测试了链式方法调用，这是 Lodash 中的一种常见模式：

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

通过提供一个透明且全面的基准测试套件，我们确保 Lodash 不仅提供丰富的实用工具集，还能提供现代 Web 应用程序所需的性能。如果您希望进一步优化您的应用程序，可以考虑创建[自定义构建版本](./guides-build-differences.md)来最小化您的打包体积。