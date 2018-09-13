# XEN-L005: Nodes addition

Specific useful nodes were created during the creation of the "uart-example" guide. Suggest to add them into the `xod-core` library.

## List of nodes

### throttle

Slows down a pulse frequency. Passes a pulse through no more than once every T seconds

- [in] :: Pulse 
- [in] T :: Number = 0 — A time between pulses in seconds 

- [out] :: Pulse

### parse-number

Transforms a string into a number

- [in] :: String

- [out] :: Number

### parse-tabular

Splits the incoming string line into parts depending on delimiter character. Outputs the specified part of string line

- [in] STR :: String - A string line to parse
- [in] D :: Byte - A delimiter character 
- [in] IDX :: Number - A part number of the string line to output. The numbering starts with 0

- [out] :: String - A parsed part of a string line

### round-fraction

Rounds value to decimal places

- [in] :: Number 
- [in] DIG :: Number - Digits after dot

- [out] :: Number 
