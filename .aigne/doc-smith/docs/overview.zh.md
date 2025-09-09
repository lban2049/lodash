# 概述

欢迎阅读 Lodash v4.17.21 的官方文档。Lodash 是一个现代 JavaScript 实用工具库，提供了模块化、高性能以及其他附加功能。它消除了处理数组、数字、对象和字符串的麻烦，让 JavaScript 的使用变得更加轻松。

Lodash 基于 [MIT 许可证](https://raw.githubusercontent.com/lodash/lodash/4.17.21/LICENSE) 发布，专为现代高性能环境而设计。

## 为什么使用 Lodash？

Lodash 的模块化方法为常见的编程任务提供了一种一致、高性能且可定制的解决方案。其核心优势在于：

*   **遍历集合**：通过强大而简洁的辅助函数，简化对数组、对象和字符串的复杂遍历操作。
*   **操控数据**：简化值的操控和测试，涵盖从简单的数据转换到复杂的对象操控。
*   **创建函数**：利用用于创建复合函数、柯里化函数和防抖函数的实用工具，构建功能强大且可复用的逻辑。

## 探索文档

本文档旨在帮助您快速找到所需内容。以下是主要部分：

<x-cards data-columns="2">
  <x-card data-title="API 参考" data-icon="lucide:book-open" data-href="/api">
    一份全面、可搜索的 Lodash 所有方法参考，按数据类型组织以便快速查找。
  </x-card>
  <x-card data-title="函数式编程指南" data-icon="lucide:function-square" data-href="/fp-guide">
    了解 Lodash 的 FP 变体，它通过自动柯里化、迭代函数优先、数据置后的方法来提倡不变性。
  </x-card>
  <x-card data-title="指南" data-icon="lucide:compass" data-href="/guides">
    探索适用于高级用例的技术指南，包括性能优化和使用不同的库构建版本。
  </x-card>
  <x-card data-title="贡献与社区" data-icon="lucide:users" data-href="/contributing">
    了解如何为项目做出贡献，并通过我们的讨论渠道与社区建立联系。
  </x-card>
</x-cards>

## 快速入门

在几分钟内即可上手使用 Lodash。有关浏览器、Node.js 和打包工具的详细说明，请参阅 [快速入门](./getting-started.md) 指南。

### 安装

要将 Lodash 添加到您的项目中，请通过 npm 安装它：

```shell npm install
$ npm i --save lodash
```

### 基本用法

安装后，您可以在代码中导入和使用 Lodash 方法：

```javascript Usage Example icon=logos:javascript
// 加载完整构建版本。
var _ = require('lodash');

var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

// 查找第一个活动用户
var activeUser = _.find(users, function(o) { return o.active; });

console.log(activeUser);
// => { 'user': 'pebbles', 'active': true }
```

---

准备好开始了吗？请前往 [快速入门](./getting-started.md) 部分，将 Lodash 集成到您的项目中。