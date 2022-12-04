# Overview
This page summarizes the emulated device supported by PiSCSI, with notes on compatibility and device drivers for various platforms.

# Device Types
Device|Key|Supported Platforms|Notes
---|---|---|---
Hard Disk Drive|SCHD|all|
CD/DVD Drive|SCCD|all|The [Apple CD-ROM drivers](https://github.com/piscsi/piscsi/wiki/Drive-Setup#Mounting_CD_ISO_or_MO_images) in combination with PiSCSI is known to lead to incompatibility with particular ISO images
Removable Disk Drive|SCRM|all*|*Functionality may depend on INQUIRY masquerading and proprietary device drivers, f.e. [Iomega Floptical](Iomega-Floptical)
Magneto-Optical Drive|SCMO|NeXT, X68000, etc.|
DaynaPORT SCSI/Link|SCDP|Macintosh, Atari ST|Requires [device drivers](Dayna-Port-SCSI-Link)
Host Bridge|SCBR|X68000|Enables ethernet networking and mounting a remote file system. Requires [device drivers](https://github.com/rdmark/RASCSI-X68k/wiki)
Host Services|SCHS|Atari ST|Enables remote control of the PiSCSI. Requires [device drivers](PiSCSI-Client-Tools)
Printer|SCLP|Atari ST|Requires [device drivers](PiSCSI-Client-Tools)

# Image Types
This describes the file endings that PiSCSI will recognize automatically, with usage notes. For non-recognized image types, you will have to specify the device type to use it as when attaching.

Image Type|File ending|Usage notes
---|---|---
SCSI Hard Disk image (generic, non-removable)|hds|SCSI-2 compliant
SCSI Hard Disk image (generic, non-removable, SCSI-1)|hd1|SCSI-1 compatible
SCSI Hard Disk image (Apple compatible)|hda|Improves compatibility with Apple Macintosh computers
SCSI Hard Disk image (NEC compatible)|hdn|Improves compatibility with NEC PC-98 computers
SCSI Hard Disk image (Anex86 proprietary)|hdi|Recognizes special headers that are created by the Anex86 PC-98 emulator
SCSI Hard Disk image (T98Next proprietary)|hdi|Recognizes special headers that are created by the T98Next PC-98 emulator
SCSI Hard Disk image (generic, removable)|hdr|Can be used with SCSI floppy drives, SyQuest drives, Zip drives, etc.
SCSI Magneto-Optical image (generic, removable)|mos|Typically used with NeXT computers, as well as Japanese home computers such as X68000, etc.
SCSI CD-ROM or DVD-ROM image (ISO 9660 image)|iso|May contain ISO extensions such as HFS, Joliet, Rock Ridge, etc.