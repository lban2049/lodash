# 性能

Lodash 专为高性能而设计，为常见操作提供了高度优化的函数。本指南概述了 Lodash 内置的性能测试套件，可帮助您运行基准测试，并了解不同函数的性能特点。

## 运行性能套件

Lodash 代码库中包含一个使用 [Benchmark.js](http://benchmarkjs.com/) 构建的综合性能测试套件。您可以在自己的硬件上运行这些测试，以比较 Lodash 与 Underscore.js 等其他库的性能。

### 基于浏览器的测试

若要以用户友好的方式运行基准测试，您可以使用 HTML 运行器：

1.  **克隆 Lodash 代码库** 并导航至项目根目录。
2.  在您的 Web 浏览器中打开 `perf/index.html` 文件。
3.  使用工具栏中的下拉菜单选择特定的 Lodash 构建版本以及您希望进行比较的其他库。
4.  基准测试将自动运行，结果会记录在浏览器的开发者控制台中。

该界面支持在不同库的版本和构建之间进行轻松的即时比较。

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

### 命令行测试

您也可以使用 Node.js 从终端运行性能套件。这对于自动化测试或编写脚本非常有用。

1.  **导航至 Lodash 项目中的 `perf/` 目录**。
2.  运行该脚本，并将您要测试的 Lodash 文件路径作为参数传入：

```bash Run Benchmark icon=mdi:console
node perf.js ../lodash.js
```

该脚本将执行所有基准测试套件，并在控制台输出结果摘要，其中包括与另一个库（默认为 Underscore.js）的最终几何平均值比较。

## 理解基准测试

性能套件由大量测试组成，每个测试都针对特定的 Lodash 函数或常见的使用模式。这些测试定义在 `perf/perf.js` 中。

基准测试涵盖的关键领域包括：

| 类别 | 测试的函数（示例） |
| :--- | :--- |
| **链式调用** | `_(...).map(...).filter(...).value()` |
| **对象操作** | `assign`, `clone`, `defaults`, `omit`, `pick` |
| **数组操作** | `compact`, `difference`, `flatten`, `intersection`, `union`, `uniq` |
| **集合迭代** | `each`, `every`, `filter`, `find`, `map`, `reduce`, `some` |
| **相等性与类型检查** | `isEqual`, `isArguments`, `isDate`, `isFunction` |
| **函数工具** | `bind`, `bindAll`, `partial`, `flowRight` |
| **实用工具** | `template`, `shuffle`, `sortBy`, `sortedIndex` |

每个套件都会将 Lodash 的实现与基准进行比较，为给定操作提供清晰的指标，说明哪个更快以及快了多少百分比。结果会根据误差范围进行调整，以提供更可靠的统计数据。

```javascript Benchmark Suite Example icon=logos:javascript
// Example from perf/perf.js

suites.push(
  Benchmark.Suite('`_.filter` iterating an array')
    .add(buildName, '\n      lodash.filter(numbers, function(num) {\n        return num % 2;\n      })')
    .add(otherName, '\n      _.filter(numbers, function(num) {\n        return num % 2;\n      })')
);
```

## 性能洞察

尽管原始性能可能因环境而异，但该基准测试套件突显了 Lodash 的几大优势：

*   **链式调用中的惰性求值**：对于复杂的数组方法链（如 `map`、`filter`、`take` 等），Lodash 的惰性求值性能可能远超原生数组方法。它能最大限度地减少迭代次数并避免创建中间数组，在处理下一个元素之前，会让当前元素完整地经过整个调用链。

*   **优化的迭代**：Lodash 包含用于迭代数组和对象的高度优化的内部循环，在某些 JavaScript 环境中，这可以为 `_.each`、`_.map` 和 `_.filter` 等函数带来性能提升。

*   **稳健的深度相等性**：`_.isEqual` 函数针对各种数据结构（如原始类型、对象、嵌套数组）进行了大量基准测试。这反映出 Lodash 专注于提供一个正确且高性能的深度比较工具。

通过运行性能套件，您可以对该库的优化建立信心，并在编写对性能要求严苛的代码时做出明智的决策。

---

如需更高级的自定义，包括仅使用您需要的函数创建构建版本，请参阅关于[构建差异](./guides-build-differences.md)的指南。