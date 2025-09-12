# 字符串

本节提供了所有用于字符串操作和检查的 Lodash 函数的详细参考。这些实用工具可帮助处理常见任务，例如大小写转换、修剪、填充、搜索和模板插值。

## _.camelCase

将 `string` 转换为[驼峰命名法](https://en.wikipedia.org/wiki/CamelCase)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回驼峰命名法格式的字符串。"></x-field>

**示例**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

## _.capitalize

将 `string` 的第一个字符转换为大写，其余字符转换为小写。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要首字母大写的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回首字母大写的字符串。"></x-field>

**示例**

```javascript
_.capitalize('FRED');
// => 'Fred'
```

## _.deburr

通过将 [Latin-1 Supplement](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) 和 [Latin Extended-A](https://en.wikipedia.org/wiki/Latin_Extended-A) 字母转换为基本的拉丁字母，并移除[组合附加符号](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks)，来去除 `string` 中的变音符号。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要去除变音符号的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回去除变音符号后的字符串。"></x-field>

**示例**

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

## _.endsWith

检查 `string` 是否以给定的目标字符串结尾。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要检查的字符串。"></x-field>
<x-field data-name="target" data-type="string" data-required="false" data-desc="要搜索的字符串。"></x-field>
<x-field data-name="position" data-type="number" data-default="string.length" data-required="false" data-desc="搜索的最大位置。"></x-field>

**返回**

<x-field data-name="" data-type="boolean" data-desc="如果字符串以目标字符串结尾，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

## _.escape

将 `string` 中的 "&"、"<"、">"、'"' 和 "'" 字符转换为其对应的 HTML 实体。

**注意：** 不会转义其他字符。如需更全面的转义，请考虑使用第三方库，例如 [_he_](https://mths.be/he)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转义的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回转义后的字符串。"></x-field>

**示例**

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

## _.escapeRegExp

转义 `string` 中 `RegExp` 的特殊字符 "^"、"$"、"\"、"."、"*"、"+"、"?"、"("、")"、"["、"]"、"{"、"}" 和 "|"。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转义的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回转义后的字符串。"></x-field>

**示例**

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

## _.kebabCase

将 `string` 转换为[短横线命名法](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回短横线命名法格式的字符串。"></x-field>

**示例**

```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

## _.lowerCase

将 `string` 转换为空格分隔的单词，并转换为小写。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回小写格式的字符串。"></x-field>

**示例**

```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

## _.lowerFirst

将 `string` 的第一个字符转换为小写。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回转换后的字符串。"></x-field>

**示例**

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

## _.pad

如果 `string` 的长度小于 `length`，则在左侧和右侧填充字符。如果填充字符无法被 `length` 整除，则会被截断。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要填充的字符串。"></x-field>
<x-field data-name="length" data-type="number" data-default="0" data-required="false" data-desc="填充长度。"></x-field>
<x-field data-name="chars" data-type="string" data-default="' '" data-required="false" data-desc="用作填充的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回填充后的字符串。"></x-field>

**示例**

```javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

## _.padEnd

如果 `string` 的长度小于 `length`，则在右侧填充字符。如果填充字符超出 `length`，则会被截断。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要填充的字符串。"></x-field>
<x-field data-name="length" data-type="number" data-default="0" data-required="false" data-desc="填充长度。"></x-field>
<x-field data-name="chars" data-type="string" data-default="' '" data-required="false" data-desc="用作填充的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回填充后的字符串。"></x-field>

**示例**

```javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

## _.padStart

如果 `string` 的长度小于 `length`，则在左侧填充字符。如果填充字符超出 `length`，则会被截断。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要填充的字符串。"></x-field>
<x-field data-name="length" data-type="number" data-default="0" data-required="false" data-desc="填充长度。"></x-field>
<x-field data-name="chars" data-type="string" data-default="' '" data-required="false" data-desc="用作填充的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回填充后的字符串。"></x-field>

**示例**

```javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

## _.parseInt

将 `string` 转换为指定基数的整数。如果 `radix` 是 `undefined` 或 `0`，则除非 `value` 是十六进制数，否则使用 `10` 作为 `radix`；如果是十六进制数，则使用 `16` 作为 `radix`。

**注意：** 此方法与 `parseInt` 的 [ES5 实现](https://es5.github.io/#x15.1.2.2)保持一致。

**参数**

<x-field data-name="string" data-type="string" data-required="true" data-desc="要转换的字符串。"></x-field>
<x-field data-name="radix" data-type="number" data-default="10" data-required="false" data-desc="用于解析 value 的基数。"></x-field>

**返回**

<x-field data-name="" data-type="number" data-desc="返回转换后的整数。"></x-field>

**示例**

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

## _.repeat

将给定的字符串重复 `n` 次。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要重复的字符串。"></x-field>
<x-field data-name="n" data-type="number" data-default="1" data-required="false" data-desc="重复字符串的次数。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回重复后的字符串。"></x-field>

**示例**

```javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

## _.replace

将 `string` 中匹配 `pattern` 的部分替换为 `replacement`。

**注意：** 此方法基于 [`String#replace`](https://mdn.io/String/replace)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要修改的字符串。"></x-field>
<x-field data-name="pattern" data-type="RegExp|string" data-required="true" data-desc="要替换的模式。"></x-field>
<x-field data-name="replacement" data-type="Function|string" data-required="true" data-desc="用于替换匹配项的内容。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回修改后的字符串。"></x-field>

**示例**

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

## _.snakeCase

将 `string` 转换为[蛇形命名法](https://en.wikipedia.org/wiki/Snake_case)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回蛇形命名法格式的字符串。"></x-field>

**示例**

```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

## _.split

通过 `separator` 分割 `string`。

**注意：** 此方法基于 [`String#split`](https://mdn.io/String/split)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要分割的字符串。"></x-field>
<x-field data-name="separator" data-type="RegExp|string" data-required="true" data-desc="用于分割的模式。"></x-field>
<x-field data-name="limit" data-type="number" data-required="false" data-desc="限制结果的长度。"></x-field>

**返回**

<x-field data-name="" data-type="Array" data-desc="返回字符串片段。"></x-field>

**示例**

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

## _.startCase

将 `string` 转换为[起始大写命名法](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage)。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回起始大写命名法格式的字符串。"></x-field>

**示例**

```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

## _.startsWith

检查 `string` 是否以给定的目标字符串开头。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要检查的字符串。"></x-field>
<x-field data-name="target" data-type="string" data-required="false" data-desc="要搜索的字符串。"></x-field>
<x-field data-name="position" data-type="number" data-default="0" data-required="false" data-desc="搜索的起始位置。"></x-field>

**返回**

<x-field data-name="" data-type="boolean" data-desc="如果字符串以目标字符串开头，则返回 true，否则返回 false。"></x-field>

**示例**

```javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

## _.template

创建一个已编译的模板函数，该函数可以插入“interpolate”分隔符中的数据属性，转义“escape”分隔符中的 HTML 数据，以及执行“evaluate”分隔符中的 JavaScript。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="模板字符串。"></x-field>
<x-field data-name="options" data-type="Object" data-default="{}" data-required="false" data-desc="选项对象。">
  <x-field data-name="escape" data-type="RegExp" data-desc="HTML 'escape' 分隔符。"></x-field>
  <x-field data-name="evaluate" data-type="RegExp" data-desc="'evaluate' 分隔符。"></x-field>
  <x-field data-name="imports" data-type="Object" data-desc="一个作为自由变量导入到模板中的对象。"></x-field>
  <x-field data-name="interpolate" data-type="RegExp" data-desc="'interpolate' 分隔符。"></x-field>
  <x-field data-name="sourceURL" data-type="string" data-desc="已编译模板的 sourceURL。"></x-field>
  <x-field data-name="variable" data-type="string" data-desc="数据对象的变量名。"></x-field>
</x-field>

**返回**

<x-field data-name="" data-type="Function" data-desc="返回已编译的模板函数。"></x-field>

**示例**

```javascript
// 使用 'interpolate' 分隔符创建一个已编译的模板。
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// 使用 HTML 'escape' 分隔符来转义数据属性值。
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'
```

## _.toLower

将整个 `string` 转换为小写，类似于 `String#toLowerCase`。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回小写格式的字符串。"></x-field>

**示例**

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'

_.toLower('__FOO_BAR__');
// => '__foo_bar__'
```

## _.toUpper

将整个 `string` 转换为大写，类似于 `String#toUpperCase`。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回大写格式的字符串。"></x-field>

**示例**

```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'

_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

## _.trim

移除 `string` 前后两端的空白字符或指定字符。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要修剪的字符串。"></x-field>
<x-field data-name="chars" data-type="string" data-default="whitespace" data-required="false" data-desc="要修剪的字符。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回修剪后的字符串。"></x-field>

**示例**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

## _.trimEnd

移除 `string` 尾部的空白字符或指定字符。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要修剪的字符串。"></x-field>
<x-field data-name="chars" data-type="string" data-default="whitespace" data-required="false" data-desc="要修剪的字符。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回修剪后的字符串。"></x-field>

**示例**

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

## _.trimStart

移除 `string` 头部的空白字符或指定字符。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要修剪的字符串。"></x-field>
<x-field data-name="chars" data-type="string" data-default="whitespace" data-required="false" data-desc="要修剪的字符。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回修剪后的字符串。"></x-field>

**示例**

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-'
```

## _.truncate

如果 `string` 的长度超过给定的最大字符串长度，则截断该字符串。被截断字符串的最后几个字符将替换为省略号字符串，默认为 "..."。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要截断的字符串。"></x-field>
<x-field data-name="options" data-type="Object" data-default="{}" data-required="false" data-desc="选项对象。">
  <x-field data-name="length" data-type="number" data-default="30" data-desc="最大字符串长度。"></x-field>
  <x-field data-name="omission" data-type="string" data-default="'...'" data-desc="表示文本被省略的字符串。"></x-field>
  <x-field data-name="separator" data-type="RegExp|string" data-desc="用于截断的模式。"></x-field>
</x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回截断后的字符串。"></x-field>

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

## _.unescape

`_.escape` 的逆操作；此方法将 `string` 中的 HTML 实体 `&amp;`、`&lt;`、`&gt;`、`&quot;` 和 `&#39;` 转换为其对应的字符。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要反转义的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回反转义后的字符串。"></x-field>

**示例**

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

## _.upperCase

将 `string` 转换为空格分隔的单词，并转换为大写。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回大写格式的字符串。"></x-field>

**示例**

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'

_.upperCase('__foo_bar__');
// => 'FOO BAR'
```

## _.upperFirst

将 `string` 的第一个字符转换为大写。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要转换的字符串。"></x-field>

**返回**

<x-field data-name="" data-type="string" data-desc="返回转换后的字符串。"></x-field>

**示例**

```javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

## _.words

将 `string` 分割成一个单词数组。

**参数**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="要检查的字符串。"></x-field>
<x-field data-name="pattern" data-type="RegExp|string" data-required="false" data-desc="匹配单词的模式。"></x-field>

**返回**

<x-field data-name="" data-type="Array" data-desc="返回字符串中的单词。"></x-field>

**示例**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```