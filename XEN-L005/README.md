---
status: draft
champion: https://xod.io/users/nkrkv
---

# Sharp Infrared Range Meters Library

Sharp infrared range meters with the analog interface are well-known sensors in the Arduino world. They are so common that deserve a library under `xod-dev`, but proprietary enough to be extracted out of `xod/common-hardware`.

Let’s move the nodes related to these sensors into a library `xod-dev/sharp-irm`.

The sensors are simple enough and provide only one function (give me the distance) not to bother with the device/actions/quickstart pattern. Having only the quick start nodes looks OK.

The current implementation lacks analog reference voltage adjustment and has it hard-coded to 5 volts which effectively make the sensor readings wrong on 3.3 and direct-battery boards. This issue can be addressed while the extraction.

## Library description

Nodes to read analog infrared range meters by Sharp (GP2Y0A) and convert the signal to distance values.

## Nodes

### gp2y0a02-range-meter

Reads Sharp infrared range meter GP2Y0A02YK0F (the one with 20…150 cm range).

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  | PORT | port    | A0      | Board port number the sensor is connected to
| in  | AVcc | number  | 5       | Analog voltage reference, i.e., the voltage level corresponding to the 1.0 value of an analog read. Usually 5 or 3.3 volts matching the board power voltage
| in  | UPD  | pulse   | Continuously | Triggers an update, that is, rereads values
| out | Dm   | number  |         | Measured distance in meters. Trustworthy only for distances in [0.3, 1.5] meters range. Returns wrong values if an object is too close to the sensor.
| out | OK   | pulse   |         | Fires when the reading completes successfully
| out | ERR  | pulse   |         | Fires if reading failed. For example, in the case of the wrong port number

### gp2y0a21-range-meter

Reads Sharp infrared range meter GP2Y0A21YK0F (the one with 10…80 cm range).

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  | PORT | port    | A0      | Board port number the sensor is connected to
| in  | AVcc | number  | 5       | Analog voltage reference, i.e., the voltage level corresponding to the 1.0 value of an analog read. Usually 5 or 3.3 volts matching the board power voltage
| in  | UPD  | pulse   | Continuously | Triggers an update, that is, rereads values
| out | Dm   | number  |         | Measured distance in meters. Trustworthy only for distances in [0.1, 0.8] meters range. Returns wrong values if an object is too close to the sensor.
| out | OK   | pulse   |         | Fires when the reading completes successfully
| out | ERR  | pulse   |         | Fires if reading failed. For example, in the case of the wrong port number

### gp2y0a41-range-meter

Reads Sharp infrared range meter GP2Y0A41SK0F (the one with 4…30 cm range).

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  | PORT | port    | A0      | Board port number the sensor is connected to
| in  | AVcc | number  | 5       | Analog voltage reference, i.e., the voltage level corresponding to the 1.0 value of an analog read. Usually 5 or 3.3 volts matching the board power voltage
| in  | UPD  | pulse   | Continuously | Triggers an update, that is, rereads values
| out | Dm   | number  |         | Measured distance in meters. Trustworthy only for distances in [0.04, 0.3] meters range. Returns wrong values if an object is too close to the sensor.
| out | OK   | pulse   |         | Fires when the reading completes successfully
| out | ERR  | pulse   |         | Fires if reading failed. For example, in the case of the wrong port number

## Backward compatibility

The existing nodes in `common-hardware` might be simply deprecated. The new nodes are a drop-in replacement.
