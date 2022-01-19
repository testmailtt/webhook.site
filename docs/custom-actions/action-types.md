## WebhookScript

!["WebhookScript" Custom Action screenshot](/images/webhookscript-in-action.png)

Executes custom scripts using a scripting language that's very similar to JavaScript and PHP. [More information here](/webhookscript.html)

## Text

### Extract JSONPath

This action runs a JSONPath query on the contents of a request. With it, you can extract any data from a JSON document and store it in a variable, which can then be used in a downstream action.

JSONPath is very similar to the `jq` commandline utility.

##### JSONPath Examples

JSONPath                  | Result
--------------------------|-------------------------------------
`$.store.books[*].author` | the authors of all books in the store
`$..author`                | all authors
`$.store..price`           | the price of everything in the store.
`$..books[2]`              | the third book
`$..books[(@.length-1)]`   | the last book in order.
`$..books[-1:]`            | the last book in order.
`$..books[0,1]`            | the first two books
`$..books[:2]`             | the first two books
`$..books[::2]`            | every second book starting from first one
`$..books[1:6:3]`          | every third book starting from 1 till 6
`$..books[?(@.isbn)]`      | filter all books with isbn number
`$..books[?(@.price<10)]`  | filter all books cheapier than 10
`$..*`                     | all elements in the data (recursively extracted)


##### JSONPath Syntax

Symbol                | Description
----------------------|-------------------------
`$`                   | The root object/element (not strictly necessary)
`@`                   | The current object/element
`.` or `[]`           | Child operator
`..`                  | Recursive descent
`*`                   | Wildcard. All child elements regardless their index.
`[,]`                 | Array indices as a set
`[start:end:step]`    | Array slice operator borrowed from ES4/Python.
`?()`                 | Filters a result set by a script expression
`()`                  | Uses the result of a script expression as the index


For more details on what's possible with JSONPath, [take a look at the docs](https://github.com/FlowCommunications/JSONPath#jsonpath-examples).

As you start entering a JSONPath, the results are validated and shown next to the input field.

### Extract Regex

This action runs a Regex (regular expression) query on the contents of a request. With it, you can extract any data from a text document and store it in a variable, which can then be used in a downstream action.

As you start entering a Regex, the results are validated and shown next to the input field.

### Extract XPath

Similar to the Extract JSONPath Custom Action, Extract XPath lets you extract values from an XML or HTML document and save the result as a variable.

##### XPath Examples

The following examples are based on this XML document:

```xml
<?xml version="1.0"?>
<organization name="ExampleCo">
  <employees>
    <employee id="1">Jack</employee>
    <employee id="2">Ann</employee>
  </employees>
</organization>
```

Example XPath                                     | Notes                                                       | Result
--------------------------------------------------|-------------------------------------------------------------|----------------
`/organization`                                   | Finds all content within the organization element           | Jack<br>Ann
`//employee[@id != 1]`                            | `//` traverses all `<employee>` elements in document, the @id query selects all except those with `id`=1 | Jack
`/organization/@name`                             | `@name` to get the "name" property of the element           | ExampleCo
`/organization/employees/employee[2]`             | `[2]` specifies 2nd element                                 | Ann
`/organization/employees/employee[2]/@id`         | Get the "id" property of second employee element            | 2
`/organization/employees/employee[@id=1]`         | Employee element with id property equal to "1"              | Jack
`/organization/employees/employee[last()]`        | Last employee element                                       | Ann
`//employee[contains(@id, "2")]`                  | Employee within any parent element where id contains "2"    | Ann

For more examples, see [W3CSchools](https://www.w3schools.com/xml/xml_xpath.asp) or [XPath Cheatsheet](https://devhints.io/xpath)

### Replace Text

An action that allows replacing multiple inputs to a string with specified replacements. Additionally, Webhook.site will replace all variables in the source text as well as the text being replaced, and the replacement.

## Network

### Send Request

This will send a request with variable contents from the Webhook.site cloud. Per default, the request contents will be identical to what was sent to the URL originally.

Variables extracted previously can be used.

The response of the request is stored in a series of variable names prefixed with a value of your choosing. The following variables are set after the request has been fired:

* `$your_prefix.content$` - response body content
* `$your_prefix.status$` - response status code
* `$your_prefix.headers$` - response headers
* `$your_prefix.url$` - the URL the request was sent to

### Send Email

This will send a email with variable contents from the Webhook.site cloud. Variables extracted previously can be used.

### Run SSH Command

Allows you to run one or more SSH command on a server. Webhook.site captures the output (stdout), stderr and the command exit code as Variables that can be used in downstream actions:

* `$ssh.stdout$`
* `$ssh.stderr$`
* `$ssh.exit$`

### FTP(S) Upload

Allows uploading a file to a FTP or FTPS (FTP with TLS/SSL) server, specifying a hostname, port, username, password, relative path to the file, whether to use SSL and whether to use passive mode. Finally, the file content can be specified, in which Variables are replaced.

We recommend storing the password as a Global Variable.

### Database Query

Allows running a database query, with support for fetching out data in a series of variables. We recommend storing the password as a Global Variable.

#### Supported Database Servers

Currently supported are:

* PostgreSQL
* MySQL

If your database server is not on the list, please [contact support](https://support.webhook.site).

#### Using Parameters

When using e.g. INSERT or UPDATE statements, we strongly recommend using *parameters* for each column value. Doing this, you avoid SQL injection attacks and other issues when using user-submitted data (e.g. via Variables), or even just data containing special characters like quotes, that could otherwise break a query.

Each parameter name should start with a colon (:) and be a single word. You can then reference these parameters inside the query, like in the following example:

![](/images/database.png)

#### Fetching data

When fetching data using e.g. SELECT statements, Webhook.site automatically inserts data in a series of Custom Action Variables, which are then available to downstream actions.

For example, when fetching rows from the following table:

![](/images/database-example-table.png)

Using the following statement:

```SQL
select * from employees
```

If the variable name prefix would be set to `output`, the following variables would be created containing specific values:

| Variable Name       | Value                          |
|---------------------|--------------------------------|
| $output.0.id$       | 1                              |
| $output.0.fname$    | Simon                          |
| $output.0.lname$    | Fredsted                       |
| $output.0.title$    | Founder                        |
| $output.1.id$       | 2                              |
| $output.1.fname$    | Jack                           |
| $output.1.lname$    | Daniels                        |
| $output.1.title$    | Assistant                      |

Additionally, a variable would be created with the name `$output.json$` containing the data in JSON format:

```json
[                              
  {
    "id": 1,
    "fname": "Simon",
    "lname": "Fredsted",
    "title": "Founder"
  },
  {
    "id": 2,
    "fname": "Jack",
    "lname": "Daniels",
    "title": "Assistant"
  }
]
```

## Behavior

### Modify Response

This action can be used to modify the response of the Webhook.site URL based on the input.

### Rate Limit

This action can be used to allow a specific amount of requests in a specific amount of time per a given IP.

If the IP is rate limited, the URL will respond with a `HTTP 429`, action execution is stopped, and the request is not saved in Webhook.site.

### Don't Save

Marks the request so it is not saved in Webhook.site, which is useful when receiving a large amount of requests.

### Stop

Immediately stops Custom Action execution and returns the default response.

## Logic

### Condition

!["Condition" Custom Action screenshot](/images/condition-action.png)

Useful if you need to validate that the request does or does not conform to certain criteria, the Condition action will either stop or continue based on a condition.

In both the *input* and the *value* fields, variables will be replaced (including Global Variables from the Control Panel), so you can compare e.g. JSONPath or Regex values - or even values from a previous HTTP request that was sent. 

Currently, two *actions* are provided: stop and continue. *Stop* will stop further action execution of the condition is a match. *Continue* will *only* continue further execution if the condition is a match, and otherwise stop.

The following "operators" are available:

* is equal to
* is not equal to
* starts with
* ends with
* contains
* does not contain
* is greater than
* is greater than or equal to
* is less than
* is less than or equal to

The "result" of the condition will be logged below the request details, so you can see what happened.

## Image Handling

### Resize Image

Takes an image from either a URL or raw image data from e.g. a file upload, email attachment, request response or another action such as Dropbox.

You can enter both width and height to contrain the image in both dimensions, or enter a single dimension.

Check "Keep Aspect Ratio" so that the image keeps the aspect ratio, but doesn't exceed the height and width constraints.

## Google Sheets

Google Sheets Custom Actions lets you manipulate and retrieve values from a Google Sheet.

The following Google Sheets Custom Actions are available:

* Add Row - appends one or more new rows to an existing spreadsheet
* Update Row - updates one or more cells in an existing spreadsheet
* Get Values - retrieves one or more cell values from an existing spreadsheet

To start, you need to make sure that you have connected a Google account in the Control Panel, [available here](https://webhook.site/providers).

After that, you can select the account in the dropdown when creating the Custom Action.

### Usage Limits

It is important to note that Google will block Write requests (i.e. adding or updating rows) at **60 requests per minute**. After that, the action will temporarilyfail with the following error message:

```
Quota exceeded for quota metric 'Write requests' and limit 'Write requests per minute per user' of service 'sheets.googleapis.com' for consumer
```

Therefore, for importing mass amounts of data in a short timespan, Google Sheets is not recommended. Instead, we recommend using the Database Query action.

### Specifying the spreadsheet

When specifying the spreadsheet, you can either just copy/paste the spreadsheet URL or enter the spreadsheet ID. Variables can be used to specify the spreadsheet.

### Ranges

All actions must specify a range, which behaves similar in all actions. For the Add Row action, Google Sheets will automatically find a "table" (e.g. a homogenous mass of data) and add the values at the bottom. 

A range is the same query as in Google Sheets, e.g. to select A1-C3 in Worksheet "Example", enter `'Example'!A1:C3`.

### Values

When inserting or updating values, you can either enter a value in the text field, or supply multiple cells and/or rows using JSON. To insert two rows, the JSON would be `["cell 1", "cell 2"]`.

### Variables

The Get Values Action allows you to define variables based on the output. Since this action can return multiple pieces of data, multiple variables are created.

For example, if you select two columns and two rows, e.g. `A1:B2`, four variables would be defined:

1. `variable_name.0.0` = value of A1
1. `variable_name.0.1` = value of A2
1. `variable_name.1.0` = value of B1
1. `variable_name.1.1` = value of B2

Additionally, the data is available in JSON, with the `variable_name.json` variable being defined, and continuing with the example above, would contain the following JSON:

```json
[
  ["A1","A2"],
  ["B1","B2"]
]
```

## Amazon Web Services (AWS)

### S3

The following actions are available for AWS S3:

* Create Bucket
* Create Object
* Delete Object
* Get Object (retrieves object contents to a Variable)

In addition to the "official" Amazon endpoints, Webhook.site also supports S3-compatible storages like DigitalOcean, MinIO, Wasabi and more. The endpoint can be specified when setting up the account in Control Panel.

### CloudFront

The "Create Invalidation" action allows you to dynamically create a CloudFront cache invalidation as a Custom Action. Both the Distribution ID and the paths to be invalidated are replaced with Webhook.site Variables.

## Discord

With the Discord Custom Action, you can send messages to a specified channel (Each bot account uses a specific channel, so you can connect more accounts to send to different channels or servers.) In addition, you can choose a custom username and avatar image for the bot user.

!["Discord" Custom Action screenshot](/images/discord.png)


## Slack

With the Slack Custom Action, you can easily use Slack's Webhook URLs to send messages to a channel.

## Dropbox

The Dropbox integration has access to the entire contents of your dropbox, and currently the following actions are available:

* Create Folder
* Download File
* Upload File
* Delete File
* Delete Folder
* Get Link - creates a temporary download link for any file in your Dropbox, and saves it in a variable.

## Twitter

The Twitter Integration supports the following actions using Twitter's API:

* Post Tweet

## RabbitMQ

The RabbitMQ Integration allows you to publish and consume messages from a RabbitMQ queue by specifying the server connection details.