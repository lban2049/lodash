# Date

Lodash 提供了用于处理 JavaScript `Date` 对象的实用函数。这些辅助函数可以简化常见的日期相关任务，例如获取当前时间戳。

若需了解用于管理函数执行时间的函数（例如 `_.defer` 和 `_.delay`），请参阅 [Function 文档](./api-function.md)。

---

## now()

获取自 Unix 纪元（1970 年 1 月 1 日 00:00:00 UTC）以来所经过的毫秒数时间戳。

### 参数

该方法不接受任何参数。

### 返回值

| Type | Description |
|---|---|
| `number` | 返回当前的时间戳（数字类型）。 |

### 示例

```javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());

// => 记录延迟调用所花费的毫秒数。
```

上述示例演示了如何测量延迟操作所耗费的时间。它首先通过 `_.now()` 捕获初始时间戳，然后在延迟函数执行后计算两者之差。