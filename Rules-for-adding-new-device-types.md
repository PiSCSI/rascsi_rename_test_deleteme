Before adding a new device type check that none of the existing types is appropriate.

Steps for adding a new device type:

1. Add the device type to the PbDeviceType enum of the protobuf definition in `rascsi_interface.proto`.
2. Add code for creating the device type to the DeviceFactory class in `devices/device_factory.cpp`.
3. Add the device type specific implementation in new .cpp/.h files located in the devices folder.
4. Ensure to initialize the device type with its device type properties and supported SCSI commands in the Init() method.
5. Verify that _scsictl -s_ reports the correct device type properties.
6. Update the manpages.

Devices have to be subclasses of PrimaryDevice or ModeSenseDevice. Only devices backed by image files may be subclasses of the StorageDevice class. See the implementations of the Host Services (SCHS) and the SCSI Printer (SCLP) for device implementations with low complexity.

## Clients

The Python based clients has class methods in the Common package for detecting device types that the backend supports, which are then exposed appropriately in the various front ends. See the RaCtlCmds class for details.

At the time of writing, the code detects three types of devices:
* Disk -- Any device that takes an image file as argument
* Removable -- Any device which can have image files inserted and ejected (overlap with the above)
* Peripheral -- Any device that does not match the above.

For most scenarios, the Python clients should not require any modification when new device types are added. However, testing the integration before releasing a stable version is strongly recommended.