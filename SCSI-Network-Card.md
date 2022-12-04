# SCSI Network Card emulation
The aim is to provide network capabilities through SCSI interface emulated by PiSCSI.
This documentation is for developer who would like to contribute to this project.


## Current status
This is not yet ready and still under development.
Packets go through `piscsi0` tun/tap and are read by PiSCSI service, and are sent to SCSI. I haven't been able to verify the packet arrived on the Mac yet.

## How does it work?
Packets can come from `wlan0` or from localhost, they are sent to a tun/tap virtual interface named `piscsi0`.
The PiSCSI software connects to `piscsi0` and reads the packets, then write those packets to the SCSI interface.
On the Mac, the device driver, reads the packets from the SCSI physical port of the Mac and provide them to the System.
Same operation happen in the other direction when packets are sent from the Mac to the SCSI (thanks the driver).
PiSCSI reads the packets from the SCSI emulation and write then to the virtual network interface `piscsi0`, packets can then travel to the internet through `wlan0`.

```
 
 [  wlan0   ] <---> [   piscsi0      ] <---> [ PiSCSI + SCSI NIC Emulation ] <---> SCSI <--> [ Mac OS Device Driver ] <-> [ Mac System ]
 [ internet ]       [ tun virtual ]       [ read packets from piscsi0 and  ]
                    [  interface  ]       [ write them to the SCSI.     ]
                                          [ read the packets from SCSI  ]
                                          [ and write them to piscsi0.     ]

```

## Tools to debug network
In order to debug how the packets are being transferred these tools can be useful.

```
sudo apt-get install iputils-arping tcpdump
```


# Debugging
## check the logs
```
tail -f /var/log/rascsi.log
```

## Tools
### arping
```
arping -c 5 -I piscsi0 D6:90:8C:7A:17:6E
arping -c 5 -I piscsi0 192.168.0.1
```

### TCP Dump
Filter tcp traffic on the tun/tap interface
```
sudo tcpdump -I piscsi0 tcp
```


