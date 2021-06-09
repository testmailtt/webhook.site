---
title: FAQ
nav_order: 50
---

# Webhook.site Frequently Asked Questions

## Q: I want to whitelist Webhook.site in our firewall, which IP do you use?

A: You'll need to whitelist the IP `46.4.105.116`. 

Both inbound and outbound originate and destinate at this IP address.

Note that this may change in the future, so sign up for the newsletter at <https://docs.webhook.site/news.html> to be notified of changes.


## Q: How do I export the data stored on Webhook.site?

A: Yes. With [Webhook.site Pro](pro.markdown), we provide a CSV Export functionality, simply click the button in the menu. Additionally, data can be saved using the [Webhook.site API](api/about.md) and Command-Line Utility.

## Q: How do I send data to my computer/localhost?

A: You can either periodically fetch the data using the API or stream requests to a local URL using the [Webhook.site API](cli.md), in a similar fashion to e.g. ngrok.

## Q: Is my data private?

A: Yes. Per default, all URLs associated with a Webhook.site Pro account are only visible for the user. Additionally, users can set passwords on individual URLs to view the data.

For free users, data is accessible to anyone who knows the ID of the URL.

## Q: Can I use Webhook.site for production workloads?

A: Yes. Thousands of our customers use Webhook.site to build workflows that help their business, without needing to hire a programmer or pay for and setup servers. We take care of the infrastructure so you can build what you need.

## Q: How much data does Webhook.site store?

A: For each URL, Webhook.site makes the latest 10.000 requests or emails available. Old requests are periodically rotated/purged. 

In Control Panel, it is also possible to configure a lower number of requests to store automatically before they are deleted.

For free users, the amount is 500 and old requests are not automatically rotated.
