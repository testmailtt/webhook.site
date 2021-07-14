# API Endpoints: Custom Actions

## Action Types

[Click here for a list of the API names and parameters for Action Types](action-types.md).

## Actions

### Create Custom Action

* Can require authentication.

**POST** `/token/:token_id/actions`

* `type` is the name of an [Action Type](action-types.md).
* `order` specified which order the action is executed in.
* `parameters` can vary depending on the [Action Type](action-types.md). 
* `disabled` if set to true, the action is skipped upon execution.

#### Request


##### Example 1: Condition action

```json
{
  "type": "condition",
  "order": 3,
  "disabled": false,
  "parameters": {
    "input": "$request.content$",
    "operator": "eq",
    "value": "",
    "action": "stop"
  }
}
```

##### Example 2: WebhookScript action

```json
{
    "type": "script",
    "order": 1,
    "parameters": {
        "script": "expiry = '2021-08-01T00:00:00.000000Z'\nnow = to_date('now')\n\nif (date_interval(now, expiry) < 0) {\n    // Respond with 410 Gone\n    respond('This content is no longer available.', 410)\n}\n"
    }
}
```

##### Example 3: Creating WebhookScript action with Python 3

Same script as Example 2. Requires the `requests` module, which can be installed using `pip install requests`.

```python
import requests

script = """
expiry = '2021-08-01T00:00:00.000000Z'
now = to_date('now')

if (date_interval(now, expiry) < 0) {
    // Respond with 410 Gone
    respond('This content is no longer available.', 410)
}
"""

data = {
    "type": "script",
    "order": 1,
    "parameters": {
        "script": script
    }
}

r = requests.post('https://webhook.site/token/7d63959e-4fec-49bd-90dc-a4615722825e/actions', json=data)
```

#### Response

```json
{
    "uuid": "7ae324d6-c65b-416b-8f83-18fb89e0c740",
    "token_id": "fe18d303-631d-4620-acb3-5c0b1b0b876d",
    "type": "condition",
    "order": 3,
    "disabled": null,
    "parameters": {
        "input": "$request.content$",
        "operator": "eq",
        "value": "",
        "action": "stop"
    }
}
```

### Get Custom Actions

* Can require authentication.

**GET** `/token/:token_id/actions`

#### Response

`200 OK`

```json
{
  "data": [
    {
      "uuid": "52055928-099a-44dc-ba31-e8d808b98ea1",
      "token_id": "fe18d303-631d-4620-acb3-5c0b1b0b876d",
      "type": "condition",
      "order": 1,
      "disabled": false,
      "parameters": {
        "input": "$request.header.content-type$",
        "operator": "nct",
        "value": "application/json",
        "action": "stop"
      }
    },
    {
      "uuid": "27b07ca7-ea83-48f5-b376-2372cf25d3a1",
      "token_id": "fe18d303-631d-4620-acb3-5c0b1b0b876d",
      "type": "condition",
      "order": 2,
      "disabled": null,
      "parameters": {
        "input": "$request.content$",
        "operator": "eq",
        "value": "",
        "action": "stop"
      }
    }
  ]
}
```

### Update Custom Action

* Can require authentication.

**PUT** `/token/:token_id/actions/:action_id`

#### Request

*See [Create Custom Action](#create-custom-action) endpoint.*

#### Response

*See [Create Custom Action](#create-custom-action) endpoint.*

### Delete Custom Action

* Can require authentication.

**DELETE** `/token/:token_id/actions/:action_id`

### Toggle Custom Actions

* Can require authentication.

***PUT*** `/token/:token_id/actions/toggle`

This endpoint toggles whether actions are enabled on a specific token.

#### Response

`200 OK`

```json
{
    "enabled": true
}
```
