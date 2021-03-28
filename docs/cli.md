---
title: Webhook.site CLI
nav_order: 400
---

# Webhook.site CLI

The Webhook.site CLI allows you to interact with your Webhook.site URLs using the command-line interface on your computer or a server.

The CLI is still in its infancy, and currently it's main functionality is to redirect traffic from your Webhook.site URL to the machine where the CLI is being run. You then specify a URL for where the requests should be sent, allowing you to redirect traffic to machines that are not able receive connections directly from the Internet.

## Installation

For installation information, please see the [Github Page](https://github.com/webhooksite/cli/tree/master#how-to-use).

## Usage

### `forward`: Forward requests

The `forward` command listens for new incoming requests sent to your Webhook.site URL and immediately relays them to a URL you specify. This URL can be any URL that the machine running Webhook.site CLI can access.

```shell
docker run webhooksite/cli -- index.js forward \
  --token=1e25c1cb-e4d4-4399-a267-cd2cf1a6c864 \
  --api-key=ef6ef2f8-3e48-4f77-a54c-3891dc11c05c \ 
  --target=https://example.com
```

The `forward` command takes 3 parameters: token ID, API key and a target.

The token ID (`--token`) parameter must specify the token ID. The token ID is the long 36-character ID at the end of your Webhook.site URL.

An API key (`--api-key`) must also be specified, and can be generated from the Webhook.site [Control Panel](https://webhook.site/control-panel).

Finally, the target (`--target`) specifies where traffic should be redirected. 

Things to note: the request method, headers and any additional path or query string parameters added to the Webhook.site URL is forwarded on to the target. For example, if the target URL is `https://example.com`, sending a POST request to `https://webhook.site/c33f3c3e-6018-4634-b406-65338edee460/example?query=value`, the target URL will also receive a POST request on `https://example.com/example?query=value`.