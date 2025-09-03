# 构建版本差异

Lodash 提供了多种构建版本和模块格式，以适应不同的环境和使用场景。选择合适的构建版本是优化应用程序包大小和性能的关键。本指南将详细介绍可用的选项，帮助你选择最适合自己需求的版本。

如需交互式构建工具，请参阅官方的 [Custom Builds](https://lodash.com/custom-builds) 页面。

## 主要构建版本

Lodash 提供两种主要的构建版本：一个全面的 **Full build** 和一个轻量级的 **Core build**。两者都以 UMD 模块形式提供，使其适合在浏览器中直接使用或与模块加载器一起使用。

| 构建版本 | Gzipped 大小（约） | 描述 |
|---|---|---|
| **Full Build** | ~24 kB | 包含所有 Lodash 方法。适用于 Node.js 中的通用场景，或在需要大量工具函数时使用。 |
| **Core Build** | ~4 kB | Lodash 的一个较小子集，包含核心的工具函数。最适合对包大小有严格要求的环境。 |

### CDN 和下载链接

你可以通过 CDN 直接下载或链接到这些构建版本：

<x-cards data-columns="2">
  <x-card data-title="Full Build" data-icon="lucide:box" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js" data-cta="下载">
    包含所有函数的完整 Lodash 库。
  </x-card>
  <x-card data-title="Core Build" data-icon="lucide:box-select" data-href="https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js" data-cta="下载">
    一个包含核心工具子集的轻量级构建版本。
  </x-card>
</x-cards>

如需更多 CDN 选项，请访问 [jsDelivr 项目页面](https://www.jsdelivr.com/projects/lodash)。

## 模块格式与优化

除了主要的构建版本，Lodash 还支持多种模块格式，以便与现代开发工作流和打包工具集成。

### 按方法打包 (Cherry-Picking)

为了最大程度地优化包大小，你可以导入单个方法。这种方法可以确保最终的包中只包含你用到的代码。在使用 Webpack、Rollup 或 Parcel 等打包工具时，这种方式非常有效。

```javascript
// 仅从主库中加载 'at' 方法。
var at = require('lodash/at');

// 仅从 FP 构建版本中加载 'curryN' 方法。
var curryN = require('lodash/fp/curryN');

// 你也可以加载整个类别。
var array = require('lodash/array');
```

### ES 模块

对于使用 ES 模块语法 (`import`/`export`) 的项目，推荐使用 `lodash-es` 包。它支持 tree-shaking，打包工具会自动移除未使用的代码。

为进一步优化此过程，你可以使用以下插件：
- [babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash)
- [lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin)

### 函数式编程 (FP) 构建版本

Lodash 为函数式编程风格提供了一个专门的构建版本。`lodash/fp` 模块提供的方法具有以下特点：

- **不可变**：不修改输入数据。
- **自动柯里化**：函数可以一次传入一个参数。
- **迭代函数优先**：要应用的函数在数据之前。
- **数据置后**：数据集合是最后一个参数。

```javascript
// 加载 FP 构建版本以使用不可变、自动柯里化的方法。
var fp = require('lodash/fp');
```

## 创建自定义构建版本

你可以使用 `lodash-cli` 生成自己的自定义构建版本。这使你能够将所需的方法打包到单个文件中。

首先，如果尚未安装，请安装 CLI 工具。然后，使用项目 `package.json` 文件中提供的构建脚本，或直接运行 `lodash-cli` 命令。

以下是用于生成标准分发文件的命令：

```shell
# 生成完整构建版本
$ lodash -o ./dist/lodash.js

# 生成核心构建版本
$ lodash core -o ./dist/lodash.core.js
```

通过利用这些不同的构建版本和模块格式，你可以根据项目的特定性能和大小限制来定制 Lodash。