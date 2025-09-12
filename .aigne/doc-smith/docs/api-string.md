# String

This section provides a detailed reference for all Lodash functions designed for string manipulation and inspection. These utilities help with common tasks like case conversion, trimming, padding, searching, and template interpolation.

## _.camelCase

Converts `string` to [camel case](https://en.wikipedia.org/wiki/CamelCase).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the camel cased string."></x-field>

**Example**

```javascript
_.camelCase('Foo Bar');
// => 'fooBar'

_.camelCase('--foo-bar--');
// => 'fooBar'

_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

## _.capitalize

Converts the first character of `string` to upper case and the remaining to lower case.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to capitalize."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the capitalized string."></x-field>

**Example**

```javascript
_.capitalize('FRED');
// => 'Fred'
```

## _.deburr

Deburrs `string` by converting [Latin-1 Supplement](https://en.wikipedia.org/wiki/Latin-1_Supplement_(Unicode_block)#Character_table) and [Latin Extended-A](https://en.wikipedia.org/wiki/Latin_Extended-A) letters to basic Latin letters and removing [combining diacritical marks](https://en.wikipedia.org/wiki/Combining_Diacritical_Marks).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to deburr."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the deburred string."></x-field>

**Example**

```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

## _.endsWith

Checks if `string` ends with the given target string.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to inspect."></x-field>
<x-field data-name="target" data-type="string" data-required="false" data-desc="The string to search for."></x-field>
<x-field data-name="position" data-type="number" data-default="string.length" data-required="false" data-desc="The position to search up to."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if string ends with target, else false."></x-field>

**Example**

```javascript
_.endsWith('abc', 'c');
// => true

_.endsWith('abc', 'b');
// => false

_.endsWith('abc', 'b', 2);
// => true
```

## _.escape

Converts the characters "&", "<", ">", '"', and "'" in `string` to their corresponding HTML entities.

**Note:** No other characters are escaped. For more comprehensive escaping, consider a third-party library like [_he_](https://mths.be/he).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to escape."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the escaped string."></x-field>

**Example**

```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

## _.escapeRegExp

Escapes the `RegExp` special characters "^", "$", "\", ".", "*", "+", "?", "(", ")", "[", "]", "{", "}", and "|" in `string`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to escape."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the escaped string."></x-field>

**Example**

```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

## _.kebabCase

Converts `string` to [kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the kebab cased string."></x-field>

**Example**

```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'

_.kebabCase('fooBar');
// => 'foo-bar'

_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

## _.lowerCase

Converts `string`, as space separated words, to lower case.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the lower cased string."></x-field>

**Example**

```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'

_.lowerCase('fooBar');
// => 'foo bar'

_.lowerCase('__FOO_BAR__');
// => 'foo bar'
```

## _.lowerFirst

Converts the first character of `string` to lower case.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the converted string."></x-field>

**Example**

```javascript
_.lowerFirst('Fred');
// => 'fred'

_.lowerFirst('FRED');
// => 'fRED'
```

## _.pad

Pads `string` on the left and right sides if it's shorter than `length`. Padding characters are truncated if they can't be evenly divided by `length`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to pad."></x-field>
<x-field data-name="length" data-type="number" data-default="0" data-required="false" data-desc="The padding length."></x-field>
<x-field data-name="chars" data-type="string" data-default="' '" data-required="false" data-desc="The string used as padding."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the padded string."></x-field>

**Example**

```javascript
_.pad('abc', 8);
// => '  abc   '

_.pad('abc', 8, '_-');
// => '_-abc_-_'

_.pad('abc', 3);
// => 'abc'
```

## _.padEnd

Pads `string` on the right side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to pad."></x-field>
<x-field data-name="length" data-type="number" data-default="0" data-required="false" data-desc="The padding length."></x-field>
<x-field data-name="chars" data-type="string" data-default="' '" data-required="false" data-desc="The string used as padding."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the padded string."></x-field>

**Example**

```javascript
_.padEnd('abc', 6);
// => 'abc   '

_.padEnd('abc', 6, '_-');
// => 'abc_-_'

_.padEnd('abc', 3);
// => 'abc'
```

## _.padStart

Pads `string` on the left side if it's shorter than `length`. Padding characters are truncated if they exceed `length`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to pad."></x-field>
<x-field data-name="length" data-type="number" data-default="0" data-required="false" data-desc="The padding length."></x-field>
<x-field data-name="chars" data-type="string" data-default="' '" data-required="false" data-desc="The string used as padding."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the padded string."></x-field>

**Example**

```javascript
_.padStart('abc', 6);
// => '   abc'

_.padStart('abc', 6, '_-');
// => '_-_abc'

_.padStart('abc', 3);
// => 'abc'
```

## _.parseInt

Converts `string` to an integer of the specified radix. If `radix` is `undefined` or `0`, a `radix` of `10` is used unless `value` is a hexadecimal, in which case a `radix` of `16` is used.

**Note:** This method aligns with the [ES5 implementation](https://es5.github.io/#x15.1.2.2) of `parseInt`.

**Parameters**

<x-field data-name="string" data-type="string" data-required="true" data-desc="The string to convert."></x-field>
<x-field data-name="radix" data-type="number" data-default="10" data-required="false" data-desc="The radix to interpret value by."></x-field>

**Returns**

<x-field data-name="" data-type="number" data-desc="Returns the converted integer."></x-field>

**Example**

```javascript
_.parseInt('08');
// => 8

_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

## _.repeat

Repeats the given string `n` times.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to repeat."></x-field>
<x-field data-name="n" data-type="number" data-default="1" data-required="false" data-desc="The number of times to repeat the string."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the repeated string."></x-field>

**Example**

```javascript
_.repeat('*', 3);
// => '***'

_.repeat('abc', 2);
// => 'abcabc'

_.repeat('abc', 0);
// => ''
```

## _.replace

Replaces matches for `pattern` in `string` with `replacement`.

**Note:** This method is based on [`String#replace`](https://mdn.io/String/replace).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to modify."></x-field>
<x-field data-name="pattern" data-type="RegExp|string" data-required="true" data-desc="The pattern to replace."></x-field>
<x-field data-name="replacement" data-type="Function|string" data-required="true" data-desc="The match replacement."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the modified string."></x-field>

**Example**

```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

## _.snakeCase

Converts `string` to [snake case](https://en.wikipedia.org/wiki/Snake_case).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the snake cased string."></x-field>

**Example**

```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'

_.snakeCase('fooBar');
// => 'foo_bar'

_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

## _.split

Splits `string` by `separator`.

**Note:** This method is based on [`String#split`](https://mdn.io/String/split).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to split."></x-field>
<x-field data-name="separator" data-type="RegExp|string" data-required="true" data-desc="The separator pattern to split by."></x-field>
<x-field data-name="limit" data-type="number" data-required="false" data-desc="The length to truncate results to."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the string segments."></x-field>

**Example**

```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

## _.startCase

Converts `string` to [start case](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage).

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the start cased string."></x-field>

**Example**

```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'

_.startCase('fooBar');
// => 'Foo Bar'

_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

## _.startsWith

Checks if `string` starts with the given target string.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to inspect."></x-field>
<x-field data-name="target" data-type="string" data-required="false" data-desc="The string to search for."></x-field>
<x-field data-name="position" data-type="number" data-default="0" data-required="false" data-desc="The position to search from."></x-field>

**Returns**

<x-field data-name="" data-type="boolean" data-desc="Returns true if string starts with target, else false."></x-field>

**Example**

```javascript
_.startsWith('abc', 'a');
// => true

_.startsWith('abc', 'b');
// => false

_.startsWith('abc', 'b', 1);
// => true
```

## _.template

Creates a compiled template function that can interpolate data properties in "interpolate" delimiters, HTML-escape data in "escape" delimiters, and execute JavaScript in "evaluate" delimiters.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The template string."></x-field>
<x-field data-name="options" data-type="Object" data-default="{}" data-required="false" data-desc="The options object.">
  <x-field data-name="escape" data-type="RegExp" data-desc="The HTML 'escape' delimiter."></x-field>
  <x-field data-name="evaluate" data-type="RegExp" data-desc="The 'evaluate' delimiter."></x-field>
  <x-field data-name="imports" data-type="Object" data-desc="An object to import into the template as free variables."></x-field>
  <x-field data-name="interpolate" data-type="RegExp" data-desc="The 'interpolate' delimiter."></x-field>
  <x-field data-name="sourceURL" data-type="string" data-desc="The sourceURL of the compiled template."></x-field>
  <x-field data-name="variable" data-type="string" data-desc="The data object variable name."></x-field>
</x-field>

**Returns**

<x-field data-name="" data-type="Function" data-desc="Returns the compiled template function."></x-field>

**Example**

```javascript
// Use the 'interpolate' delimiter to create a compiled template.
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'

// Use the HTML 'escape' delimiter to escape data property values.
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'
```

## _.toLower

Converts `string`, as a whole, to lower case, similar to `String#toLowerCase`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the lower cased string."></x-field>

**Example**

```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'

_.toLower('fooBar');
// => 'foobar'

_.toLower('__FOO_BAR__');
// => '__foo_bar__'
```

## _.toUpper

Converts `string`, as a whole, to upper case, similar to `String#toUpperCase`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the upper cased string."></x-field>

**Example**

```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'

_.toUpper('fooBar');
// => 'FOOBAR'

_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

## _.trim

Removes leading and trailing whitespace or specified characters from `string`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to trim."></x-field>
<x-field data-name="chars" data-type="string" data-default="whitespace" data-required="false" data-desc="The characters to trim."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the trimmed string."></x-field>

**Example**

```javascript
_.trim('  abc  ');
// => 'abc'

_.trim('-_-abc-_-', '_-');
// => 'abc'

_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

## _.trimEnd

Removes trailing whitespace or specified characters from `string`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to trim."></x-field>
<x-field data-name="chars" data-type="string" data-default="whitespace" data-required="false" data-desc="The characters to trim."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the trimmed string."></x-field>

**Example**

```javascript
_.trimEnd('  abc  ');
// => '  abc'

_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

## _.trimStart

Removes leading whitespace or specified characters from `string`.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to trim."></x-field>
<x-field data-name="chars" data-type="string" data-default="whitespace" data-required="false" data-desc="The characters to trim."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the trimmed string."></x-field>

**Example**

```javascript
_.trimStart('  abc  ');
// => 'abc  '

_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-'
```

## _.truncate

Truncates `string` if it's longer than the given maximum string length. The last characters of the truncated string are replaced with the omission string which defaults to "...".

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to truncate."></x-field>
<x-field data-name="options" data-type="Object" data-default="{}" data-required="false" data-desc="The options object.">
  <x-field data-name="length" data-type="number" data-default="30" data-desc="The maximum string length."></x-field>
  <x-field data-name="omission" data-type="string" data-default="'...'" data-desc="The string to indicate text is omitted."></x-field>
  <x-field data-name="separator" data-type="RegExp|string" data-desc="The separator pattern to truncate to."></x-field>
</x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the truncated string."></x-field>

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

## _.unescape

The inverse of `_.escape`; this method converts the HTML entities `&amp;`, `&lt;`, `&gt;`, `&quot;`, and `&#39;` in `string` to their corresponding characters.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to unescape."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the unescaped string."></x-field>

**Example**

```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

## _.upperCase

Converts `string`, as space separated words, to upper case.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the upper cased string."></x-field>

**Example**

```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'

_.upperCase('fooBar');
// => 'FOO BAR'

_.upperCase('__foo_bar__');
// => 'FOO BAR'
```

## _.upperFirst

Converts the first character of `string` to upper case.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to convert."></x-field>

**Returns**

<x-field data-name="" data-type="string" data-desc="Returns the converted string."></x-field>

**Example**

```javascript
_.upperFirst('fred');
// => 'Fred'

_.upperFirst('FRED');
// => 'FRED'
```

## _.words

Splits `string` into an array of its words.

**Parameters**

<x-field data-name="string" data-type="string" data-default="''" data-required="false" data-desc="The string to inspect."></x-field>
<x-field data-name="pattern" data-type="RegExp|string" data-required="false" data-desc="The pattern to match words."></x-field>

**Returns**

<x-field data-name="" data-type="Array" data-desc="Returns the words of string."></x-field>

**Example**

```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']

_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```