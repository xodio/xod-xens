# XEN-L004: PN532 library

Some xoders may want to use RFID/NFC reader in their projects.
One of the most popular RFID/NFC readers are based on PN532 chip and there is
a library on GitHub for it.
Let's wrap the library and share it with the world.

Let it be `xod-dev/pn532-nfc`.

## Internal Representation

There will be two custom types:
1. `pn532-device` to store class instance
   ```cpp
    struct State {
        uint8_t mem[sizeof(Adafruit_PN532)];
        Adafruit_PN532* nfc;
    };
   ```
2. `nfc-uid` to store NFC TAG UID, which might be 4-7 bytes length
   ```cpp
    union Type {
      uint8_t items[7];
      struct {
          uint8_t i0;
          uint8_t i1;
          uint8_t i2;
          uint8_t i3;
          uint8_t i4;
          uint8_t i5;
          uint8_t i6;
          uint8_t i7;
      };
    };
   ```

## Project description
Support for RFID/NFC modules based on a PN532 chip.

## Nodes

### pn532-device
Constructs an instance of an RFID/NFC module, based on a PN532 chip.

- [in] IRQ :: Port — A port number used by the module to indicate that an NFC tag detected
- [out] DEV :: pn532-device

### init
Initializes RFID/NFC module

- [in] DEV :: pn532-device
- [in] INIT :: pulse = On Boot — Triggers initialization of the module
- [out] OK :: pulse — Fires on the successful initialization
- [out] ERR :: pulse — Fires if the initialization failed

### pair-tag
Pairs module with an NFC tag and reads the UID

- [in] DEV :: pn532-device
- [in] PAIR :: pulse = Never — Triggers pairing with an NFC tag
- [out] UID :: nfc-uid — The UID of the paired NFC tag
- [out] OK :: pulse — Fires on successful pairing
- [out] ERR :: pulse — Fires if there is no NFC tag

### read-page
Reads one page of a Mifare Ultralight NFC tag.
To read data from a tag it should be paired first (use `pair-tag`)

- [in] DEV :: pn532-device
- [in] PAGE :: number = 2 — A page number to read data from in range [0, 16]. Notice that first pages contains UID
- [in] READ :: pulse = Never — Trigger reading from an NFC tag
- [out] :: byte
- [out] :: byte
- [out] :: byte
- [out] :: byte
- [out] OK :: pulse — Fires on successful reading
- [out] ERR :: pulse — Fires on failed reading

### write-page
Writes data to the specified page of a Mifare Ultralight NFC tag.
To write data to a tag it should be paired first (use `pair-tag`)

- [in] DEV :: pn532-device
- [in] PAGE :: number = 2 — A page number to write data to in range [0, 16]. Notice that first pages contains UID
- [in] :: byte
- [in] :: byte
- [in] :: byte
- [in] :: byte
- [in] UPD :: pulse — Trigger writing to an NFC tag
- [out] OK :: pulse — Fires on successful writing
- [out] ERR :: pulse — Fires on failed writing

### nfc-scanner
A quick-start node which represents an RFID/NFC module.
Initializes the module and reads the UID of a detected card

- [in] IRQ :: port — A port number used by the module to indicate that an NFC tag detected
- [in] SCAN :: pulse = Continuously — Triggers scan for an NFC tag
- [out] UID :: nfc-uid — The UID of a readed NFC tag
- [out] TAG :: bool — True when the most recent scan detected an NFC tag
- [out] OK :: pulse — Fires on successful reading
- [out] ERR :: pulse — Fires if there is no NFC tag

### nfc-uid
Constructs the UID type from bytes.
If the UID is shorter than 7 bytes it begins from the first position
and the rest of bytes are equal to zero

- [in] :: byte
- [in] :: byte
- [in] :: byte
- [in] :: byte
- [in] :: byte
- [in] :: byte
- [in] :: byte
- [out] UID :: nfc-uid

### unpack-nfc-uid
Destructs the UID type to bytes
If the UID of the tag is longer than 7 bytes, then the first 7 bytes will be
here and the rest are cut off

- [in] UID :: nfc-uid
- [out] :: byte
- [out] :: byte
- [out] :: byte
- [out] :: byte
- [out] :: byte
- [out] :: byte
- [out] :: byte

### equal(nfc-uid)
Compares two UIDs

- [in] :: nfc-uid
- [in] :: nfc-uid
- [out] :: boolean
