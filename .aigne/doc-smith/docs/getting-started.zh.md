# 入门指南

欢迎使用 Lodash！本指南将帮助你快速上手。Lodash 通过简化数组、数字、对象和字符串的操作，让 JavaScript 编程变得更加轻松。

我们将介绍如何在浏览器和 Node.js 环境中安装和使用 Lodash。

## 安装

根据你的环境，可以通过多种方式将 Lodash 添加到项目中。

### 在浏览器中

要在浏览器中直接使用，你可以使用 `<script>` 标签。你可以下载完整版本或链接到 CDN。

```html HTML Setup icon=logos:html-5
<script src="lodash.js"></script>
```

你可以在 [jsDelivr](https://www.jsdelivr.com/projects/lodash) 上找到各种 CDN 选项，包括压缩版和核心版。

**使用 CDN 的示例：**
```html Using a CDN icon=logos:html-5
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

### 在 Node.js 中（使用 npm）

对于 Node.js 项目，推荐通过 npm 安装 Lodash。

```shell Install with npm icon=logos:npm
$ npm i --save lodash
```

安装后，你可以在项目中引入它：

```javascript Basic Usage icon=logos:nodejs
// 加载完整版本。
const _ = require('lodash');

const anArray = [1, 2, 3, 4, 5, 6];
const chunkedArray = _.chunk(anArray, 2);

console.log(chunkedArray);
// => [[1, 2], [3, 4], [5, 6]]
```

## 模块格式

Lodash 是高度模块化的，允许你只加载需要的部分，以保持项目包的体积较小。以下是常用的使用方式：

*   **完整版**：加载整个库。适用于快速原型开发或需要使用多个函数的情况。
    ```javascript icon=logos:javascript
    const _ = require('lodash');
    ```

*   **核心版**：一个较小的版本，包含基本和常用的函数。
    ```javascript icon=logos:javascript
    const _ = require('lodash/core');
    ```

*   **单独引入方法**：导入单个函数以最小化你的包体积。这是生产环境 Web 应用程序的最佳方法。
    ```javascript icon=logos:javascript
    const at = require('lodash/at');
    const curryN = require('lodash/fp/curryN');
    ```

*   **FP 模块**：用于函数式编程，提供不可变、自动柯里化、迭代优先和数据置后的方法。
    ```javascript icon=logos:javascript
    const fp = require('lodash/fp');
    ```

有关可用版本的更详细比较以及如何创建你自己的版本，请参阅我们的 [构建差异](./guides-build-differences.md) 指南。

## 接下来做什么？

既然你已经安装了 Lodash，接下来可以继续你的学习之旅：

<x-cards>
  <x-card data-title="API 参考" data-icon="lucide:book-open" data-href="/api">
    浏览按类别组织的 Lodash 函数完整列表，每个函数都附有详细示例。
  </x-card>
  <x-card data-title="函数式编程指南" data-icon="lucide:function-square" data-href="/fp-guide">
    了解 Lodash 的 FP 变体，它为函数式编程模式提供了强大的工具。
  </x-card>
</x-cards>