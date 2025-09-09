# 构建差异

Lodash 提供了多种构建版本和模块格式，以适应不同的环境和项目需求。选择合适的构建版本是优化应用程序性能和包大小的关键。本指南将解释可用的选项以及如何创建自定义构建。

## 官方构建版本

Lodash 提供两种主要的预编译构建版本：全面的 **完整构建** 和轻量级的 **核心构建**。这些构建版本非常适合在浏览器或偏好使用单个文件的环境中进行快速设置。

| 构建版本 | Gzipped 大小 | 描述 |
| :--- | :--- | :--- |
| [完整构建](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.js) | ~24 kB | 包含 Lodash 方法的全集。最适合服务器端应用程序或包大小不是关键限制的场景。 |
| [核心构建](https://raw.githubusercontent.com/lodash/lodash/4.17.21/dist/lodash.core.js) | ~4 kB | 一个最小化的构建版本，包含一部分流行的核心 Lodash 工具。非常适合对每个千字节都很在意的项目。 |

如需更多 CDN 选项，可以访问 [jsDelivr](https://www.jsdelivr.com/projects/lodash)。

## 模块格式

针对现代开发工作流，Lodash 提供了多种模块格式，这些格式提供了更大的灵活性和优化机会。

<x-cards data-columns="2">
  <x-card data-title="UMD (lodash)" data-icon="mdi:npm">
    npm 上的标准包。它使用 UMD 格式，使其能够通过 `<script>` 标签与浏览器兼容，并能通过 `require('lodash')` 在 Node.js 中使用。
  </x-card>
  <x-card data-title="ES Modules (lodash-es)" data-icon="logos:esmodules">
    提供 ES 模块，允许 Webpack 或 Rollup 等现代打包工具执行 tree-shaking，从而只包含你使用的代码。
  </x-card>
  <x-card data-title="Functional (lodash/fp)" data-icon="material-symbols:function">
    一种函数式编程变体，其方法具有不可变、自动柯里化、迭代优先和数据置后的特点。详情请参阅 [FP 指南](./fp-guide.md)。
  </x-card>
  <x-card data-title="Per-Method Packages" data-icon="ph:package-duotone">
    每个 Lodash 方法都作为独立的包发布（例如，`lodash.at`）。这为实现最小包大小提供了最细粒度的控制。
  </x-card>
</x-cards>

## 优化包大小

除了选择合适的构建版本，你还可以使用多种技术进一步减小包大小。

### 按需引入方法

你可以只导入你需要的方法，而不是导入整个库。这是帮助打包工具消除未使用代码的最直接方法。

```javascript Cherry-picking in Node.js icon=logos:nodejs-icon
// 只加载 'at' 方法
var at = require('lodash/at');

// 只从 FP 构建中加载 'curryN' 方法
var curryN = require('lodash/fp/curryN');
```

### 使用构建工具和插件

对于较大的项目，手动按需引入可能很繁琐。生态系统提供了能够自动化此过程的插件。

- **[babel-plugin-lodash](https://www.npmjs.com/package/babel-plugin-lodash)**：一个 Babel 插件，可将你的 Lodash 导入转换为按需引入的方式，因此你可以编写 `import { at } from 'lodash'` 并获得优化后的结果。
- **[lodash-webpack-plugin](https://www.npmjs.com/package/lodash-webpack-plugin)**：一个 Webpack 插件，与 `babel-plugin-lodash` 配合使用，通过将方法调用替换为更具体或更小的替代方案来进一步优化构建。

### 生成自定义构建

你可以使用 `lodash-cli` 直接从源代码生成你自己的自定义构建。这使你可以完全控制所包含的模块。

```shell Generating Builds with lodash-cli icon=mdi:console
# 生成标准完整构建
$ lodash -o ./dist/lodash.js

# 生成核心构建
$ lodash core -o ./dist/lodash.core.js
```