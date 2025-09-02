# Getting Started

本指南提供了在不同环境中安装和使用 Lodash 的简洁说明，帮助您快速上手。Lodash 是一个强大的 JavaScript 工具库，通过提供处理数组、数字、对象、字符串等任务的辅助函数，简化了编程过程。

## 浏览器环境

要在浏览器中直接使用 Lodash，您可以通过 CDN 引入脚本文件。我们提供多种构建版本以满足不同需求。

在 HTML 文件中添加以下代码：

```html
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

### 构建版本

您可以根据项目需求选择不同的构建版本。核心版本体积更小，包含了最常用的工具函数。

| 构建版本 | 大小 (Gzip 压缩后) | 描述 |
|---|---|---|
| [Core build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js) | ~4 kB | 包含核心的、最常用的 Lodash 函数。 |
| [Full build](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js) | ~24 kB | 包含 Lodash 的全部功能。 |

更多 CDN 选项，请访问 [jsDelivr](https://www.jsdelivr.com/projects/lodash)。

### 快速示例

引入脚本后，`_` 变量将作为 Lodash 的全局命名空间。您可以通过它来调用所有 Lodash 函数。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Lodash Example</title>
  <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
</head>
<body>
  <script>
    const users = [
      { 'user': 'barney',  'active': false },
      { 'user': 'fred',    'active': false },
      { 'user': 'pebbles', 'active': true }
    ];

    // 使用 _.filter 查找 active 为 true 的用户
    const activeUsers = _.filter(users, { 'active': true });
    console.log(activeUsers);
    // => [{ 'user': 'pebbles', 'active': true }]

    // 使用 _.chunk 将数组拆分成指定大小的块
    const chunks = _.chunk(['a', 'b', 'c', 'd'], 2);
    console.log(chunks);
    // => [['a', 'b'], ['c', 'd']]
  </script>
</body>
</html>
```

## Node.js 和打包工具 (Webpack/Rollup)

对于 Node.js 项目或使用打包工具的前端项目，推荐使用 npm 或其他包管理器进行安装。

### 安装

通过 npm 安装 Lodash：
```shell
npm i --save lodash
```

### 使用方法

安装后，您可以根据需要导入整个库、特定构建版本或单个函数。

**1. 导入完整版**

加载完整的 Lodash 库。
```javascript
const _ = require('lodash');

const result = _.chunk(['a', 'b', 'c', 'd'], 2);
console.log(result);
// => [['a', 'b'], ['c', 'd']]
```

**2. 导入核心版**

如果只需要核心功能，可以导入体积更小的核心构建版本。
```javascript
const _ = require('lodash/core');
```

**3. 按需导入（Cherry-picking）**

为了优化最终打包体积，强烈建议按需导入您需要的函数。这样可以确保只有使用到的代码被包含进来。

```javascript
const at = require('lodash/at');
const curryN = require('lodash/fp/curryN');

const object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

const result = at(object, ['a[0].b.c', 'a[1]']);
console.log(result);
// => [3, 4]
```

### 其他模块格式

Lodash 还提供了多种模块格式以适应不同的开发需求：

- **`lodash-es`**: ES 模块版本，便于 Tree Shaking。
- **`babel-plugin-lodash`** & **`lodash-webpack-plugin`**: 配合 Babel 和 Webpack 使用，可以自动将代码中的 Lodash 调用转换为按需导入，从而极大地优化打包体积。
- **`lodash/fp`**: 函数式编程版本，提供不可变、自动柯里化、函数优先、数据置后的方法。
- **`lodash-amd`**: 适用于 AMD 规范的模块加载器。

## 下一步

现在您已经了解了如何在项目中引入和使用 Lodash。接下来，我们建议您浏览 [API 参考](./api.md) 以了解 Lodash 提供的所有强大功能。