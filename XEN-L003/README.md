---
status: closed
champion: https://xod.io/users/gabbapeople
issue: https://github.com/xodio/xod/pull/1438
---

# XEN-L003: RTC Device Library

XOD should provide a library which includes nodes for hardware devices that operate time and date (RTC devices).
A user should be able to use most of RTC devices functions without leaving XOD environment.

Let the library be `xod-dev/ds-rtc`.

## Internal Representation

a custom type `rtc-device` for the DS1302/DS1307/DS3231 based breakout RTC boards.

```cpp
struct Type {
    TwoWire* wire;
    uint8_t addr;
};
```

## RTC Device Nodes

### rtc-device

Constructs a rtc-device value for a DS1302/DS1307/DS3231 RTC board

- [in] I2C :: i2c 
- [in] ADDR :: Byte = 68h — I²C address of the device 

- [out] DEV :: rtc-device

### unpack-rtc-device

Destructs an rtc-device value into its components

- [in] DEV :: rtc-device

- [out] I2C :: i2c 
- [out] ADDR :: Byte - I²C address of the device

### write

Writes a datetime value into the memory of a RTC device

- [in] DEV :: rtc-device
- [in] DT :: datetime - A datetime value to write 
- [in] UPD :: Pulse = On boot - Triggers a new write

- [out] DONE :: Pulse - Fires on a successful write
- [out] ERR :: Pulse - Fires if a write failed

### read

Reads a datetime value from a RTC device

- [in] DEV :: rtc-device
- [in] UPD :: Pulse = Never - Triggers a new read

- [out] DT :: datetime - The last datetime value read successfully. The default startup value is 1970-01-01 00:00:00
- [out] DONE :: Pulse - Fires on a successful read
- [out] ERR :: Pulse - Fires if a read faied

### rtc

Represents a real-time clock module based on a DS1302/DS1307/DS3231 chip. Use the node to track the current wall-clock time which was previously set in the module

- [in] I2C :: i2c 
- [in] ADDR :: Byte = 68h — I²C address of the device 

- [in] UPD :: Pulse = Never - Triggers a new read

- [out] DT :: datetime - A datetime value
- [out] DONE :: Pulse - Fires on a successful read
- [out] ERR :: Pulse - Fires if a read faied

