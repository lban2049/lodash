# 性能

Lodash 专为高性能而设计，其函数经过精心优化，可在各种 JavaScript 环境中高速运行。为了验证和展示这些优化成果，该库包含一个全面的基准测试套件，用于衡量其函数相对于 Underscore.js 等其他流行实用工具库的性能。

本指南将概述性能测试的设置，并说明如何运行基准测试及解读其结果。

## 基准测试套件

该性能套件基于 [Benchmark.js](https://benchmarkjs.com/) 构建，这是一个功能强大的库，可用于创建准确可靠的性能测试。它包含众多测试用例，每个测试用例都针对特定 Lodash 函数在不同场景下的表现，例如迭代数组与对象，或处理不同大小的数据。

该套件旨在在多个 JavaScript 环境中运行，包括现代浏览器和 Node.js 等服务器端运行时，确保性能在各平台间保持一致。

### 基准测试工作原理

下图展示了性能测试过程的工作流程。一个运行脚本会执行 `perf.js` 中定义的一系列测试套件。这些套件使用 `Benchmark.js` 将 Lodash 的性能与指定的备选库（如 Underscore）进行比较，最终生成详细的性能报告。

```d2
direction: down

"Benchmark-Runner": {
  shape: package
  label: "基准测试运行器"
  grid-columns: 2

  "Browser-Test": {
    label: "浏览器\n(perf/index.html)"
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
  label: "待比较库"
  grid-columns: 2

  "Lodash": { 
    shape: document
  }
  "Underscore": {
    shape: document
  }
}

"Results": {
  label: "性能报告\n(操作数/秒，快 %)"
  shape: document
}

"Benchmark-Runner" -> "Benchmark-js": "使用"
"Benchmark-js" -> "Libraries-to-Compare": "测试"
"Benchmark-js" -> "Results": "输出"
```

## 运行基准测试

您可以自行运行性能套件，以在您自己的机器上查看结果。

### 在浏览器中

要在浏览器中运行基准测试，请从本地服务器打开 `perf/index.html` 文件。该页面提供一个用户界面，您可以在其中选择不同版本的 Lodash 以及您希望与之比较的库。结果会记录到页面内嵌的 Firebug Lite 控制台中。

### 从命令行

要在 Node.js 环境中运行测试，请从终端执行 `perf/perf.js` 脚本。该脚本将加载 Lodash 和待比较的库，运行所有基准测试套件，并将结果直接打印到控制台。

```bash
node perf/perf.js
```

## 解读结果

每项测试的输出都会显示**每秒操作数 (ops/sec)**，该数值越高表示性能越好。脚本还会报告百分比差异，使您可以轻松看出哪个函数更快。

在所有单个套件完成后，会显示最终摘要。该摘要使用所有测试分数的**几何平均值**来提供一个可靠的整体比较，从而得出哪个库的平均速度更快以及快多少的结论。

单个套件的输出示例如下：

```text
`_.assign`:
lodash x 45,932,749 ops/sec ±0.79% (96 runs sampled)
underscore x 38,198,391 ops/sec ±0.83% (98 runs sampled)
lodash 的速度快 20%。
```

最终报告提供了一个高级摘要：

```text
lodash 的速度比 underscore 快 42% (1.42 倍)。
```

## 关键优化领域

基准测试套件涵盖了 Lodash 的广泛功能。下表重点介绍了一些经过严格性能测试的关键领域。

| 类别 | 基准测试的函数示例 |
|---|---|
| **链式调用** | `_(...).map(...).filter(...).value()` |
| **对象操作** | `assign`, `clone`, `isEqual`, `defaults`, `omit`, `pick` |
| **集合迭代** | `each`, `map`, `filter`, `reduce`, `every`, `some`, `find` |
| **函数工具** | `bind`, `bindAll`, `partial`, `flowRight`, `wrap` |
| **数组操作** | `difference`, `intersection`, `union`, `uniq`, `flatten`, `zip` |
| **类型检查** | `isArguments`, `isDate`, `isFunction`, `isObject`, etc. |
| **实用程序** | `template`, `times`, `shuffle`, `sortBy` |

---

Lodash 全面而透明的基准测试过程彰显了其对性能的承诺。为了在生产环境中获得进一步的性能提升（尤其是在打包体积方面），可以考虑根据您的特定需求创建一个自定义构建。您可以在我们的 [构建差异](./guides-build-differences.md) 指南中找到更多信息。