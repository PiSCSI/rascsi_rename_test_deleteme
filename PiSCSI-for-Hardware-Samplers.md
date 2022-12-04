1. [FAQ](https://github.com/piscsi/piscsi/wiki/PiSCSI-for-Hardware-Samplers#faq)
2. [Setup](https://github.com/piscsi/piscsi/wiki/PiSCSI-for-Hardware-Samplers#setup)
3. [Troubleshooting](https://github.com/piscsi/piscsi/wiki/PiSCSI-for-Hardware-Samplers#troubleshooting)
4. [Compatibility](https://github.com/piscsi/piscsi/wiki/PiSCSI-for-Hardware-Samplers#compatibility)
5. [Performance Tests](https://github.com/piscsi/piscsi/wiki/PiSCSI-for-Hardware-Samplers#performance-tests)

# Introduction

The PiSCSI is a SCSI emulator that is built on the Raspberry Pi Ultra Low Cost Computer platform. It will mount virtual CD-ROM's and Hard Drives directly into your sampler using the SCSI port on the back.

The benefits of using a PiSCSI are:

* Easy to use with a web-based admin interface
* Low cost ($60 for a basic setup, $150 for a high-end setup)
* Use wifi to transfer and back up files
* Effectively a CD-ROM jukebox that can manage dozens of ISO images without SD card swapping
* Create and mount hard drive images

If you get comfort from the clicking and clacking and whirring of old SCSI devices then the PiSCSI isn't for you.  If you enjoy the thrill of wondering whether or not your Zip cartridge will save your sample editing session, we don't judge.

If you want to learn more about the best mass storage solution for vintage samplers then you should read on.

# FAQ


<details><summary>Where do I buy one?</summary>
<p>
<table><tr><td>
<p>
The project lead sells them on Tindie.  Ignore the signs about it being a product for Macintosh, he was a little confused when he created that page and didn't realize how awesome this product would be for all of us sampler users.  This is the version to get:

PiSCSI [Tindie Store](https://www.tindie.com/products/landogriffin/rascsi-english-version-assembled/)
</p>
</td></tr></table>

</p>
</details>


<details><summary>What else will I need?</summary>
<p>
<table><tr><td>
<p>

**1 - A Raspberry Pi Host Computer**

The Zero +WH (with Wifi and Headers) works well or if you want more power the 4B models provide a performance boost. If you're planning on hooking up more USB storage or use Gigabit Ethernet for very fast transfer speeds, choose any 4B that fits your budget.

Check out the [PiSCSI compatibility page](https://github.com/piscsi/piscsi/wiki/Compatibility) if you are thinking of using an older 1/2/3 Raspberry Pi.

Current Raspberry Pi computers are found on the [RaPi project's product page](https://www.raspberrypi.org/products/).

**2 - USB Power Supply**

This is sold separately, you can include this when you purchase the Raspberry Pi or you can use a USB cable that you already own.  Make sure the connector matches the specific Raspberry Pi you will be using.

**3 - Micro-SD card**

As fast and as large as you are comfortable buying, minimum recommended is 16GB.

**4 - SCSI cable**

Check the tables below to see which cable you need for your sampler(s).  The PiSCSI needs DB25 on one end and the appropriate connector for your sampler on the other.

**5 - Keyboard, Mouse, Monitor for setup**

To set up the device you will need a micro-HDMI cable, monitor, and USB keyboard and mouse.  Once it's set up you can put all those away.
</p>
</td></tr></table>

</p>
</details>



<details><summary>Is a case available?</summary>
<p>
<table><tr><td>

We are actively working to get a groovy 3d printed case designed.  Sitting exposed on your desktop won't damage the PiSCSI, just don't lick it by mistake.

</td></tr></table>

</p>
</details>

<details><summary>Can I mount it inside the sampler?</summary>
<p>
<table><tr><td>
Sure you could probably figure out how to do this and you'd need to either drill holes or create a custom mount for the floppy bay. Even after all that it is better to keep it outside where the PiSCSI can stay cooler - this is healthy for both the PiSCSI and your sampler.
</td></tr></table>
</p>
</details>


<details><summary>What SD card should I buy?</summary>
<p>
<table><tr><td>
At the time of writing this, amazon.com is selling a 64GB Sandisk Ultra microSD card for $12, 128GB for $20, and 256GB for $35.  At those prices the 64GB is a no-brainer for a well-spec'ed PiSCSI setup.  

The OS and PiSCSI software will take a little over 8GB, leaving you the balance of the card to store disk images.

A CD-ROM image will have a maximum size of 650MB but most are in the 200-300MB range. Roland CD-ROM's are a little different as for some strange reason they specified that all discs must fill up the empty space with zeros, so they're all 650MB no matter what. Let's also assume that the average hard drive for sampler use is 500MB - you can definitely have larger drives but most older samplers don't have folder/subfolder implementations and it's a PITA to scroll through hundreds of banks/multis/programs to find what you're looking for.

Using that logic, a 64GB SD card will give you roughly 56GB of storage.  Let's be conservative and round that down to 52GB so we're not completely running out of space.  52GB will let you store 10 virtual hard drives and 188 CD-ROM images.

If that's not enough for you, spend the extra $8 on the 128GB card and you'll have enough capacity for 20 virtual hard drives and over 400 CD-ROM images.

Also remember that PiSCSI has an awesome web admin interface that lets you transfer files directly onto the Raspberry Pi, so it's very easy to swap out CD-ROM images if you have a very large library stored on another computer somewhere.  You could also hook up an external USB 3.0 hard drive if you bought the Raspberry Pi 4B and use that as your local high-speed PiSCSI image library location.

It should also be noted that over the years of using SD cards in samplers that generic cards seem to have higher failure rates than name-brand cards, and counterfeit name-brand SD cards are more common than you might think on auction sites.  Generally speaking, you get what you pay for.
</td></tr></table>

</p>
</details>


<details><summary>Can I connect multiple samplers at once?</summary>
<p>
<table><tr><td>
Sure, the SCSI bus can handle up to eight devices at once with no limitations on what those devices are. Just make sure that everything has a unique SCSI ID, both ends of the chain are terminated, then go to town.
<br><br>


You could connect two Roland S-760 samplers at ID's 6 and 7, a PiSCSI configured with two virtual Roland-formatted hard drives at ID's 0 and 1, then four Roland CD-ROM images from the same PiSCSI at ID's 2, 3, 4, and 5.

You could also connect a Kurzweil K2000 as ID 0, an e-mu E6400 Classic as ID 2, an Akai S1000 as ID 4, and a Yamaha A4000 as ID 6.  Then set up the PiSCSI with a Kurzweil hard drive on ID 1, an e-mu drive on ID 3, and Akai drive on ID 5, and a Yamaha drive on ID 7.  Of course you'd need a number of SCSI Y-splitters and none of the samplers could access the drives that are formatted using another file system (i.e. Akai can't read Kurzweil) but this is completely possible with only one PiSCSI in the chain.

The one universal caution was always to not allow two devices to write to the same SCSI hard drive at the same time, but with a PiSCSI there's no danger of physical drive damage so maybe we should test that too.
</td></tr></table>
</p>
</details>


<details><summary>Can I connect my old Zip/Jaz/Hard Drive/CD-ROM at the same time?</summary>
<p>
<table><tr><td>
Completely 100% totally A-OK.  
<br><br>
If you have content from an old 1GB external hard drive that you'd like to back up, just create a virtual 1GB hard drive in the PiSCSI and mount it to a free SCSI ID.  Then use your sampler to copy all of the files from the physical drive to the virtual drive.

You could use the same method to copy content from your favorite physical CD-ROM's or Zip Disks and consolidate them on a virtual hard drive.  Then put them in a box in that dark corner of the garage no one ever looks at, give them to the local tech-friendly recycle depot, or sell them on ebay to people who have never heard of PiSCSI.
</td></tr></table>
</p>
</details>



<details><summary>How is this different from a SCSI2SD? What about the BlueSCSI?</summary>
<p>
<table><tr><td>

These devices are directly comparable to the PiSCSI, but in the opinion of the unofficial PiSCSI Sampler Team it's the clearly superior solution and can be recommended to all sampler users who use SCSI-equipped electronic musical instruments.

SCSI2SD has been the leading modern mass storage solution since soon after its introduction in 2013.  Relative to the more expensive SCSI2SD V6 the PiSCSI offers:

- (+) Vastly more intuitive administration/management
- (+) Wi-Fi/network connectivity
- (~) Similar performance
- (-) Can't easily be mounted internally

Relative to the SCSI2SD V5.5 the PiSCSI scores:

- (+) Vastly more intuitive administration/management
- (+) Wi-Fi/network connectivity
- (+) Significantly better performance
- (-) More expensive
- (-) Larger physical footprint


Blue SCSI is another new SCSI emulation device which shows a lot of promise as an inexpensive drive emulator, however the PiSCSI is a far more powerful solution for sampler users:

- (+) Much faster performance
- (+) Mounts ISO images as virtual CD-ROM's
- (-) More expensive
- (-) Can't easily be mounted internally

</td></tr></table>
</p>
</details>



<details><summary>How is this different from a Gotek (or Lotharek or Nalbantov) emulator?</summary>
<p>
<table><tr><td>

The vendors of these floppy drive emulators can be really deceptive with their descriptions (we're looking at you, Nalbantov).  You might read the highly optimistic marketing fluff and come away thinking that an expensive USB floppy emulator will solve all of your storage problems, but there are some key limitations they don't tell you about:

- The floppy bus is not some data superhighway in your sampler, it's just as fast as a floppy drive which means SLOW
- The floppy controller is still limited to 1.44MB disk images, so if you save a 4MB file you will actually need three separate floppy image files and manually switch the active image on the drive after each one is full - now just imagine how much fun this is with a 16MB file

A lot of people see "USB Storage" and think "Oh this is awesome because transferring files to my computer using that USB stick is so fast!" so you'd definitely not be the first person to get excited then experience the letdown of the cold, hard truth of the floppy ribbon cable of life.

A USB floppy emulator is perfect for older samplers without SCSI, and their on-board memory capacity is usually less than the 720KB or 1.44MB floppies that they use. However, if your sampler has SCSI, you should be using a PiSCSI.

If you are interested in a floppy emulator for an older sampler then check out [HxC](http://hxc2001.free.fr/floppy_drive_emulator/index.html#Download_HxCFirmwareForGotek) or [FlashFloppy](https://github.com/keirf/FlashFloppy/wiki) and don't pay a crazy price for an underpowered and oversold floppy emulator.  $30-$60 is a fair price for a USB emulator, and in our opinion you should avoid anyone selling them for over $100.

</td></tr></table>
</p>
</details>


<details><summary>Should I buy the kit or preassembled version?</summary>
<p>
<table><tr><td>
We strongly recommend the preassembled version for 99% of sampler users based on decades supporting DIY projects on various sampler-specific forums and groups around the Internet.
<br><br>
If you rate your soldering skills as "Advanced" or "Strong Intermediate" then you should be fine with a kit.  You're comfortable diagnosing circuits that aren't working, soldering surface-mount components, and have a microscope or strong magnifying glass on hand to look at small solder joints.
<br><br>
If you are just learning how to solder, don't have quality soldering/desoldering equipment, or you don't know the difference between through-hole and surface-mount then the $15 extra for the preassembled version is money well spent.


</td></tr></table>
</p>
</details>



# Setup

### Step 1 - Set up Raspberry Pi

Connect the PiSCSI to the Raspberry Pi using the header pins (there's only one way it will fit).  Connect a monitor to the HDMI port and a keyboard and mouse to the USB ports.

### Step 2 - Install the Raspberry Pi software onto the SD card

Follow the [standard instructions](https://www.raspberrypi.org/documentation/installation/installing-images/) to install the Raspberry Pi image onto your SD card.  The Raspberry Pi Imager is a very handy tool.

### Step 3 - Configure your Raspberry Pi

Insert the SD card into the Raspberry Pi and power it up.  Follow the on-screen instructions to configure it, and connect it to your Wi-Fi network at this time if you like.

Then follow the [PiSCSI setup procedure](https://github.com/piscsi/piscsi/wiki/Setup-Instructions) to install that software.

### Step 4 - Connect to the admin web page

The admin program is running by default on port 80 and the default hostname is "raspberrypi", so you can connect to it using a very simple URL:

[http://raspberrypi](http://raspberrypi)

That's it, you should be off and running a minute or so after browsing the admin console!

<details><summary>Additional Setup for Windows Users</summary>
<p>
<table><tr><td>
<p>

### Remote Desktop

If you want to use Windows Remote Desktop to access your Raspberry Pi in future, run the command `sudo apt-get install xrdp` in a terminal window.

You will then be able to log in using the user "pi" and the password you provided during setup.


### Windows File Sharing

(NOTE: this section is a work in progress)

Although you can use the web interface to manage files on the PiSCSI, it's often easier just to mount the images folder to a Windows share then you can cut/copy/paste files from your main computer.

`sudo apt install samba -y`

`sudo chown -R pi:pi /home/pi/images`

`sudo cp /etc/samba/smb.conf /etc/samba/smb.bak`

`sudo nano /etc/samba/smb.conf`

Add this to the bottom of the file:

> [PiSCSI Images]
> comment = PiSCSI Images
> path = /home/pi/images/
> directory mask = 0777
> create mask = 0777
> writeable = yes
> browsable = yes
> public = no


`sudo smbpasswd -a pi`

`sudo systemctl restart smbd`

</p>
</td></tr></table>

</p>
</details>


# Troubleshooting

We're still in the early stages of developing this knowledge base and are only starting to collect troubleshooting information.  However, the vast majority of SCSI problems that sampler users have encountered over the past 30 years come down to two things: 1) Improper SCSI termination or 2) Duplicate SCSI ID's on the same chain.

If you've checked those things, please join us on the [PiSCSI-Samplers Discord Channel](https://discord.com/channels/749261651978748014/839337309752262696) or the [PiSCSI for Samplers Facebook Group](www.facebook.com/groups/RaSCSIforsamplers/) for more support.

There are also several hardware sampler groups on Facebook providing peer support for the samplers themselves:

- [Akai Hardware Samplers](https://www.facebook.com/groups/akaisamplers)
- [E-mu Sampler Users](https://www.facebook.com/groups/348204318721)
- [Emulator IV User Group](https://www.facebook.com/groups/Emulator4UserGroup/)
- [Ensoniq User Group](https://www.facebook.com/groups/ensoniq/)
- [Roland Sampler Information Exchange](https://www.facebook.com/groups/rolandsamplers)
- [Hardware Sampler Users](https://www.facebook.com/groups/hardwaresamplerusers/)

# Compatibility
The tables below show the testing status for all known samplers with SCSI.  It is usually a good idea to update a sampler to the final firmware version as most manufacturers improved SCSI compatibility and performance significantly using these updates.

<details><summary>SCSI Connector Types</summary>
<p>
<table><tr><td>
<p>

There are three major connector types used in hardware samplers: DB25, CN50, and HD50.  Although PiSCSI uses a DB25 connector, the SCSI standard ensures that every connector is compatible with the others.  The most convenient way to connect a PiSCSI to a sampler with CN50 or HD50 is to buy a cable with DB25 on one end and the appropriate SCSI connector for your sampler on the other end.  You can also use adapters, but they do tend to put stress on the SCSI jacks that they are connected to which might cause maintenance issues.

DB25 is the oldest of the connector types, and was also common among Macintosh computers. The prevalence of the Macintosh computer in studios of all levels through the 80's and 90's is probably why the vast majority of hardware samplers used this connector.

CN50, also known simply as "Centronics", was used by Akai on the S1000 and S1100, and e-mu on the Emulator IV series.

HD50 is a very sturdy connector that was used mainly by Akai in later years.

CN50 (left) and DB25 (right) can be seen in the following picture:

![CN50 & DB25](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/SCSI_25-50.jpg/640px-SCSI_25-50.jpg)

HD50 can be seen in this picture:

![HD50](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6c/HD-50_SCSI_Cable_and_Terminators.jpg/640px-HD-50_SCSI_Cable_and_Terminators.jpg)

</p>
</td></tr></table>

</p>
</details>

### Akai S/Z

Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
S950|ver|DB25|-|Not tested
S1000/S1000PB|ver|CN50|-|Not tested
S1100|ver|CN50|-|Working
S2800/S3000/S3200/CD3000|ver|DB25|-|Not tested
S2800i|ver|CN50|-|Working
S3000XL/S3200XL/CD3000XL|2.0|DB25|-|Working
S2000|2.0|DB25|-|Working
S5000/S6000|ver|HD50|-|Not tested
Z4/Z8|1.45|HD50|-|Working
Caveats: Akai S-series CD-ROM images may need the extension .hds and be mounted as HDD images.


### Akai MPC
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
MPC60/MPC60 mk2|ver|DB25|-|Not tested
MPC3000|ver|DB25|-|Not tested
MPC2000|ver|DB25|-|Working
MPC2000XL|ver|HD50|-|Working
MPC4000|ver|HD50|-|Not tested

### E-mu
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
Emulator III|ver|DB25|-|Not tested
Emulator IIIXS/XP|ver|CN50|-|Not tested
Emulator IV Classic|3.00b|CN50|-|Not tested
Emulator IV Classic|4.62|CN50|-|Working
Emulator IV Ultra|4.7|CN50|-|Working
Emax|Plus 1.0|DB25|-|Not tested
Emax II|2.14|DB25|-|Not tested
ESI-32/ESI-4000/ESI-2000|3.02|CN50|-|Working

### Ensoniq
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
EPS/EPSm|ver|DB25|-|Not working with SP-1 interface, SP-2 not untested
EPS 16+|ver|-|-|Not tested
ASR 10/88|ver|-|-|Working
ASR-X/ASR-X Pro|ver|-|-|Not tested
TS-10/12|2.3|DB25|-|Working
Caveats: Ensoniq CD-ROM images may need the extension .hds and be mounted as HDD images

### Fairlight
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
CMI|ver|-|-|Not tested


### Kurzweil
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
K2000|ver|-|-|Not tested
K2500|ver|-|-|Not tested
K2600/K2661|ver|-|-|Not tested

### Peavey
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
SP/SP Plus/SXII|ver|-|-|Not tested


### Roland
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
S-550|ver|-|-|Not tested
W-30|ver|DB25|80M|Working (remove boot floppy; must be ID6) 
S-750/S-770|ver|-|-|Not tested
S-760|ver|-|-|Working
SP-700|ver|-|-|Not tested
DJ-70mk2|ver|-|-|Not tested
XV-5080|ver|DB25|-|Working

### Synclavier
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
Synclavier|ver|-|-|Not tested


### Yamaha
Model|Version|Connector|Max HD Size|Status
---|---|---|---|---
A3000|ver|-|-|Working
A4000/A5000|ver|-|-|A4000 working
EX5/EX5R|ver|-|-|EX5R working
RS7000|v1.22|HD50|-|Working


# Performance Tests

## e-mu Tests

-|Configuration
---|---
Sampler|e-mu E-Synth Ultra (EOS 4.7)
Sample Library|e-mu Formula 4000 Analog Odyssey
Raspberry Pi|4B 8GB, Pi Zero
SD Card|Sandisk Ultra 32GB

Device|Analog Odyssey (32MB)|Vintage Combo (16MB)|Moog Synths (8MB)
---|---|---|---
PiSCSI (4B 8GB)|0:31|0:17|0:09
PiSCSI (pi Zero)|0:33|0:19|0:09
SCSI2SD 5.5|0:58|0:31|0:16
SCSI2SD 6.0|0:26|0:15|0:08


***


-|Configuration
---|---
Sampler|e-mu E-Synth Classic (EOS 4.62)
Sample Library|e-mu Formula 4000 Analog Odyssey
Raspberry Pi|4B 8GB
SD Card|Sandisk Ultra 32GB

Device|Analog Odyssey (32MB)|Vintage Combo (16MB)|Moog Synths (8MB)
---|---|---|---
PiSCSI|0:50|0:30|0:16
SCSI2SD 5.5|1:10|0:41|0:21
SCSI2SD 6.0|0:51|0:32|0:16


***


-|Configuration
---|---
Sampler|e-mu ESI-4000 Turbo (v 3.02)
Sample Library|e-mu Formula 4000 Analog Odyssey
Raspberry Pi|4B 8GB
SD Card|Sandisk Ultra 32GB

Device|Analog Odyssey (32MB)|Vintage Combo (16MB)|Moog Synths (8MB)
---|---|---|---
PiSCSI|1:40|0:53|0:27
SCSI2SD 5.5|1:39|0:53|0:27
SCSI2SD 6.0|1:39|0:53|0:27

### Akai Tests

-|Configuration
---|---
Sampler|Akai Z8 (v1.45)
Sample Library|Akai Factory Library Vol. 1 - XL
Raspberry Pi|4B 8GB
SD Card|Sandisk Ultra 32GB

Device|Partition A (32MB)|Partition M (24MB)
---|---|---
PiSCSI|0:00|0:00
SCSI2SD 5.5|1:13|0:00
SCSI2SD 6.0|0:37|0:00

***

-|Configuration
---|---
Sampler|Akai Z8 (v1.45)
Sample Library|Akai 24-bit Grand Piano
Raspberry Pi|4B 8GB
SD Card|Sandisk Ultra 32GB

Device|24bit G Piano (320MB)
---|---
PiSCSI|6:36
SCSI2SD 5.5|
SCSI2SD 6.0|
USB CD|8:30
USB Flash Drive|8:41