# 字符串

Lodash 提供了一套全面的函数，用于字符串操作和检查。这些实用工具简化了常见的任务，例如更改大小写、修剪空白、填充和转义字符，使 JavaScript 中的字符串处理更加一致和强大。

有关其他实用函数，你可能需要查看 [Util](./api-util.md) 部分。

---

## `camelCase`

将字符串转换为[驼峰命名法](https://en.wikipedia.org/wiki/CamelCase)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回驼峰命名法的字符串。

### 示例

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

---

## `capitalize`

将字符串的第一个字符转换为大写，其余字符转换为小写。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要大写的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回大写后的字符串。

### 示例

```javascript
_.capitalize('FRED');
// => 'Fred'
```

---

## `deburr`

通过将 [Latin-1 Supplement](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) 和 [Latin Extended-A](https://en.wikipedia.org/wiki/Latin_Extended-A) 字母转换为基本的拉丁字母并移除[组合附加符号](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks)来去除字符串中的变音符号。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要去除变音符号的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回去除变音符号后的字符串。

### 示例

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

---

## `endsWith`

检查字符串是否以给定的目标字符串结尾。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要检查的字符串。默认为 `''`。 |
| `target` | `string` | 要搜索的字符串。 |
| `position` | `number` | 搜索的截止位置。默认为 `string.length`。 |

### 返回值

(`boolean`): 如果 `string` 以 `target` 结尾，则返回 `true`，否则返回 `false`。

### 示例

```javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

---

## `escape`

将字符串中的字符 `&`、`<`、`>`、`"` 和 `'` 转换为其对应的 HTML 实体。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转义的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回转义后的字符串。

### 示例

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

---

## `escapeRegExp`

转义字符串中的 `RegExp` 特殊字符 `^`、`$`、`\`、`.`、`*`、`+`、`?`、`(`、`)`、`[`、`]`、`{`、`}` 和 `|`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转义的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回转义后的字符串。

### 示例

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

---

## `kebabCase`

将字符串转换为[短横线命名法](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回短横线命名法的字符串。

### 示例

```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

---

## `lowerCase`

将字符串（视为空格分隔的单词）转换为小写。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回小写字符串。

### 示例

```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'
```

---

## `lowerFirst`

将字符串的第一个字符转换为小写。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回转换后的字符串。

### 示例

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

---

## `pad`

如果字符串比 `length` 短，则在其左侧和右侧进行填充。如果填充字符无法被 `length` 均匀分割，则会被截断。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要填充的字符串。默认为 `''`。 |
| `length` | `number` | 填充长度。默认为 `0`。 |
| `chars` | `string` | 用作填充的字符串。默认为 `' '`。 |

### 返回值

(`string`): 返回填充后的字符串。

### 示例

```javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'
```

---

## `padEnd`

如果字符串比 `length` 短，则在其右侧进行填充。如果填充字符超过 `length`，则会被截断。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要填充的字符串。默认为 `''`。 |
| `length` | `number` | 填充长度。默认为 `0`。 |
| `chars` | `string` | 用作填充的字符串。默认为 `' '`。 |

### 返回值

(`string`): 返回填充后的字符串。

### 示例

```javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'
```

---

## `padStart`

如果字符串比 `length` 短，则在其左侧进行填充。如果填充字符超过 `length`，则会被截断。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要填充的字符串。默认为 `''`。 |
| `length` | `number` | 填充长度。默认为 `0`。 |
| `chars` | `string` | 用作填充的字符串。默认为 `' '`。 |

### 返回值

(`string`): 返回填充后的字符串。

### 示例

```javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'
```

---

## `parseInt`

将字符串转换为指定基数的整数。如果 `radix` 未定义或为 `0`，则使用基数 `10`，除非值是十六进制数，此时使用基数 `16`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。 |
| `radix` | `number` | 用于解析值的基数。默认为 `10`。 |

### 返回值

(`number`): 返回转换后的整数。

### 示例

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

---

## `repeat`

将给定的字符串重复 `n` 次。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要重复的字符串。默认为 `''`。 |
| `n` | `number` | 重复字符串的次数。默认为 `1`。 |

### 返回值

(`string`): 返回重复后的字符串。

### 示例

```javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'
```

---

## `replace`

将字符串中与 `pattern` 匹配的部分替换为 `replacement`。此方法基于 [`String#replace`](https://mdn.io/String/replace)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修改的字符串。默认为 `''`。 |
| `pattern` | `RegExp` \| `string` | 要替换的模式。 |
| `replacement` | `Function` \| `string` | 匹配项的替换内容。 |

### 返回值

(`string`): 返回修改后的字符串。

### 示例

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

---

## `snakeCase`

将字符串转换为[蛇形命名法](https://en.wikipedia.org/wiki/Snake_case)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回蛇形命名法的字符串。

### 示例

```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'
```

---

## `split`

通过 `separator` 拆分字符串。此方法基于 [`String#split`](https://mdn.io/String/split)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要拆分的字符串。默认为 `''`。 |
| `separator` | `RegExp` \| `string` | 用于拆分的分割符模式。 |
| `limit` | `number` | 截断结果的长度。 |

### 返回值

(`Array`): 返回字符串片段。

### 示例

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

---

## `startCase`

将字符串转换为[首字母大写命名法](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage)。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回首字母大写命名法的字符串。

### 示例

```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'
```

---

## `startsWith`

检查字符串是否以给定的目标字符串开头。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要检查的字符串。默认为 `''`。 |
| `target` | `string` | 要搜索的字符串。 |
| `position` | `number` | 开始搜索的位置。默认为 `0`。 |

### 返回值

(`boolean`): 如果 `string` 以 `target` 开头，则返回 `true`，否则返回 `false`。

### 示例

```javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b', 1);
// => true
```

---

## `template`

创建一个可以插入数据属性的已编译模板函数。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 模板字符串。默认为 `''`。 |
| `options` | `Object` | 选项对象。 |

### 返回值

(`Function`): 返回已编译的模板函数。

### 示例

```javascript
// 使用 "interpolate" 分隔符创建一个已编译的模板。
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// 使用 HTML "escape" 分隔符来转义数据属性值。
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'
```

---

## `toLower`

将整个字符串转换为小写，类似于 `String#toLowerCase`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回小写字符串。

### 示例

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'
```

---

## `toUpper`

将整个字符串转换为大写，类似于 `String#toUpperCase`。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回大写字符串。

### 示例

```javascript
_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

---

## `trim`

从字符串中移除前导和尾随的空白或指定字符。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修剪的字符串。默认为 `''`。 |
| `chars` | `string` | 要修剪的字符。默认为空白字符。 |

### 返回值

(`string`): 返回修剪后的字符串。

### 示例

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'
```

---

## `trimEnd`

从字符串中移除尾随的空白或指定字符。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修剪的字符串。默认为 `''`。 |
| `chars` | `string` | 要修剪的字符。默认为空白字符。 |

### 返回值

(`string`): 返回修剪后的字符串。

### 示例

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

---

## `trimStart`

从字符串中移除前导的空白或指定字符。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修剪的字符串。默认为 `''`。 |
| `chars` | `string` | 要修剪的字符。默认为空白字符。 |

### 返回值

(`string`): 返回修剪后的字符串。

### 示例

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-' 
```

---

## `truncate`

如果字符串的长度超过给定的最大字符串长度，则截断该字符串。被截断字符串的最后几个字符将被替换为省略字符串。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要截断的字符串。默认为 `''`。 |
| `options` | `Object` | 包含截断选项的对象：`length` (number, 默认 30)，`omission` (string, 默认 '...')，`separator` (RegExp 或 string)。 |

### 返回值

(`string`): 返回截断后的字符串。

### 示例

```javascript
_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'
```

---

## `unescape`

`_.escape` 的逆操作；此方法将字符串中的 HTML 实体 `&amp;`、`&lt;`、`&gt;`、`&quot;` 和 `&#39;` 转换为其对应的字符。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要反转义的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回反转义后的字符串。

### 示例

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

---

## `upperCase`

将字符串（视为空格分隔的单词）转换为大写。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回大写字符串。

### 示例

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'
```

---

## `upperFirst`

将字符串的第一个字符转换为大写。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

### 返回值

(`string`): 返回转换后的字符串。

### 示例

```javascript
_.upperFirst('fred');
// => 'Fred'
```

---

## `words`

将字符串拆分为其单词数组。

### 参数

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要检查的字符串。默认为 `''`。 |
| `pattern`| `RegExp` \| `string` | 匹配单词的模式。 |

### 返回值

(`Array`): 返回字符串的单词。

### 示例

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

---

字符串 API 参考到此结束。有关其他实用函数，请参阅 [Util](./api-util.md) 部分。