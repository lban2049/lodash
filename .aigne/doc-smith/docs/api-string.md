# String

This section provides a detailed reference for all Lodash functions designed for string manipulation and inspection. These utilities help with common tasks like changing case, trimming, padding, and creating templates.

For other utility functions, you might find the [Util](./api-util.md) and [Lang](./api-lang.md) sections helpful.

---

### camelCase

Converts a string to [camel case](https://en.wikipedia.org/wiki/CamelCase).

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The camel-cased string.

**Example**

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

Converts the first character of a string to upper case and the remaining to lower case.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to capitalize. Defaults to `''`. |

**Returns**

- `(string)`: The capitalized string.

**Example**

```javascript
_.capitalize('FRED');
// => 'Fred'
```

---

### deburr

Deburrs a string by converting [Latin-1 Supplement](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) and [Latin Extended-A](https://en.wikipedia.org/wiki/Latin_Extended-A) letters to basic Latin letters and removing [combining diacritical marks](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks).

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to deburr. Defaults to `''`. |

**Returns**

- `(string)`: The deburred string.

**Example**

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

---

### endsWith

Checks if a string ends with the given target string.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to inspect. Defaults to `''`. |
| `target` | `string` | The string to search for. |
| `position` | `number` | The position to search up to. Defaults to `string.length`. |

**Returns**

- `(boolean)`: Returns `true` if `string` ends with `target`, else `false`.

**Example**

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

Converts the characters `&`, `<`, `>`, `"`, and `'` in a string to their corresponding HTML entities.

**Since**: 0.1.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to escape. Defaults to `''`. |

**Returns**

- `(string)`: The escaped string.

**Example**

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

---

### escapeRegExp

Escapes the RegExp special characters `^`, `$`, `\`, `.`, `*`, `+`, `?`, `(`, `)`, `[`, `]`, `{`, `}`, and `|` in a string.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to escape. Defaults to `''`. |

**Returns**

- `(string)`: The escaped string.

**Example**

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

---

### kebabCase

Converts a string to [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The kebab-cased string.

**Example**

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

Converts a string, as space-separated words, to lower case.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The lower-cased string.

**Example**

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

Converts the first character of a string to lower case.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The converted string.

**Example**

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

---

### pad

Pads a string on the left and right sides if it's shorter than `length`. Padding characters are truncated if they can't be evenly divided by `length`.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to pad. Defaults to `''`. |
| `length` | `number` | The padding length. Defaults to `0`. |
| `chars` | `string` | The string used as padding. Defaults to `' '`. |

**Returns**

- `(string)`: The padded string.

**Example**

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

Pads a string on the right side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to pad. Defaults to `''`. |
| `length` | `number` | The padding length. Defaults to `0`. |
| `chars` | `string` | The string used as padding. Defaults to `' '`. |

**Returns**

- `(string)`: The padded string.

**Example**

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

Pads a string on the left side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to pad. Defaults to `''`. |
| `length` | `number` | The padding length. Defaults to `0`. |
| `chars` | `string` | The string used as padding. Defaults to `' '`. |

**Returns**

- `(string)`: The padded string.

**Example**

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

Converts a string to an integer of the specified radix. If `radix` is `undefined` or `0`, a `radix` of `10` is used unless `value` is a hexadecimal, in which case a `radix` of `16` is used.

**Since**: 1.1.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. |
| `radix` | `number` | The radix to interpret `value` by. Defaults to `10`. |

**Returns**

- `(number)`: The converted integer.

**Example**

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

---

### repeat

Repeats the given string `n` times.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to repeat. Defaults to `''`. |
| `n` | `number` | The number of times to repeat the string. Defaults to `1`. |

**Returns**

- `(string)`: The repeated string.

**Example**

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

Replaces matches for `pattern` in `string` with `replacement`. This method is based on [`String#replace`](https://mdn.io/String/replace).

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to modify. Defaults to `''`. |
| `pattern` | `RegExp` \| `string` | The pattern to replace. |
| `replacement` | `Function` \| `string` | The match replacement. |

**Returns**

- `(string)`: The modified string.

**Example**

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

---

### snakeCase

Converts a string to [snake case](https://en.wikipedia.org/wiki/Snake_case).

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The snake-cased string.

**Example**

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

Splits `string` by `separator`. This method is based on [`String#split`](https://mdn.io/String/split).

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to split. Defaults to `''`. |
| `separator` | `RegExp` \| `string` | The separator pattern to split by. |
| `limit` | `number` | The length to truncate results to. |

**Returns**

- `(Array)`: The string segments.

**Example**

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

---

### startCase

Converts a string to [start case](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage).

**Since**: 3.1.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The start-cased string.

**Example**

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

Checks if a string starts with the given target string.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to inspect. Defaults to `''`. |
| `target` | `string` | The string to search for. |
| `position` | `number` | The position to search from. Defaults to `0`. |

**Returns**

- `(boolean)`: Returns `true` if `string` starts with `target`, else `false`.

**Example**

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

Creates a compiled template function that can interpolate data properties in "interpolate" delimiters, HTML-escape values in "escape" delimiters, and execute JavaScript in "evaluate" delimiters. Data properties may be accessed as free variables in the template.

**Since**: 0.1.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The template string. Defaults to `''`. |
| `options` | `Object` | The options object. |

**Options**

| Name | Type | Description |
|---|---|---|
| `escape` | `RegExp` | The HTML "escape" delimiter. |
| `evaluate` | `RegExp` | The "evaluate" delimiter. |
| `imports` | `Object` | An object to import into the template as free variables. |
| `interpolate` | `RegExp` | The "interpolate" delimiter. |
| `sourceURL` | `string` | The sourceURL of the compiled template. |
| `variable` | `string` | The data object variable name. |

**Returns**

- `(Function)`: The compiled template function.

**Example**

```javascript
// Use the "interpolate" delimiter to create a compiled template.
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// Use the HTML "escape" delimiter to escape data property values.
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'

// Use the "evaluate" delimiter to execute JavaScript and generate HTML.
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
```

---

### toLower

Converts a string, as a whole, to lower case, similar to `String#toLowerCase`.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The lower-cased string.

**Example**

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'
```

---

### toUpper

Converts a string, as a whole, to upper case, similar to `String#toUpperCase`.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The upper-cased string.

**Example**

```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'
```

---

### trim

Removes leading and trailing whitespace or specified characters from a string.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to trim. Defaults to `''`. |
| `chars` | `string` | The characters to trim. Defaults to whitespace. |

**Returns**

- `(string)`: The trimmed string.

**Example**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'
```

---

### trimEnd

Removes trailing whitespace or specified characters from a string.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to trim. Defaults to `''`. |
| `chars` | `string` | The characters to trim. Defaults to whitespace. |

**Returns**

- `(string)`: The trimmed string.

**Example**

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

---

### trimStart

Removes leading whitespace or specified characters from a string.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to trim. Defaults to `''`. |
| `chars` | `string` | The characters to trim. Defaults to whitespace. |

**Returns**

- `(string)`: The trimmed string.

**Example**

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-' 
```

---

### truncate

Truncates a string if it's longer than the given maximum string length. The last characters of the truncated string are replaced with an omission string which defaults to "...".

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to truncate. Defaults to `''`. |
| `options` | `Object` | The options object. |

**Options**

| Name | Type | Description |
|---|---|---|
| `length` | `number` | The maximum string length. Defaults to `30`. |
| `omission` | `string` | The string to indicate text is omitted. Defaults to `'...'`. |
| `separator` | `RegExp` \| `string` | The separator pattern to truncate to. |

**Returns**

- `(string)`: The truncated string.

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

---

### unescape

The inverse of `_.escape`; this method converts the HTML entities `&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&#39;` in a string to their corresponding characters.

**Since**: 0.6.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to unescape. Defaults to `''`. |

**Returns**

- `(string)`: The unescaped string.

**Example**

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

---

### upperCase

Converts a string, as space-separated words, to upper case.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The upper-cased string.

**Example**

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'
```

---

### upperFirst

Converts the first character of a string to upper case.

**Since**: 4.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. Defaults to `''`. |

**Returns**

- `(string)`: The converted string.

**Example**

```javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

---

### words

Splits a string into an array of its words.

**Since**: 3.0.0

**Parameters**

| Name | Type | Description |
|---|---|---|
| `string` | `string` | The string to inspect. Defaults to `''`. |
| `pattern` | `RegExp` \| `string` | The pattern to match words. |

**Returns**

- `(Array)`: The words of the string.

**Example**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```
