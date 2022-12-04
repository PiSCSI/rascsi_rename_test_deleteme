<b>Work on the Nuvolink emulation has stopped. The Nuvolink relies on the Reselection operation, which is NOT currently supported by PiSCSI. Since the <a href="https://github.com/piscsi/piscsi/wiki/Dayna-Port-SCSI-Link">Dayna Port SCSI/Link</a>  functionality is working, no additional effort is planned for the Nuvolink.<b>

---------

# Background
[Saybur](https://github.com/saybur) has developed some fantastic [documentation](https://github.com/saybur/scuznet/blob/master/PROTOCOL.md) about how the Nuvolink SCSI protocol works. He has taken that and implemented it into the ["Scuznet"](https://github.com/saybur/scuznet) device. 

# Nuvolink & PiSCSI
The first attempt at a SCSI Ethernet device was using the documentation from Saybur. All of this code is in the "nuvolink" Github branch. The current status is:
- The Macintosh driver will recognize the simulated Nuvolink device
- Outgoing traffic from the Macintosh will go out the SCSI bus and be received by the PiSCSI. It is then passed on to the TAP Linux device, where it can be seen in wireshark.

Below is a summary of the SCSI commands and their current status:
- 0x00: TEST UNIT READY (cmmd_tstrdy) **WORKING**
- 0x02: "Reset Statistics" Vendor Specific Command (cmmd_ethrst) **NOT IMPLEMENTED**
- 0x03: REQUEST SENSE (cmmd_rqsens) **NOT IMPLEMENTED**
- 0x05: "Send Packet" Vendor Specific Command (cmd_ethwrt) **WORKING, BUT NOT THOROUGHLY TESTED**
- 0x06: "Change MAC Address" Vendor Specific Command (cmd_addr) **INCOMPLETE IMPLEMENTATION**
- 0x08: GET MESSAGE(6) (probably cmmd_getmsg) **NOT IMPLEMENTED**
- 0x09: "Set Multicast Registers" (cmmd_mcast) **INCOMPLETE IMPLEMENTATION**
- 0x0A: SEND MESSAGE(6) (probably cmmd_sndmsg) **NOT IMPLEMENTED**
- 0x0C: Unknown Vendor Specific Command (probably cmmd_mdsens) **NOT IMPLEMENTED**
- 0x12: INQUIRY (cmmd_inq) **WORKING, STATISTICS ARE STATIC DATA**
- 0x1C: RECEIVE DIAGNOSTIC RESULTS (cmmd_rdiag) **NOT IMPLEMENTED**
- 0x1D: SEND DIAGNOSTIC (cmmd_sdiag) **NOT IMPLEMENTED**

# Current status - ON HOLD
The "Standard Packet Reception" functionality of the NuvoLink relies on a RESELECT SCSI function. Typically, only the computer will initiate a SCSI transaction using a SELECT operation. However, the NuvoLink will initiate a transaction with the host computer whenever a new packet is received.

This approach prevents the host driver from needing to periodically "poll" the Nuvolink device, which is a definite benefit. However, in its current design, PiSCSI is set up to do a RESELECT. 

It will be a non-trivial architectural change to enable RESELECT functionality. Therefore, the PiSCSI NuvoLink emulation is indefinitely **ON HOLD**. The DaynaPort SCSI Link driver for the Mac OS appears to periodically poll the DaynaPort, which means that the RESELECT function may not be needed.