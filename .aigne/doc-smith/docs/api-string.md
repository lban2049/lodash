# String

Lodash provides a robust suite of functions designed for powerful and flexible string manipulation and inspection. These utilities simplify common tasks such as case conversion, trimming, padding, and creating templates. They are optimized for performance and handle edge cases gracefully, making string manipulation in JavaScript more predictable and declarative.

For an overview of all available function categories, please refer to the main [API Reference](./api.md).

## _.camelCase

Converts a string to [camel case](https://en.wikipedia.org/wiki/CamelCase).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the camel-cased string.

### Example

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

Converts the first character of a string to upper case and the remaining to lower case.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to capitalize. |

### Returns

`(string)`: Returns the capitalized string.

### Example

```javascript icon=logos:javascript
_.capitalize('FRED');
// => 'Fred'
```

---

## _.deburr

Deburrs a string by converting [Latin-1 Supplement](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) and [Latin Extended-A](https://en.wikipedia.org/wiki/Latin_Extended-A) letters to basic Latin letters and removing [combining diacritical marks](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to deburr. |

### Returns

`(string)`: Returns the deburred string.

### Example

```javascript icon=logos:javascript
_.deburr('déjà vu');
// => 'deja vu'
```

---

## _.endsWith

Checks if a string ends with the given target string.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to inspect. |
| `[target]` | `string` | The string to search for. |
| `[position=string.length]` | `number` | The position to search up to. |

### Returns

`(boolean)`: Returns `true` if the string ends with the target, else `false`.

### Example

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

Converts the characters `&`, `<`, `>`, `"`, and `'` in a string to their corresponding HTML entities.

**Note:** No other characters are escaped. For more comprehensive escaping, consider a third-party library like [_he_](https://mths.be/he).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to escape. |

### Returns

`(string)`: Returns the escaped string.

### Example

```javascript icon=logos:javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

---

## _.escapeRegExp

Escapes the `RegExp` special characters `^`, `$`, `\`, `.`, `*`, `+`, `?`, `(`, `)`, `[`, `]`, `{`, `}`, and `|` in a string.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to escape. |

### Returns

`(string)`: Returns the escaped string.

### Example

```javascript icon=logos:javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

---

## _.kebabCase

Converts a string to [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the kebab-cased string.

### Example

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

Converts a string, as space-separated words, to lower case.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the lower-cased string.

### Example

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

Converts the first character of a string to lower case.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the converted string.

### Example

```javascript icon=logos:javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

---

## _.pad

Pads a string on the left and right sides if it's shorter than `length`. Padding characters are truncated if they can't be evenly divided by `length`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to pad. |
| `[length=0]` | `number` | The padding length. |
| `[chars=' ']` | `string` | The string used as padding. |

### Returns

`(string)`: Returns the padded string.

### Example

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

Pads a string on the right side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to pad. |
| `[length=0]` | `number` | The padding length. |
| `[chars=' ']` | `string` | The string used as padding. |

### Returns

`(string)`: Returns the padded string.

### Example

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

Pads a string on the left side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to pad. |
| `[length=0]` | `number` | The padding length. |
| `[chars=' ']` | `string` | The string used as padding. |

### Returns

`(string)`: Returns the padded string.

### Example

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

Converts a string to an integer of the specified radix. If `radix` is `undefined` or `0`, a `radix` of `10` is used unless the value is a hexadecimal, in which case a `radix` of `16` is used.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `string` | `string` | The string to convert. |
| `[radix=10]` | `number` | The radix to interpret `value` by. |

### Returns

`(number)`: Returns the converted integer.

### Example

```javascript icon=logos:javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

---

## _.repeat

Repeats the given string `n` times.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to repeat. |
| `[n=1]` | `number` | The number of times to repeat the string. |

### Returns

`(string)`: Returns the repeated string.

### Example

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

Replaces matches for `pattern` in a string with `replacement`. This method is based on [`String#replace`](https://mdn.io/String/replace).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to modify. |
| `pattern` | `RegExp` \| `string` | The pattern to replace. |
| `replacement` | `Function` \| `string` | The match replacement. |

### Returns

`(string)`: Returns the modified string.

### Example

```javascript icon=logos:javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

---

## _.snakeCase

Converts a string to [snake case](https://en.wikipedia.org/wiki/Snake_case).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the snake-cased string.

### Example

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

Splits a string by `separator`. This method is based on [`String#split`](https://mdn.io/String/split).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to split. |
| `separator` | `RegExp` \| `string` | The separator pattern to split by. |
| `[limit]` | `number` | The length to truncate results to. |

### Returns

`(Array)`: Returns the string segments.

### Example

```javascript icon=logos:javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

---

## _.startCase

Converts a string to [start case](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage).

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the start-cased string.

### Example

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

Checks if a string starts with the given target string.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to inspect. |
| `[target]` | `string` | The string to search for. |
| `[position=0]` | `number` | The position to search from. |

### Returns

`(boolean)`: Returns `true` if the string starts with the target, else `false`.

### Example

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

Creates a compiled template function that can interpolate data properties in "interpolate" delimiters, HTML-escape values in "escape" delimiters, and execute JavaScript in "evaluate" delimiters. Data properties are accessible as free variables within the template.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The template string. |
| `[options={}]` | `Object` | The options object. |

### Returns

`(Function)`: Returns the compiled template function.

### Examples

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

Converts a string, as a whole, to lower case, similar to `String#toLowerCase`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the lower-cased string.

### Example

```javascript icon=logos:javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'
```

---

## _.toUpper

Converts a string, as a whole, to upper case, similar to `String#toUpperCase`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the upper-cased string.

### Example

```javascript icon=logos:javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'
```

---

## _.trim

Removes leading and trailing whitespace or specified characters from a string.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to trim. |
| `[chars=whitespace]` | `string` | The characters to trim. |

### Returns

`(string)`: Returns the trimmed string.

### Example

```javascript icon=logos:javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'
```

---

## _.trimEnd

Removes trailing whitespace or specified characters from a string.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to trim. |
| `[chars=whitespace]` | `string` | The characters to trim. |

### Returns

`(string)`: Returns the trimmed string.

### Example

```javascript icon=logos:javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

---

## _.trimStart

Removes leading whitespace or specified characters from a string.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to trim. |
| `[chars=whitespace]` | `string` | The characters to trim. |

### Returns

`(string)`: Returns the trimmed string.

### Example

```javascript icon=logos:javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-' 
```

---

## _.truncate

Truncates a string if it's longer than the given maximum string length. The last characters of the truncated string are replaced with an omission string which defaults to `...`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to truncate. |
| `[options={}]` | `Object` | The options object. |
| `[options.length=30]`| `number`| The maximum string length.|
| `[options.omission='...']`| `string`| The string to indicate text is omitted.|
| `[options.separator]`| `RegExp`\|`string`| The separator pattern to truncate to.|

### Returns

`(string)`: Returns the truncated string.

### Example

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

The inverse of `_.escape`; this method converts the HTML entities `&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&#39;` in a string to their corresponding characters.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to unescape. |

### Returns

`(string)`: Returns the unescaped string.

### Example

```javascript icon=logos:javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

---

## _.upperCase

Converts a string, as space-separated words, to upper case.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the upper-cased string.

### Example

```javascript icon=logos:javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'
```

---

## _.upperFirst

Converts the first character of a string to upper case.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to convert. |

### Returns

`(string)`: Returns the converted string.

### Example

```javascript icon=logos:javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

---

## _.words

Splits a string into an array of its words.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `[string='']` | `string` | The string to inspect. |
| `[pattern]` | `RegExp` \| `string` | The pattern to match words. |

### Returns

`(Array)`: Returns the words of the string.

### Example

```javascript icon=logos:javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

## Next Steps

Now that you've explored the string manipulation functions, you might be interested in other utility functions that can help with your development workflow.

<x-card data-title="Util API" data-icon="lucide:wrench" data-href="/api/util">
Explore miscellaneous utility functions, including function composition, iteration, and unique ID generation.
</x-card>