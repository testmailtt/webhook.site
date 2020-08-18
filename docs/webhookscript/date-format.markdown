---
nav_exclude: true
---

# Date format characters

WebhookScript uses the ISO format for converting and formatting dates, and the format is compatible with the [Moment.js format method](https://momentjs.com/docs/#/parsing/string-format/).

The following examples are based on the date `2017-01-05 17:04:05.084512`.

| Code      | Example       | Description                                                                                                                                       |
|-----------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| OD        | 5             | Day number with alternative numbers such as 三 for 3 if locale is ja_JP                                                                           |
| OM        | 1             | Month number with alternative numbers such as ၀၂ for 2 if locale is my_MM                                                                         |
| OY        | 2017          | Year number with alternative numbers such as ۱۹۹۸ for 1998 if locale is fa                                                                        |
| OH        | 17            | 24-hours number with alternative numbers such as ႑႓ for 13 if locale is shn_MM                                                                    |
| Oh        | 5             | 12-hours number with alternative numbers such as 十一 for 11 if locale is lzh_TW                                                                  |
| Om        | 4             | Minute number with alternative numbers such as ୫୭ for 57 if locale is or                                                                          |
| Os        | 5             | Second number with alternative numbers such as 十五 for 15 if locale is ja_JP                                                                     |
| D         | 5             | Day of month number (from 1 to 31)                                                                                                                |
| DD        | 05            | Day of month number with trailing zero (from 01 to 31)                                                                                            |
| Do        | 5th           | Day of month with ordinal suffix (from 1st to 31th), translatable                                                                                 |
| d         | 4             | Day of week number (from 0 (Sunday) to 6 (Saturday))                                                                                              |
| dd        | Th            | Minified day name (from Su to Sa), transatable                                                                                                    |
| ddd       | Thu           | Short day name (from Sun to Sat), transatable                                                                                                     |
| dddd      | Thursday      | Day name (from Sunday to Saturday), transatable                                                                                                   |
| DDD       | 5             | Day of year number (from 1 to 366)                                                                                                                |
| DDDD      | 005           | Day of year number with trailing zeros (3 digits, from 001 to 366)                                                                                |
| DDDo      | 5th           | Day of year number with ordinal suffix (from 1st to 366th), translatable                                                                          |
| e         | 4             | Day of week number (from 0 (Sunday) to 6 (Saturday)), similar to "d" but this one is translatable (takes first day of week of the current locale) |
| E         | 4             | Day of week number (from 1 (Monday) to 7 (Sunday))                                                                                                |
| H         | 17            | Hour from 0 to 23                                                                                                                                 |
| HH        | 17            | Hour with trailing zero from 00 to 23                                                                                                             |
| h         | 5             | Hour from 0 to 12                                                                                                                                 |
| hh        | 05            | Hour with trailing zero from 00 to 12                                                                                                             |
| k         | 17            | Hour from 1 to 24                                                                                                                                 |
| kk        | 17            | Hour with trailing zero from 01 to 24                                                                                                             |
| m         | 4             | Minute from 0 to 59                                                                                                                               |
| mm        | 04            | Minute with trailing zero from 00 to 59                                                                                                           |
| a         | pm            | Meridiem am/pm                                                                                                                                    |
| A         | PM            | Meridiem AM/PM                                                                                                                                    |
| s         | 5             | Second from 0 to 59                                                                                                                               |
| ss        | 05            | Second with trailing zero from 00 to 59                                                                                                           |
| S         | 0             | Second tenth                                                                                                                                      |
| SS        | 08            | Second hundredth (on 2 digits with trailing zero)                                                                                                 |
| SSS       | 084           | Millisecond (on 3 digits with trailing zeros)                                                                                                     |
| SSSS      | 0845          | Second ten thousandth (on 4 digits with trailing zeros)                                                                                           |
| SSSSS     | 08451         | Second hundred thousandth (on 5 digits with trailing zeros)                                                                                       |
| SSSSSS    | 084512        | Microsecond (on 6 digits with trailing zeros)                                                                                                     |
| SSSSSSS   | 0845120       | Second ten millionth (on 7 digits with trailing zeros)                                                                                            |
| SSSSSSSS  | 08451200      | Second hundred millionth (on 8 digits with trailing zeros)                                                                                        |
| SSSSSSSSS | 084512000     | Nanosecond (on 9 digits with trailing zeros)                                                                                                      |
| M         | 1             | Month from 1 to 12                                                                                                                                |
| MM        | 01            | Month with trailing zero from 01 to 12                                                                                                            |
| MMM       | Jan           | Short month name, translatable                                                                                                                    |
| MMMM      | January       | Month name, translatable                                                                                                                          |
| Mo        | 1st           | Month with ordinal suffix from 1st to 12th, translatable                                                                                          |
| Q         | 1             | Quarter from 1 to 4                                                                                                                               |
| Qo        | 1st           | Quarter with ordinal suffix from 1st to 4th, translatable                                                                                         |
| G         | 2017          | ISO week year (see ISO week date)                                                                                                                 |
| GG        | 2017          | ISO week year (on 2 digits with trailing zero)                                                                                                    |
| GGG       | 2017          | ISO week year (on 3 digits with trailing zeros)                                                                                                   |
| GGGG      | 2017          | ISO week year (on 4 digits with trailing zeros)                                                                                                   |
| GGGGG     | 02017         | ISO week year (on 5 digits with trailing zeros)                                                                                                   |
| g         | 2017          | Week year according to locale settings, translatable                                                                                              |
| gg        | 2017          | Week year according to locale settings (on 2 digits with trailing zero), translatable                                                             |
| ggg       | 2017          | Week year according to locale settings (on 3 digits with trailing zeros), translatable                                                            |
| gggg      | 2017          | Week year according to locale settings (on 4 digits with trailing zeros), translatable                                                            |
| ggggg     | 02017         | Week year according to locale settings (on 5 digits with trailing zeros), translatable                                                            |
| W         | 1             | ISO week number in the year (see ISO week date)                                                                                                   |
| WW        | 01            | ISO week number in the year (on 2 digits with trailing zero)                                                                                      |
| Wo        | 1st           | ISO week number in the year with ordinal suffix, translatable                                                                                     |
| w         | 1             | Week number in the year according to locale settings, translatable                                                                                |
| ww        | 01            | Week number in the year according to locale settings (on 2 digits with trailing zero)                                                             |
| wo        | 1st           | Week number in the year according to locale settings with ordinal suffix, translatable                                                            |
| x         | 1483635845085 | Millisecond-precision timestamp (same as date.getTime() in JavaScript)                                                                            |
| X         | 1483635845    | Timestamp (number of seconds since 1970-01-01)                                                                                                    |
| Y         | 2017          | Full year from -9999 to 9999                                                                                                                      |
| YY        | 17            | Year on 2 digits from 00 to 99                                                                                                                    |
| YYYY      | 2017          | Year on 4 digits from 0000 to 9999                                                                                                                |
| YYYYY     | 02017         | Year on 5 digits from 00000 to 09999                                                                                                              |
| YYYYYY    | +002017       | Year on 5 digits with sign from -09999 to +09999                                                                                                  |
| z         | UTC           | Abbreviated time zone name                                                                                                                        |
| zz        | UTC           | Time zone name                                                                                                                                    |
| Z         | +00:00        | Time zone offset HH:mm                                                                                                                            |
| ZZ        | +0000         | Time zone offset HHmm                                                                                                                             |

Source: [Carbon Docs](https://carbon.nesbot.com/docs/#api-localization)
