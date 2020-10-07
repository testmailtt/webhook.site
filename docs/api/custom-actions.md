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

