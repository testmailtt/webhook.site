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


## Repeating Actions

Webhook.site allows some action types to be repeating, which makes Webhook.site "loop over" one or more values without needing to use scripts.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/PDNSHyhMWcQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

Currently, repetition is only supported by the Extract JSONPath and Extract Regex action types.

Currently, the maximum amount of items that are supported is **100** to prevent abuse. This limit may be raised in the future. Items above that are ignored.

The repeating action should be ordered *before* the actions that are to be repeated. The actions that are repeated will run for each item that is extracted, using the same variable name.

## Queued Actions

By checking the *Queued* checkbox when creating a Custom Action, Webhook.site will run that specific action in a background queue (asynchronously).

This is useful when you need your Webhook.site URL to respond quickly, but your Custom Actions are taking a long time to run.

For example, if your Webhook.site URL should respond in 5 seconds, but you need to call an endpoint with a Send Request action that responds in 10 seconds, you can queue the Send Request action.

As the a queued action will inherit the execution scope up until the action, there are a few things to be aware of when using Queued Actions:

* Only variables defined in actions ordered *before* the queued action will be available to the action.
* Variables defined by a queued action is not available to actions coming *after* it. You cannot, for example, mark a *Send Request* action as queued and use the response in a *Modify Response* action.
* If you mark several Custom Actions as queued, they will execute independently and not share variables. 
* The amount of time until the queued action is executed can vary, but is usually in the order of seconds.
* If you have several actions marked as queued, it is not guaranteed that they will execute in order.
