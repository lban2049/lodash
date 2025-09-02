# String

本节详细介绍了 Lodash 中用于字符串操作和检查的函数。这些工具可以帮助您轻松处理大小写转换、修剪、填充、截断等常见的字符串任务。要了解其他数据类型的函数，请参阅我们的 [API 参考](./api.md) 主页。

## 函数列表

| 函数 | 描述 |
| --- | --- |
| [camelCase](#camelcase) | 将字符串转换为驼峰命名法。 |
| [capitalize](#capitalize) | 将字符串的第一个字符转换为大写，其余字符转换为小写。 |
| [deburr](#deburr) | 清除字符串中的毛刺，将拉丁字母补充-1和拉丁字母扩充-A的字母转换为基本的拉丁字母，并移除组合变音标记。 |
| [endsWith](#endswith) | 检查字符串是否以给定的目标字符串结尾。 |
| [escape](#escape) | 将字符串中的 `&`, `<`, `>`, `"`, 和 `'` 字符转换为其对应的HTML实体。 |
| [escapeRegExp](#escaperegexp) | 转义 `RegExp` 特殊字符。 |
| [kebabCase](#kebabcase) | 将字符串转换为短横线命名法。 |
| [lowerCase](#lowercase) | 将字符串（以空格分隔）转换为小写。 |
| [lowerFirst](#lowerfirst) | 将字符串的第一个字符转换为小写。 |
| [pad](#pad) | 如果字符串比指定的长度短，则在左侧和右侧填充字符。 |
| [padEnd](#padend) | 如果字符串比指定的长度短，则在右侧填充字符。 |
| [padStart](#padstart) | 如果字符串比指定的长度短，则在左侧填充字符。 |
| [parseInt](#parseint) | 将字符串转换为指定基数的整数。 |
| [repeat](#repeat) | 将给定的字符串重复 `n` 次。 |
| [replace](#replace) | 替换字符串中与 `pattern` 匹配的部分。 |
| [snakeCase](#snakecase) | 将字符串转换为蛇形命名法。 |
| [split](#split) | 根据 `separator` 拆分字符串。 |
| [startCase](#startcase) | 将字符串转换为首字母大写的单词。 |
| [startsWith](#startswith) | 检查字符串是否以给定的目标字符串开头。 |
| [template](#template) | 创建一个编译好的模板函数。 |
| [toLower](#tolower) | 将整个字符串转换为小写。 |
| [toUpper](#toupper) | 将整个字符串转换为大写。 |
| [trim](#trim) | 从字符串中移除前导和尾随的空白或指定字符。 |
| [trimEnd](#trimend) | 从字符串中移除尾随的空白或指定字符。 |
| [trimStart](#trimstart) | 从字符串中移除前导的空白或指定字符。 |
| [truncate](#truncate) | 如果字符串超过给定的最大长度，则截断字符串。 |
| [unescape](#unescape) | `_.escape` 的反向方法；将HTML实体转换回其对应的字符。 |
| [upperCase](#uppercase) | 将字符串（以空格分隔）转换为大写。 |
| [upperFirst](#upperfirst) | 将字符串的第一个字符转换为大写。 |
| [words](#words) | 将字符串拆分为一个单词数组。 |

---

### camelCase

将字符串转换为[驼峰命名法](https://en.wikipedia.org/wiki/CamelCase)。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回驼峰命名法的字符串。

**示例**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

### capitalize

将字符串的第一个字符转换为大写，其余字符转换为小写。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要大写的字符串。 |

**返回**

`(string)`: 返回大写化的字符串。

**示例**

```javascript
_.capitalize('FRED');
// => 'Fred'
```

### deburr

清除字符串中的毛刺，将[拉丁字母补充-1](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table)和[拉丁字母扩充-A](https://en.wikipedia.org/wiki/Latin_Extended-A)的字母转换为基本的拉丁字母，并移除[组合变音标记](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks)。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要清除毛刺的字符串。 |

**返回**

`(string)`: 返回清除毛刺后的字符串。

**示例**

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

### endsWith

检查字符串是否以给定的目标字符串结尾。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要检查的字符串。 |
| `[target]` | `string` | 要搜索的字符串。 |
| `[position=string.length]` | `number` | 搜索的位置。 |

**返回**

`(boolean)`: 如果字符串以 `target` 结尾，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

### escape

将字符串中的 `&`, `<`, `>`, `"`, 和 `'` 字符转换为其对应的HTML实体。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转义的字符串。 |

**返回**

`(string)`: 返回转义后的HTML字符串。

**示例**

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

### escapeRegExp

转义 `RegExp` 特殊字符 `^`, `$`, `\`, `.`, `*`, `+`, `?`, `(`, `)`, `[`, `]`, `{`, `}`, 和 `|`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转义的字符串。 |

**返回**

`(string)`: 返回转义后的正则表达式字符串。

**示例**

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

### kebabCase

将字符串转换为[短横线命名法](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles)。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回短横线命名法的字符串。

**示例**

```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

### lowerCase

将字符串（以空格分隔）转换为小写。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回小写的字符串。

**示例**

```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

### lowerFirst

将字符串的第一个字符转换为小写。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回转换后的字符串。

**示例**

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

### pad

如果字符串 `string` 比 `length` 短，则在左侧和右侧填充字符。如果无法平均分配，则截断填充字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要填充的字符串。 |
| `[length=0]` | `number` | 填充长度。 |
| `[chars=' ']` | `string` | 用于填充的字符串。 |

**返回**

`(string)`: 返回填充后的字符串。

**示例**

```javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

### padEnd

如果字符串 `string` 比 `length` 短，则在右侧填充字符。如果超出 `length`，则截断填充字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要填充的字符串。 |
| `[length=0]` | `number` | 填充长度。 |
| `[chars=' ']` | `string` | 用于填充的字符串。 |

**返回**

`(string)`: 返回填充后的字符串。

**示例**

```javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

### padStart

如果字符串 `string` 比 `length` 短，则在左侧填充字符。如果超出 `length`，则截断填充字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要填充的字符串。 |
| `[length=0]` | `number` | 填充长度。 |
| `[chars=' ']` | `string` | 用于填充的字符串。 |

**返回**

`(string)`: 返回填充后的字符串。

**示例**

```javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

### parseInt

将字符串转换为指定基数的整数。如果 `radix` 是 `undefined` 或 `0`，则 `radix` 默认为 `10`，除非 `value` 是十六进制字符串，此时 `radix` 为 `16`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `string` | `string` | 要转换的字符串。 |
| `[radix=10]` | `number` | 解释 `value` 的基数。 |

**返回**

`(number)`: 返回转换后的整数。

**示例**

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

### repeat

将给定的字符串重复 `n` 次。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要重复的字符串。 |
| `[n=1]` | `number` | 重复的次数。 |

**返回**

`(string)`: 返回重复后的字符串。

**示例**

```javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

### replace

替换字符串中与 `pattern` 匹配的部分为 `replacement`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要修改的字符串。 |
| `pattern` | `RegExp`\|`string` | 要替换的模式。 |
| `replacement` | `Function`\|`string` | 匹配项的替换内容。 |

**返回**

`(string)`: 返回修改后的字符串。

**示例**

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

### snakeCase

将字符串转换为[蛇形命名法](https://en.wikipedia.org/wiki/Snake_case)。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回蛇形命名法的字符串。

**示例**

```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

### split

根据 `separator` 拆分字符串。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要拆分的字符串。 |
| `separator` | `RegExp`\|`string` | 拆分的模式。 |
| `[limit]` | `number` | 截断结果的长度。 |

**返回**

`(Array)`: 返回字符串段的数组。

**示例**

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

### startCase

将字符串转换为[首字母大写的单词](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage)。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回首字母大写的字符串。

**示例**

```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

### startsWith

检查字符串是否以给定的目标字符串开头。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要检查的字符串。 |
| `[target]` | `string` | 要搜索的字符串。 |
| `[position=0]` | `number` | 搜索的起始位置。 |

**返回**

`(boolean)`: 如果字符串以 `target` 开头，则返回 `true`，否则返回 `false`。

**示例**

```javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

### template

创建一个编译好的模板函数，可以插入数据属性。如果提供了设置对象，它将优先于 `_.templateSettings` 的值。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 模板字符串。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.escape]` | `RegExp` | HTML“转义”分隔符。 |
| `[options.evaluate]` | `RegExp` | “求值”分隔符。 |
| `[options.imports]` | `Object` | 导入到模板中作为自由变量的对象。 |
| `[options.interpolate]` | `RegExp` | “插值”分隔符。 |
| `[options.sourceURL]` | `string` | 编译模板的 sourceURL。 |
| `[options.variable]` | `string` | 数据对象变量名。 |

**返回**

`(Function)`: 返回编译后的模板函数。

**示例**

```javascript
// 使用 "interpolate" 分隔符创建编译模板
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// 使用 HTML "escape" 分隔符转义数据属性值
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// 使用 "evaluate" 分隔符执行 JavaScript 并生成 HTML
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
```

### toLower

将整个字符串转换为小写，类似于 `String#toLowerCase`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回小写的字符串。

**示例**

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'

_.toLower('__FOO_BAR__');
// => '__foo_bar__'
```

### toUpper

将整个字符串转换为大写，类似于 `String#toUpperCase`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回大写的字符串。

**示例**

```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'

_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

### trim

从字符串中移除前导和尾随的空白或指定字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要修剪的字符串。 |
| `[chars=whitespace]` | `string` | 要修剪的字符。 |

**返回**

`(string)`: 返回修剪后的字符串。

**示例**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

### trimEnd

从字符串中移除尾随的空白或指定字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要修剪的字符串。 |
| `[chars=whitespace]` | `string` | 要修剪的字符。 |

**返回**

`(string)`: 返回修剪后的字符串。

**示例**

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

### trimStart

从字符串中移除前导的空白或指定字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要修剪的字符串。 |
| `[chars=whitespace]` | `string` | 要修剪的字符。 |

**返回**

`(string)`: 返回修剪后的字符串。

**示例**

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-'
```

### truncate

如果字符串超过给定的最大长度，则截断字符串。截断的字符串的最后几个字符将替换为省略号字符串，默认为 `...`。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要截断的字符串。 |
| `[options={}]` | `Object` | 选项对象。 |
| `[options.length=30]` | `number` | 最大字符串长度。 |
| `[options.omission='...']` | `string` | 表示文本被省略的字符串。 |
| `[options.separator]` | `RegExp`\|`string` | 用于截断的分隔符模式。 |

**返回**

`(string)`: 返回截断后的字符串。

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

### unescape

`_.escape` 的反向方法。此方法将HTML实体 `&amp;`, `&lt;`, `&gt;`, `&quot;`, 和 `&#39;` 转换回其对应的字符。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要反转义的字符串。 |

**返回**

`(string)`: 返回反转义后的字符串。

**示例**

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

### upperCase

将字符串（以空格分隔）转换为大写。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回大写的字符串。

**示例**

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'

_.upperCase('__foo_bar__');
// => 'FOO BAR'
```

### upperFirst

将字符串的第一个字符转换为大写。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要转换的字符串。 |

**返回**

`(string)`: 返回转换后的字符串。

**示例**

```javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

### words

将字符串拆分为一个单词数组。

**参数**

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `[string='']` | `string` | 要检查的字符串。 |
| `[pattern]` | `RegExp`\|`string` | 匹配单词的模式。 |

**返回**

`(Array)`: 返回字符串中的单词数组。

**示例**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

以上是 Lodash 中所有字符串相关函数的详细参考。