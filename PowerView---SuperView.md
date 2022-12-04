# Beta Version Quickstart

* You'll need to install the [PowerView Drivers](https://macintoshgarden.org/apps/radius-powerview-driver-101) on your Mac
* [Other Versions](https://www.macintoshrepository.org/27766-powerview) are available to try as well. Version 1.01 is what the developer is using to test.
* The current beta of the Powerview emulation takes over the HDMI output of the Raspberry Pi
* You won't be able to use the HDMI output for a console, so make sure you have SSH set up
* Make sure you're using a monitor/display with a resolution higher than 1024x768 (even though the PowerView can only display 800x600)
* The web interface will NOT work with this feature branch (yet)
* To use this branch, perform the following:
```
cd ~/piscsi
git checkout feature_powerview
git pull
./easyinstall.sh
# After easyinstall is completed...
scsictl -c attach -i 4 -f powerview
# Currently, there is a special case in PiSCSI where it keys off the filename "powerview"
```
* I've never tried to emulate multiple PowerViews at the same time.

## Known limitations
* Debug text information is displayed below the window
* If you re-start the PowerView emulation, you need to change resolution/color depth OR reboot the host. Right now, the emulation only detects color depth and resolution upon a change (or during boot-up). 


# Background
The Radius PowerView is an external graphics card built on a TMS34010 that has SCSI-in, SCSI-out, and then VGA and DB-15 connectors for you to hook up a PC or Mac monitor to it.

They were all powered by the TMS34010 CPU, a 32bit CPU/GPU hybrid designed by TI in 1986. They ran it at 6.25mhz.

_The Aura Scuzzygraph, Radius PowerView, and Radius SuperView external SCSI graphics cards for Apple Macintosh computers are based on the TMS34010._
https://en.wikipedia.org/wiki/TMS34010

![](https://pbs.twimg.com/media/EarBuJqUcAAcZhW?format=jpg&name=900x900)
![](https://pbs.twimg.com/media/Eaq_N7GVAAAyyLE?format=jpg&name=large)
![](https://pbs.twimg.com/media/EarBDHgUcAAwiNa?format=jpg&name=large)
![](https://pbs.twimg.com/media/EarAjYbUEAA668V?format=png&name=small)

# Radius Powerview Details
## Command Set

## Inquiry Response
Output from [TattleTech 2.17](https://macintoshgarden.org/apps/tattletech):
```
¥ SCSI Device# = 3
   × Device Status = Device Connected
   × Name = NA
   × Driver# = -36
   × Type = 3   (Processor)
   × Manufacturer = RADIUS
   × Product = PowerView
   × Revision = V1.0
   × ROM Revision = 47D62000408001F7
   × Device Attributes :
      + ANSI Compliant = Yes  (SCSI 1)
      + ECMA-111 Compliant = No
      + ISO IS 9316 Compliant = No
      + Wide SCSI (32-bit Transfers) = No
      + Wide SCSI (16-bit Transfers) = No
      + Fast SCSI (Synchronous Transfers) = No
      + Linked Commands = No
      + Tagged Command Queuing = No
      + Soft Reset = No
      + Relative Addressing = No
      + Terminate I/O Process = No
      + Asynchronous Event Notification = No
      + Response Data Format = 1
```

***
References:

## General info
- https://www.reddit.com/r/VintageApple/comments/qvnz8w/radius_powerview_the_weird_powerbook_scsi/

## Graphics chip
- https://twitter.com/Foone/status/1273041667961040897
- https://en.wikipedia.org/wiki/TMS34010
- Masters Thesis: https://ttu-ir.tdl.org/bitstream/handle/2346/13183/31295005958391.pdf;sequence=1
- MAME TMS34010 Simulator: https://github.com/MisterTea/MAMEHub/blob/master/Sources/Emulator/src/emu/cpu/tms34010/tms34010.c
- TMS34010 Article: https://www.computer.org/publications/tech-news/chasing-pixels/Famous-Graphics-Chips-IBMs-professional-graphics-the-PGC-and-8514A/Famous-Graphics-Chips-TI-TMS34010-and-VRAM
- TMS34010 Graphics Library manual: https://www.ti.com/lit/ug/spvu027/spvu027.pdf
- TMS34010 Users Guide: https://fabiensanglard.net/nbajamte/t34010_user_guide.pdf
- TMS34010 Data Sheet: http://www.farnell.com/datasheets/84292.pdf
- 68kmla discussion: https://68kmla.org/forums/topic/52647-so-what-is-a-scuzzygraph-exactly/

## Other implementations
 - https://github.com/jcs/RASCSI/commit/6da9e9f3ffcd38eb89413cd445f7407739c54bca