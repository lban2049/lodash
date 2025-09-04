# 概述

欢迎查阅 Lodash v4.17.21 的官方文档。Lodash 是一个现代化的 JavaScript 实用工具库，提供了模块化、高性能以及其他附加功能。它简化了处理数组、数字、对象和字符串的繁琐工作，使 JavaScript 的使用变得更加轻松。

Lodash 的模块化方法非常适用于：
*   迭代数组、对象和字符串
*   操作和测试值
*   创建复合函数

本篇文档旨在帮助您快速高效地找到所需信息，无论您是新用户还是经验丰富的开发者。

## 核心概念

Lodash 基于几项关键原则构建，这些原则使其成为任何 JavaScript 项目的强大工具。

```d2
direction: down

Your-Application: {
  shape: rectangle
  label: "你的应用程序"
}

Lodash-Ecosystem: {
  shape: package
  label: "Lodash 生态系统"
  grid-columns: 1

  Lodash-Library: {
    label: "Lodash 库 (v4.17.21)"
    grid-columns: 2

    Core-Modules: {
      label: "标准模块"
      grid-columns: 3
      Array: {}
      Object: {}
      String: {}
      Function: {}
      Util: {}
      "...": {}
    }

    FP-Variant: {
      label: "FP 变体 (lodash/fp)"
      "不可变、自动柯里化、\n迭代优先、数据置后"
    }
  }

  Build-Tools: {
    label: "构建与优化工具"
    grid-columns: 3
    lodash-cli: {}
    babel-plugin-lodash: {}
    lodash-webpack-plugin: {}
  }
}

Your-Application -> Lodash-Ecosystem.Lodash-Library: "导入和使用"
Lodash-Ecosystem.Build-Tools -> Lodash-Ecosystem.Lodash-Library: "生成自定义构建"

```

<x-cards data-columns="2">
  <x-card data-title="模块化与性能" data-icon="lucide:boxes">
    Lodash 提供多种构建版本。您可以加载完整库、核心构建版本，甚至可以只挑选单个方法，以保持项目包的最小体积。这种模块化的方法确保您只包含所需的代码。
  </x-card>
  <x-card data-title="函数式编程" data-icon="lucide:function-square">
    对于偏好函数式编程风格的开发者，`lodash/fp` 模块提供了 Lodash 方法的不可变、自动柯里化、迭代优先、数据置后的版本。
  </x-card>
</x-cards>

## 如何使用本文档

本文档分为几个关键部分，以帮助您充分利用 Lodash。无论您是在寻找安装说明、详细的 API 规范还是高级指南，都可以在这里找到。

<x-cards data-columns="2">
  <x-card data-title="入门指南" data-icon="lucide:rocket" data-href="/getting-started">
    初次接触 Lodash？从这里开始。查找可快速复制粘贴的说明，了解如何在项目中安装和使用 Lodash。
  </x-card>
  <x-card data-title="API 参考" data-icon="lucide:book-open" data-href="/api">
    每个 Lodash 方法的完整参考，按数据类型组织。如果您清楚自己要查找的内容，这是最快找到它的方法。
  </x-card>
  <x-card data-title="函数式编程指南" data-icon="lucide:workflow" data-href="/fp-guide">
    深入了解 Lodash 的函数式编程能力，包括自动柯里化和不变性等概念。
  </x-card>
  <x-card data-title="指南" data-icon="lucide:compass" data-href="/guides">
    探索高级主题，例如创建自定义构建、性能基准测试以及理解不同模块格式之间的差异。
  </x-card>
</x-cards>

## 社区与贡献

Lodash 是一个由专注的社区维护的开源项目。我们欢迎各种贡献和讨论。

*   **聊天：** 在 [Gitter](https://gitter.im/lodash/lodash) 上加入对话。
*   **贡献：** 阅读我们的[贡献指南](https://github.com/lodash/lodash/blob/master/.github/CONTRIBUTING.md)以开始。
*   **关注：** 在 [Twitter](https://twitter.com/bestiejs) 上关注我们以获取最新信息。

## 下一步

准备好深入了解了吗？请前往我们的[入门指南](./getting-started.md)，快速完成安装并进行首次函数调用。
