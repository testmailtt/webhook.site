---
title: Custom Actions
nav_order: 400
---

# Custom Actions

![Custom Actions editor screenshot](/images/custom-actions.png)

With Custom Actions, it is possible to create a workflow out of a set of actions that are executed whenever a Webhook.site URL receives a request or email.

Using this functionality, you can connect APIs that aren't compatible, convert a HTTP request to an email or vice versa, build workflows that would otherwise require a developer, and much, much more.

## Demo

In the following demo, webshop order details are received in a webhook. We then use Extract JSONPath and Google Sheets actions to insert their name in a Google Sheet. It also shows how variables interact with downstream actions.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/9Cbuf5T6Tqo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Variables

Variables are an important part of Custom Actions, and are characterized by a name surrounded by two dollar signs: `$example$`. Variables can be used in any field that has a ⓥ icon in the editor. They act as placeholders that are replaced by dynamic content as the request or email is received.

Each request or email has a set of Base Variables (see below) that contain information like the request IP, method, headers, query string values, form values and the request content. To see a list of variables, click the Variables button in the editor. Clicking on a variable copies it to the clipboard.

![Variables Menu](/images/variables.png)

Many of the the available Custom Actions can register a variable during the runtime of the actions, so for example you can register the result of a JSONPath query and use it in a "Modify Response" action to make the response dynamic, or even use it to send a request to another HTTP address, and then use the response of that. Files can referred to and be used through Variables.

This works since Custom Actions are executed synchronously in a chain, sharing data as they're being executed.

The format of variables are dollar signs surrounded by a word, for example: `$example$`.

### Variable Modifiers

Adding specific suffixes to variable names will let you process the value in the following ways:

| Variable             | Output                     | Description |
|----------------------|----------------------------|-------------|
| $example$            | `{"json": "<b>value</b>"}`        | *no modifier*
| $example.json$      | `{\"json\": \"<b>value</b>\"}`     | Allows using the value in a JSON string as-is |
| $example.html$      | `{&quot;json&quot;: &quot;&lt;b&gt;value&lt;/b&gt;&quot;}`     | Escapes all special HTML characters |
| $example.base64_encode$ | eyJqc29uIjogIjxiPnZhbHVlPC9iPiJ9Cg== | |
| $example.base64_decode$ | | |

### Base Variables

These variables are automatically available for each request or email. Different variables are available depending on the type.

| Variable Name                     | Available For | Description                                                                                            |
|------------------------------- ---|---------------|--------------------------------------------------------------------------------------------------------|
| request.uuid                      | All           | The UUID of the request                                                                                |
| request.token_id                  | All           | The Token UUID (URL ID) of the request                                                                 |
| request.content                   | All           | The body content of the request                                                                        |
| request.date                      | All           | Creation date in Y-m-d H:m:s format                                                                    |
| request.date                      | All           | Creation date in UNIX timestamp format                                                                 |
| request.hostname                  | All           | Hostname of the request (usually `webhook.site`)                                                       |
| request.header.[name]             | All           | Created for each HTTP header                                                                           |
| request.size                      | All           | Request body size in bytes                                                                             |
| request.type                      | All           | Request type (`email` or `web`)                                                                        |
| request.file.[name].filename      | All           | Created for each file upload, with `name` being the input name property. Contains the client file name |
| request.file.[name].size          | All           | Contains the file size in bytes                                                                        |
| request.file.[name].content       | All           | Contains the file content                                                                              |
| request.file.[name].content_type  | All           | Contains the file content type (e.g. image/png)                                                        |
| request.query.[name]              | Web           | Created for each query string (e.g. ?name=value)                                                       |
| request.form.[name]               | Web           | Created for each form field                                                                            |
| request.ip                        | Web           | IP of the host making the request                                                                      |
| request.user_agent                | Web           | User agent header                                                                                      |
| request.url                       | Web           | Full URL of the request (e.g. https://webhook.site/xxx-xxx...)                                         |
| request.method                    | Web           | HTTP method (GET, POST, etc.)                                                                          |
| request.sender                    | Email         | Sender address                                                                                         |
| request.message_id                | Email         | Email message ID                                                                                       |
| request.text_content              | Email         | Parsed plaintext content                                                                               |
| request.destinations              | Email         | Comma separated list of recipients.                                                                    |
| request.checks.[name]             | Email         | True or false for email checks (DKIM, SPF, etc.)                                                       |

## Repeating Actions (Beta)

Webhook.site allows some action types to be repeating, which makes Webhook.site "loop over" one or more values without needing to use scripts.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/PDNSHyhMWcQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

Currently, repetition is only supported by the Extract JSONPath and Extract Regex action types.

Currently, the maximum amount of items that are supported is 10 to prevent abuse. This limit may be raised in the future. Items above that are ignored.

The repeating action should be ordered *before* the actions that are to be repeated. The actions that are repeated will run for each item that is extracted, using the same variable name.

