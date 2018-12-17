# XEN-L006: Nodes addition

The `xod/uart` library has the `print` node. This node "Writes a string bytes per byte into UART.". Also `print` writes bytes for the `\r`, `\n` escape sequences. Obviously the `read` node should be added to the `xod/uart` library. 

On a pulse or true/false bool state, the `read` node should output accumulated string or a group of strings from a UART byte stream. 

## List of nodes

### accumulate-line

Utility?
The target library is under consideration

Accumulates a string from a stream of characters by appending each new character to the end of the string until the end of the line escape sequence if found. Drops the carriage return escape sequence if it is found

- [in] CHAR :: Byte - A new character to be pushed to the end of the string line
- [in] PUSH :: Pulse - Push new character
- [in] RST :: Pulse - Empty the accumulated string line and start over

- [out] LINE :: String - Accumulated line
- [out] LINE :: Pulse - Fires on a new accumulated line

### read

`xod/uart` 

Streams string lines from UART

- [in] UART :: uart - An UART object
- [in] READ :: Pulse - Triggers read of a string line ???
- [in] READ :: Bool - The true value turns on the stream of the string lines ???

- [out] LINE :: String - String line that is read ???
- [OUT] UPD :: Pulse - Fires if a new line is read ???

