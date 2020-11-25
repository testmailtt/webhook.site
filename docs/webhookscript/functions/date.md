# Date and Time Manipulation

In WebhookScript, dates are not a specific type, but rather expressed as strings that WebhookScript will attempt to parse using a very powerful date parsing engine.

However, if possible, we recommend using either a specific date format like **ISO-8601**, or specifying the date format precisely using the `to_date` function, which removes the risk of misparsing.

### Supported date and time formats

WebhookScript supports a variety of date formats, and functions taking a date will attempt to guess the format of the input string in order to parse the date into a ISO-8601 format. If possible, it's recommended to use the ISO-8601 format, for example `2020-05-27T04:00:00.000000Z`.

#### Special format examples

In addition to date strings, these special formats can also be used to generate dates.

* `now` - current date and time
* `+1 day` - adds 1 day to the current date and time
* `+1 week`
* `next Thursday` - next Thursday from now
* `last Monday` - last Monday from now
* `first day of January 2008`
* `first Saturday of July 2008`
* `Monday next week`

### Date format characters

[Click here for a list of possible date format characters](/webhookscript/date-format.html) for the `to_date` and `date_format` functions.

### Date locales available

[Click here for a list of possible locales/translations available for date display functions.](/webhookscript/date-locales.html)

### to_date(***string*** date, ***?string*** format, ***?locale*** locale, ***?string*** timezone, ***bool*** keep_timezone = false): ***string***

Returns a ISO-8601 formatted date string in UTC time from the provided `date` string. For more information about the accepted dates, see [Supported date formats](#supported-date-formats). If specified, `format` is used to parse the date without having to guess the format (see the [Date Format Characters](/webhookscript/date-format.html) specification.) If the `keep_timezone` parameter is set to true, the resulting date string will keep the timezone. The `locale` parameter will attempt to parse the date using the specified locale.

If the date is invalid or could not be guessed, `null` is returned.

```javascript
// Current date and time
'now'.to_date()                        // 2020-11-25T00:00:00.000000Z

// Relative formats
to_date('last wednesday 4 am')         // 2020-05-27T04:00:00.000000Z
'first monday august 2019'.to_date()   // 2019-08-05T00:00:00.000000Z

// Automatic format guessing
'2020-01-01 23:02:01'.to_date()        // 2020-01-01T23:02:01.000000Z

// Timezone handling
'2020-01-01 23:02:01'.to_date(null, null, 'GMT-5') // "2020-01-02T04:02:01.000000Z", interpreted as GMT-5 and converted to UTC
'2020-01-01 23:02:01'.to_date(null, null, 'GMT-5', true) // "2020-01-01T23:02:01.000000-05:00", date keeps timezone

// Unix timestamp
'@1215282385'.to_date()                // 2008-07-05T18:26:25.000000Z

// Custom date format
'2/4/12 06:03'.to_date('M/D/YY HH:mm') // 2012-02-04T06:03:00.000000Z

// To escape characters in the format string, backslashes can be used
'2020-01-05 12h30m15s'.to_date('YYYY-MM-DD HH\\hmm\\mss\\s') // 2020-01-05T12:30:15.000000Z
```

### date_format(***string*** date, ***?string*** format, ***?string*** locale, ***?string*** timezone): ***string***

Returns a date parsed to the format specified in `format`. For more information about the accepted dates, see [Supported date formats](#supported-date-formats). For a full list of date format characters, see the [Date Format Characters](/webhookscript/date-format.html) specification.

```javascript
'now'.date_format('x') // 1606329669220 (current date in UNIX timestamp with microseconds)

date_format('2008-07-05T18:26:25.000000Z', 'YYYY-MM-DD') // 2008-07-05

date_format('2008-07-05T18:26:25.000000Z', 'LLLL', 'da') // lørdag d. 5. juli 2008 kl. 18:26

date_format('2020-01-01T23:02:01.000000-05:00', 'LLLL', null, 'GMT+2') // Thursday, January 2, 2020 6:02 AM

// If no format is specified, a default human readable readable string is returned
date_format('2008-07-05T18:26:25.000000Z') // Sat Jul 05 2008 18:26:25 GMT+0000
```

### date_to_array(***string***): ***array***

Returns an array containing all the components of a given date.

```javascript
dump(date_to_array('2008-07-05T18:26:25.324542Z'))

// [
//   "year": 2008,
//   "month": 7,
//   "day": 5,
//   "dayOfWeek": 6,
//   "dayOfYear": 187,
//   "hour": 18,
//   "minute": 26,
//   "second": 25,
//   "micro": 324542,
//   "timestamp": 1215282385,
//   "formatted": "2008-07-05 18:26:25",
//   "timezone": "Z"
// ]
```

### date_interval(***string*** date1, ***string*** date2, ***?string*** format): ***string/int***

Calculates the interval between `date1` and `date2`.

If no format string is specified, the interval is returned as the number of seconds between the dates, with the number being negative if `date2` is before `date1`.

Note that for the format string, this function does not use the ISO format, but rather the uses the [PHP `DateInterval` format specification](https://www.php.net/manual/en/dateinterval.format.php).

```javascript
date_interval('2008-07-16T23:13:26.234212Z', '2008-07-05T18:26:25.324542Z') // -967620

date_interval(
    '2008-07-16T23:13:26.234212Z',
    '2008-07-05T18:26:25.324542Z',
    '%d days, %h hours, %i minutes'
)
// 11 days, 4 hours, 47 minutes
```

### date_interval_human(***string*** date1, ***string*** date2, ***?string*** locale): ***string/int***

Formats the difference between 2 dates in a way that's easy to read for humans.

If no locale is specified, English is used.

```javascript
date_interval_human(
    '2008-07-16T23:13:26.234212Z',
    '2008-07-05T18:26:25.324542Z'
)
// 1 week after

date_interval_human(
    '2008-07-16T23:13:26.234212Z',
    '2008-07-05T18:26:25.324542Z',
    'es'
)
// 1 semana después
```
