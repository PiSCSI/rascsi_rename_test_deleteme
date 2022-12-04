= What is PiSCSI =
{|
|PiSCSI is a virtual [https://en.wikipedia.org/wiki/Parallel_SCSI SCSI] device emulator that runs on a [https://en.wikipedia.org/wiki/Raspberry_Pi Raspberry Pi]. It is a two piece solution, with a hardware and software component. PiSCSI can emulate multiple SCSI devices concurrently, provides a control interface to attach / detach drives, as well as insert and eject removable media. Simply connect the PiSCSI interface board to your system, launch the PiSCSI software on the Raspberry Pi, and the virtual devices will be accessible as physical SCSI devices!
|[[images/rascsi_logo2_scaled.png]]
|}


== Where can I get one?? ==
{|
|[[images/320px-Flag_of_the_United_States.svg.png]]
|<dl>
<dt>[https://www.tindie.com/stores/landogriffin/ [[images/tindie-logo-small.png]] akuker's Tindie Store] </dt>
<dd>- Support the maintainer of the Github repository ;]</dd>
<dd>- All PiSCSI configurations, daisy chain daughter board plus others</dd>
<dt>[https://samplerzone.com/products/chicken-rascsi-sd-scsi-drive SamplerZone]</dt>
<dd>- Configured and ready to go, out of the box</dd>
<dt>[https://www.vintagecomputercenter.com/product/rascsi Vintage Computer Center]</dt>
<dd>- Configured and ready to go, out of the box</dd>
<dd>- Kits and Fully Assembled versions</dd>
<dd>- Wide Range of 8bit Computer Accessories and Parts</dd>
</dl>
|-
|[[images/320px-Flag_of_Europe.svg.png]]
|<dl>
<dt>[https://samplerspa.de/ SamplerSpa.de] </dt>
<dd>- Pre-assembled versions available for sale in Germany.</dd>
<dd>- Great assortment of vintage storage accessories</dd>
</dl>
|-
|[[images/320px-Flag_of_the_United_Kingdom.svg.png]]
|<ul>
<li><a href="https://www.intriguingindustries.co.uk/product-category/rascsi/">intriguing industries</a></li>
<dd>- Complete virtually Plug&Play PiSCSI in PotatoFi Cases and DIY Kits </dd>
<dd>- Comprehensive selection of accessories and other Mac Upgrades</dd>
<ul>
<li>[http://amigakit.amiga.store/rascsi-adapter-board-p-91280.html?aksid=bjnke5i310a60fqi2mq80ttda4&currency=GBP&aksid=bjnke5i310a60fqi2mq80ttda4 AmigaKit]</li>
<ul>
|-
|[[images/320px-Flag_of_Japan.svg.png]]
| <dl><dt>[https://gimons.booth.pm/ Gimons Developer Works]</dt>
<dd> - Original creator of the PiSCSI</dd></dl>
|-
|[[images/do_it_yourself.png]]
| <dl>
<dt>You are welcome to build your own!</dt>
<dd>- The [https://github.com/piscsi/piscsi/raw/master/hw/rascsi_2p4/gerbers/gerbers_rascsi_2p4a.zip Gerber files] are available in the Github repo. You can order these from any PCB manufacturer.</dd>
<dd>- [https://www.jlcpcb.com JLCPCB] is commonly used, since they are able to pre-install the tiny resistors in the factory for a low fee.</dd>
</dl>
|}

- 

== Want to chat? ==
<a href="https://discord.gg/PyS58u6">[[images/discard_logo_scaled.png | 100px]]</a> Join us on [https://discord.gg/PyS58u6 Discord] with questions, concerns or to just socialize with some vintage computing users.

__TOC__

= Introduction and history =
RaSCSI was originally developed by [http://retropc.net/gimons/rascsi/ by GIMONS] for use with the [https://en.wikipedia.org/wiki/X68000 Sharp X68000]. As GIMON's web site and documentation is in Japanese, the essence of that information has been captured and translated on the [[X68000]] wiki page.

The purpose of this repository is to take the awesome work by GIMONS and build upon it, using the open source community. This project was forked from version 1.47 of GIMONS' RaSCSI project. Over time, this project has had significant updates and architectural changes, providing unique capabilities beyond the original RaSCSI project.

PiSCSI has been demonstrated on dozens of retro computing platforms and digital samplers. A [https://github.com/piscsi/piscsi/wiki/Compatibility compatibility list] is available showing which platforms have been tested. Additional testing is appreciated, along with updating the system comparability table with your findings.

== Select Tutorial Videos ==
Warning: Older videos may contain outdated information, since PiSCSI is a rapidly developing project.

* [https://www.youtube.com/watch?v=-qRG-0Pne-I The Macintosh Librarian tutorial and demonstration on a Color Classic] (Dec 30, 2021)
* [https://www.youtube.com/watch?v=dMgAJnxiYGQ Introduction to using PiSCSI on DEC VAXstation / Alphaserver] (Nov 6, 2021)
* [https://www.youtube.com/watch?v=Pat42MNRhhA Mac84 tutorial and DaynaPORT Ethernet interface how-to] (Jul 31, 2021)
* [https://www.youtube.com/watch?v=kLyDP9FLHlk Demonstration of PiSCSI in use on a SE/30] (Oct 11, 2020)
* [https://www.youtube.com/watch?v=tUgxcchH2yg Livestream of PiSCSI assembly] (Oct 10, 2020)

= Project Comparison =
{|class="wikitable"
!scope="col"| 
!scope="col"| PiSCSI<BR>(68kmla edition)
!scope="col"| RaSCSI<BR>(GIMONS)
!scope="col"| BlueSCSI
!scope="col"| SCSI2SD
!scope="col"| MacSD
|-
|Links to more information
|[https://github.com/piscsi/piscsi/wiki Wiki], [https://github.com/piscsi/piscsi GitHub]
|[http://retropc.net/gimons/rascsi/ Homepage]
|[http://scsi.blue Homepage]
|[http://www.codesrc.com/mediawiki/index.php/SCSI2SD Wiki]
|[http://macsd.com macsd.com]
|-
|Cost
|$$
|$$
|$
|$$
|$$$
|-
|Code & Documentation
|English
|Japanese
|English
|English
|English
|-
|Primary target systems
|[https://en.wikipedia.org/wiki/Timeline_of_Macintosh_models SCSI Macintosh PCs],<br />
[https://en.wikipedia.org/wiki/Atari_ST Atari 16/32 Bit Computers]
|[https://en.wikipedia.org/wiki/X68000 Sharp X68000]
|[https://en.wikipedia.org/wiki/Timeline_of_Macintosh_models SCSI Macintosh PCs]
|General SCSI
|[https://en.wikipedia.org/wiki/Timeline_of_Macintosh_models SCSI Macintosh PCs]
|-
|Run-time configurable
|✅
|✅
|❌
|❌
|❌
|-
|HTML control interface
|✅
|❌
|❌
|❌
|❌
|-
|[https://play.google.com/store/apps/details?id=de.rascsi Android App]
|✅
|❌
|❌
|❌
|❌
|-
|HD device
|✅
|✅
|✅
|✅
|✅
|-
|CD device
|✅
|✅
|❌
|✅
|✅
|-
|Floppy device
|✅
|❌
|❌
|✅
|❌
|-
|Removable device
|✅
|❌
|❌
|✅
|❌
|-
|MO device
|✅
|✅
|❌
|✅
|❌
|-
|Sharp X68000 Net device
|❌
|✅
|❌
|❌
|❌
|-
|DaynaPort SCSI/Link
|✅
|❌
|❌
|❌
|❌
|-
|CD Audio
|❌
|❌
|❌
|❌
|✅
|}

= Raspberry Pi and System compatibility = 

With many people working on and testing PiSCSI on their own systems, you can find details on what Raspberry Pis and which computers work together. Check out the [https://github.com/piscsi/piscsi/wiki/Compatibility Compatibility] page.

= Benchmarks =
Benchmark testing has been performed with the PiSCSI on a few different Raspberry Pi models. Please check the [https://github.com/piscsi/piscsi/wiki/Benchmarks benchmarks] page for additional details.

-----

= Hardware Component =
== Connection Method ==
The hardware component of PiSCSI interfaces with GPIO pins on the Raspberry Pi to read/control the SCSI signals. As the Raspberry Pi GPIO pins operate at 3.3v and SCSI signalling is 5v, the PiSCSI interface uses bus transceivers allowing the Raspberry Pi to safely communicate on the SCSI bus. The SCSI I/O signal is used to control the direction of the Data signals, and a dedicated GPIO pin is used to control the direction of several control signals. As of Sept 2020, the suggested transceiver is the SN74LS641-1 from Texas Instruments. As development is still underway, a [[Transceiver-Comparison|comparison of different transceivers]] has been compiled.

{|
|[[images/rascsi.png | width = 275px]]
|[[images/Block_diagram.png]]
|}

== Assembling your own ==
For those who have purchased the DIY kit on [https://www.tindie.com/products/landogriffin/rascsi-macintosh-version/ Tindie], or have procured your own PCBs and components, check the [[assembly]] page for instructions on building your own PiSCSI board. 

== Alternate Connection Method ==
Some people have reported successfully connecting the Raspberry Pi GPIO pins directly to a SCSI interface. This may work, but runs the Raspberry Pi GPIO beyond the specifications, and ''is not recommended''.

== Expansion options ==
The PiSCSI board has had an additional header installed exposing the I2C bus. With this you can install additional features like an OLED display. Read more on how to [[OLED Status Display (Optional)|connect an OLED display to the PiSCSI ]].

-----

= Software Component =
== Downloading and installing the software ==
Once you have an PiSCSI board, instructions on how to setup your Raspberry Pi, and downloading and installing the PiSCSI software can be found on the [[Setup Instructions]] page.

== Connecting PiSCSI to your computer ==
Now that you have the PiSCSI board connected to your Raspberry Pi, and have the software downloaded and installed, next is to connect the PiSCSI device to your computer. Details on SCSI devices, termination and cabling can be found on the [[Connecting the PiSCSI]] page.

== I have the software and everything connected, what next? ==
With the PiSCSI board attached to your computer, and PiSCSI downloaded and installed, instructions on creating and attaching disk images can be found on the [[Drive Setup]] page.

Additionally, a web interface can be used to attach and detach images, manage the images, and the Raspberry Pi itself. More details on the web interface and how to set it up can be found on the [[Web Interface]] page.

-----

= Additional Information =

== What is 68kmla? ==
[https://68kmla.org/forums/ 68kmla] is the “68k Mac Liberation Army”. Its a group of vintage Mac (and Apple) enthusiasts who talk about nerdy stuff on the forum. This development started as [https://68kmla.org/bb/index.php?threads/rascsi-development-thread.6868/ part of a forum thread]. This PiSCSI project has grown far beyond the original 68k MLA community though.

----

= Reference =

== PiSCSI manpages ==
* [https://raw.githubusercontent.com/piscsi/piscsi/master/doc/rascsi_man_page.txt rascsi manpage]
* [https://raw.githubusercontent.com/piscsi/piscsi/master/doc/scsictl_man_page.txt scsictl manpage]
* [https://raw.githubusercontent.com/piscsi/piscsi/master/doc/scsimon_man_page.txt scsimon manpage]

== Software ==

* [http://mirror.informatimago.com/next/developer.apple.com/documentation/macos8/mac8.html Mirror of Mac OS 8 Documentation]
* [https://wiki.osdev.org/ATAPI ATAPI list of SCSI commands]
* [http://www.epicycle.org.uk/pioneercd/SCSI-2%20Command%20Set.pdf Pioneer CD-ROM SCSI command set]
* [https://origin-www.seagate.com/files/staticfiles/support/docs/manual/Interface%20manuals/100293068j.pdf Seagate SCSI Commands Reference Manual (maybe  too new to use as a reference?)]
* [http://mirror.informatimago.com/next/developer.apple.com/documentation/mac/Devices/Devices-2.html Inside Macintosh "devices" mirror]
* [http://www.pioneerelectronics.com/pio/pe/images/portal/cit_3424/11898459DVDCommandSet.pdf DVD Command Set]
* Mirror of Apple's original SCSI Manager documentation  
** [http://mirror.informatimago.com/next/developer.apple.com/documentation/mac/Devices/Devices-119.html OG SCSI Manager]
** [http://mirror.informatimago.com/next/developer.apple.com/documentation/mac/Devices/Devices-151.html SCSI Manager 4.3]
* PDF versions of the SCSI Manager documentation
** [https://developer.apple.com/library/archive/documentation/mac/pdf/Devices/SCSI_Manager.pdf OG SCSI Manager]
** [https://developer.apple.com/library/archive/documentation/mac/pdf/Devices/SCSI_Manager_4.3.pdf SCSI Manager 4.3]
* [https://siber-sonic.com/mac/Vintage/CD_DVDdriver.html Apple CD-ROM and Apple CD/DVD Driver Reference]
* [https://www.vintageapple.org/macdrivers/disk.shtml CD-ROM Drivers]
* [http://mirror.informatimago.com/next/developer.apple.com/documentation/macos8/pdf/NetworkSetup.pdf Inside Macintosh "Network Setup" (mirror)]
* [http://mirror.informatimago.com/next/developer.apple.com/documentation/macos8/pdf/CommToolbox.pdf Inside Macintosh "Communications Toolbox" (mirror)]
* [http://mirror.informatimago.com/next/developer.apple.com/documentation/macos8/pdf/NSL_Mgr.pdf Network Services Location manager Developers Kit]
* [https://www.staff.uni-mainz.de/tacke/scsi/SCSI2.html Very detailed, thorough document]
* [https://www.t10.org/drafts.htm T10 Working Drafts for the SCSI standard]
* [https://www.rascsi.de PiSCSI Control App for Android]

== Hardware ==

* Microchip SCSI documentation
** [https://storage.microsemi.com/en-us/support/scsi/2930/aha-2930cu/use_prod/scsi_event_codes.htm?nc=/en-us/support/scsi/2930/aha-2930cu/use_prod/scsi_event_codes.htm SCSI Sense Codes Described]
** [https://storage.microsemi.com/en-us/support/scsi/2930/aha-2930cu/use_prod/scsi_terms.htm?nc=/en-us/support/scsi/2930/aha-2930cu/use_prod/scsi_terms.htm SCSI terms defined]
* [http://ps-2.retropc.se/ppc850tp/scsi-laptop-drive_dprs_spw.pdf IBM OEM Hard Disk Specifications for 2.5" SCSI drives]
* [http://www.bitsavers.org/pdf/adaptec/ACB-4000/400003-00A_ACB-4000A_Users_Manual_Oct85.pdf Seagate HD Technical Information]