# 入门指南

本指南提供了简洁、即拷即用的说明，帮助你在项目中快速上手并运行 Lodash。无论你是在 Web 浏览器还是 Node.js 环境中工作，只需几个简单的步骤，即可开始使用 Lodash 强大的实用工具函数。

## 在浏览器中使用

在浏览器中使用 Lodash 最简单的方法是通过 `<script>` 标签引入。你可以直接下载副本，也可以使用内容分发网络 (CDN) 来提供文件。

```html title="index.html"
<script src="lodash.js"></script>
```

为方便起见，你可以使用像 jsDelivr 这样的流行 CDN 来引入 Lodash，无需自行托管文件：

```html title="index.html"
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

引入后，Lodash 库将通过全局变量 `_` 提供。

```javascript Example Usage icon=logos:javascript
const array = [1, 2, 3, 4];
const chunkedArray = _.chunk(array, 2);

console.log(chunkedArray);
// => [[1, 2], [3, 4]]
```

<x-card data-title="查找 CDN 副本" data-icon="lucide:package-check" data-href="https://www.jsdelivr.com/projects/lodash" data-cta="查看 CDN">
  探索 jsDelivr CDN 上提供的不同版本和构建的 Lodash。
</x-card>

## 在 Node.js 和 npm 中使用

对于服务器端应用程序或使用模块打包工具（如 Webpack、Rollup 或 Browserify）的项目，你可以使用 npm 将 Lodash 作为依赖项进行安装。

### 安装

在项目终端中运行以下命令：

```shell Installation Command icon=logos:npm
npm i --save lodash
```

### 基本用法

安装后，你可以在 Node.js 文件中引入完整的库。

```javascript icon=logos:nodejs
// 加载完整版本。
const _ = require('lodash');

const users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

const activeUser = _.find(users, { 'active': true });

console.log(activeUser);
// => { user: 'pebbles', active: true }
```

### 模块化导入

Lodash 是高度模块化的，允许你只加载所需的部分，从而保持应用程序的构建包体积小巧。这对于性能优化非常重要，尤其是在前端应用中。

以下是几种加载模块的方法：

**核心版本**

加载一个较小的核心版本，其中包含最基本的功能。

```javascript Core Build
const _ = require('lodash/core');
```

**函数式编程 (FP) 版本**

适用于函数式编程风格，其方法具有不可变、自动柯里化和数据后置的特点。

```javascript FP Build
const fp = require('lodash/fp');
```

**按需引入方法**

为最大限度地优化构建包体积，你可以单独导入各个方法。这是现代 Web 开发中推荐的方法。

```javascript Cherry-picking
const at = require('lodash/at');
const curryN = require('lodash/fp/curryN');

const object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
const values = at(object, ['a[0].b.c', 'a[1]']);

console.log(values);
// => [3, 4]
```

## 后续步骤

现在你已经安装了 Lodash，可以开始探索其强大的功能。请深入阅读完整的 [API 参考文档](./api.md)，查看所有可用方法的列表，找到满足你需求的完美工具函数。