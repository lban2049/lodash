# 入门

要开始使用 Lodash，请将其集成到您的项目中。本指南提供了通过包管理器安装、在不同 JavaScript 环境中设置的步骤，以及一个快速入门示例。

## 下载 Lodash

您可以直接下载特定构建版本的 Lodash 或使用 CDN：

*   [核心构建版本](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js) (~4 KB gzip 压缩，针对大小优化)
*   [完整构建版本](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js) (~24 KB gzip 压缩，包含所有功能)
*   [CDN 副本](https://www.jsdelivr.com/projects/lodash) (用于快速浏览器集成)

请查看[构建版本差异](https://github.com/lodash/lodash/wiki/build-differences)，以选择适合您项目的正确版本。

## 安装方法

Lodash 支持多种安装方法，以适应您的开发环境。

### 在浏览器中

使用 `<script>` 标签直接将 Lodash 库包含在您的 HTML 中：

```html
<script src="lodash.js"></script>
```

### 使用 npm

如果您正在使用 Node Package Manager (npm)，可以将 Lodash 作为项目的依赖项进行安装。首先，请确保 npm 已更新到最新版本，然后安装 Lodash：

```shell
$ npm i -g npm
$ npm i --save lodash
```

此命令将安装完整的 Lodash 构建版本，并将其保存为您的 `package.json` 中的依赖项。

### 在 Node.js 中

通过 npm 安装后，您可以在 Node.js 应用程序中 `require` Lodash 模块。根据您的需求，有以下几种选项：

*   **加载完整构建版本：** 导入所有 Lodash 方法。

    ```js
    var _ = require('lodash');
    ```

*   **加载核心构建版本：** 导入一组更小、更集中的实用工具方法。

    ```js
    var _ = require('lodash/core');
    ```

*   **加载 FP 构建版本：** 用于函数式编程范式，具有不可变、自动柯里化、迭代器优先和数据在后的方法。

    ```js
    var fp = require('lodash/fp');
    ```

*   **加载方法类别：** 仅导入特定类别的方法以减小打包大小。

    ```js
    var array = require('lodash/array');
    var object = require('lodash/fp/object');
    ```

*   **挑选单个方法：** 对于最小的 browserify/rollup/webpack 包，只导入您需要的方法。

    ```js
    var at = require('lodash/at');
    var curryN = require('lodash/fp/curryN');
    ```

**注意：** 如果您正在使用 Node.js 6 以下版本进行 REPL (Read-Eval-Print Loop) 操作，请安装 `n_` 以获得最佳 Lodash 使用体验：

```shell
$ npm i -g n_
```

## 为什么使用 Lodash？

Lodash 通过简化对数组、数字、对象和字符串的常见操作，从而简化了 JavaScript 开发。其模块化方法对于以下方面特别有效：

*   遍历数组、对象和字符串。
*   操作和测试值。
*   创建组合函数。

## Lodash 的“Hello World”示例

让我们编写一个简单的 Node.js 示例，看看 Lodash 的实际应用。本示例使用 `_.camelCase` 方法来转换字符串。

```javascript
const _ = require('lodash');

const greeting = "hello world lodash";
const camelCasedGreeting = _.camelCase(greeting);

console.log(camelCasedGreeting);
```

**示例输出：**

```
helloWorldLodash
```

这展示了 Lodash 如何处理简单的字符串转换，使常见任务更加简洁和可读。

---

现在您已经安装了 Lodash 并了解了其基本优势，请继续阅读[核心概念](./core-concepts.md)部分，深入了解其模块化设计和各种分发格式。