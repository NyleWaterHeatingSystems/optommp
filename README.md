# optommp

Working with Python 3.5. To install 

```
sudo pip3 install git+https://github.com/NyleWaterHeatingSystems/optommp.git
```

---

Python toolkit to access data on Opto 22 _groov_ EPIC using the OptoMMP protocol. See [OptoMMP Protocol Guide](https://www.opto22.com/support/resources-tools/documents/1465-optommp-protocol-guide "opto22 support") (form 1465) and the Opto 22 [developer site for more details](http://developer.opto22.com/). Hosted on the [Python Package Index (PyPI)](https://pypi.org/project/optommp/).

To use this package do `sudo pip install optommp` to get the package from PyPI, `import optommp` at the top of your \*.py Python script, and then use the following functions to interface with your device(s):


* **O22MMP(host)** - Initialize an Opto22 Memory Mapped object residing at 'host' address.

	* **O22MMP()** - Default to `localhost` / `127.0.0.1`

<details><summary>Misc. Functions</summary>

* **ReadRawOffset(offset, size, data_type)** - Rads the raw address at `offset` collecting `size` bytes and using `data_type` formatting to unpack it.

* **LastError()** - Returns the last error response code.

* **UnitDescription()** - Returns the device unit description. For example, `GRV-EPIC-PR1`

* **FirmwareVersion()** - Returns the device firmware version. For example, 'R1.1a'

</details>
<details><summary>Ethernet Status Access Functions</summary>

* **IPAddressE0()** - Returns the IP address associated with Ethernet 0 on the controller.

* **MACAddressE0()** - Returns the MAC address associated with Ethernet 0 on the controller.

* **IPAddressE1()** - Returns the IP address associated with Ethernet 1 on the controller.

* **MACAddressE1()** - Returns the MAC address associated with Ethernet 1 on the controller.

</details>
<details><summary>Analog & Digital I/O Access Functions</summary>

* **SetDigitalPointState(module, channel, state)** - The HD digital output at `channel` on `module` will be toggled to `state`, which should be either 1 or 0. Returns status code.

* **GetDigitalPointState(module, channel)** - The state of the HD digital output at `channel` on `module` will be fetched. Returns state either 1 or 0.


* **GetAnalogPointValue(module, channel)** - Return the current float value of the analog I/O installed at `channel` on `module`.

* **SetAnalogPointValue(module, channel, value)** - Set the analog I/O installed at `channel` on `module` to be `value`. `value` should be a float.

* **GetAnalogPointMin(module, channel)** - Return the minimum float value of the analog I/O installed at `channel` on `module`.

* **GetAnalogPointMax(module, channel)** - Return the maximum float value of the analog I/O installed at `channel` on `module`.

</details>
<details><summary>ScratchPad Area Access Functions</summary>

* **GetScratchPadIntegerArea(index)** - Returns the `index`<sup>th</sup> scratch pad integer.

* **SetScratchPadIntegerArea(index, value)** - Sets the `index`<sup>th</sup> scratch pad integer to be `value`.

* **GetScratchPadFloatArea(index)** - Returns the `index`<sup>th</sup> scratch pad float.

* **SetScratchPadFloatArea(index, value)** - Sets the `index`<sup>th</sup> scratch pad float to be `value`.

* **GetScratchPadStringArea(index)** - Returns the `index`<sup>th</sup> scratch pad string.

* **SetScratchPadStringArea(index, data)** - Sets the `index`<sup>th</sup> scratch pad string to be `data`.

</details>
<details><summary>Internal Memory-Map Functions</summary>

* **UnpackReadResponse(data, data_type)** - Unpacks the string data from bytes 16-20 of a read response. Returns formatted data.<br>
	`data_type` --> struct format characters 'c', 'i', 'd', 'f', etc., or specifically 'FIRMWARE', 'IP', or 'MAC' for custom formatting, or 'NONE' for raw binary data.

* **UnpackWriteResponse(data)** - Unpacks the integer status code from bytes 4-8 of a write response. Returns int status.<br>

* **PackFloat(value)** - Packs floating point `vlaue` into a four-byte hexidecimal array.

* **PackInteger(value)** - Packs integer point `vlaue` into a four-byte hexidecimal array.


* **ReadBlock(address)** - Read value at memory location `address`. Relies on `BuidReadBlockRequest()`, wraps up `.send()` and `.recv()` methods. Returns unpacked string data.

* **WriteBlock(address, value)** - Write `value` into memory location `address`. Relies on `BuildWriteBlockRequest()`, wraps up `.send()` and `.recv()` methods. Returns int status.


* **BuildReadBlockRequest(dest, size)** - Build the read block request bytearray. Returns bytearray block.<br>
	This is an internally used utility method to build a read request. Client code isn't likely to need it.

* **BuildWriteBlockRequest(dest, value)** - Build the write block request bytearray. Returns bytearray block.<br>
	This is an internally used utility method to build a read request. Client code isn't likely to need it.

* **close()** - Closes the socket connection to the device. Call this before the end of the script.

</details>
