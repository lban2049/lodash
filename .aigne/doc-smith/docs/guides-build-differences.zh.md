# 构建版本差异

Lodash 是一个功能多样的库，提供多种构建版本和模块格式，让你能够为项目的特定需求选择最佳选项，无论是在优化打包体积、在不同 JavaScript 环境中工作，还是在使用函数式编程风格。

本指南将解释主要的构建版本、可用的模块格式，以及如何创建自定义构建版本以实现最高效率。

## 主要构建版本

Lodash 提供两个主要的构建版本，你可以直接下载或通过 CDN 访问。它们之间的选择取决于你所需方法的数量和打包体积的限制。

| 构建版本 | Gzipped 大小 (约) | 描述 |
|---|---|---|
| **完整构建** | ~24 kB | 完整的 Lodash 库。包含所有可用方法，是通用场景下最常见的选择。 |
| **核心构建** | ~4 kB | 一个轻量级版本，包含一部分流行和核心的 Lodash 方法。非常适合对体积要求严格的项目。 |

## 模块格式与用法

根据你的环境，Lodash 可以通过多种方式集成到你的项目中。

### 在浏览器中使用

要在浏览器中直接使用，你可以通过 `<script>` 标签引入完整构建版本。这会创建一个全局变量 `_`。

```html HTML icon=logos:html-5
<script src="lodash.js"></script>
```

也可以通过 [jsDelivr](https://www.jsdelivr.com/projects/lodash) 等服务获取 CDN 副本。

### 在 Node.js 中使用 (CommonJS)

使用 Node.js 时，你可以通过 npm 安装 Lodash，并 `require` 你需要的构建版本。

```shell Shell icon=mdi:bash
$ npm i --save lodash
```

```javascript Node.js Usage icon=logos:nodejs
// 加载完整构建版本。
var _ = require('lodash');

// 加载核心构建版本以减小体积。
var _ = require('lodash/core');

// 加载 FP 构建版本以进行函数式编程。
var fp = require('lodash/fp');
```

### 配合现代打包工具使用 (ES 模块)

对于使用 webpack、Rollup 或 Vite 等打包工具的应用程序，你可以通过仅导入所需的方法来显著减小最终的打包体积。这通常被称为“按需挑选”。

这种方法与 `lodash-es` 等提供 ES 模块的包结合使用效果最好，可以实现有效的摇树优化。

```javascript Cherry-picking Methods icon=logos:javascript
// 按需挑选方法以减小打包体积。
import at from 'lodash/at';
import curryN from 'lodash/fp/curryN';
```

要自动化此过程，你可以使用 [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash) 和 [lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin) 等工具。

## 专用构建版本

除了主要的构建版本，Lodash 还为不同的编程范式和使用场景提供了专门的版本。

### 函数式编程 (FP)

`lodash/fp` 构建版本提供的方法是不可变的、自动柯里化的，并遵循迭代函数优先、数据最后的参数顺序。这种风格受到函数式编程实践者的青睐。

```javascript Loading the FP Build icon=logos:javascript
var fp = require('lodash/fp');
```

### 按方法划分的包

为了最大限度地控制打包体积，每个 Lodash 方法都可作为独立的 npm 包使用。这对于只需要一两个辅助函数的小型项目或库来说是理想的选择。

示例包包括 `lodash.at`、`lodash.curry` 等。你可以在 npm 上通过 [`lodash-modularized` 关键词](https://www.npmjs.com/browse/keyword/lodash-modularized)找到所有这些包。

### 其他模块格式

Lodash 也适用于其他模块系统：
- **`lodash-amd`**：适用于使用异步模块定义 (AMD) 的项目。

## 创建自定义构建版本

你可以使用 `lodash-cli` 生成自己的自定义 Lodash 构建版本。这允许你创建一个只包含项目所用特定方法的文件。

```shell Creating Builds with lodash-cli icon=mdi:bash
# 生成完整构建版本
$ lodash -o ./dist/lodash.js

# 生成核心构建版本
$ lodash core -o ./dist/lodash.core.js
```