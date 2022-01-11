---
title: FAQ
nav_order: 50
---

# Webhook.site Frequently Asked Questions

## I want to whitelist Webhook.site in our firewall, which IP do you use?

You'll need to whitelist the IP `46.4.105.116`. 

Both inbound and outbound originate and destinate at this IP address.

Note that this may change in the future, so sign up for the [newsletter](news.markdown) to be notified of changes.

## The JSON data is in a weird format/can't be parsed by Extract JSONPath

The JSON data might have been attached to the request as form data rather than as request body data, which is usually how JSON is sent.

The data might look like this on Webhook.site:

![JSON Form Data](/images/json-form-data.png)

To remediate this in Extract JSONPath, you'll need to set the source field to the form field variable, which is automatically set by Webhook.site. In the screenshot above, the variable name would be `$request.form.my_json_data$`, which works with Extract JSONPath:

![JSON Form Data in JSONPath](/images/json-form-data-jsonpath.png)

## I'm using the Send Request action to send JSON, but it's invalid

If you use any variables in the JSON that could contain e.g. new lines or quote characters, you'll need to escape the JSON properly so that it remains valid.

Webhook.site provides an easy way to do this with the `.json` Variable Modifier, which will automatically escape any special JSON characters. [More info here](/custom-actions/variables.html#variable-modifiers).

Before:

```json
{
  "message": "$request.query.message$"
}
```

After, with the JSON Escape Variable Modifier:

```json
{
  "message": "$request.query.message.json$"
}
```

## How do I export the data stored on Webhook.site?

With [Webhook.site Pro](pro.markdown), there's 3 ways to export data sent to your URL or email address.

1. We provide a CSV Export functionality, simply click the button in the menu. 

    ![CSV Export](/images/csv-export.png)

2. Data can be saved using the [Webhook.site API](api/tokens.md#get-requests) using any programming language.

3. The Webhook.site CLI (Command-Line Interface) can be used to forward requests from Webhook.site to a workstation or server. [More info here](cli.md) 

## How do I send data to my computer/localhost?

You can either periodically fetch the data using the [Webhook.site API](api/tokens.md#get-requests) or stream requests to a local URL using the [Webhook.site CLI](cli.md), in a similar fashion to e.g. ngrok.

## I'm getting a 404 Not Found, what's wrong? / When does Webhook.site URLs expire?

Using the free version of Webhook.site, URLs automatically expire in 7 days. After that, the URL is no longer available and data is deleted.

With the paid version, Webhook.site Pro, URLs never expire automatically.

## I'm getting a 405 Method Not Allowed, what's wrong?

You might be copying the URL for the Webhook.site application, and not the actual URL.

Webhook.site app (wrong):<br>`https://webhook.site/#!/6dbb3859-4ad5-4e85-acae-e44d6e37ea4a`

Webhook.site url (correct):<br>`https://webhook.site/6dbb3859-4ad5-4e85-acae-e44d6e37ea4a`

## I'm getting a 429 Too Many Requests, what's wrong?

The URL was automatically blocked due to a large amount of requests, as per our Terms of Service. This is done to prevent a decrease in service level for our other customers. 

For Webhook.site Pro customers, it is possible to have a URL whitelisted so it will not be automatically blocked. To request a whitelisting, please contact [Support](https://support.webhook.site). 

Additionally, the limit for automatically blocking the URL is many times higher than for the free version. 

## I'm getting a 413 Payload Too Large, what's wrong? / What's the request size limit?

The HTTP body data (e.g. files or JSON data) submitted to Webhook.site must be below 10 megabytes. More than that will cause a HTTP 413 response.

## I'm getting an "Access Control Check error"

If you're requesting the Webhook.site endpoint from another domain via JavaScript, you'll need to enable CORS so the browser allows the request. Simply check this checkbox to add the necessary headers.

![JSON Form Data](/images/corsenable.png)

## I'm getting a "Certificate Expired" error

Our SSL certificate is fully working; the issue lies with your system. In september 2021, our SSL provider, LetsEncrypt, [updated their root certificate](https://letsencrypt.org/docs/dst-root-ca-x3-expiration-september-2021/). This can mean that if your locally installed trusted root certificates are of an old version, you'll be seeing a certificate error as Webhook.site now runs a certificate that is based on the new root certificate chain.

To remediate this problem, you'll need to update your local certificate trust store:

* Debian-based systems: Use `update-ca-certificates`; [more info here](https://manpages.debian.org/buster/ca-certificates/update-ca-certificates.8.en.html).
* Red Hat based systems: `yum update ca-certificates`; [more info here](https://access.redhat.com/solutions/1549003)

Some systems and packages, like [Python certifi/urllib3](https://github.com/certifi/python-certifi/pull/162), also come with static certificates. We cannot support updating these.

## Is my data private?

Yes. Per default, all URLs associated with a Webhook.site Pro account are only visible for the user. Additionally, users can set passwords on individual URLs to view the data.

For free users, data is accessible to anyone who knows the ID of the URL.

## Can I use Webhook.site for production workloads?

Yes. Thousands of our customers use Webhook.site to build workflows that help their business, without needing to hire a programmer or pay for and setup servers. We take care of the infrastructure so you can build what you need.

## How much data does Webhook.site store?

For each URL associated with a Webhook.site Pro account, Webhook.site makes the latest 10.000 requests or emails available. Old requests are automatically rotated/purged periodically.

In Control Panel, it is also possible to configure a lower number of requests to store automatically before they are deleted.

For free users, the amount is 500 and old requests are not automatically rotated.
