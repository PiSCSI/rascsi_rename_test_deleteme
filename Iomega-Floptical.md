# SCSI Details for Iomega Floptical Drive

Report from TattleTech 2.59 for the Iomega Floptical 21MB/1.44MB SCSI drive (also sold under the "Insite" brand).

Report taken on a Mac Classic II running OS 7.5.3, and v4.04 of the Iomega Floptical Driver.

I don't have a report of what it looks like with a 21MB disk in the drive because I haven't got one yet.

## Usage with PiSCSI

As of PiSCSI v21.11.01, an Iomega Floptical 1.44MB named drive profile comes standard with the package which can be used on the fly from the Web Interface. You can also use the -n option with scsictl on the command line to set up a simulated Floptical device with PiSCSI.

```
$ scsictl -i 6 -c attach -t scrm -n "IOMEGA:Io20S         *F:PP33" -f floppy_image.hdr
```

The Floptical driver seems to only recognize an image if it is 1474560 bytes long. An existing HFS formatted image can be adjusted to fit this size.

```
$ sudo truncate --size 1474560 floppy_image.hdr
```

For convenience, it is recommended to give the floppy image files the file ending 'hdr' in order for PiSCSI to auto-detect them as removable disk images.

What works:
* Disk images can be read from and written to. 
* Applications and be launched and used off the image. 
* Disks ejected by dragging them to the trash can, and new ones inserted via PiSCSI.

Current known limitations:
* The inability to format disk images. An error is thrown when attempting to initialize. As a workaround, use existing good HFS formatted images or a [blank 1.44MB image](files/Blank_Floppy_HFS_1_44MB.hdr).
* Automatic ejections triggered by Mac OS (f.e. multi-disk installers) aren't recognized by PiSCSI. Manual ejection in PiSCSI are not recognized by Mac OS.
* Booting from a floppy disk. I have tried modifying existing boot disks and add the Floptical driver to them (e.g. Mac OS 8.1 Disk Tools) with a Power Mac 8600. The machine stalls for a minute on a grey screen attempting to boot off the Floptical device, but ultimately fails to recognize it.

## Report with no disk in drive

```text
� SCSI Device# = 4
   � Device Status = Device Connected
   � Name = [NA]
   � Driver# = -37
   � Type = 0   (Direct Access)
   � Capacity = [Unknown]
   � Manufacturer = IOMEGA
   � Product = Io20S         *F
   � Revision = PP33
   � ROM Revision = $000000D9B0273C20
   � Device Attributes :
      + Removable Media = Yes
      + ANSI Compliant = Yes  (SCSI 2)
      + ECMA-111 Compliant = No
      + ISO IS 9316 Compliant = No
      + Wide SCSI (32-bit Transfers) = No
      + Wide SCSI (16-bit Transfers) = No
      + Fast SCSI (Synchronous Transfers) = No  (5MB/sec max)
      + Linked Commands = No
      + Tagged Command Queuing = No
      + Soft Reset = No
      + Relative Addressing = No
      + Terminate I/O Process = No
      + Asynchronous Event Notification = [NA]
      + Response Data Format = 2
```
## Report with 1.44MB disk in drive

```text
� SCSI Device# = 4
   � Device Status = Device Connected
   � Name = untitled
   � Driver# = -37
   � Type = 0   (Direct Access)
   � Capacity = 1,474,048 Bytes  (1.4 MB)
   � Manufacturer = IOMEGA
   � Product = Io20S         *F
   � Revision = PP33
   � ROM Revision = $000000D9B0273C20
   � Device Attributes :
      + Removable Media = Yes
      + ANSI Compliant = Yes  (SCSI 2)
      + ECMA-111 Compliant = No
      + ISO IS 9316 Compliant = No
      + Wide SCSI (32-bit Transfers) = No
      + Wide SCSI (16-bit Transfers) = No
      + Fast SCSI (Synchronous Transfers) = No  (5MB/sec max)
      + Linked Commands = No
      + Tagged Command Queuing = No
      + Soft Reset = No
      + Relative Addressing = No
      + Terminate I/O Process = No
      + Asynchronous Event Notification = [NA]
      + Response Data Format = 2
```

## Driver

MacOS 6+ driver can be found on the [driver page at vintageapple.org](https://vintageapple.org/macdrivers/disk.shtml).

GS/OS driver can be found on [MacGUI.com](https://macgui.com/downloads/?file_id=11793).

## Other Notes

Some models have automatic eject (my model Io20S rev PP33 does), but not all.

The Mac Classic II tested with could not boot from the drive. The machine would boot using the hard drive regardless of if there was a disk in the Floptical drive or not.

The drive cannot read 720KB PC floppies nor 800KB Mac GCR floppies. Iomega was reportedly working on a version that could (for the PowerBook) but it never materialized.

If Iomega Zip/Jaz utils are installed they will recognize the drive as an Iomega device but they can't do much with it.


