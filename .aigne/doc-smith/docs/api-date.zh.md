# 日期

Lodash 提供了一个用于处理日期的工具函数，主要用于获取当前时间戳。该函数可用于性能测量、日志记录或任何需要高分辨率时间戳的场景。

---

## now

获取自 Unix 纪元（1970 年 1 月 1 日 00:00:00 UTC）以来经过的毫秒数时间戳。

该方法是 `Date.now()` 的高分辨率替代方案。

### 参数

该函数不接受任何参数。

### 返回值

(`number`): 返回当前时间戳。

### 示例

```javascript icon=logos:javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => 记录延迟调用所花费的毫秒数。
```

---

本节介绍了 Lodash 的日期工具。如需了解更复杂的与时间相关的函数调度，请浏览 [函数](./api-function.md) 分类下的方法，例如 `_.defer` 和 `_.delay`。