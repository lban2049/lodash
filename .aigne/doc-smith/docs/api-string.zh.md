# 字符串

本节提供了所有用于字符串操作和检查的 Lodash 函数的详细参考。这些实用工具可帮助完成常见任务，如大小写转换、修剪、填充和创建模板。

有关其他实用函数，你可能会发现 [Util](./api-util.md) 和 [Lang](./api-lang.md) 部分很有帮助。

---

### camelCase

将字符串转换为[驼峰命名法](https://en.wikipedia.org/wiki/CamelCase)。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 驼峰命名法格式的字符串。

**示例**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

---

### capitalize

将字符串的第一个字符转换为大写，其余字符转换为小写。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要首字母大写的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 首字母大写后的字符串。

**示例**

```javascript
_.capitalize('FRED');
// => 'Fred'
```

---

### deburr

通过将[拉丁语-1 补充](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table)和[拉丁语扩充-A](https://en.wikipedia.org/wiki/Latin_Extended-A)字母转换为基本拉丁字母并删除[组合音标符号](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks)来去除字符串中的毛刺。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要去毛刺的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 去毛刺后的字符串。

**示例**

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

---

### endsWith

检查字符串是否以给定的目标字符串结尾。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要检查的字符串。默认为 `''`。 |
| `target` | `string` | 要搜索的字符串。 |
| `position` | `number` | 搜索的位置上限。默认为 `string.length`。 |

**返回值**

- `(boolean)`: 如果 `string` 以 `target` 结尾，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

---

### escape

将字符串中的 `&`、`<`、`>`、`"` 和 `'` 字符转换为其对应的 HTML 实体。

**自**：0.1.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转义的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 转义后的字符串。

**示例**

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

---

### escapeRegExp

转义字符串中的 RegExp 特殊字符 `^`、`$`、`\`、`.`、`*`、`+`、`?`、`(`、`)`、`[`、`]`、`{`、`}` 和 `|`。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转义的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 转义后的字符串。

**示例**

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

---

### kebabCase

将字符串转换为[短横线命名法](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles)。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 短横线命名法格式的字符串。

**示例**

```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

---

### lowerCase

将字符串（视为空格分隔的单词）转换为小写。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 小写格式的字符串。

**示例**

```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

---

### lowerFirst

将字符串的第一个字符转换为小写。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 转换后的字符串。

**示例**

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

---

### pad

如果字符串短于 `length`，则在左右两侧填充字符串。如果填充字符不能被 `length` 整除，则会被截断。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要填充的字符串。默认为 `''`。 |
| `length` | `number` | 填充长度。默认为 `0`。 |
| `chars` | `string` | 用作填充的字符串。默认为 `' '`。 |

**返回值**

- `(string)`: 填充后的字符串。

**示例**

```javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

---

### padEnd

如果字符串短于 `length`，则在右侧填充字符串。如果填充字符超出 `length`，则会被截断。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要填充的字符串。默认为 `''`。 |
| `length` | `number` | 填充长度。默认为 `0`。 |
| `chars` | `string` | 用作填充的字符串。默认为 `' '`。 |

**返回值**

- `(string)`: 填充后的字符串。

**示例**

```javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

---

### padStart

如果字符串短于 `length`，则在左侧填充字符串。如果填充字符超出 `length`，则会被截断。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要填充的字符串。默认为 `''`。 |
| `length` | `number` | 填充长度。默认为 `0`。 |
| `chars` | `string` | 用作填充的字符串。默认为 `' '`。 |

**返回值**

- `(string)`: 填充后的字符串。

**示例**

```javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

---

### parseInt

将字符串转换为指定基数的整数。如果 `radix` 是 `undefined` 或 `0`，则使用 `10` 作为基数，除非 `value` 是十六进制数，此时使用 `16` 作为基数。

**自**：1.1.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。 |
| `radix` | `number` | 用于解析 `value` 的基数。默认为 `10`。 |

**返回值**

- `(number)`: 转换后的整数。

**示例**

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

---

### repeat

将给定的字符串重复 `n` 次。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要重复的字符串。默认为 `''`。 |
| `n` | `number` | 重复字符串的次数。默认为 `1`。 |

**返回值**

- `(string)`: 重复后的字符串。

**示例**

```javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

---

### replace

用 `replacement` 替换 `string` 中与 `pattern` 匹配的部分。此方法基于 [`String#replace`](https://mdn.io/String/replace)。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修改的字符串。默认为 `''`。 |
| `pattern` | `RegExp` \| `string` | 要替换的模式。 |
| `replacement` | `Function` \| `string` | 匹配项的替换内容。 |

**返回值**

- `(string)`: 修改后的字符串。

**示例**

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

---

### snakeCase

将字符串转换为[蛇形命名法](https://en.wikipedia.org/wiki/Snake_case)。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 蛇形命名法格式的字符串。

**示例**

```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

---

### split

通过 `separator` 分割 `string`。此方法基于 [`String#split`](https://mdn.io/String/split)。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要分割的字符串。默认为 `''`。 |
| `separator` | `RegExp` \| `string` | 用于分割的分隔符模式。 |
| `limit` | `number` | 截断结果的长度。 |

**返回值**

- `(Array)`: 字符串片段。

**示例**

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

---

### startCase

将字符串转换为[起始大写](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage)。

**自**：3.1.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 起始大写格式的字符串。

**示例**

```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

---

### startsWith

检查字符串是否以给定的目标字符串开头。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要检查的字符串。默认为 `''`。 |
| `target` | `string` | 要搜索的字符串。 |
| `position` | `number` | 搜索的起始位置。默认为 `0`。 |

**返回值**

- `(boolean)`: 如果 `string` 以 `target` 开头，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

---

### template

创建一个编译后的模板函数，该函数可以在“插值”分隔符中插入数据属性，在“转义”分隔符中对值进行 HTML 转义，并在“求值”分隔符中执行 JavaScript。数据属性可以在模板中作为自由变量访问。

**自**：0.1.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 模板字符串。默认为 `''`。 |
| `options` | `Object` | 选项对象。 |

**选项**

| 名称 | 类型 | 描述 |
|---|---|---|
| `escape` | `RegExp` | HTML“转义”分隔符。 |
| `evaluate` | `RegExp` | “求值”分隔符。 |
| `imports` | `Object` | 一个作为自由变量导入到模板中的对象。 |
| `interpolate` | `RegExp` | “插值”分隔符。 |
| `sourceURL` | `string` | 已编译模板的 sourceURL。 |
| `variable` | `string` | 数据对象的变量名。 |

**返回值**

- `(Function)`: 编译后的模板函数。

**示例**

```javascript
// 使用“插值”分隔符创建编译后的模板。
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// 使用 HTML“转义”分隔符来转义数据属性值。
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// 使用“求值”分隔符执行 JavaScript 并生成 HTML。
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
```

---

### toLower

将整个字符串转换为小写，类似于 `String#toLowerCase`。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 小写格式的字符串。

**示例**

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'
```

---

### toUpper

将整个字符串转换为大写，类似于 `String#toUpperCase`。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 大写格式的字符串。

**示例**

```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'
```

---

### trim

从字符串中移除前导和尾随的空白字符或指定字符。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修剪的字符串。默认为 `''`。 |
| `chars` | `string` | 要修剪的字符。默认为空白字符。 |

**返回值**

- `(string)`: 修剪后的字符串。

**示例**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'
```

---

### trimEnd

从字符串中移除尾随的空白字符或指定字符。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修剪的字符串。默认为 `''`。 |
| `chars` | `string` | 要修剪的字符。默认为空白字符。 |

**返回值**

- `(string)`: 修剪后的字符串。

**示例**

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

---

### trimStart

从字符串中移除前导的空白字符或指定字符。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要修剪的字符串。默认为 `''`。 |
| `chars` | `string` | 要修剪的字符。默认为空白字符。 |

**返回值**

- `(string)`: 修剪后的字符串。

**示例**

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-' 
```

---

### truncate

如果字符串的长度超过给定的最大字符串长度，则截断该字符串。被截断字符串的最后几个字符将被替换为省略字符串，默认为“...”。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要截断的字符串。默认为 `''`。 |
| `options` | `Object` | 选项对象。 |

**选项**

| 名称 | 类型 | 描述 |
|---|---|---|
| `length` | `number` | 最大字符串长度。默认为 `30`。 |
| `omission` | `string` | 用于表示文本被省略的字符串。默认为 `'...'`。 |
| `separator` | `RegExp` \| `string` | 用于截断的分隔符模式。 |

**返回值**

- `(string)`: 截断后的字符串。

**示例**

```javascript
_.truncate('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'

_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'
```

---

### unescape

`_.escape` 的反向操作；此方法将字符串中的 HTML 实体 `&amp;`、`&lt;`、`&gt;`、`&quot;` 和 `&#39;` 转换为其对应的字符。

**自**：0.6.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要反转义的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 反转义后的字符串。

**示例**

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

---

### upperCase

将字符串（视为空格分隔的单词）转换为大写。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 大写格式的字符串。

**示例**

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'
```

---

### upperFirst

将字符串的第一个字符转换为大写。

**自**：4.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要转换的字符串。默认为 `''`。 |

**返回值**

- `(string)`: 转换后的字符串。

**示例**

```javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

---

### words

将字符串分割成其单词组成的数组。

**自**：3.0.0

**参数**

| 名称 | 类型 | 描述 |
|---|---|---|
| `string` | `string` | 要检查的字符串。默认为 `''`。 |
| `pattern` | `RegExp` \| `string` | 用于匹配单词的模式。 |

**返回值**

- `(Array)`: 字符串中的单词。

**示例**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```
