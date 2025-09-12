# 日期

本节提供了处理 Date 对象的 Lodash 函数的详细参考。这些实用工具可用于获取当前时间戳和执行与日期相关的操作。

如需更多实用函数，您可能也会对 [Util](./api-util.md) 和 [Lang](./api-lang.md) API 类别感兴趣。

---

## now

获取自 Unix 纪元（1970 年 1 月 1 日 00:00:00 UTC）以来经过的毫秒数时间戳。

### 参数

此函数不接受任何参数。

### 返回值

<x-field data-name="timestamp" data-type="number" data-desc="返回自 Unix 纪元以来的当前时间戳（以毫秒为单位）。"></x-field>

### 示例

`_.now()` 函数可用于性能计时和创建唯一时间戳。

```javascript Measuring Time icon=logos:javascript
// 延迟执行一个函数，并测量其执行所需的时间。
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => 输出延迟调用所需的毫秒数。
```

---

## 后续步骤

在处理日期之后，您可能会发现这些相关的 API 部分对您的项目很有用。

<x-cards>
  <x-card data-title="Function" data-icon="lucide:function-square" data-href="/api/function">
    探索用于控制函数执行的去抖动、节流、柯里化等函数。
  </x-card>
  <x-card data-title="Lang" data-icon="lucide:languages" data-href="/api/lang">
    探索用于类型检查、克隆和类型转换的语言实用工具。
  </x-card>
</x-cards>