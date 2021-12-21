---
title: News & Changelog
nav_order: 50
---

# News

Subscribe below to receive updates about improvements and new features on Webhook.site as well as infrastructure changes like new IP addresses for e.g. firewall whitelisting. Expect a newsletter a few times a year at most.

<link href="//cdn-images.mailchimp.com/embedcode/horizontal-slim-10_7.css" rel="stylesheet" type="text/css">
<style type="text/css">
	#mc_embed_signup form {text-align: left;padding: 0;}
</style>
<div id="mc_embed_signup">
<form action="https://site.us19.list-manage.com/subscribe/post?u=a4698f7ac47cff759ecdcca24&amp;id=6c5386b81d" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">
  	  <input type="email" value="" name="EMAIL" class="email" id="mce-EMAIL" placeholder="email address" required>
      <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
      <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_a4698f7ac47cff759ecdcca24_6c5386b81d" tabindex="-1" value=""></div>
      <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
</form>
</div>

## 21 December 2021

* Improved handling of binary data received from Send Request actions. 
* Added a `group_id` parameter when creating or updating Tokens.
* Fixed an issue with the Twitter Custom Action.
* Requests to `/token/:tokenId/requests` are now throttled at 60 requests/minute.

## 24 November 2021

* WebhookScript: Fixed an issue that would cause strings to be interpreted as integers when encoding JSON.

## 30 October 2021

* Webhook.site's requests to itself, e.g. via Send Request action or Schedules by Webhook.site, now shows more clearly as coming from Webhook.site in the request list. Outgoing requests are now sent with a User-Agent header of `Webhook.site/1.0`, which can be overwrited if specifying a User-Agent header manually.
* Error deleting Global Variables fixed.
* It is now possible for Webhook.site Enterprise customers to manage their Custom Domains from the control panel.

## 15 October 2021

* Fix invalid charset configurations causing issues saving requests.

## 4 October 2021

* Webhook.site now supports multiple sub-users on an account, with different access permissions, available to Webhook.site Enterprise users. For more information, please [contact us](https://support.webhook.site).

## 29 September 2021

* Webhook.site CLI: New minor version, fixes a bug causing `Invalid namespace` errors.

## 17 September 2021

* New Custom Action Variable Modifiers: `.html_decode`, `.url_encode`, and `.url_decode`. [More info here](/custom-actions.html#variable-modifiers)

## 12 September 2021

* New WebhookScript function: array_merge(), that merges two arrays into one. [More info here](/webhookscript/functions/array.html)
* New WebhookScript function: array_chunk(), that splits an array into chunks. [More info here](/webhookscript/functions/array.html)
* Functions dd(), dump() and echo() can now take a variable amount of arguments. [More info here](/webhookscript/functions/general.html)
* New WebhookScript date function: now(), which returns the current date in ISO format. [More info here](/webhookscript/functions/date.html)
* The date_interval() and date_interval_human() functions now defaults to "now" if the second parameter isn't specified.
* Script editor now has more space for outputs in full screen mode.

## 18 August 2021

* New API Endpoint: Get tokens, which returns a list of all tokens belonging to the account. [More info here](/api/tokens.html#get-tokens)
* Fixed a bug that caused logins to be slow on especially older accounts.
* Fixed a bug that caused the FTP Upload action to error when the Port field was missing.

## 12 August 2021

* Google Sheet actions that consistently cause errors are now disabled automatically. Users are sent an email when this occurs.

## 30 July 2021

* New WebhookScript function: hmac(), which allows easily verifying strings using the HMAC method.  [More info here](/webhookscript/functions/string.html#hmacstring-value-string-algo-string-secret-stringfalse)

## 14 July 2021

* New Custom Action: Replace Text, which allows easily making text replacements from variable input, and either overwrites an existing variable or creates a new one with the replaced content.

## 4 July 2021

* Fixed bug causing the "Use Request Content" checkbox in the Send Email action to not work.

## 15 June 2021

* New Custom Action: Twitter, so you can easily send tweets using Webhook.site.
* New WebhookScript functions: convert_kana(), string_slice(), string_upper(), string_lower(), string_title() [More info here](/webhookscript/functions/string.html).

## 10 June 2021

* Individual Custom Actions can now be set as *queued*, which causes them to be run in the background, or asynchronously. [More info here](/custom-actions.html#queued)

## 7 June 2021

* Raised the limit for the amount of items processed by repeating actions to 100.
* Fixed a bug that would cause an error when updating notification settings in Control Panel.
* Fixed a bug where emails containing attachments would be stored.

## 23 May 2021

* API: It's now possible to filter requests by date. [More info here](/api/tokens.html#query-string-parameters)

## 13 May 2021

* Documented `clone_from` option when using the API to create Tokens (URLs)
* WebhookScript: `json_decode` / `json_encode` now output error messages if they fail due to e.g. bad data.

## 1 May 2021

* Webhook.site Schedules now has an API. [More info here](/api/schedules.html)
* Fixed a bug where URLs could be in two groups at the same time.

## 20 April 2021

* Added base64 encoding and decoding *variable modifiers*. [More info here](/custom-actions.html#variable-modifiers)

## 11 April 2021

* New Custom Action and WebhookScript function: Don't Save, which marks the request so it is not saved in Webhook.site. The request can still be seen when it comes in, but will not be available through through the app later, or through the API. 
* New Custom Action: Stop, which immediately stops Custom Action execution and returns the default response.
* The Extract Regex now supports the Repeat function. [More info here](/custom-actions.html#repeating-actions-beta).

## 7 April 2021

* New powerful feature: Repeating actions. Currently supported by the Extract JSONPath action, it is now possible to "loop over" items in a JSON array. [More info here](/custom-actions.html#repeating-actions-beta)

## 2 April 2021

* It is now possible to enable or disable Custom Actions on a specific Token with the API. [More info here](/api/custom-actions.html#toggle-custom-actions) or [here](/api/tokens.html#create-token).
* When exporting CSVs, the sorting selected in the application is now used automatically.

## 28 March 2021

* Today we've released the first version of the Webhook.site Command-line Interface (CLI), which allows you to forward requests from your Webhook.site URL to your local machine. [More info here](/cli.html)

## 24 March 2021

* WebhookScript: Added `array_sort`, `array_join` and `json_escape` functions.
* Added *modifiers* for variables. [More info here](/custom-actions.html#variable-modifiers)

## 23 March 2021

* Control Panel: It's now possible to clone URLs, including their Custom Actions and other configuration.
* Control Panel: URLs with a password can be deleted more easily.

## 13 March 2021

* Control Panel: It's now possible to set a password for a Webhook.site URL in the Control Panel. Additionally, it's now possible to easily select and delete multiple URLs at once.

## 11 March 2021

* API: It's now possible to specify an alias when creating a URL via the API. [More info here](/api/tokens.html)

## 6 March 2021

* New Action: Database Query - allows running database queries on PostgreSQL and MySQL servers, inserting, changing and fetching data in specific variables or JSON format. [More info here](/custom-actions.html#database-query)

## 3 March 2021

* Webhook.site Premium has changed name to Webhook.site Pro. Functionality, pricing and everything else remains the same; it's a cosmetic change.
* More currencies are now supported for Webhook.site Pro subscriptions: GBP and EUR. To change the currency of an existing subscription, please contact [Webhook.site Support](https://support.webhook.site).
* Custom Action output is now included in CSV Exports.

## 17 Feburary 2021

* New Action: FTP(S) Upload - allows easy file upload to FTP servers.

## 5 Feburary 2021

* New WebhookScript functions: html_strip_tags, html_decode, html_encode, markdown_to_html. For more information, [see here](/webhookscript/functions/string.html).

## 1 Feburary 2021

* Webhook.site has had intermittent downtime today due abuse from a user. We've identified them and blocked them from our systems. We're very sorry for the inconvenience.

## 31 January 2021

* We have discontinued support for subscriptions via Patreon, who will need to create a new subscription. For more information please contact [support](https://support.webhook.site).

## 19 January 2021

* Happy new year!
* New Action Type: Conditions 2.0. Now supports adding multiple conditions in a single action.
* New Action Type: Set Variable. Working similarly to the Store Global Variable action, this action sets a runtime variable that is not persisted.
* Actions can now individually be executed depending on a previous set of conditions.
* The Debug Output section in the Custom Actions builder now shows the action number and type from where it came.
* The Modify Response action now supports returning the response immediately.

## 5 December 2020

* Added new Custom Action: Store Global Variable, which does what it says on the tin.
* Bug fix: In Control Panel, the update date for each Global Variable now actually updates when a Global Variable is updated.

## 26 November 2020

* Webhook.site had downtime during the night. The problem has been fixed.

## 25 November 2020

* WebhookScript: It's now possible to store non-string values in set(). If the value is an array, however, it is JSON encoded first.
* WebhookScript: Added more examples for the date functions.

## 1 November 2020

* Added new Custom Action: Rate Limit, which lets you specify the maximum amount of requests in a given duration per IP to allow to request the Webhook.URL.
* Dates shown in the application now include seconds.

## 29 October 2020

* Added new Custom Action: Run SSH Command, which allows you to run SSH commands on your server.

## 22 October 2020

* WebhookScript: Added `array_keys` and `array_values` functions. For more information, [see here](/webhookscript/functions/array.html).

## 19 October 2020

* It's now possible to set a timeout for the Send Request action. A new `timeout` parameter can also be given to the `request()` function in WebhookScript. Both places accept a value in seconds, with decimals.
* When exporting Custom Actions, if the URL has an alias, this is now used for the resulting filename.

## 11 October 2020

* It's now possible to export and import Custom Actions to a file using the new Import/Export buttons in the Custom Actions builder.

## 7 October 2020

* Added documentation for managing Custom Actions via the API. For more information, [see here](/api/custom-actions.html).
* Fixed a bug causing the Operator of an action to be reset to "is equal to" when testing.

## 6 October 2020

* Action output is no longer displayed twice when testing Condition actions.

## 24 September 2020

* New feature: Customize Auto-Cleanup threshold. This lets you specify how many requests or emails to keep for your URLs, if you want to keep fewer than the default amount of 10.000 for e.g. data protection reasons. Available from the brand new Settings page in Control Panel. The setting applies to all URLs that have the Auto Cleanup feature enabled - click Edit on a URL to enable it.
* New feature: URL groups, which lets you categorize your URLs into groups. Available from the URLs page in Control Panel. Click Edit on a URL to change its group.
* The URLs page in Control Panel has a new design which is less cluttered and allows you to more quickly change certain settings, URL aliases, and the description of a URL.

## 23 September 2020

* Regrettably, we saw a long period of downtime again from approx 20:00 to 05.40 UTC. The cause of the downtime was a user flooding their Webhook.site URLs with many gigabytes of data, causing the system to be overloaded. The same user was responsible for the downtime at 15 September 2020 and we've now terminated their license to use Webhook.site. We are also going prioritize changes that will automatically limit this kind of abuse, as well as move to another database system that will be more resilient.

## 15 September 2020

* We've seen spurious instances of downtime in the last 24 hours, the longest one lasting from approx. 14:00 to 14:50 UTC. We apologize for the inconvenience.

## 13 September 2020

* WebhookScript: Added `override` parameter to request(), which prevents content from the source request from being included.

## 3 September 2020

* WebhookScript: It is now possible to set a default for the `var()` function.
## 29 August 2020

* A bug in the Extract JSONPath action has been fixed so that it is now also possible to filter for keys containing punctuation, e.g. `.data[?(@.Employee.FirstName)]`.

## 18 August 2020

* WebhookScript: The `to_date` and `date_format` functions have been improved with timezone handling capabilities.

## 15 August 2020

* It's now possible to set a custom timeout for Schedules, up to 30 seconds.

## 8 August 2020

* You can now specify a custom Cron expression for your Webhook.site Schedule, in addition to the predefined intervals. This lets you decide exactly the hour, day and minute, etc., of when the schedule runs (based on UTC time.)
* It's now possible to enable email notifications for whenever a Schedule run fails to execute. To enable this, simply check the checkbox in [Notification Settings.](https://webhook.site/notifications).

## 7 August 2020

* It's now possible to change the name of your Provider accounts to e.g. something that's easier to remember.

## 5 August 2020

* Webhook.site had an unplanned outage starting at 03.30 UTC. The site was down for around an hour.

## 2 August 2020

* It is now possible to specify a default value in the Extract JSONPath, Extract Regex and Extract XPath actions, so that if the extraction could not find the item, the variable is set to the default value that is defined. This field also takes variables.
* Request list is now sorted by Newest First per default.
* Custom Action number and type is now shown next to the output in the request details. If the Action was deleted, the UUID is shown instead.

## 1 August 2020

* It is now possible to enable email notifications for whenever a Custom Action encountered an error. To enable this, simply check the checkbox in [Notification Settings.](https://webhook.site/notifications).

## 29 July 2020

* New WebhookScript function: `trim(string)`, which removes space, newline and tab characters from the beginning and end of a string, similar to PHP's own trim() function.
* New Schedule intervals: weekly (every monday), monthly (every 1st day of month)

## 25 July 2020

* New WebhookScript function: `action(action_type, parameters)`, to run Custom Actions inside a WebhookScript. [More info here.](/webhookscript/functions.html#actionstring-action_type-array-parameters-array)
* It's now possible to download email attachments or uploaded files directly from the Webhook.site app.
* When sending a request using either the Send Request Custom Action or the request() function, the response is now truncated if the response content is over 20KiB. This means the whole contents is not visible in the app, but is still available to Actions.

## 16 July 2020

* Better file handling for emails: attached files are now also extracted as variables
* New file management functions for WebhookScript: `files()` retrieves a an array of all files, `file_content(fileId)` returns the content of a specific file. [More info here.](/webhookscript/functions.html#files)

## 5 July 2020

* New "Resize Image" action added for resizing images from either a file upload, email attachment or other Action. 
* Better handling of downloaded files: the contents won't be shown in the debug overlay to prevent very large files from crashing the browser.
* Fixed a bug in the Dropbox provider returning creating an empty variable when downloading large files.

## 3 July 2020

* Webhook.site was down for about 30 minutes starting 07:20 UTC due to a memory upgrade.
* Max request size has been increased to 10 MB from 2 MB.

## 23 June 2020

* Added new Dropbox Custom Actions: Create Folder, Download, Upload, Delete, Get Link. 

## 14 June 2020

* WebhookScript editor syntax highlighting improved with regards to multiline strings, escape characters and more
* New WebhookScript editor keyboard shortcut for saving (Mac: Cmd-S, Windows: Ctrl-S.)
* Fix WebhookScript fullscreen mode not being disengaged when saving
* URLs can now accept file uploads via multipart. File contents are available via variables: `request.file.<formname>.content`, `request.file.<formname>.size`, `request.file.<formname>.filename`
* New WebhookScript function: `csv_to_array()`, which converts a CSV file from a string to an array that can easily be parsed.
* Added an [example script](/webhookscript/examples#uploading-and-parsing-csv-file) demoing file uploads and CSV parsing

## 7 June 2020

* Added new Slack Send Message Custom Action, which lets you send Slack messages via a Slack Webhook URL.

## 5 June 2020

* Added "Formula Mode" checkbox for Add and Update Row Google Sheets actions, which parses values like entered in a cell, and allows inserting formulas.

## 4 June 2020

* Added new endpoints to fetch the content and information about the latest request on a URL. See [here](/api#get-single-request) and [here](/api#get-raw-request-content).

## 2 June 2020

* Added Amazon Web Services CloudFront Cache Invalidation Custom Action.
* Added ability to toggle Auto Cleanup, which automatically cleans up requests/emails.

## 30 May 2020

* Added Discord Custom Action for sending messages. [Read more in the docs](/custom-actions#discord)

## 29 May 2020

* New set of date functions added to WebhookScript, namely: `to_date()`, `date_format()`, `date_to_array()`, `date_interval()`, `date_interval_human()`. [Read more in the docs](webhookscript/functions#date-manipulation)

## 25 May 2020

* New set of Amazon Web Services S3 actions: Create Bucket, Put Object, Delete Object and Get Object (which retrieves object contents to a Variable.)

## 22 May 2020

* New Schedule intervals: every 1 minute and every 10 minutes, in addition to the already [existing ones](/schedules).

## 17 May 2020

* New WebhookScript function: `delay()`, which lets you delay and execute WebhookScript code a set amount of seconds in the future.
* New WebhookScript function: `exec()`, which lets you dynamically execute code in a string.
* New WebhookScript function: `import()`, which downloads and executes code from a URL - great if you want to reuse your code, just put it on Github and import it with the URL!

## 16 May 2020

* It's now possible to set a Token (URL or email address) to expire automatically, even for Premium users. This is useful for creating tokens for automated testing.

## 3 May 2020

* New Google Sheets Custom Actions (Beta). 3 initial actions are available: Append Row, Update Row and Get Values, which allow you to manipulate or retrieve the values of a Google Sheet without writing any code.

## 24 April 2020

* New fullscreen mode in WebhookScript editor
* Ability to edit your user profile
* New WebhookScript functions: `base64_encode()`, `base64_decode()`.

## 21 April 2020

* New WebhookScript function: store() - creates or updates an existing Global Variable

## 20 April 2020

* New Global Variables section in Control Panel.

## 19 April 2020

* New WebhookScript math functions: max(), min(), mod(), pi(), rand() - for more, see the [Reference](/webhookscript/reference)

## 28 March 2020

* New feature: Webhook.site Schedules lets you request any URL – including Webhook.site URLs – automatically on an interval, so you can for example run Custom Actions every 5 minutes, or make a health check for your Web site.
* Send Request action request timeout has been raised from 5 to 10 seconds. Applies to both the Custom Action and the WebhookScript request() function.

## 24 March 2020

* New feature: API Keys can now be created so you can use the API with URLs that have the "Require Authentication" or "Password" options set.
* Fix: It's now possible to test Send Email actions before creating them. Prior to this, the Test button would not do anything for the Send Email action.

## 6 March 2020

* New feature: Extract XPath Custom Action with accompanying xpath() WebhookScript function. [Read more.](/custom-actions#extract-xpath)

## 29 Feburary 2020

* Values are no longer required for Condition actions, so it's possible to compare an empty string or missing value.
* Fixed an issue where a tooltip in the Custom Actions modal would not disappear.
* Removed Beta label from WebhookScript.

## 27 Feburary 2020

* Fixed a bug where slashes at the end of Webhook.site Single Page App URLs didn't work.
* Fixed a bug where Copy To CURL sometimes wouldn't return a valid CURL command.

## 26 Feburary 2020

* It's no longer a requirement to specify a variable for the Send Request action.

## 25 Feburary 2020

* New feature: It's now possible to receive emails, which are treated like Webhooks – so you can automate emails with Custom Actions on Webhook.site. You can also test email deliverability using DKIM, DMARC and SPF validation.
* JSON formatting is now always enabled per default.
* The requests view is cleared after deleting the last request, and the tutorial text is shown.

## 16 Feburary 2020

* WebhookScript: Added `regex_extract` and `regex_extract_first` functions.

## 15 Feburary 2020

* WebhookScript: Added `hash` function.

## 14 Feburary 2020

* New feature: Export to CSV lets you export all requests on a given URL to a CSV file.
* Fixed a bug where duplicate in-app notifications would appear on new requests.

## 12 Feburary 2020

* WebhookScript: Added `url_encode`, `url_decode`, and `query` functions.

## 8 Febuary 2020

* New Custom Action type: Condition, which lets you conditionally stop a set of actions based on comparisons.

## 28 January 2020

* WebhookScript now supports newline literals (`\\n`) in strings, escaped by 2 backslashes.

## 25 January 2020

* Global Variables are now available in the Control Panel, which lets you keep configuration like API keys in a separate place from your Custom Actions and scripts while managing them at a central place.

* Changed the font of the WebhookScript editor, which resulted in uneven selection of text.

## 23 January 2020

* You can now specify a source variable for JSONPath and Regex actions, so you can extract text from not only the request content.

## 12 January 2020

* Switched to using Ace as editor for WebhookScript.
