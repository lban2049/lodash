# 日期 (Date)

本部分详细介绍了 Lodash 中用于处理日期和时间戳的函数。这些工具函数可以帮助你轻松获取当前时间。

Lodash 的日期函数专注于提供核心功能。有关更广泛的实用工具，请参阅 [工具 (Util)](./api-util.md) 和 [语言 (Lang)](./api-lang.md) 部分。

---

## `_.now()`

获取自 Unix 纪元（1970年1月1日 00:00:00 UTC）以来经过的毫秒数作为时间戳。该方法是对 `Date.now()` 的封装，提供了跨环境的一致性。

### 参数

此函数不接受任何参数。

### 返回

`(number)`: 返回当前的时间戳（毫秒）。

### 示例

你可以使用 `_.now()` 来简单地测量代码块的执行时间。

```javascript
const start = _.now();

// 执行一些耗时操作...
for (let i = 0; i < 1000000; i++) {
  // 模拟工作
}

const end = _.now();
const duration = end - start;

console.log(`操作耗时: ${duration} 毫秒`);
// => "操作耗时: 5 毫秒" (具体数值会因执行环境而异)
```

另一个例子是结合 `_.defer` 来检查延迟调用的时间差：

```javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => 在大约 1ms 后打印出延迟调用的毫秒数
```

`_.now` 是一个简单而高效的获取高精度时间戳的方法，常用于性能测量和计时。

---

浏览完日期函数后，可以继续探索 [函数 (Function)](./api-function.md) 部分，了解更多用于函数式编程的辅助函数。