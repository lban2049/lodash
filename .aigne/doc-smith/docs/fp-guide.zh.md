# 函数式编程指南

The Lodash FP 指南为标准的 Lodash 库提供了一个函数式编程的替代方案。它通过遵循不变性、自动柯里化和数据置后的参数顺序等关键原则，提倡一种更具声明性和可组合性的代码编写风格。

该模块非常适合偏好函数式方法并希望轻松构建复杂数据处理管道的开发人员。

## 核心原则

`lodash/fp` 模块对标准的 Lodash 函数进行了转换，使其遵循一套一致的函数式编程规则。

### 1. 不变性

FP 方法被设计为纯函数，不会修改其输入数据。这些方法不会就地修改数组或对象，而是返回一个应用了更改的、新的克隆实例。这可以防止副作用，并使应用程序的状态更具可预测性。

例如，在标准 Lodash 中可变的方法，如 `assign`、`defaults`、`merge`、`pull` 和 `reverse`，在 FP 版本中都变成了不可变的。

```javascript In Node.js icon=logos:nodejs
// 加载 FP 模块
const fp = require('lodash/fp');

const originalArray = [1, 2, 3, 4];

// fp 中的 'remove' 返回一个新数组，而不是修改原始数组
const newArray = fp.remove(n => n % 2 === 0)(originalArray);

console.log(newArray);
// => [1, 3]

console.log(originalArray);
// => [1, 2, 3, 4] (原始数组保持不变)
```

### 2. 自动柯里化

`lodash/fp` 中的所有方法都是自动柯里化的。这意味着你可以用比预期少的参数来调用一个函数，它会返回一个等待接收剩余参数的新函数。这对于创建专门的、可重用的函数非常有用。

```javascript icon=logos:javascript
const fp = require('lodash/fp');

const users = [
  { 'user': 'barney', 'active': false },
  { 'user': 'fred',   'active': true },
  { 'user': 'pebbles', 'active': true }
];

// 仅提供 iteratee 来创建一个专门的函数
const findActiveUser = fp.find({ 'active': true });

// 稍后，将此函数应用于你的数据
const firstActiveUser = findActiveUser(users);

console.log(firstActiveUser);
// => { user: 'fred', active: true }
```

你还可以使用占位符（`fp.placeholder` 或其别名 `__`）来不按顺序地提供参数。

```javascript icon=logos:javascript
const fp = require('lodash/fp');

// 占位符允许我们先指定数据参数
const getOrFred = fp.getOr('fred', fp.__, { 'a': { 'b': 'barney' } });

// 现在我们可以指定路径
const result = getOrFred('a.b');

console.log(result);
// => 'barney'
```

### 3. Iteratee 优先，数据置后

方法参数经过重新排列，始终将数据（如数组或对象）作为最后一个参数。Iteratee 或配置参数则排在前面。这种一致的签名使得将多个函数组合成一系列操作变得非常简单。

最常见的用例是与 `fp.flow`（或 `fp.pipe`）一起使用，它会创建一个函数管道，其中一个函数的输出会成为下一个函数的输入。

```javascript icon=logos:javascript
const fp = require('lodash/fp');

const users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred', 'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1, 'active': true }
];

// 创建一个数据处理管道
const getActiveUserNames = fp.flow(
  fp.filter('active'), // 首先，筛选出活动用户
  fp.map('user'),      // 然后，获取他们的名字
  fp.join(', ')       // 最后，将它们连接成一个字符串
);

const activeNames = getActiveUserNames(users);

console.log(activeNames);
// => 'barney, pebbles'
```

## 方法别名和重映射

为了与函数式编程的惯例保持一致，并与 Ramda 等库兼容，许多 Lodash 方法都有别名。这有助于开发人员平滑过渡并使用熟悉的术语。

下表是一些常见的别名。请注意，这并非详尽的列表。

| Lodash FP 方法 | 标准 Lodash 方法 | 常用别名 |
|---|---|---|
| `forEach` | `forEach` | `each` |
| `toPairs` | `toPairs` | `entries` |
| `assignIn` | `assignIn` | `extend` |
| `head` | `head` | `first` |
| `isMatch` | `isMatch` | `whereEq`, `matches` |
| `get` | `get` | `prop`, `path`, `property` |
| `placeholder` | (仅 FP) | `__` |
| `stubFalse` | `stubFalse` | `F` |
| `stubTrue` | `stubTrue` | `T` |
| `every` | `every` | `all` |
| `some` | `some` | `any` |
| `constant` | `constant` | `always` |
| `flowRight` | `flowRight` | `compose` |
| `includes` | `includes` | `contains` |
| `flow` | `flow` | `pipe` |
| `flatten` | `flatten` | `unnest` |

## 自定义转换

Lodash 提供了一个功能强大的 `convert` 方法，允许你生成具有自定义行为的、你自己的 FP 风格的工具对象。你可以控制诸如不变性、柯里化和参数重排等选项。

```javascript icon=logos:javascript
const _ = require('lodash');
const convert = require('lodash/fp/convert');

// 创建一个未经柯里化的自定义 FP 版本的 `map`
const fp = convert('map', _.map, { 'curry': false });

// 现在它的工作方式类似于标准的 _.map，但参数顺序经过了重新排列
fp(x => x * 2, [1, 2, 3]);
// => [2, 4, 6]
```

对于需要对其工具函数进行精细控制的用户来说，这是一项高级功能。