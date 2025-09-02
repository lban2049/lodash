# 性能

Lodash 的核心设计理念之一就是提供卓越的性能。为了兑现这一承诺，我们建立了一套全面的性能测试套件，持续将 Lodash 与 Underscore.js 等其他流行库进行基准比较。本指南将分享这些测试得出的见解，并指导您如何利用 Lodash 的内部优化来编写高性能代码。

## 性能测试框架

Lodash 使用 [Benchmark.js](https://benchmarkjs.com/) 库来确保测试结果的统计显著性和可靠性。测试流程旨在模拟真实世界的使用场景，涵盖了从简单的数组迭代到复杂的对象深比较等各种操作。这保证了我们的优化是针对实际应用而非微不足道的基准测试。

以下是性能测试的基本流程：

```d2
direction: down

"Setup": {
  "Load Libraries": "Lodash, Underscore.js, Benchmark.js"
  "Prepare Data": "Arrays, Objects, Strings, etc."
}

"Execution": {
  shape: sequence_diagram

  "Benchmark.js": {}

  "Benchmark.js" -> "Lodash Test": "Run Suite"
  "Lodash Test" -> "Benchmark.js": "Ops/sec (Hz)"

  "Benchmark.js" -> "Competitor Test": "Run Suite"
  "Competitor Test" -> "Benchmark.js": "Ops/sec (Hz)"
}

"Analysis": {
  "Compare Results": "Calculate percentage difference for each suite"
  "Aggregate Score": "Calculate geometric mean for overall score"
  "Generate Report": "Log detailed results to the console"
}

"Setup" -> "Execution": "Start Tests"
"Execution" -> "Analysis": "Process Results"
```

每个测试套件都会比较 Lodash 和另一个库（通常是 Underscore.js）在相同任务上的表现，并报告哪个更快以及快了多少。最终，所有测试的结果会被汇总，通过几何平均数计算出一个总体的性能优劣势。

## 运行您自己的基准测试

我们鼓励您在自己的环境中运行性能测试，以验证 Lodash 在您的特定用例中的表现。您可以轻松地在浏览器中运行我们的性能测试套件：

1.  克隆 Lodash 的代码仓库：`git clone https://github.com/lodash/lodash.git`
2.  在您的浏览器中直接打开 `lodash/perf/index.html` 文件。
3.  页面的右上角提供了下拉菜单，允许您选择不同的 Lodash 和 Underscore.js 构建版本进行比较。
4.  测试将自动开始运行，结果会实时输出到浏览器的开发者工具控制台中。

## 关键基准测试场景

性能测试覆盖了 Lodash 的绝大部分功能。下表列出了一些有代表性的测试场景，这些场景凸显了 Lodash 的性能优势和内部优化机制。

| 类别 | 测试函数/方法 | 测试场景描述 |
|---|---|---|
| 链式调用 | `_(...).map(...).filter(...).take(...).value()` | 测试链式调用中的惰性求值性能，通过融合多个操作来避免生成中间数组，从而提升效率。 |
| 对象操作 | `_.assign` | 分别测试合并单个和多个源对象的性能，这是对象扩展和合并的常见操作。 |
| 函数 | `_.bind` | 覆盖多种绑定场景，包括多次绑定、偏函数应用等，确保函数调用的开销最小化。 |
| 数组 | `_.difference`, `_.intersection`, `_.union` | 针对不同大小的数组进行集合运算的基准测试，这些操作在数据处理中非常常见。 |
| 集合迭代 | `_.each`, `_.filter`, `_.map` | 测量在数组和对象上进行迭代的性能，并测试使用属性名简写等内部优化路径。 |
| 深比较 | `_.isEqual` | 对比不同类型的原始值、对象、嵌套数组和对象数组，确保在复杂数据结构下依然保持高效和准确。 |
| 工具 | `_.clone`, `_.flattenDeep` | 测试常用工具函数的性能，如对象的浅克隆和深度扁平化数组。 |

## 性能优化技巧

基于我们的基准测试和库的设计，这里有一些技巧可以帮助您编写性能更高的代码：

### 1. 利用惰性求值 (Lazy Evaluation)

当您将多个方法链接在一起时，Lodash 会使用惰性求值来延迟执行，直到显式或隐式地调用 `value()`。这种机制通过将多个操作合并为一次迭代来最小化迭代次数，从而显著提升性能，尤其是在处理大型数据集时。

```javascript
// 这个链式调用只会对数据进行一次遍历，而不是三次
const result = _(largeArray)
  .map(square)
  .filter(even)
  .take(100)
  .value();
```

更多关于链式调用的信息，请参阅 [Seq API](./api-seq.md) 部分。

### 2. 使用属性简写

在许多集合函数中（如 `_.filter`, `_.map`, `_.find`, `_.sortBy`），您可以使用属性名字符串、属性路径数组或对象作为迭代器。这些简写方式不仅使代码更简洁，而且通常会调用内部的优化路径，比提供自定义回调函数更快。

```javascript
// 性能更佳的方式
lodash.filter(objects, { 'active': true, 'role': 'admin' });

lodash.map(objects, 'user.name');

// 相比于
lodash.filter(objects, o => o.active && o.role === 'admin');

lodash.map(objects, o => o.user.name);
```

### 3. 选择合适的构建版本

Lodash 提供了多种构建版本。对于性能敏感且关注加载时间的应用程序，请考虑创建一个仅包含您所需方法的自定义构建。一个更小的库意味着更快的解析和初始化时间。有关详细信息，请参阅我们的 [构建版本差异指南](./guides-build-differences.md)。

---

性能是 Lodash 的一个持续关注点。通过理解其内部优化并应用上述技巧，您可以确保您的应用程序充分利用 Lodash 提供的速度和效率。如果您对特定用例的性能有疑问，运行基准测试是找到答案的最佳方式。