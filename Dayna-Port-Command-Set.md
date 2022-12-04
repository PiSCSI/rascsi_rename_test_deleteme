
# DaynaPort SCSI/Link: SCSI Command Set
[Original version](http://www.bitsavers.org/pdf/apple/scsi/dayna/daynaPORT/SLINKCMD.TXT) Copyright 2002-2005 by Roger Burrows.

The current version is made available under [Creative Commons BY-SA](https://creativecommons.org/licenses/by-sa/4.0/legalcode). For additional information, see the end of this document.

Some reference data captures are available here:
https://github.com/piscsi/PiSCSI/tree/daynaport/doc/data_captures/daynaport

# SCOPE
This document applies to the following hardware devices:
- DaynaPort SCSI/Link-T (Model DP0801)
- DaynaPort SCSI/Link-3 (Model DP0802)

and to the following firmware revisions:
- 1.4a
- 2.0f

It probably also applies to other firmware revisions; it may also apply to other Dayna SCSI/Link devices.  Any feedback on this is welcomed.

All numbers are expressed in hexadecimal, unless otherwise noted.

# COMMAND SET SUMMARY
The following is a partial list of implemented SCSI commands:
- 03    Request Sense
- 08    Read
- 09    Retrieve Statistics
- 0a    Write
- 0c    Set Interface Mode / Set MAC Address
- 0d    Multicast Enable Command
- 0e    Enable/disable Interface
- 12    Inquiry

A number of other SCSI commands are implemented, but their usage is not yet fully known.

## Multicast Enable Command (0d)
Command:  0d 00 00 00 06 00

Function: Configures the DaynaPort SCSI/Link to accept/reject multicast address.

Type:     Input (Transitions to DATAOUT)

Host then sends: `00 09 00 07 FF FF FF 00` (The last 00 might not actually be there?)

Note: The AppleTalk broadcast address is 09:00:07:ff:ff:ff.

This is configuring the Multicast Address Registers of the [DP83902A Ethernet receiver](./docs/DP83902A.pdf) inside the DaynaPort SCSI Link

    10.9 MULTICAST ADDRESS REGISTERS (MAR0 –MAR7)
    
    The multicast address registers provide filtering of multicast 
    addresses hashed by the CRC logic. All destination addresses 
    are fed through the CRC logic and as the last bit of the 
    destination address enters the CRC, the 6 most significant bits 
    of the CRC generator are latched. These 6 bits are then decoded 
    by a 1 of 64 decode to index a unique filter bit (FB0 –63) in 
    the multicast address registers. If the filter bit selected is 
    set, the multicast packet is accepted. The system designer 
    would use a program to determine which filter bits to set in 
    the multicast registers. All multicast filter bits that 
    correspond to multicast address accepted by the node are then 
    set to one. To accept all multicast packets all of the 
    registers are set to all ones.



## Enable/disable Interface (0e)
Command:  0e 00 00 00 00 XX (XX = 80 or 00)

Function: Enable (80) / disable (00) Ethernet interface

Type:     No data transferred

Notes:    After issuing an Enable, the initiator should avoid sending
          any subsequent commands to the device for approximately 0.5
          seconds

## Inquiry (12)
Command:  `12 00 00 00 LL 00` (LL is data length)

Function: Perform a standard SCSI Inquiry command: reference the
          SCSI spec for further information

Type:     Input; reference the SCSI spec for the data returned

Example Response:
  |Byte Num|Value|Decoded| \| |Byte Num|Value|Decoded| \| |Byte Num|Value|Decoded|
  |--------|-----|-------|---|--------|-----|-------|---|--------|-----|-------|
  |0 | 03| Peripheral Type = 3 (CPU)|\|| 16| 53| S |\|| 32| 31| 1 |
  |1 | 00|                          |\|| 17| 43| C |\|| 33| 2E| . |
  |2 | 01| SCSI Version 1           |\|| 18| 53| S |\|| 34| 34| 4 |
  |3 | 00|                          |\|| 19| 49| I |\|| 35| 61| a |
  |4 | 1E| Additional Length = 30   |\|| 20| 2F| / |
  |5 | 00|                          |\|| 21| 4C| L |
  |6 | 00|                          |\|| 22| 69| i |
  |7 | 00|                          |\|| 69| 6E| n |
  |8 | 44| D                        |\|| 24| 6B| k |
  |9 | 61| a                        |\|| 25| 20| (sp) |
  |10| 79| y                        |\|| 26| 20| (sp) |
  |11| 6E| n                        |\|| 27| 20| (sp) |
  |12| 61| a                        |\|| 28| 20| (sp) |
  |13| 20| (sp)                     |\|| 29| 20| (sp) |
  |14| 20| (sp)                     |\|| 30| 20| (sp) |
  |15| 20| (sp)                     |\|| 31| 20| (sp) |

Notes:    
- The length is user-selectable to a maximum of 25 (37 decimal)
- Some tools send other SCSI lengths. Example: SCSIProbe on 68k Macs has a length of 05

## Read (08)
Command:  08 00 00 LL LL XX (LLLL is data length, XX = c0 or 80)

Function: Read a packet at a time from the device (standard SCSI Read)

Type:     Input; the following data is returned:
          LL LL NN NN NN NN XX XX XX ... CC CC CC CC

where:

          LLLL      is normally the length of the packet (a 2-byte
                    big-endian hex value), including 4 trailing bytes
                    of CRC, but excluding itself and the flag field.
                    See below for special values

          NNNNNNNN  is a 4-byte flag field with the following meanings:
                    FFFFFFFF  a packet has been dropped (?); in this case
                              the length field appears to be always 4000
                    00000010  there are more packets currently available
                              in SCSI/Link memory
                    00000000  this is the last packet

          XX XX ... is the actual packet

          CCCCCCCC  is the CRC


Notes:
- When there is no data to be received, the DaynaPort will respond by going to the DataIn phase snd sending ``00 00 00``
-  When all packets have been retrieved successfully, a length field of 0000 is returned; however, if a packet has been dropped, the SCSI/Link will instead return a non-zero length field with a flag of FFFFFFFF when there are no more packets available.  This behaviour seems to continue until a disable/enable sequence has been issued.
- The SCSI/Link apparently has about 6KB buffer space for packets.

Example:
Sending an ARPING to the Mac host from an attached Linux device. 
- Raw ARPING Data: 

    ``00 80 19 10 98 e3 dc a6 32 1c 4e 69 08 00 45 00``

    ``00 1c dc 51 00 00 40 01 76 a7 a9 fe 7d ea ff ff``
    
    ``ff ff 08 00 1b aa dc 51 00 04 00 00 00 00 00 00``
    
    ``00 00 00 00 00 00 00 00 00 00``

- Read request command:   `08 00 00 05 F4 C0`

- Mac's response (DATAIN):
  
    ``00 40 00 00 00 00`` *Length & Flag fields*
    
    ``00 80 19 10 98 e3 dc a6 32 1c 4e 69 08 00 45 00``

    ``00 1c dc 51 00 00 40 01 76 a7 a9 fe 7d ea ff ff``

    ``ff ff 08 00 1b aa dc 51 00 04 00 00 00 00 00 00``
    
    ``00 00 00 00 00 00 00 00 00 00``
    
    ``a1 85 ed ff 5b`` *CRC*

## Request Sense (03)
Command:  `03 00 00 00 00 00`

Function: Perform a standard SCSI Request Sense command

Type:     Input; reference the SCSI spec for the data returned

Notes:
- This command always transfers exactly 9 bytes of data (note that cdb byte 4 is always zero, however).
- If the sense key is 5, the driver should reinitialise the device via a disable/enable sequence; otherwise, it need do nothing.

## Retrieve Statistics (09)
Command:  `09 00 00 00 12 00`

  ***(akuker note)***: `09 00 00 00 06 00` was observed during hardware diagnostics

Function: Retrieve MAC address and device statistics

Type:     Input; returns 18 (decimal) bytes of data as follows:
- bytes 0-5:  the current hardware ethernet (MAC) address
- bytes 6-17: three long word (4-byte) counters (little-endian).

Notes:
- The contents of the three longs are typically zero, and their usage is unclear; they are suspected to be:
  - long #1: frame alignment errors
  - long #2: CRC errors
  - long #3: frames lost

## Set Interface Mode (0c)
Command:  0c 00 00 00 FF 80 (FF = 08 or 04)

Function: Allow interface to receive broadcast messages (FF = 04); the
          function of (FF = 08) is currently unknown.

Type:     No data transferred

Notes:    This command is accepted by firmware 1.4a & 2.0f, but has no
          effect on 2.0f, which is always capable of receiving broadcast
          messages.  In 1.4a, once broadcast mode is set, it remains set
          until the interface is disabled.


## Set MAC Address (0c)
Command:  0c 00 00 00 FF 40 (FF = 08 or 04)

Function: Set MAC address

Type:     Output; overrides built-in MAC address with user-specified
          6-byte value

Notes:    This command is intended primarily for debugging/test purposes.
          Disabling the interface resets the MAC address to the built-in
          value.

## Write (0a)
Command:  0a 00 00 LL LL XX (LLLL is data length, XX = 80 or 00)

Function: Write a packet at a time to the device (standard SCSI Write)

Type:     Output; the format of the data to be sent depends on the value
          of XX, as follows:

           if XX = 00, LLLL is the packet length, and the data to be sent
             must be an image of the data packet
           if XX = 80, LLLL is the packet length + 8, and the data to be
             sent is:
               PP PP 00 00 XX XX XX ... 00 00 00 00
             where:
               PPPP      is the actual (2-byte big-endian) packet length
               XX XX ... is the actual packet






# Hardware Diagnostics
When the DaynaPort Hardware Diagnostics tool is executed, the following behavior is observed:
- The SCSI bus is scanned for all SCSI IDs, but doing a Selection and waiting for the device to respond. This will go from SCSI 6..0
  - When a device responds to the selection, a 0E (Enable/Disable Interface) command is sent to the SCSI device, with the last byte set to 00 (indicating that the device should be disabled).
- The SCSI bus is scanned a second time, with an Inquiry command (12). This time, the scan will stop when the DaynaPort device is detected.
- Next, the host will send a Retrieve Statistics (09) command to the DaynaPort. `09 00 00 00 06 00`
  - The DaynaPort will respond with the requested data - 18 bytes long `00 80 10 FB E3 00 00 00 ...` (Note: scsimon wasn't able to accuratly capture the REQ/ACK signals - so I'm only assuming the response was 18 bytes long)
- The host will then send an INQUIRY command to the DaynaPort `09 00 00 00 12 00`
  - The DaynaPort will respond with `80 19 10 FB E3 00 00 00 00`
  - The host will send the Enable/Disable Interface command (0E) with the last byte set to 00 (indicating the device should be disabled)

After this, Hardware Diagnostics tool will wait for the user to reboot the Mac.

# Software Diagnostics
When the Software Diagnostics application is launched, it appears to only send a Request Statistics (09) command to the DaynaPort. `09 00 00 00 12 00`

The DaynaPort appears to respond with the standard 18 byte response. For example: `80 19 10 98 E3 00 00 00 00 ...`

The statistics information doesn't appear to be reported anywhere (that I can find).

# Mac Startup Sequence
At startup, the Mac will issue a Read command (08) (`08 00 00 00 01 00`). The target will then respond by going into the status state with data of `02`, followed by a MSGIN of 00




========================= END OF DOCUMENT =========================

# Document History
The original version of this document was distributed by Roger Burrows with the following copyright information:

``Copyright 2002-2005 by Roger Burrows.  All Rights Reserved.  Permission is granted to copy this document providing that no changes are made to the contents.``

``LIMITATION OF LIABILITY AND DISCLAIMER OF WARRANTY``

``The information cantained in this document is provided "as-is", without warranty of any kind, expressed or implied, including without limitation any warranty concerning the accuracy, adequacy, or completeness of such information or material.  The Author shall not be responsible for any claims attributable to errors, omissions, or other inaccuracies in the information or material contained in this document, and in no event shall the Author be liable for direct, indirect, special, incidental, or consequential damages arising out of the use of such information or material.``

[akuker](https://www.github.com/akuker) has contacted Roger Burrows and has received permission to modify and re-distribute this information. The Creative Commons (CC BY-SA) license is currently used to distribute this documentation.

The original revision history of this document follows:
- Version 1.00 (8/August/2002) Original version
- Version 1.10 (22/April/2005) Added description of 'Set Interface Mode/Set MAC Address' command
- Version 1.20 (16/July/2005) Corrected description of 'Set Interface Mode/Set MAC Address' command

The current version history of this document is maintained in the PiSCSI Github Wiki at: https://github.com/piscsi/piscsi/wiki/Dayna-Port-Command-Set