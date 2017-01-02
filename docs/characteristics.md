# Bluetooth BLE GATT services and characteristics

Services have been identified by using the official GATT services registry (https://www.bluetooth.com/specifications/gatt/services), except for `0xFE7B` which is assumed to be the Onyx device service.  Information has been read via `gatttool` on Linux and `LightBlue Explorer` on an iPhone.

## Service 0000180a-0000-1000-8000-00805f9b34fb (0x180A)

[Device information service.](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.service.device_information.xml)

### Characteristic 00002a29-0000-1000-8000-00805f9b34fb (0x2A29)

**Characteristic:** Manufacturer Name String  
**Properties:** Read  
**Type:** string

Should read "Orion" (`0x4F72696F6E00`).  Orion Labs manufactures and sells the Onyx.

### Characteristic 00002a24-0000-1000-8000-00805f9b34fb (0x2A24)

**Characteristic:** Model Number String  
**Properties:** Broadcast, Read  
**Type:** string

Should read "ONYX2" (`0x4F4E59583200`).  The "Oynx" sold by Orion Labs is the second generation of the hardware.

### Characteristic 00002a25-0000-1000-8000-00805f9b34fb (0x2A25)

**Characteristic:** Serial Number String  
**Properties:** Broadcast, Read  
**Type:** string

Should read the serial number printed on the back of the device: V5C1XXXX.

### Characteristic 00002a27-0000-1000-8000-00805f9b34fb (0x2A27)

**Characteristic:** Hardware Revision String  
**Properties:** Read  
**Type:** string

Should read the hardware revision of the Onyx: "1.5.0" (`0x312E352E3000`) on my Onyx.

### Characteristic 00002a26-0000-1000-8000-00805f9b34fb (0x2A26)

**Characteristic:** Firmware Revision String  
**Properties:** Read  
**Type:** string

Should read "null" (`0x6E756C6C00`).

### Characteristic 00002a28-0000-1000-8000-00805f9b34fb (0x2A28)

**Characteristic:** Software Revision String  
**Properties:** Read  
**Type:** string

Should read the currently running firmware on the Onyx.

### Characteristic 00002a23-0000-1000-8000-00805f9b34fb (0x2A23)

**Characteristic:** System ID  
**Properties:** Read

### Characteristic 00002a2a-0000-1000-8000-00805f9b34fb (0x2A2A)

**Characteristic:** IEEE 11073-20601 Regulatory  
**Properties:** Read

### Characteristic 0000a200-0000-1000-8000-00805f9b34fb (0xA200)

**Characteristic:** Unknown  
**Properties:** Read

## Service 00001800-0000-1000-8000-00805f9b34fb (0x1800)

[Generic access service.](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.service.generic_access.xml)

### Characteristic 00002a00-0000-1000-8000-00805f9b34fb (0x2A00)

**Characteristic:** Device Name  
**Properties:** Read  
**Type:** string

Will appear in the format of "ONYX-XXXX", with XXXX containing the last four characters of the serial number.  Useful for differentiating multiple units in the same physical space.

### Characteristic 00002a01-0000-1000-8000-00805f9b34fb (0x2A01)

**Characteristic:** Appearance  
**Properties:** Read  
**Type:** int16

Will read 0x0000.  This is the undefined device apperance.

### Characteristic 00002a02-0000-1000-8000-00805f9b34fb (0x2A02)

**Characteristic:** Peripheral Privacy Flag  
**Properties:** Read, Write

### Characteristic 00002a03-0000-1000-8000-00805f9b34fb (0x2A03)

**Characteristic:** Reconnection Address  
**Properties:** Write

### Characteristic 00002a04-0000-1000-8000-00805f9b34fb (0x2A04)

**Characteristic:** Peripheral Preferred Connection Parameters  
**Properties:** Read, Write

## Service 00001801-0000-1000-8000-00805f9b34fb (0x1801)

[Generic attribute service.](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.service.generic_attribute.xml)

### Characteristic 00002a05-0000-1000-8000-00805f9b34fb

**Characteristic:** Service Changed  
**Properties:** Read, Notify

## Service 0000180f-0000-1000-8000-00805f9b34fb (0x180F)

[Battery service.](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.service.battery_service.xml)

### Characteristic 00002a19-0000-1000-8000-00805f9b34fb (0x2A19)

**Characteristic:** Battery Level  
**Properties:** Read, Notify  
**Type:** int8

Returns a value between 0% (`0x00`) and 100% (`0x64`).

## Service 00001804-0000-1000-8000-00805f9b34fb (0x1804)

[Tx power service.](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.service.tx_power.xml)

### Characteristic 00002a07-0000-1000-8000-00805f9b34fb (0x2A07)

**Characteristic:** Tx Power Level  
**Properties:** Read

## Service 0000fe7b-0000-1000-8000-00805f9b34fb (0xFE7B)

Onyx service.

### Characteristic 0000a000-0000-1000-8000-00805f9b34fb (0xA000)

**Characteristic:** Device State  
**Properties:** Read, Notify  
**Type:** int8

*Unsure, currently returns 0x00.*

### Characteristic 0000a001-0000-1000-8000-00805f9b34fb (0xA001)

**Characteristic:** Mute State  
**Properties:** Read, Notify  
**Type:** int8

Returns `0x00` if the Oynx is not muted and `0x01` if the Oynx is muted.  The Oynx is muted by rotating its face.

### Characteristic 0000a003-0000-1000-8000-00805f9b34fb (0xA003)

**Characteristic:** Charging State  
**Properties:** Read, Notify  
**Type:** int8

Returns `0x00` if the Onyx is not plugged in and is discharging, `0x01` if the Oynx is plugged in and fully charged, and `0x02` if the Onyx is plugged in and charging.  This value is populated a short while after the charging lights on the front of the unit display.

### Characteristic 0000a007-0000-1000-8000-00805f9b34fb (0xA007)

**Characteristic:** "James Bonding"  
**Properties:** Read

### Characteristic 0000a00a-0000-1000-8000-00805f9b34fb (0xA00A)

**Characteristic:** Audio Transmit State  
**Properties:** Read, Notify  
**Type:** int8

Returns `0x00` if the Oynx is not transmitting audio and `0x01` if the Onyx is transmitting audio (has audio available on the buffer).

### Characteristic 0000a10f-0000-1000-8000-00805f9b34fb (0xA10F)

**Characteristic:** Log Flags  
**Properties:** Read, Write

### Characteristic 0000a110-0000-1000-8000-00805f9b34fb (0xA110)

**Characteristic:** Orion Client Error  
**Properties:** Read, Write  
**Type:** int32

*Read and write the orion client error register, value is 0x00000000 by default and will remain at any value written.*

### Characteristic 0000a111-0000-1000-8000-00805f9b34fb (0xA111)

**Characteristic:** Orion Audio Prequeue Length  
**Properties:** Read, Write, Notify  
**Type:** int8

Read and write the prequeue length, value is 10 (`0x0A`) by default and will remain at any value written.

### Characteristic 0000a112-0000-1000-8000-00805f9b34fb (0xA112)

**Characteristic:** Orion Console  
**Properties:** Write

### Characteristic 0000a113-0000-1000-8000-00805f9b34fb (0xA113)

**Characteristic:** Battery Status  
**Properties:** Read, Notify

### Characteristic 0000a114-0000-1000-8000-00805f9b34fb (0xA114)

**Characteristic:** PTT Source Event  
**Properties:** Read, Notify  
**Type:** int8

Returns `0x01` if the push-to-talk button on the Oynx was pressed, initiating the audio transmit event, and no bytes if the button was released.

### Characteristic 0000a115-0000-1000-8000-00805f9b34fb (0xA115)

**Characteristic:** PTT Sink Event  
**Properties:** Write  
**Type:** int8

Write `0x01` when transmitting audio to the Onyx and `0x00` when the transmission has completed.

### Characteristic 0000ae01-0000-1000-8000-00805f9b34fb (0xAE01)

**Characteristic:** Voyager Log Sink  
**Properties:** Read, Notify

### Characteristic 0000af00-0000-1000-8000-00805f9b34fb (0xAF00)

**Characteristic:** FW Update Info  
**Properties:** Read, Write

### Characteristic 0000af01-0000-1000-8000-00805f9b34fb (0xAF01)

**Characteristic:** FW Update Request  
**Properties:** Read, Notify

### Characteristic 0000af02-0000-1000-8000-00805f9b34fb (0xAF02)

**Characteristic:** FW Update Data  
**Properties:** Read, Write without response, Write, Extended properties

### Characteristic 0000b001-0000-1000-8000-00805f9b34fb (0xB001)

**Characteristic:** Orion App Notification  
**Properties:** Read, Write  
**Type:** byte[20]

### Characteristic 0000b002-0000-1000-8000-00805f9b34fb (0xB002)

**Characteristic:** Bluetooth API Device State  
**Properties:** Read, Notify  
**Type:** int32

Returns four bytes: unknown, unknown, charging state, and mute state (e.g. `0x02000201`).

### Characteristic f2076886-d8f4-4246-8d81-c6b155e9fc80

**Characteristic:** Microphone audio buffer 1  
**Properties:** Notify  
**Type:** byte[20]

First buffer of data sent to the BLE client from the Oynx when recording on the microphone.  If any more data is available it will come from the second buffer.

### Characteristic f2076886-d8f4-4246-8d81-c6b155e9fc81

**Characteristic:** Microphone audio buffer 2  
**Properties:** Notify  
**Type:** byte[20]

Second buffer of data sent to the BLE client from the Oynx when recording on the microphone.  If any more data is available it will come from the third buffer.

### Characteristic f2076886-d8f4-4246-8d81-c6b155e9fc82

**Characteristic:** Microphone audio buffer 3  
**Properties:** Notify  
**Type:** byte[20]

Third buffer of data sent to the BLE client from the Oynx when recording on the microphone.  If any more data is available it will come from the fourth buffer.

### Characteristic f2076886-d8f4-4246-8d81-c6b155e9fc83

**Characteristic:** Microphone audio buffer 4  
**Properties:** Notify  
**Type:** byte[20]

Fourth buffer of data sent to the BLE client from the Oynx when recording on the microphone.  If any more data is available it will come from the first buffer.

### Characteristic 777445ea-22f0-4254-b206-66aef2ec7540

**Characteristic:** Speaker audio buffer 1  
**Properties:** Write without response, Write, Extended properties  
**Type:** byte[20]

First buffer of data sent from the BLE client to play over the Onyx speaker.  If any more data is available it will write to the second buffer.

### Characteristic 777445ea-22f0-4254-b206-66aef2ec7541

**Characteristic:** Speaker audio buffer 2  
**Properties:** Write without response, Write, Extended properties  
**Type:** byte[20]

Second buffer of data sent from the BLE client to play over the Onyx speaker.  If any more data is available it will write to the third buffer.

### Characteristic 777445ea-22f0-4254-b206-66aef2ec7542

**Characteristic:** Speaker audio buffer 3  
**Properties:** Write without response, Write, Extended properties  
**Type:** byte[20]

Third buffer of data sent from the BLE client to play over the Onyx speaker.  If any more data is available it will write to the fourth buffer.

### Characteristic 777445ea-22f0-4254-b206-66aef2ec7543

**Characteristic:** Speaker audio buffer 4  
**Properties:** Write without response, Write, Extended properties  
**Type:** byte[20]

Fourth buffer of data sent from the BLE client to play over the Onyx speaker.  If any more data is available it will write to the first buffer.