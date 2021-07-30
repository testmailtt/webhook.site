## General string functions

### string_contains(***string*** subject, ***number/string/regex*** value) : bool

Returns boolean if ***subject*** contains ***value***

### string_find_first(***string*** subject, ***number/string*** value) : number

Returns position of ***value*** in ***subject***, or false if not found

### string_find_last(***string*** subject, ***number/string*** value) : number

Returns position of ***value*** in ***subject***, or false if not found

### string_format(***string*** formatString, ...***any*** items) : string

Sprintf-like formatting of formatString with ***items***, see PHP sprintf docs.

### string_join(***string*** subject, ***array*** items (number/string/bool/array)) : string

Joins items with string ***subject***

### string_length(***string*** string) : number

Returns length of string (multibyte-aware)

### string_lower(***string*** string) : string

Converts `string` to lowercase (multibyte-aware)

### string_number_of(***string*** string) : number

Returns number value of ***string***

### string_replace(***string*** subject, ***string*** search, ***string*** replace) : string

Replaces string ***search*** with ***replace*** found in ***subject***.

### string_reverse(***string*** subject) : string

Reverses string ***subject*** 

### string_slice(***string*** subject, ***number*** from, ***number*** to = null) : string

Extracts a segment of a string. Multibyte-aware.

`string_slice('hello world', 0, 5)` returns `hello`.

`string_slice('hello world', 6)` returns `world`.

### string_shuffle(***string*** string) : string

Returns string where the individual characters has been shuffled.

### string_split(***string*** subject, ***string/regex*** delimiter) : array

Returns array of split string ***subject*** with ***delimiter*** 

### string_title(***string*** string) : string

Returns `string` converted to *title case*.

`string_title('hello world')` returns `Hello World`.

### string_upper(***string*** string) : string

Converts `string` to UPPERCASE (multibyte-aware).

### to_regex(***string*** regex) : regex

Converts a regex string to a regex type

### to_string(***string/number/bool*** value) : string

Returns ***value*** as string 

### trim(***string*** string): string

Returns `string` with space, tab and newline characters removed from the beginning and end of the string.

## CSV

### csv_to_array(***string*** content, ***string*** delimiter, ***?int*** header_offset, ***string*** enclosure, ***string*** escape) : array

Takes a CSV string and outputs to an array, with each row being an item in the array.

* `content` should be a string containing the CSV document.
* `delimiter` will explicitly set the CSV delimiter the parser will attempt to use (e.g. `;`). Must be a single character. Defaults to `,` (comma.)
* `header_offset`, when specified, causes the output array item's keys to be set to the header values. Setting to `0` will mark the first row as the header row. 
* `enclosure` sets the field enclosure character. Must be a single character. Defaults to `"` (double quote.)
* `escape` sets the field escape character. Must be a single character. Defaults to `\` (backslash.)

```javascript
csv_content = 'firstname,lastname,title
"M. J.",Plumley,"Sr. Developer"
Emily,"Jenna Platt","Chief Information Officer"'

array = csv_to_array(csv_content, ',', 0)

echo(json_encode(array))

// [
//     {
//         "firstname": "John",
//         "lastname": "Doe",
//         "title": "Sr. Developer"
//     },
//     {
//         "firstname": "Emily",
//         "lastname": "Jenna Platt",
//         "title": "Chief Information Officer"
//     }
// ]
```

## Base64

### base64_decode(***string*** string) : string

Returns a base64-encoded string.

### base64_encode(***string*** string) : string

Returns decoded base64 string.

## Hashing

### hash(***string/number*** value, ***string*** algo) : string

Returns a hashed version of `value` using the `algo` algorithm.

```javscript
'hello world'.hash('md5')  // 5eb63bbbe01eeed093cb22bb8f5acdc3
```
<br>

The following built-in algorithms are available: `md2`, `md4`, `md5`, `sha1`, `sha224`, `sha256`, `sha384`, `sha512/224`, `sha512/256`, `sha512`, `sha3-224`, `sha3-256`, `sha3-384`, `sha3-512`, `ripemd128`, `ripemd160`, `ripemd256`, `ripemd320`, `whirlpool`, `tiger128,3`, `tiger160,3`, `tiger192,3`, `tiger128,4`, `tiger160,4`, `tiger192,4`, `snefru`, `snefru256`, `gost`, `gost-crypto`, `adler32`, `crc32`, `crc32b`, `fnv132`, `fnv1a32`, `fnv164`, `fnv1a64`, `joaat`, `haval128,3`, `haval160,3`, `haval192,3`, `haval224,3`, `haval256,3`, `haval128,4`, `haval160,4`, `haval192,4`, `haval224,4`, `haval256,4`, `haval128,5`, `haval160,5`, `haval192,5`, `haval224,5`, `haval256,5`.

### hmac(***string*** value, ***string*** algo, ***string*** secret) : string/false

Returns the hexadecimal hash if the authentication succeeds, and `false` if it doesn't.

For a list of possible values for `algo`, see `hash()` above.

## HTML and Markdown

### html_strip_tags(***string*** string) : string

Returns a string with all HTML tags removed.

`html_strip_tags('<b>test</b>')` returns `test`.

### html_decode(***string*** string) : string

Decodes all HTML entities (for example, `&nbsp;`) to normal characters.

### html_encode(***string*** string) : string

Replaces characters in a string with HTML encoded versions.

### markdown_to_html(***string*** string, ***bool*** safe_mode = false) : string

Converts a Markdown string to HTML.

`markdown_to_html('# Hello world')` returns `<h1>Hello world</h1>`.

If `safe_mode` is set to true, HTML tags are encoded.

## JSON

### json_decode(***string*** json) : array

Decodes `json` and returns an array

### json_encode(***array*** array) : string

Takes an array and encodes it as a JSON string

### json_path(***string*** json, ***string*** jsonpath, ***bool*** return_first = true) : string

Returns the result of a `json` string parsed using the [JSONPath](/custom-actions.html#extract-jsonpath) functionality.

Per default, if there's just one match (e.g. if matching on a property value that's a string), this value is returned. To always return an array, set `return_first` to false. 

```javascript
dump(json_path('{"v": []}', 'v[*]', false))
dump(json_path('{"v": []}', 'v[*]'))
// []
// ""
 
dump(json_path('{"v": ["item1"]}', 'v[*]', false))
dump(json_path('{"v": ["item1"]}', 'v[*]'))
// [0: "item1"]
// "item1"
 
dump(json_path('{"v": ["item1", "item2"]}', 'v[*]', false))
dump(json_path('{"v": ["item1", "item2"]}', 'v[*]'))
// [0: "item1", 1: "item2"]
// [0: "item1", 1: "item2"]
```

### json_escape(***string*** json) : string

JSON-escapes all special JSON characters like double quotes, newlines, etc.

## Regex

### regex_extract(***regex*** regex, ***string*** subject) : array/false

Returns the matching string and all match groups as an array, and `false` on failure.

```javascript
input = "You're a good bot"

output = regex_extract(r"You're (\w) (.*)", input)

dump(output) // [0: "You're a good bot", 1: "a", 2: "good bot"]
```

### regex_extract_first(***regex*** regex, ***string*** subject) : string/false

Returns the first match group of a regex, and `false` on failure.

```javascript
input = "You're a good bot"

output = regex_extract(r"You're (.*)", input)

dump(output) // "a good bot"
```

### regex_match(***regex*** regex, ***string*** subject) : string/false

Returns the first matching string, otherwise false.

```javascript
input = "You're a good bot"

output = regex_match(r"You're .*", input)

dump(output) // "You're a good bot"
```

### regex_to_string(***regex*** regex) : string

Returns the regex converted to a string

## XML XPath

### xpath(***string*** xpath, ***string*** input): string/null

Returns the first result of an XPath query on XML document `input`.

Given a request with the following content:

```
<?xml version="1.0"?>
<organization name="ExampleCo">
  <employees>
    <employee id="1">Jack</employee>
    <employee id="2">Ann</employee>
  </employees>
</organization>
```

* `xpath(var('$request.content$'), '//employee[1]') // returns "Jack"`
* `var('$request.content$').xpath('//employee[1]') // returns "Jack"`

[More information and examples regarding XPath](/custom-actions.html#extract-xpath).

### xpath_all(***string*** xpath, ***string*** input): string/null

Returns the results of an XPath query on XML document `input` as an array.

Given a request with the following content:

```
<?xml version="1.0"?>
<organization name="ExampleCo">
  <employees>
    <employee id="1">Jack</employee>
    <employee id="2">Ann</employee>
  </employees>
</organization>
```

* `xpath_all(var('$request.content$'), '//employee]') // returns [0: "Jack", 1: "Ann"]`
* `var('$request.content$').xpath('//employee') // returns [0: "Jack", 1: "Ann"]`

[More information and examples regarding XPath](/custom-actions.html#extract-xpath).

## Special string functions

### convert_kana(***string***, ***mode***) : string

Performs a "han-kaku" - "zen-kaku" conversion for string string. This function is only useful for Japanese. [See here](https://www.php.net/manual/en/function.mb-convert-kana.php) for more info.
