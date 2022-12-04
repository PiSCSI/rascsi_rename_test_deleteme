A SCSI printer is implemented as ''SCLP'' device since PiSCSI release 22.05.

Device drivers for [Atari ST/TT/Falcon and the Milan](https://github.com/piscsi/piscsi/wiki/PiSCSI-Client-Tools) are available. The device driver sources are [provided on GitHub](https://github.com/uweseimet/atari_public/tree/main/RASCSI).

# Development Resources

## Classic Macintosh

Apple produced *two* SCSI printers which could be emulated. They made the low cost [LaserWriter SC], which uses bitmaps like the ImageWriter while the [LaserWriter IISC] is a higher cost PostScript printer. Emulating these devices in PiSCSI would be one way to support printing using Apple drivers.

[LaserWriter SC]: https://lowendmac.com/1990/personal-laserwriter-sc
[LaserWriter IISC]: https://lowendmac.com/1988/laserwriter-iisc

A second way would be to develop a 3rd party print driver from scratch. Information on developing print drivers for classic Mac OS is provided in the [Learning to Drive] document. This is a .hqx archive that contains a Microsoft Word document that describes the structure of PMRF drivers. It is unclear whether this is the latest or best documentation, but I examined the resource forks of several Apple provided print drivers and also of James Walker's [PrintToPDF] and found that it followed the general structure described in the document.

[Learning to Drive]: https://web.archive.org/web/20170606211537/http://staticky.com/mirrors/ftp.apple.com/developer/Tool_Chest/Graphics_-_Imaging/Learning_to_Drive.sit.hqx
[PrintToPDF]: https://web.archive.org/web/20210425215827/https://www.jwwalker.com/pages/pdf.html