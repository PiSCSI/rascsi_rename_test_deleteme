# Farallon EtherMac SCSI
- Pictures: http://pictures.kyozou.com/pictures.aspx?id=0&prdet=6313459
- "made for Farallon by Dayna and is identical to the DaynaPORT DP0801"

# Farallon EtherMac MicroSCSI
- archived support page: https://web.archive.org/web/19980524084211/http://www.farallon.com:80/support/faqs/en/scsifaq.html
- Looks to be the same thing as a DaynaPort SCSI/Link-T (https://68kmla.org/forums/topic/29592-farallon-ethermac-adapter/)

# Sonic miniSCSI
- BSD Driver: http://members.iinet.net.au/~eyaleb/microSCSI/if_ssce.c
- According to forum post (https://www.applefritter.com/node/4959), this version should support OpenTransport

# Cabletron Systems EA419
From the BSD driver comments:
 * This is a weird device! It doesn't conform to the scsi spec in much
 * at all. About the only standard command supported is inquiry. Most
 * commands are 6 bytes long, but the recv data is only 1 byte.  Data
 * must be received by periodically polling the device with the recv
 * command.

- Ebay link: https://www.ebay.com/itm/Cabletron-Systems-EA419-SCSI-To-10Base-T-Adapter-With-Lanview/313320139796?hash=item48f355ec14:g:79EAAOSw4gRfwaOs


# Other interesting devices:
## USB XpressSCSI
USB 2.0 to SCSI adapter
- http://www.psism.com/usbxpressscsi.htm
