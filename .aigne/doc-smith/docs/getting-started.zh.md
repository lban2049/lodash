# 入门指南

欢迎使用 Lodash！本指南将帮助你在项目中快速上手并运行该库。Lodash 解决了处理数组、数字、对象和字符串时的繁琐问题，让 JavaScript 编程变得更加简单。

如需查看所有可用函数的完整列表，请参阅 [API 参考](./api.md)。

## 安装

Lodash 以 [UMD](https://github.com/umdjs/umd) 模块的形式提供，可在多种环境中使用。你可以通过在浏览器中使用 script 标签，或通过 npm 等包管理器进行安装，将其添加到你的项目中。

### 在浏览器中使用

要在浏览器中直接使用 Lodash，可以通过 `<script>` 标签引入。你可以从官网下载完整构建版本，或链接到 CDN 副本。

```html
<script src="lodash.js"></script>
```

你可以在 [jsdelivr](https://www.jsdelivr.com/projects/lodash) 上找到多种 CDN 选项。

### 使用 npm

对于 Node.js 应用或使用 webpack、Rollup 等打包工具的项目，推荐通过 npm 安装 Lodash。

```shell
$ npm i --save lodash
```

## 基本用法

安装后，你可以在你的 Node.js 文件中 require Lodash，或在你的现代 JavaScript 项目中 import 它。

### 在 Node.js 中

以下是在 Node.js 环境中加载 Lodash 的常见方法：

```javascript
// 加载完整构建版本。
var _ = require('lodash');

// 加载核心构建版本（函数的较小子集）。
var _ = require('lodash/core');

// 加载 FP 构建版本，用于函数式编程，其方法具有不可变、自动柯里化的特点。
var fp = require('lodash/fp');
```

### 按需选择方法

为了保持较小的打包体积，你可以单独导入各个方法。这对于前端项目尤其有用。

```javascript
// 按需选择一个特定方法。
var at = require('lodash/at');

// 从 FP 构建版本中按需选择一个方法。
var curryN = require('lodash/fp/curryN');
```

### 你的第一个函数调用

让我们尝试一个简单的示例。我们将使用 `_.chunk` 方法，该方法可以将一个数组按指定大小分割成多个组。

```javascript
const _ = require('lodash');

const data = ['a', 'b', 'c', 'd', 'e'];

const chunks = _.chunk(data, 2);

console.log(chunks);
// => [['a', 'b'], ['c', 'd'], ['e']]
```

这展示了 Lodash 如何通过清晰简洁的代码来简化常见的数据操作任务。

## 后续步骤

既然你已经安装了 Lodash，就可以开始探索其强大的功能了。请深入阅读 [API 参考](./api.md)，发现所有可用的函数。