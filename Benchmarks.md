# Overview
Below are some benchmarks comparing the PiSCSI running on different variants of Raspberry Pi's, along with the SCSI2SD version 5 and an original Apple hard drive as a comparison.

# Test results
## Overall Disk scores
[[images/benchmark_overall.png|Overall Benchmark]]

_Some notes on this:_ 
* _There are multiple SCSI2SD scores. I ran the test on two different volumes on the SCSI2SD and got slightly different scores._
* _I suspect that the Pi 0 got higher scores because the PiSCSI software only uses one core. This gives the Pi 0 a slight clock speed advantage_

## Disk Read Scores
[[images/benchmark_read.png|Disk Read Benchmark]]
## Disk Write scores
[[images/benchmark_write.png|Disk Write Benchmark]]

# Test setups
## Common components
Macintosh Quadra 840av
* 68040 Processor at 40MHz
* 128MB RAM
* 1MB VRAM
* Seagate ST3600N 500MB HD w/stock Apple firmware
* MacOS 8.1
* Drive cache configured at 128KB
* Norton System Info 3.5 [Part of Norton Utilities](http://macintoshgarden.org/apps/norton-utilities-353)

## PiSCSI - Raspberry Pi 4
* 1.5GHz ARM Cortex-A72 - Quad core
* 4GB RAM
* Samsung 32GB EVO Plus SD Card
* Raspberry Pi OS - 2020-05-27-raspios-buster-full-armhf
* PiSCSI - piscsi version 1.5 - [[https://github.com/akuker/RASCSI-68kmlaver/tree/dual_connector]]

## PiSCSI - Raspbery Pi 2
* 900MHz ARM Cortex 7 - Quad core
* 1GB RAM
* Samsung 32GB EVO Plus SD Card
* Raspberry Pi OS - 2020-05-27-raspios-buster-full-armhf
* PiSCSI - piscsi version 1.5 - [[https://github.com/piscsi/RASCSI-68kmlaver/tree/dual_connector]]

## PiSCSI - Raspberry Pi Zero
* 1GHz ARM11 - Single core
* 512MB RAM
* Samsung 32GB EVO Plus SD Card
* Raspberry Pi OS - 2020-05-27-raspios-buster-full-armhf
* PiSCSI - piscsi version 1.5 - [[https://github.com/piscsi/RASCSI-68kmlaver/tree/dual_connector]]

## SCSI2SD
* Version v5.0a - [[http://inertial.biz/index.php?title=SCSI2SD]]
* Firmware version 4.8.04
* Samsung 32GB EVO Plus SD Card

# Other benchmark datapoints
erichelgeson ran SCSI2SD v6 on a PowerMac G3 with Norton version 5 and received a score of 247. This high score was probably influenced by a much faster computer than a Quadra 840av, which was used on the other tests. But, its also likely that the SCSI2SD v6 also has a lot better performance.
