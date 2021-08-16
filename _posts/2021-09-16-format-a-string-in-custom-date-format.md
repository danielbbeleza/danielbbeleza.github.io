---
layout: post
title: "Format a UTC date string into a custom date format"
---

Recently I had ran into a task of converting a simple UTC date into a string with a custom format.

This seemed (and actually is) such a simple task, but despite that I took longer than expected to solve this without depending on other dependencies then default Java ones.

### Problem

When receiving a UTC date string - e.g. `2021-05-21T00:00:00Z` - convert it to the following formats:

1. `dd-MM-yyyy` - if date is from one of the past years
2. `dd MMMM` (complete month name) - if date is from the current year

Here's how I solved it:

First, we need to parse the date and create an instance of `Date` so we can manipulate the data easier.

```
val defaultDateFormatter = SimpleDateFormat("yyyy-MM-dd", Locale.getDefault()) 

val parsedDate = defaultDateFormatter.parse(dateToParse)
```

Secondly, we need to format the parsed date already in `Date` type, by calling the `DateFormat.format(Date)` function.

```
val customDateFormatter = SimpleDateFormat("dd-MM-yyyy", Locale.getDefault())
val formattedDate = customDateFormatter.format(parsedDate)
```

Finally, grouping both steps this would be the final result:
```
fun parseDateIntoPastYearFormat(dateToParse: String): String {
```
