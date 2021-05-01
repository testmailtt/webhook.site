---
title: Schedules
nav_order: 395
---

# Webhook.site Schedules

Included in your Webhook.site Pro subscription is **Webhook.site Schedules**, which enables you to periodically send requests to specified URLs (also including your Webhook.site URLs, so your Custom Actions can be executed periodially) with a custom method, headers, and interval.

Schedules can be used for a variety of purposes, including cache warming, uptime monitoring, automatic data transfer, etc.

After creating the Schedule, you can view the logs for the last 100 scheduled requests.

Per default, the timeout for the Schedule requests is 5 seconds, but can range from 1 to 30 seconds. A timeout will trigger an error notification email if enabled in Control Panel.

Schedules can also be managed using the [Schedules API](/api/schedules.html).

![Schedules editor](/images/schedules-editor.png)

## Schedule Intervals

In addition to be able to use a custom Cron-style expression string, Schedules can be executed at the following preset intervals:

* 1 minute
* 5 minutes
* 10 minutes
* 1 hour
* 24 hours (at 00:00)
* Every week (mondays at 00:00)
* Every month (1st day at 00:00)

Schedule intervals are based on UTC time.