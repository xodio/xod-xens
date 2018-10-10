---
status: closed
champion: https://xod.io/users/gabbapeople
issue: https://github.com/xodio/xod/pull/1436
---

# XEN-L002: Datetime library

XOD should provide a library which operates with the concept of date and time.
Main library purposes are:

- to make a single custom type `datetime`. It contains date and time values in XOD.
- to make a set of nodes, which a user can use to make mathematic operations with date and time type.

Let the library be `xod/datetime`.

## Internal Representation

To store time and date values the "Unix time" or "POSIX time" is used.
Time and date are stored as a single scalar real number (unsigned 32 bytes integer) which represents the number of seconds that have passed since the beginning of 00:00:00 UTC Thursday, 1 January 1970.

```cpp
using Type = uint32_t;
Type seconds;
```

## Datetime Nodes

### datetime

Constructs a datetime value from a year, month, day, hour, minute, and second

- [in] YEAR :: Number = 1970 — Year value in range [1970, 2105]
- [in] MON :: Number = 1 — Month value in range [1, 12] 
- [in] DAY :: Number = 1 — Days value in range [1, 28-31]
- [in] HOUR :: Number — Hours value in range [0, 23]
- [in] MIN :: Number — Minutes value in range [0, 59] 
- [in] SEC :: Number — Seconds value in range [0, 59]

- [out] :: datetime

### unpack-datetime

Destructs a datetime value into a year, month, day, weekday, hour, minute, and second 

- [in] :: datetime

- [out] YEAR :: Number — Year value in range [1970, 2105]
- [out] MON :: Number — Month value in range [1, 12] 
- [out] DAY :: Number — Days value in range [1, 28-31]
- [out] WD :: Number — Day of the week value in range [1, 7]. Count starts from Monday 
- [out] HOUR :: Number — Hours value in range [0, 23]
- [out] MIN :: Number — Minutes value in range [0, 59] 
- [out] SEC :: Number — Seconds value in range [0, 59]

### add-seconds

Adds seconds to a datetime

- [in] :: datetime 
- [in] T :: Number - Seconds to add. A negative value rewinds datetime back.

- [out] :: datetime

### diff-seconds

Calculates the difference between two datetimes in seconds

- [in] :: datetime
- [in] :: datetime

- [out] :: Number - Difference in seconds. It is negative if IN1 precedes IN2

### am-pm

Changes format of hours from 24-hours to 12-hours 

- [in] 24H :: Number - Hours value in range [0,23]

- [out] 12H :: Number - Hours value in range [1, 12]
- [out] AM :: Boolean - Outputs true from midnight to noon and false from noon to the end of the day

### format-timestamp

Transforms a datetime into a string timestamp in the form "2018-03-25 23:35:04"

- [in] :: datetime

- [out] :: String

### pad-with-zeroes

`xod/core`

Transforms a number into a string and adds zeroes to the beginning of the string until it is W-sized. Ignores a fractional part of the value and a sign. If the width of a string for a number is greater than the specified W value, node produces a string with the untransformed number

- [in] :: Number
- [in] W :: Number

- [out] :: String
