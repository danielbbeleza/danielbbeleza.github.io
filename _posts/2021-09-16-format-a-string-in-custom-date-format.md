---
layout: post
title: "Format a UTC date string into a custom date format"
---

Recently I had ran into a task of converting a simple UTC date into a string with a custom format.

This seemed (and actually is) such a simple task, but despite that I took longer than expected to solve this without depending on other dependencies then default Java ones.

## Problem

When receiving a UTC date string - e.g. `2021-05-21T00:00:00Z` - convert it to the following formats:

1. `dd-MM-yyyy` - if date is from one of the past years
2. `dd MMMM` (complete month name) - if date is from the current year

Here's how I solved:

## 1 - Date format `dd-MM-yyyy`

As an example, this is our use case

GIVEN, we have this utc string date `2021-05-21T00:00:00Z`,
WHEN, we parse the string,
THEN, return `21-05-2021` 


### Solution

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
val defaultDateFormatter = SimpleDateFormat("yyyy-MM-dd", Locale.getDefault()) 

val parsedDate = defaultDateFormatter.parse(dateToParse)

val customDateFormatter = SimpleDateFormat("dd-MM-yyyy", Locale.getDefault())

val formattedDate = customDateFormatter.format(parsedDate)
```

## 2 - Date format `dd MMMM`

Using the same example, this is our use case for this similar but different problem:

GIVEN, we have this utc string date `2021-05-21T00:00:00Z`,
WHEN, we parse the string,
THEN, return `21 May` 

This solution will be very similar to the previous one. The only thing that changes is the `SimpleDateFormat` first `String` parameter, that refers to our intended date pattern.

```
val defaultDateFormatter = SimpleDateFormat("yyyy-MM-dd", Locale.getDefault()) 

val parsedDate = defaultDateFormatter.parse(dateToParse)

val customDateFormatter = SimpleDateFormat("dd MMMM", Locale.getDefault()) // This line is our only change

val formattedDate = customDateFormatter.format(parsedDate)
```

## Conclusion

This is something very simple to do, but it seems there are a lot of other solutions in the internet, using other dependencies (most of them that or not maintained anymore), or using the most recent Android APIs that require you to support a relatively high SDK version.

These solutions also work for any other date types you may want. For more date formats just check [Java official documentation](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html).

Let me know if you have any question or suggestion to this small article.

Will be really happy to help!
