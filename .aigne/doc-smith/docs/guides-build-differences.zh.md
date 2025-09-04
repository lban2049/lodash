# 构建差异

Lodash 提供了多种构建版本和模块格式，以适应不同的项目要求、环境和包大小限制。了解这些差异有助于您根据需求选择最高效的构建版本。

## 可用的构建版本

Lodash 提供两种主要的预编译构建版本：包含所有方法的完整版和轻量级的核心版。

| 构建版本 | Gzipped 大小（约） | 描述 |
|---|---|---|
| **完整版** | ~24 kB | 包含完整的 Lodash 库。适用于不以包大小为主要考虑因素的环境，例如 Node.js 后端。 |
| **核心版** | ~4 kB | Lodash 最核心函数的轻量级子集，适用于需要最大限度减小 JavaScript 负载的项目。 |

这两种构建版本都可直接下载或通过各种 CDN 获取。

*   [下载核心版](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js)
*   [下载完整版](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js)
*   [查看 CDN 副本](https://www.jsdelivr.com/projects/lodash)

## 模块格式与用法

根据您的模块系统和优化策略，可以通过多种方式将 Lodash 集成到项目中。

### UMD (通用模块定义)

要在浏览器中直接使用，您可以通过 `<script>` 标签引入 UMD 构建版本。这是一种无需构建过程即可快速上手的方法。

```html
<script src="lodash.js"></script>
```

### CommonJS (Node.js)

在 Node.js 环境中，您可以使用标准的 CommonJS 语法来引入 Lodash。

```javascript
// 加载完整版。
var _ = require('lodash');

// 加载核心版。
var _ = require('lodash/core');
```

### 函数式编程 (FP) 构建版本

对于使用函数式编程风格的开发者，Lodash 提供了专用的 FP 构建版本。这些方法是不可变的、自动柯里化的，并且采用 iteratee-first、data-last 的签名。

```javascript
// 加载 FP 构建版本
var fp = require('lodash/fp');
```

### 单方法包 (Cherry-Picking)

要实现尽可能小的包大小，您可以导入单个方法。当与 Webpack、Rollup 或 Browserify 等打包工具结合使用时，这种方法非常有效，因为它能确保最终输出中只包含您实际使用的代码。

```javascript
// 按需挑选一个标准方法
var at = require('lodash/at');

// 按需挑选一个 FP 方法
var curryN = require('lodash/fp/curryN');
```

### ES 模块与构建工具

对于现代 JavaScript 项目，有几个包可以帮助实现 tree-shaking 和自动化优化：

*   **`lodash-es`**：Lodash 的 ES 模块版本，非常适合与支持 tree-shaking 的打包工具一起使用。
*   **`babel-plugin-lodash`**：一个 Babel 插件，可自动将您的代码转换为使用单方法导入，从而简化 cherry-picking 过程。
*   **`lodash-webpack-plugin`**：一个 Webpack 插件，通过将方法实现替换为更小、更具体的版本来进一步优化 Lodash 构建。

## 创建自定义构建

您可以使用 `lodash-cli` 生成满足特定需求的自定义构建。这使您可以创建一个仅包含所需方法的构建。

以下命令演示了如何生成标准的完整版和核心版构建：

```shell
# 从源码生成完整版构建
$ lodash -o ./dist/lodash.js

# 生成核心版构建
$ lodash core -o ./dist/lodash.core.js
```

--- 

通过选择合适的构建版本和模块格式，您可以优化项目的性能和包大小。有关更深入的优化技术，请参阅 [性能](./guides-performance.md) 指南。