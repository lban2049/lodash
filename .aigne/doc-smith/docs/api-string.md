# String

This section details the functions in Lodash for string manipulation and inspection. These tools can help you easily handle common string tasks like case conversion, trimming, padding, truncating, and more. For functions that operate on other data types, please refer to our [API Reference](./api.md) home page.

## Function List

| Function | Description |
| --- | --- |
| [camelCase](#camelcase) | Converts string to camel case. |
| [capitalize](#capitalize) | Converts the first character of a string to upper case and the remaining to lower case. |
| [deburr](#deburr) | Deburrs a string by converting Latin-1 Supplement & Latin Extended-A letters to basic Latin letters and removing combining diacritical marks. |
| [endsWith](#endswith) | Checks if a string ends with the given target string. |
| [escape](#escape) | Converts the characters `&`, `<`, `>`, `"`, and `'` in a string to their corresponding HTML entities. |
| [escapeRegExp](#escaperegexp) | Escapes the `RegExp` special characters. |
| [kebabCase](#kebabcase) | Converts a string to kebab case. |
| [lowerCase](#lowercase) | Converts a string, as space-separated words, to lower case. |
| [lowerFirst](#lowerfirst) | Converts the first character of a string to lower case. |
| [pad](#pad) | Pads a string on the left and right sides if it's shorter than the specified length. |
| [padEnd](#padend) | Pads a string on the right side if it's shorter than the specified length. |
| [padStart](#padstart) | Pads a string on the left side if it's shorter than the specified length. |
| [parseInt](#parseint) | Converts a string to an integer of the specified radix. |
| [repeat](#repeat) | Repeats the given string `n` times. |
| [replace](#replace) | Replaces matches for `pattern` in a string. |
| [snakeCase](#snakecase) | Converts a string to snake case. |
| [split](#split) | Splits a string by `separator`. |
| [startCase](#startcase) | Converts a string to start case. |
| [startsWith](#startswith) | Checks if a string starts with the given target string. |
| [template](#template) | Creates a compiled template function. |
| [toLower](#tolower) | Converts the entire string to lower case. |
| [toUpper](#toupper) | Converts the entire string to upper case. |
| [trim](#trim) | Removes leading and trailing whitespace or specified characters from a string. |
| [trimEnd](#trimend) | Removes trailing whitespace or specified characters from a string. |
| [trimStart](#trimstart) | Removes leading whitespace or specified characters from a string. |
| [truncate](#truncate) | Truncates a string if it's longer than the given maximum length. |
| [unescape](#unescape) | The inverse of `_.escape`; converts HTML entities back to their corresponding characters. |
| [upperCase](#uppercase) | Converts a string, as space-separated words, to upper case. |
| [upperFirst](#upperfirst) | Converts the first character of a string to upper case. |
| [words](#words) | Splits a string into an array of its words. |

---

### camelCase

Converts a string to [camel case](https://en.wikipedia.org/wiki/CamelCase).

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the camel-cased string.

**Example**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

### capitalize

Converts the first character of a string to upper case and the remaining to lower case.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to capitalize. |

**Returns**

`(string)`: Returns the capitalized string.

**Example**

```javascript
_.capitalize('FRED');
// => 'Fred'
```

### deburr

Deburrs a string by converting [Latin-1 Supplement](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) and [Latin Extended-A](https://en.wikipedia.org/wiki/Latin_Extended-A) letters to basic Latin letters and removing [combining diacritical marks](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks).

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to deburr. |

**Returns**

`(string)`: Returns the deburred string.

**Example**

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

### endsWith

Checks if a string ends with the given target string.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to inspect. |
| `[target]` | `string` | The string to search for. |
| `[position=string.length]` | `number` | The position to search up to. |

**Returns**

`(boolean)`: Returns `true` if the string ends with `target`, else `false`.

**Example**

```javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

### escape

Converts the characters `&`, `<`, `>`, `"`, and `'` in a string to their corresponding HTML entities.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to escape. |

**Returns**

`(string)`: Returns the escaped HTML string.

**Example**

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

### escapeRegExp

Escapes the `RegExp` special characters `^`, `$`, `\`, `.`, `*`, `+`, `?`, `(`, `)`, `[`, `]`, `{`, `}`, and `|`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to escape. |

**Returns**

`(string)`: Returns the escaped RegExp string.

**Example**

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

### kebabCase

Converts a string to [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the kebab-cased string.

**Example**

```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

### lowerCase

Converts a string, as space-separated words, to lower case.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the lower-cased string.

**Example**

```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

### lowerFirst

Converts the first character of a string to lower case.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the converted string.

**Example**

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

### pad

Pads `string` on the left and right sides if it's shorter than `length`. Padding characters are truncated if they can't be evenly divided.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to pad. |
| `[length=0]` | `number` | The padding length. |
| `[chars=' ']` | `string` | The string used as padding. |

**Returns**

`(string)`: Returns the padded string.

**Example**

```javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

### padEnd

Pads `string` on the right side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to pad. |
| `[length=0]` | `number` | The padding length. |
| `[chars=' ']` | `string` | The string used as padding. |

**Returns**

`(string)`: Returns the padded string.

**Example**

```javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

### padStart

Pads `string` on the left side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to pad. |
| `[length=0]` | `number` | The padding length. |
| `[chars=' ']` | `string` | The string used as padding. |

**Returns**

`(string)`: Returns the padded string.

**Example**

```javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

### parseInt

Converts a string to an integer of the specified radix. If `radix` is `undefined` or `0`, `radix` defaults to `10` unless `value` is a hexadecimal string, in which case `radix` is `16`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `string` | `string` | The string to convert. |
| `[radix=10]` | `number` | The radix to interpret `value` by. |

**Returns**

`(number)`: Returns the converted integer.

**Example**

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

### repeat

Repeats the given string `n` times.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to repeat. |
| `[n=1]` | `number` | The number of times to repeat. |

**Returns**

`(string)`: Returns the repeated string.

**Example**

```javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

### replace

Replaces matches for `pattern` in a string with `replacement`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to modify. |
| `pattern` | `RegExp`\|`string` | The pattern to replace. |
| `replacement` | `Function`\|`string` | The replacement for matches. |

**Returns**

`(string)`: Returns the modified string.

**Example**

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

### snakeCase

Converts a string to [snake case](https://en.wikipedia.org/wiki/Snake_case).

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the snake-cased string.

**Example**

```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

### split

Splits a string by `separator`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to split. |
| `separator` | `RegExp`\|`string` | The separator pattern. |
| `[limit]` | `number` | The length to truncate results to. |

**Returns**

`(Array)`: Returns the array of string segments.

**Example**

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

### startCase

Converts a string to [start case](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage).

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the start-cased string.

**Example**

```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

### startsWith

Checks if a string starts with the given target string.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to inspect. |
| `[target]` | `string` | The string to search for. |
| `[position=0]` | `number` | The position to search from. |

**Returns**

`(boolean)`: Returns `true` if the string starts with `target`, else `false`.

**Example**

```javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

### template

Creates a compiled template function that can interpolate data properties. If an options object is provided, it will override `_.templateSettings`'s values.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The template string. |
| `[options={}]` | `Object` | The options object. |
| `[options.escape]` | `RegExp` | The HTML "escape" delimiter. |
| `[options.evaluate]` | `RegExp` | The "evaluate" delimiter. |
| `[options.imports]` | `Object` | An object of values to import into the template as free variables. |
| `[options.interpolate]` | `RegExp` | The "interpolate" delimiter. |
| `[options.sourceURL]` | `string` | The sourceURL of the compiled template. |
| `[options.variable]` | `string` | The data object variable name. |

**Returns**

`(Function)`: Returns the compiled template function.

**Example**

```javascript
// Use the "interpolate" delimiter to create a compiled template
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// Use the HTML "escape" delimiter to escape data property values
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// Use the "evaluate" delimiter to execute JavaScript and generate HTML
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
```

### toLower

Converts the entire string to lower case, similar to `String#toLowerCase`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the lower-cased string.

**Example**

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'

_.toLower('__FOO_BAR__');
// => '__foo_bar__'
```

### toUpper

Converts the entire string to upper case, similar to `String#toUpperCase`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the upper-cased string.

**Example**

```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'

_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

### trim

Removes leading and trailing whitespace or specified characters from a string.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to trim. |
| `[chars=whitespace]` | `string` | The characters to trim. |

**Returns**

`(string)`: Returns the trimmed string.

**Example**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

### trimEnd

Removes trailing whitespace or specified characters from a string.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to trim. |
| `[chars=whitespace]` | `string` | The characters to trim. |

**Returns**

`(string)`: Returns the trimmed string.

**Example**

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

### trimStart

Removes leading whitespace or specified characters from a string.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to trim. |
| `[chars=whitespace]` | `string` | The characters to trim. |

**Returns**

`(string)`: Returns the trimmed string.

**Example**

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-'
```

### truncate

Truncates a string if it's longer than the given maximum length. The last characters of the truncated string are replaced with an omission string, which defaults to `...`.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to truncate. |
| `[options={}]` | `Object` | The options object. |
| `[options.length=30]` | `number` | The maximum string length. |
| `[options.omission='...']` | `string` | The string to indicate text is omitted. |
| `[options.separator]` | `RegExp`\|`string` | The separator pattern to truncate to. |

**Returns**

`(string)`: Returns the truncated string.

**Example**

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

The inverse of `_.escape`. This method converts the HTML entities `&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&#39;` back to their corresponding characters.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to unescape. |

**Returns**

`(string)`: Returns the unescaped string.

**Example**

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

### upperCase

Converts a string, as space-separated words, to upper case.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the upper-cased string.

**Example**

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'

_.upperCase('__foo_bar__');
// => 'FOO BAR'
```

### upperFirst

Converts the first character of a string to upper case.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to convert. |

**Returns**

`(string)`: Returns the converted string.

**Example**

```javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

### words

Splits a string into an array of its words.

**Arguments**

| Argument | Type | Description |
| --- | --- | --- |
| `[string='']` | `string` | The string to inspect. |
| `[pattern]` | `RegExp`\|`string` | The pattern to match words. |

**Returns**

`(Array)`: Returns the array of words from the string.

**Example**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

The above is a detailed reference for all string-related functions in Lodash.
