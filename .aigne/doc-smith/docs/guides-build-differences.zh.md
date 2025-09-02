# 构建版本的差异

Lodash 提供多种构建版本和模块格式，以适应不同的开发环境和性能需求。选择合适的构建版本可以显著优化应用程序的包大小和加载时间。本指南将解释不同构建版本之间的差异，并帮助您选择最适合您项目的版本。

## 核心版与完整版构建

Lodash 提供两种主要的预编译构建版本：轻量级的**核心版**构建和功能全面的**完整版**构建。

| 特性 | 完整版构建 | 核心版构建 |
|---|---|---|
| **描述** | 包含所有 Lodash 函数，提供广泛的实用功能。 | 一个轻量级版本，包含最常用函数的一个子集，适用于包大小至关重要的环境。 |
| **Gzipped 大小** | ~24 kB | ~4 kB |
| **Node.js 导入** | `require('lodash')` | `require('lodash/core')` |
| **使用场景** | 适用于 Node.js 应用程序或对包大小没有主要考量的项目。 | 推荐用于前端应用程序、移动 Web 或任何优先考虑初始加载性能的场景。 |

您可以直接下载这些构建版本或使用 CDN：

- **核心版构建**: [lodash.core.js](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js)
- **完整版构建**: [lodash.js](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js)
- **CDN 选项**: [jsdelivr](https://www.jsdelivr.com/projects/lodash)

## 模块格式与优化

为了与现代 JavaScript 工具链集成，Lodash 支持多种模块格式，这些格式可以实现诸如摇树优化（tree-shaking）等优化。

### UMD (通用模块定义)

标准的 `lodash` 包使用 UMD 格式，使其与各种环境兼容。

**在浏览器中：**
```html
<script src="lodash.js"></script>
```

**在 Node.js 中：**
```javascript
// 加载完整版构建。
var _ = require('lodash');

// 加载核心版构建。
var _ = require('lodash/core');
```

### 按需引入方法

对于前端项目，最有效的优化是只导入您需要的方法。这使得像 webpack 或 Rollup 这样的打包工具能够执行摇树优化（tree-shaking），从而从最终的包中排除未使用的代码。

```javascript
// 按需引入方法以减小包大小。
var at = require('lodash/at');
var curryN = require('lodash/fp/curryN');
```

### ES 模块

对于使用 ES 模块的项目，推荐使用 `lodash-es` 包。它提供原生的 ES 模块导出，这使得现代构建工具可以进行更高效的摇树优化。为了进一步自动化此过程，您可以使用 [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash) 和 [lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin)。

### 函数式编程 (FP) 构建版

Lodash 还提供了一个用于函数式编程的构建版本。该版本具有不可变、自动柯里化、函数优先、数据置后的方法。

```javascript
// 加载 FP 构建版。
var fp = require('lodash/fp');
```
要深入了解这种范式，请参阅[函数式编程指南](./fp-guide.md)。

## 如何选择

使用此图表来确定最适合您需求的构建版本：

```d2
direction: down

start: "开始：选择 Lodash 构建版本"

env_check: "您的环境是什么？"

start -> env_check

subgraph "浏览器" {
  direction: down
  bundle_sensitive: "包大小是否至关重要？"
  use_core: "使用核心版构建 (lodash.core.js) 或按需引入方法。"
  use_full: "使用完整版构建 (lodash.js)。"

  bundle_sensitive -> use_core: "是"
  bundle_sensitive -> use_full: "否"
}

subgraph "Node.js" {
  direction: down
  use_full_node: "使用完整的 'lodash' 包。"
}

subgraph "现代打包工具 (webpack, Vite)" {
  direction: down
  use_es: "使用 'lodash-es' 或按需引入方法以实现最佳的摇树优化。"
}

env_check -> bundle_sensitive: "浏览器"
env_check -> use_full_node: "Node.js"
env_check -> use_es: "现代打包工具"

fp_check: "您是否偏好函数式编程风格？"

use_core --> fp_check
use_full --> fp_check
use_full_node --> fp_check
use_es --> fp_check

end: "选择完成"

use_fp: "使用 'lodash/fp' 变体。"

fp_check -> use_fp: "是"
fp_check -> end: "否"
use_fp -> end
```

## 自定义构建

为了完全控制，您可以使用 `lodash-cli` 创建一个自定义构建，仅包含您项目所需的特定方法。构建过程可以通过 `package.json` 中定义的 npm 脚本来启动。

**生成标准构建**

此命令将在 `./dist/` 目录下生成主发行版和 FP 发行版文件。
```shell
$ npm run build
```

**直接使用 lodash-cli**

或者，您也可以使用 `lodash-cli` 来生成特定的构建版本。

```shell
# 创建一个完整版构建
$ lodash -o ./dist/lodash.js

# 创建一个核心版构建
$ lodash core -o ./dist/lodash.core.js
```

通过了解这些构建版本的差异，您可以做出明智的选择，以平衡功能与性能。要进一步优化您的代码，请考虑阅读我们的[性能指南](./guides-performance.md)。