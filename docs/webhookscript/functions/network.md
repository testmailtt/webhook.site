## HTTP

### query(***array*** form_values) : string

Converts an associative array into a form-style string, used for e.g. `application/x-www-form-urlencoded` requests or HTTP query strings.

```javascript
query(['country': 'Curaçao', 'population': 158665]) 
// country=Cura%C3%A7ao&population=158665
```

### request(***string*** url, ***string*** body, ***string*** method = 'GET', ***array*** headers, ***bool*** override = false) : array

Sends a HTTP request and returns an array with the following keys containing response data:

* `content`
* `status`
* `headers`
* `url`

The headers should be an array of strings, for example:

```javascript
[
  'Content-Type: application/json',
  'Accept: application/json, text/plain, */*'
]
```

To get a JSON document, validate if valid JSON, and get a property:

```javascript
response = request('https://example.com')

decoded = json_decode(response['content'])
if (decoded) {
  value = decoded['value']
}
```

If `override` is set to true, none of the content from the original request is included (e.g. query strings, headers, content.)

### url_decode(***string*** value) : string

Returns an URL-decoded version of *value*.

### url_encode(***string*** value) : string

Returns an URL-encoded version of *value*.

```javascript
url_encode('here\'s a value') // here%27s+a+value
```