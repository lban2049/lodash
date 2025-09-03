# 快速入门

Lodash 解决了处理数组、数字、对象和字符串时的麻烦，让 JavaScript 编程变得更加轻松。按照以下说明，你可以在几分钟内快速上手。

## 安装

你可以通过在浏览器中使用 script 标签或通过 npm 等包管理器来将 Lodash 添加到你的项目中。

### 在浏览器中使用

要在浏览器中开始使用，请在你的页面上引入 Lodash 脚本。你可以自行托管该文件，也可以使用 CDN。

```html
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
```

这样，Lodash 库就可以通过全局变量 `_` 来使用。

<x-cards>
  <x-card data-title="完整构建版" data-icon="lucide:box" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js">
    包含所有 Lodash 方法，功能全面（gzip 压缩后约 24 kB）。
  </x-card>
  <x-card data-title="核心构建版" data-icon="lucide:box-select" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js">
    包含核心方法的轻量版本，适用于小型项目（gzip 压缩后约 4 kB）。
  </x-card>
</x-cards>

更多 CDN 选项，请访问 [jsDelivr](https://www.jsdelivr.com/projects/lodash)。

### 使用 npm

对于 Node.js 应用程序或使用 Webpack、Rollup 等构建工具的项目，请通过 npm 安装 Lodash：

```shell
$ npm i --save lodash
```

## 基本用法

安装完成后，你就可以立即开始使用 Lodash 的函数了。

### 在 Node.js 中

引入完整的库并调用一个方法：

```javascript
// 加载完整构建版。
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

### 在浏览器中使用

引入 script 标签后，`_` 变量即可在全局范围内使用：

```html
<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
<script>
  var users = [
    { 'user': 'barney',  'active': false },
    { 'user': 'fred',    'active': false },
    { 'user': 'pebbles', 'active': true }
  ];

  var activeUser = _.find(users, { 'active': true });

  console.log(activeUser);
  // => { 'user': 'pebbles', 'active': true }
</script>
```

## 模块化加载以减小打包体积

你可以通过导入单个方法（而不是整个库）来优化应用程序的打包体积。这对于文件大小至关重要的前端项目尤其有用。

### 按需引入方法

你可以逐个引入所需的方法：

```javascript
// 仅加载 'at' 方法。
var at = require('lodash/at');

var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };

at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

### 函数式编程 (FP) 构建版

如果你偏好函数式编程风格（其方法具有不可变、自动柯里化、迭代优先、数据置后的特点），请使用 FP 构建版。

```javascript
// 加载 FP 构建版。
var fp = require('lodash/fp');

var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false }
];

// FP 风格是数据置后的。
var getActiveUsers = fp.filter({ 'active': true });

getActiveUsers(users);
// => [{ 'user': 'barney', 'age': 36, 'active': true }]
```

有关该范式的完整指南，请参阅[函数式编程指南](./fp-guide.md)。

---

现在你已经安装了 Lodash 并了解了基本用法，可以浏览我们的 [API 参考](./api.md) 来查看完整的函数列表。
