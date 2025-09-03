# 概述

Lodash 是一个现代 JavaScript 实用工具库，提供了模块化、高性能以及附加功能。它通过简化处理数组、数字、对象和字符串的复杂操作，来简化常见的编程任务。本文档涵盖 Lodash v4.17.21，该版本在 MIT 许可下发布，并支持现代环境，包括 Node.js v4.0.0 及更高版本。

## 为何选择 Lodash？

Lodash 的模块化方法非常适合：

*   **迭代**数组、对象和字符串
*   **操作**和测试值
*   **创建**复合函数

它提供了一套全面的工具集，帮助你编写更简洁、更易于维护的代码。

## 核心特性

Lodash 在设计时充分考虑了专业开发者的需求，提供了几个关键的架构优势。

```d2
direction: down

"Lodash 库": {
  shape: package
  grid-columns: 1

  "核心理念": {
    shape: rectangle
    "简洁性": "让 JavaScript 更简单"
    "一致性": "可靠的实用函数"
  }

  "核心模块": {
    shape: rectangle
    grid-columns: 2
    "标准构建": "功能齐全的 UMD 模块"
    "核心构建": "满足基本需求的轻量级子集"
    "FP 模块": "函数式编程变体"
    "单方法包": "最大化模块性"
  }

  "核心模块" -> "核心理念": "遵循"
}
```

### 模块化与自定义构建

Lodash 提供多种构建版本和模块格式，使你能够将项目的打包体积保持在最小。你可以挑选单个方法，使用 ES 模块（`lodash-es`），或利用 `babel-plugin-lodash` 和 `lodash-webpack-plugin` 等插件进行优化构建。

更多详情，请参阅 [构建差异](./guides-build-differences.md) 指南。

### 函数式编程变体

对于偏好函数式编程风格的开发者，Lodash 提供了一个专门的 `lodash/fp` 模块。它提供了不可变、自动柯里化、迭代函数优先和数据置后的方法，使组合函数和构建函数式管道变得更加容易。

要了解更多信息，请阅读 [FP 指南](./fp-guide.md)。

## 文档导航

本站结构清晰，旨在帮助你高效地找到所需信息。以下是主要部分的指南：

<x-cards data-columns="2">
  <x-card data-title="入门指南" data-href="/getting-started" data-icon="lucide:play-circle">
    为在项目中安装和使用 Lodash 提供了简洁、可直接复制粘贴的说明。
  </x-card>
  <x-card data-title="API 参考" data-href="/api" data-icon="lucide:book-open">
    按数据类型组织的、全面的、可搜索的 Lodash 方法参考。
  </x-card>
  <x-card data-title="指南" data-href="/guides" data-icon="lucide:compass">
    针对高级用例的技术指南，包括性能优化和自定义构建。
  </x-card>
  <x-card data-title="贡献与社区" data-href="/contributing" data-icon="lucide:users">
    关于如何贡献和与 Lodash 社区建立联系的信息。
  </x-card>
</x-cards>


## 社区与支持

通过我们的社区渠道加入讨论，并与其他 Lodash 用户建立联系。有关如何参与、报告问题或为项目做出贡献的信息，请访问 [贡献与社区](./contributing.md) 部分。