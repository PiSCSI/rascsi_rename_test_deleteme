## PiSCSI Client Tools for Atari 16/32 Bit Computers

With the SCSI Printer device (SCLP) and the Host Services device (SCHS) PiSCSI supports two devices that are neither mass storage nor network devices. For both device types special free drivers for Atari 16/32 bit computers (ST/TT/Falcon) and clones like the Milan are available: The <a href="https://www.hddriver.net/en/rascsi_tools.html">PiSCSI Client Tools</a>.

With these tools you can print files from the Atari via PiSCSI and set the Atari's clock based on PiSCSI's realtime clock service. In addition, you can shut down PiSCSI or the Raspberry Pi, e.g. as part of the Atari shutdown sequence in case you are using the MiNT operating system. Please refer to the <a href="https://www.hddriver.net/en/rascsi_tools.html">PiSCSI Client Tools</a> webpage for further information and a download link. The sources are [available on GitHub](https://github.com/uweseimet/atari_public/tree/main/RASCSI).

