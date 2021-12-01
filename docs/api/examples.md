# API Examples

Before using the API, please first [create an API key here](https://webhook.site/api-keys).

## cURL

### Quick upload file to Token

Uploads the file `example.png` from the current directory.

```bash
curl -F 'file=@example.png' https://webhook.site/00000000-0000-0000-0000-000000000000
```

To download the file, click the Download link in the Webhook.site interface, or via the API, use the [download endpoint](/api/tokens.html#download-request-file).

## PHP

### Create Token (URL/Email address)

Creates a Webhook.site Token and outputs its Web URL. You'll need to replace the API key.

```php
<?php
$apiKey = '00000000-0000-0000-0000-000000000000';

// Create a stream context
$context = stream_context_create(['http' => [
	'method' => 'POST',
	'header' => "Api-Key: $apiKey\r\n"
]]);

// Send API request
$response = json_decode(file_get_contents('https://webhook.site/token', false, $context), true);

echo "URL Created: https://webhook.site/{$response['uuid']}";
```

### Fetch latest data

Simple example of how to loop through the latest requests or emails sent to a Webhook.site URL or email and display in a friendly manner. 

You'll need to replace the API key and token ID. 

```php
<?php
$apiKey = '00000000-0000-0000-0000-000000000000';
$tokenId = '00000000-0000-0000-0000-000000000000';

$url = "https://webhook.site/token/$tokenId/requests?sorting=newest";

$context = stream_context_create(['http' => ['header' => "Api-Key: $apiKey\r\n"]]);

$response = json_decode(file_get_contents($url, false, $context), true);

foreach ($response['data'] as $req) {
	echo "\n";
	echo "ID        : {$req['uuid']}\n";
	echo "Type      : {$req['type']}\n";
	echo "Date      : {$req['created_at']}\n";
	echo "User-Agent: {$req['headers']['user-agent'][0] ?? 'Unknown'}\n";
	echo "--- content begin ---\n";
	echo $req['content'];
	echo "\n--- content end ---\n";
}

```

Example output after running e.g. `curl -X POST https://webhook.site/00000000-0000-0000-0000-000000000000 -d "Hello world"`:

```text
ID        : 58980c49-7e09-4cd8-8d64-bbfcfc38a1c5
Type      : web
Date      : 2021-12-01 19:24:10
User-Agent: Paw/3.3.1 (Macintosh; OS X/11.6.0) GCDHTTPRequest
--- content begin ---
Hello world!
--- content end ---
```

## Python

### Create Token (URL/Email address)

Requires the `requests` module, which can be installed using `pip install requests`. 

You'll also need to replace the API key. 

```python
import requests

json = {
  "default_status": 200,
  "default_content": "Hello world!",
  "default_content_type": "text/html",
}

headers = {
    "api-key": "00000000-0000-0000-0000-000000000000"
}

r = requests.post('https://webhook.site/token', json=json, headers=headers)

print('URL Created: https://webhook.site/' + r.json()['uuid'])
```