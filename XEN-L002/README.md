# XEN-L002: Datetime library

XOD should provide a library which operates with the concept of date and time.
Main library targets are:

- to make a single custom type `datetime`. It contains date and time values in XOD.
- to make a set of nodes, which a user can use to make mathematic operations with date and time type.

Let the library be `xod/datetime`.

## Internal Representation

### Datetime type

To store time and date values the "Unix time" or "POSIX time" is used.
Time and date are stored as a single scalar real number (unsigned 32 bytes integer) which represents the number of seconds that have passed since the beginning of 00:00:00 UTC Thursday, 1 January 1970.

```cpp
using Type = uint32_t;
Type seconds;
```

## Datetime Nodes

### datetime

Constructs a datetime value from a year, month, day, hour, minute, and second

- [in] YEAR :: Number — year value in range [1970, 2038]
- [in] MON :: Number — month value in range [1, 12] 
- [in] DAY :: Number — days value in range [1, 28-31]
- [in] HOUR :: Number — hours value in range [0, 23]
- [in] MIN :: Number — minutes value in range [0, 59] 
- [in] SEC :: Number — seconds value in range [0, 59]

- [out] :: datetime

### datetime-unpack

Destructs a datetime value into a year, month, day, weekday, hour, minute, and second 

- [in] :: datetime

- [out] YEAR :: Number — year value in range [1970, 2038]
- [out] MON :: Number — month value in range [1, 12] 
- [out] DAY :: Number — days value in range [1, 28-31]
- [out] WD :: Number — day of the week value in range [1, 7]. Count starts from Monday 
- [out] HOUR :: Number — hours value in range [0, 23]
- [out] MIN :: Number — minutes value in range [0, 59] 
- [out] SEC :: Number — seconds value in range [0, 59]


### add-seconds

Adds seconds to a datetime

- [in] :: datetime 
- [in] T :: Number - seconds to add. A negative value rewinds datetime back.

- [out] :: datetime

### diff-seconds

Calculates the difference between two datetimes in seconds

- [in] IN1 :: datetime
- [in] IN2 :: datetime

- [out] :: Number - difference in seconds

### am-pm

Changes format of hours from 24-hours to 12-hours 

- [in] 24H :: Number - hours value in range [0,23]

- [out] 12H :: Number - hours value in range [1, 12]
- [out] AM :: Boolean - outputs true from midnight to noon and false from noon to the end of the day

### format-timestamp

Transforms a datetime into a string timestamp in the form "2018-03-25 23:35:04"

- [in] :: datetime - a datetime value

- [out] :: String - formated timestamp

### pad-with-zeroes

`xod/core`

Transforms a number into a string and adds zeroes to the beginning of the string until it is W-sized. Ignores a fractional part of the value and a sign. If the width of a string for a number is greater than the specified W value, node produces a string with a untransformed number

- [in] :: Number - number to format
- [in] W :: Number - width of string

- [out] :: String - formated value
