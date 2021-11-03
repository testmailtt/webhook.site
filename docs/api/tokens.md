---
title: Tokens (URLs & Email Addresses)
nav_order: 100
---

# API Endpoints:<br>Tokens (URLs & Email Addresses)

## Tokens

A **token** is a container for incoming requests and emails, and corresponds to a Webhook.site URL or Email. A **token ID** is a 36 character UUID consisting of hexadecimal characters and dashes.

Simply, the token ID is the part after `https://webhook.site/` in the URL, or before `@email.webhook.site` in the email address.


### Create token

**POST** `/token`

After creating a token, the URL at `https://webhook.site/{token.uuid}` becomes accessible, and emails can be sent to `{token.uuid}@email.webhook.site`.

* `default_*` parameters sets the response of the URL.
* `timeout` waits an amount of seconds before returning the response (intended for testing timeouts)
* `expiry` set to `true` will cause the token to automatically be deleted within 7 days of no activity, even if creating the token as a Pro user. If you're using tokens for automated testing, for example, you can enable this to avoid filling up your user profile.
* `cors` set to true will add CORS headers to the request so browsers will send cross-domain requests to the URL
* `alias` allows setting the alias of the token.
* `actions` specifies if Custom Actions are enabled and executed on every request/email (true), or disabled (false.)
* `clone_from` specifies a token UUID (or alias) that will act as a template for the new token. When specified, settingssuch as default content, timeout, password as well as Custom Actions are copied to the new token.

#### Request

##### Example 1: JSON

```json
{
  "default_status": 200,
  "default_content": "Hello world!",
  "default_content_type": "text/html",
  "timeout": 0,
  "cors": false,
  "expiry": true,
  "alias": "my-webhook",
  "actions": true
}
```

##### Example 2: Creating with Python 3

Requires the `requests` module, which can be installed using `pip install requests`.

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

#### Response

`200 OK`

```json
{
  "redirect": false,
  "alias": null,
  "timeout": 0,
  "premium": true,
  "uuid": "9981f9f4-657a-4ebf-be7c-1915bedd4775",
  "ip": "127.0.0.1",
  "user_agent": "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest",
  "default_content": "Hello world!",
  "default_status": 200,
  "default_content_type": "text\/plain",
  "premium_expires_at": "2019-10-22 10:52:20",
  "created_at": "2019-09-22 10:52:20",
  "updated_at": "2019-09-22 10:52:20"
}
```

Note about expiry: If there's no incoming requests for about a week, and the token is not upgraded to premium, the token is automatically deleted along with any other data.


### Get tokens

* Requires authentication.

#### Request

**GET** `/token`

Returns a list of all Tokens associated with an account.

##### Query string parameters

* `per_page` - amount of requests returned, defaults to 50 (max 100)
* `page` -  page number to retrieve (default 1)

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "uuid": "44fb1548-cd1f-4928-880c-cce094e5e179",
      "redirect": false,
      "alias": null,
      "actions": true,
      "cors": false,
      "expiry": false,
      "timeout": 0,
      "premium": true,
      "user_id": null,
      "password": true,
      "ip": "127.0.0.1",
      "user_agent": "Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit\/605.1.15 (KHTML, like Gecko) Version\/14.0.3 Safari\/605.1.15",
      "default_content": "",
      "default_status": 200,
      "default_content_type": "text\/plain",
      "premium_expires_at": null,
      "created_at": "2021-08-11 18:34:44",
      "updated_at": "2021-08-11 18:34:44",
      "require_auth": true,
      "latest_request_id": "ea5f5920-0398-465c-8f9c-8074f0d805a4",
      "latest_request_at": "2021-08-12 19:56:50",
      "category_id": null,
      "requests": 1
    },
    ...
  ],
  "first_page_url": "https:\/\/webhook.site\/token?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.site\/token?page=1",
  "next_page_url": null,
  "path": "https:\/\/webhook.site\/token",
  "per_page": 50,
  "prev_page_url": null,
  "to": 2,
  "total": 2
}
```

### Update token

* Can require authentication.

**PUT** `/token/:token_id`

#### Request

[*See **POST** `/token`*](#11-create-token)

#### Response

[*See **POST** `/token`*](#11-create-token)

### Set password (Pro)

* Can require authentication.
* Requires user with Pro upgrade.

**PUT** `/token/:token_id/password`

Sets a password to view the requests of a token.

#### Request

```json
{"password": "hunter2", "old_password": "hunter1"}
```

#### Response

[*See **POST** `/token`*](#11-create-token)

### Set alias (Pro)

* Can require authentication.
* Requires user with Pro upgrade.

**PUT** `/token/:token_id/alias`

Sets the alias for the token, which makes the token available at `https://webhook.site/<alias>` or `<alias>@email.webhook.site` in addition to its 36 character UUID.

Rules for alias format: Length between 3-32 characters. Allowed characters: A-Z, a-z and - (dash.)

#### Request

```json
{"alias": "my-webhook"}
```

#### Response

[*See **POST** `/token`*](#11-create-token)

### Toggle CORS

Attaches CORS headers to the response of the Token, allowing browsers to request it from all domains.

**PUT** `/token/:token_id/cors/toggle`

#### Response

```json
{ "enabled": true}
```

### Get token

* Can require authentication.

**GET** `/token/:token_id`

#### Response

[*See **POST** `/token`*](#11-create-token)

### Delete token 

* Can require authentication.

**DELETE** `/token/:token_id`

#### Response

`204 No Content`

## Requests

### Create request

***(any method)*** `/:tokenId` <br>
***(any method)*** `/:tokenId/:statusCode` <br>
***(any method)*** `/:tokenId/(anything)`

If `statusCode` is valid, that HTTP status will be used in the response (instead of the default.)

Instead of `tokenId`, an alias can also be supplied.

#### Request

*(Anything.)*

#### Response

*(The default response of the Token.)*

### Get requests

* Can require authentication.

**GET** `/token/:token_id/requests`

Lists all request sent to a token. 

#### Query string parameters

* `sorting` - either `newest` or `oldest` (default)
* `per_page` - amount of requests returned, defaults to 50 (max 100)
* `page` -  page number to retrieve (default 1)
* `date_from`, `date_to` - filter requests by date, format `yyyy-MM-dd HH:mm:ss`

#### Response

```json
{
  "data": [
    {
      "uuid": "a2a6a4ae-4130-4063-953a-84fa29d81d43",
      "token_id": "a94a7294-c4aa-4074-ab77-c4cf86fd53b1",
      "ip": "127.0.0.1",
      "hostname": "webhook.site",
      "method": "POST",
      "user_agent": "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest",
      "content": "{\"first_name\":\"Arch\",\"last_name\":\"Weber\"}",
      "query": {
        "action": "create"
      },
      "headers": {
        "content-length": [
          "271"
        ],
        "user-agent": [
          "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest"
        ]
      },
      "url": "https:\/\/webhook.site\/a94a7294-c4aa-4074-ab77-c4cf86fd53b1\/201?",
      "created_at": "2019-10-03 19:06:35",
      "updated_at": "2019-10-03 19:06:35"
    }
  ],
  "total": 1,
  "per_page": 50,
  "current_page": 1,
  "is_last_page": true,
  "from": 1,
  "to": 1
}
```

### Get single request

* Can require authentication.

**GET** `/token/:token_id/request/:request_id`

**GET** `/token/:token_id/request/latest` - retrieves the latest request sent to the URL

#### Response

```json
{
  "uuid": "a2a6a4ae-4130-4063-953a-84fa29d81d43",
  "token_id": "a94a7294-c4aa-4074-ab77-c4cf86fd53b1",
  "ip": "127.0.0.1",
  "hostname": "webhook.site",
  "method": "POST",
  "user_agent": "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest",
  "content": "{\"first_name\":\"Arch\",\"last_name\":\"Weber\"}",
  "query": {
    "action": "create"
  },
  "headers": {
    "content-length": [
      "271"
    ],
    "user-agent": [
      "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest"
    ]
  },
  "files": {
    "foo": {
      "id": "65d6e0ce-a840-47bc-b6b6-ff1ff38c34ca",
      "filename": "example.json",
      "size": 5132873,
      "content_type": "text/plain"
    }
  },
  "url": "https:\/\/webhook.site\/a94a7294-c4aa-4074-ab77-c4cf86fd53b1\/201?",
  "created_at": "2019-10-03 19:06:35",
  "updated_at": "2019-10-03 19:06:35"
}
```

### Get raw request content

* Can require authentication.

**GET** `/token/:token_id/request/:request_id/raw`

**GET** `/token/:token_id/request/latest/raw` - retrieves the latest request sent to the URL

Returns the request as a response (body, content-type.)

### Download request file

* Can require authentication.

**GET** `/token/:tokenId/request/:requestId/download/:fileId`

Files that are included in a request or as email attachments are available to download using this endpoint.

### Delete request

* Can require authentication.

**DELETE** `/token/:token_id/request/(:request_id)`

Deletes a request. 

If no ID, all requests related to the token will be deleted.

#### Response

`204 No Content`
