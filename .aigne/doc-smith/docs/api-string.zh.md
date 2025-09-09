# 字符串

Lodash 提供了一套功能强大且灵活的函数，专为字符串操作和检查而设计。这些实用工具简化了大小写转换、修剪、填充和创建模板等常见任务。它们经过性能优化，能妥善处理边界情况，使 JavaScript 中的字符串操作更具可预测性和声明性。

有关所有可用函数类别的概览，请参阅主 [API 参考](./api.md)。

## _.camelCase

将字符串转换为[驼峰命名法](https://en.wikipedia.org/wiki/CamelCase)。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回驼峰命名法格式的字符串。

### 示例

```javascript icon=logos:javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

---

## _.capitalize

将字符串的第一个字符转换为大写，其余字符转换为小写。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要大写首字母的字符串。 |

### 返回

`(string)`: 返回首字母大写的字符串。

### 示例

```javascript icon=logos:javascript
_.capitalize('FRED');
// => 'Fred'
```

---

## _.deburr

通过将[拉丁语-1 补充](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table)和[拉丁语扩充-A](https://en.wikipedia.org/wiki/Latin_Extended-A)字母转换为基本拉丁字母并删除[组合音标](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks)来去除字符串中的变音符号。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要去除变音符号的字符串。 |

### 返回

`(string)`: 返回去除变音符号后的字符串。

### 示例

```javascript icon=logos:javascript
_.deburr('déjà vu');
// => 'deja vu'
```

---

## _.endsWith

检查字符串是否以给定的目标字符串结尾。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要检查的字符串。 |
| `[target]` | `string` | 要搜索的字符串。 |
| `[position=string.length]` | `number` | 搜索的截止位置。 |

### 返回

`(boolean)`: 如果字符串以目标字符串结尾，则返回 `true`，否则返回 `false`。

### 示例

```javascript icon=logos:javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

---

## _.escape

将字符串中的 `&`、`<`、`>`、`"` 和 `'` 字符转换为其对应的 HTML 实体。

**注意：** 不会转义其他字符。如需更全面的转义，请考虑使用像 [_he_](https://mths.be/he) 这样的第三方库。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转义的字符串。 |

### 返回

`(string)`: 返回转义后的字符串。

### 示例

```javascript icon=logos:javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

---

## _.escapeRegExp

转义字符串中的 `RegExp` 特殊字符 `^`、`$`、`\`、`.`、`*`、`+`、`?`、`(`、`)`、`[`、`]`、`{`、`}` 和 `|`。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转义的字符串。 |

### 返回

`(string)`: 返回转义后的字符串。

### 示例

```javascript icon=logos:javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

---

## _.kebabCase

将字符串转换为[短横线命名法](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles)。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回短横线命名法格式的字符串。

### 示例

```javascript icon=logos:javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

---

## _.lowerCase

将字符串转换为小写，单词之间用空格分隔。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回小写格式的字符串。

### 示例

```javascript icon=logos:javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

---

## _.lowerFirst

将字符串的第一个字符转换为小写。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回转换后的字符串。

### 示例

```javascript icon=logos:javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

---

## _.pad

如果字符串比 `length` 短，则在左右两侧填充字符串。如果填充字符不能被 `length` 整除，则会被截断。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要填充的字符串。 |
| `[length=0]` | `number` | 填充的长度。 |
| `[chars=' ']` | `string` | 用作填充的字符串。 |

### 返回

`(string)`: 返回填充后的字符串。

### 示例

```javascript icon=logos:javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

---

## _.padEnd

如果字符串比 `length` 短，则在右侧填充字符串。如果填充字符超出 `length`，则会被截断。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要填充的字符串。 |
| `[length=0]` | `number` | 填充的长度。 |
| `[chars=' ']` | `string` | 用作填充的字符串。 |

### 返回

`(string)`: 返回填充后的字符串。

### 示例

```javascript icon=logos:javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

---

## _.padStart

如果字符串比 `length` 短，则在左侧填充字符串。如果填充字符超出 `length`，则会被截断。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要填充的字符串。 |
| `[length=0]` | `number` | 填充的长度。 |
| `[chars=' ']` | `string` | 用作填充的字符串。 |

### 返回

`(string)`: 返回填充后的字符串。

### 示例

```javascript icon=logos:javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

---

## _.parseInt

将字符串转换为指定基数的整数。如果 `radix` 是 `undefined` 或 `0`，则使用 `10` 作为基数，除非值是十六进制数，此时使用 `16` 作为基数。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `string` | `string` | 要转换的字符串。 |
| `[radix=10]` | `number` | 用于解析 `value` 的基数。 |

### 返回

`(number)`: 返回转换后的整数。

### 示例

```javascript icon=logos:javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

---

## _.repeat

将给定的字符串重复 `n` 次。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要重复的字符串。 |
| `[n=1]` | `number` | 重复字符串的次数。 |

### 返回

`(string)`: 返回重复后的字符串。

### 示例

```javascript icon=logos:javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

---

## _.replace

用 `replacement` 替换字符串中与 `pattern` 匹配的部分。此方法基于 [`String#replace`](https://mdn.io/String/replace)。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要修改的字符串。 |
| `pattern` | `RegExp` \| `string` | 要替换的模式。 |
| `replacement` | `Function` \| `string` | 匹配项的替换内容。 |

### 返回

`(string)`: 返回修改后的字符串。

### 示例

```javascript icon=logos:javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

---

## _.snakeCase

将字符串转换为[蛇形命名法](https://en.wikipedia.org/wiki/Snake_case)。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回蛇形命名法格式的字符串。

### 示例

```javascript icon=logos:javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

---

## _.split

通过 `separator` 分割字符串。此方法基于 [`String#split`](https://mdn.io/String/split)。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要分割的字符串。 |
| `separator` | `RegExp` \| `string` | 用于分割的分隔符模式。 |
| `[limit]` | `number` | 截断结果的长度。 |

### 返回

`(Array)`: 返回字符串片段。

### 示例

```javascript icon=logos:javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

---

## _.startCase

将字符串转换为[首字母大写命名法](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage)。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回首字母大写命名法格式的字符串。

### 示例

```javascript icon=logos:javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

---

## _.startsWith

检查字符串是否以给定的目标字符串开头。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要检查的字符串。 |
| `[target]` | `string` | 要搜索的字符串。 |
| `[position=0]` | `number` | 开始搜索的位置。 |

### 返回

`(boolean)`: 如果字符串以目标字符串开头，则返回 `true`，否则返回 `false`。

### 示例

```javascript icon=logos:javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

---

## _.template

创建一个已编译的模板函数，该函数可以在“interpolate”分隔符中插入数据属性，在“escape”分隔符中对值进行 HTML 转义，并在“evaluate”分隔符中执行 JavaScript。数据属性在模板中可作为自由变量访问。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 模板字符串。 |
| `[options={}]` | `Object` | 选项对象。 |

### 返回

`(Function)`: 返回已编译的模板函数。

### 示例

```javascript Using the 'interpolate' delimiter icon=logos:javascript
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'
```

```javascript Using the HTML 'escape' delimiter icon=logos:javascript
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'
```

```javascript Using the 'evaluate' delimiter icon=logos:javascript
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
```

---

## _.toLower

将整个字符串转换为小写，类似于 `String#toLowerCase`。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回小写格式的字符串。

### 示例

```javascript icon=logos:javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'
```

---

## _.toUpper

将整个字符串转换为大写，类似于 `String#toUpperCase`。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回大写格式的字符串。

### 示例

```javascript icon=logos:javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'
```

---

## _.trim

从字符串中删除开头和结尾的空白字符或指定字符。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要修剪的字符串。 |
| `[chars=whitespace]` | `string` | 要修剪的字符。 |

### 返回

`(string)`: 返回修剪后的字符串。

### 示例

```javascript icon=logos:javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'
```

---

## _.trimEnd

从字符串中删除结尾的空白字符或指定字符。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要修剪的字符串。 |
| `[chars=whitespace]` | `string` | 要修剪的字符。 |

### 返回

`(string)`: 返回修剪后的字符串。

### 示例

```javascript icon=logos:javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

---

## _.trimStart

从字符串中删除开头的空白字符或指定字符。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要修剪的字符串。 |
| `[chars=whitespace]` | `string` | 要修剪的字符。 |

### 返回

`(string)`: 返回修剪后的字符串。

### 示例

```javascript icon=logos:javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-' 
```

---

## _.truncate

如果字符串的长度超过给定的最大字符串长度，则截断该字符串。被截断字符串的最后几个字符将被替换为省略字符串，默认为 `...`。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要截断的字符串。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.length=30]`| `number`| 最大字符串长度。|
| `[options.omission='...']`| `string`| 用于表示文本被省略的字符串。|
| `[options.separator]`| `RegExp`\|`string`| 用于截断的分隔符模式。|

### 返回

`(string)`: 返回截断后的字符串。

### 示例

```javascript icon=logos:javascript
_.truncate('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'

_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'
```

---

## _.unescape

`_.escape` 的逆操作；此方法将字符串中的 HTML 实体 `&amp;`、`&lt;`、`&gt;`、`&quot;` 和 `&#39;` 转换为其对应的字符。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要反转义的字符串。 |

### 返回

`(string)`: 返回反转义后的字符串。

### 示例

```javascript icon=logos:javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

---

## _.upperCase

将字符串转换为大写，单词之间用空格分隔。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回大写格式的字符串。

### 示例

```javascript icon=logos:javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'
```

---

## _.upperFirst

将字符串的第一个字符转换为大写。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要转换的字符串。 |

### 返回

`(string)`: 返回转换后的字符串。

### 示例

```javascript icon=logos:javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

---

## _.words

将字符串分割成其单词数组。

### 参数

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | 要检查的字符串。 |
| `[pattern]` | `RegExp` \| `string` | 用于匹配单词的模式。 |

### 返回

`(Array)`: 返回字符串的单词。

### 示例

```javascript icon=logos:javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

## 后续步骤

既然您已经了解了字符串操作函数，您可能对其他有助于您开发工作流程的实用函数感兴趣。

<x-card data-title="实用工具 API" data-icon="lucide:wrench" data-href="/api/util">
探索各种实用函数，包括函数组合、迭代和唯一 ID 生成。
</x-card>