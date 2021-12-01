# Webhook.site API

The Webhook.site API is public, free to use, doesn't require authentication and is relatively easy to use. 

!!! note
    Please note that fair use guidelines and other limitations apply as described by the [Terms of Service](https://webhook.site/terms).
    
## General Usage

Base URL: `https://webhook.site`.

We recommend that you set the `Accept` and `Content-Type` headers to `application/json`.

## Authentication

While most functions in the Webhook.site API work without any authentication whatsoever, some endpoints do require authentication, or will return a `401 Unauthorized` status code.

### API Key

An API Key can be generated in the Control Panel, and provides access to Tokens that are either a) password protected or b) require login.

<div class="center">
<a href="https://webhook.site/api-keys" class="md-button md-button--default no-underline">Create API Key</a>
</div>

To specify an API Key in a request, use the `Api-Key` HTTP header: `Api-Key: [your API Key]`

### Password

If you have set a password on a Webhook.site URL/token, to access the API resources for that token, you can use either of the following methods:

1. Specify the password using the `password` query string: `?password=[your password]` 
2. Set the password using HTTP Basic Auth, using the Authorization header. [More info](https://en.wikipedia.org/wiki/Basic_access_authentication#Client_side)