The original PiSCSI uses the [SN74LS641](https://www.ti.com/lit/ds/symlink/sn74ls641.pdf) bus transceiver. However, with each device needed 4 of these @ $3.30 each, the amounts to a significant percentage of the cost. The following contains some notes regarding what other SCSI emulators have used.


| Suitable for PiSCSI? | Product | Chip and Datasheet | Cost ($) | Qty needed | Notes |
| - | - | - |  - |  - |  - | 
| ✅ | PiSCSI Original Version | [SN74LS641-1](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74LS641-1DW?qs=SL3LIuy2dWxXHvPKLk%252BfLw%3D%3D) | [$3.66 US](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74LS641-1DW?qs=SL3LIuy2dWxXHvPKLk%252BfLw%3D%3D)|  4 |  VCC is 5v |
| ✅❓ | Potential Candidate | [SN74ALS245A-1](https://www.ti.com/lit/ds/symlink/sn74als245a.pdf) | [$1.42 US](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74ALS245A-1NSR?qs=zhgwDAIOVxtxt0cXsshpuw%3D%3D) | 4 | VCC 5v, -1 unit will sink 48mA |
| ✅❓ | Potential Candidate | [SN74F245DW](https://www.ti.com/lit/ds/symlink/sn74f245.pdf?)| [$1.11 US](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74F245DW?qs=rshUhwi3fbYzYsqSsk5U6A%3D%3D) | 4 | Low state current can sink 48mA|
| ✅❓ | Potential Candidate | [SN74ABT245B](https://www.ti.com/lit/ds/symlink/sn74abt245b.pdf) | [$1.00 - $1.30 US](https://www.mouser.com/c/semiconductors/logic-ics/bus-transceivers/?m=Texas%20Instruments&series=SN74ABT245B) | 4 | |
| ✅ | [AIBOM RaSCSI](http://products.aibom.net/rascsi/) Transceiver | [SN75LBC968](https://www.ti.com/lit/ds/symlink/sn75lbc968.pdf?ts=1644640425194&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FSN75LBC968) | [$10.98 US](https://www.ti.com/product/SN75LBC968#order-quality) | 2 | |
| ❌ | [Scuznet](https://github.com/saybur/scuznet) | [SN74LVTH126DR](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74LVTH126DR/?qs=sGAEpiMZZMtYFXwiBRPs0%252b5WI0cyeyLc) |  0.64 |  4 |  - | 
| ❌ | Scsi2SD - According to [LC-SCSI](https://github.com/pgodwin/LC-SCSI/wiki) | [SN74LVT245B](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74LVT245BPWR?qs=afYny40WCj1v38f4br9Q%2Fg%3D%3D), [Data Sheet](https://www.ti.com/lit/ds/symlink/sn74lvt245b.pdf) |  0.90 |  4 |  VCC is 3.3v | 
| ❌ | Scsi2SD V5.1 (2018d) | SN74LVT125 [SOIC-14](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74LVT125DR?qs=6gY4t2uohMwiYO%252BkwyNnEQ%3D%3D), [TSSOP-14](https://www.mouser.com/ProductDetail/Texas-Instruments/SN74LVT125PWR?qs=%252BWCn1GN4mVw7a5M8tQ6X9A%3D%3D), [Data Sheet](https://www.ti.com/lit/ds/symlink/sn74lvt125.pdf) | 0.87 | ? | "3.3V ABT Quadruple Bus Buffer with 3-state outputs"
| ❌ | Unsuitable | [74AHC245](https://datasheet.lcsc.com/szlcsc/Nexperia-74AHCT245PW-118_C173388.pdf) |  [0.22](https://lcsc.com/product-detail/74-Series_Nexperia-74AHCT245PW-118_C173388.html) |  4 |  VCC is 5v. Datasheet reads input clamping current -20mA | 
| ❌ | Unsuitable | [SN74LS245DW](https://www.ti.com/lit/ds/symlink/sn74ls245.pdf?HQS=TI-null-null-mousermode-df-pf-null-wwe&ts=1599280883179&ref_url=https%253A%252F%252Fwww.mouser.ca%252F) | 1.34| 4 | Can only sink 24mA, SCSI protocol requires 48mA |
| ❌ | Unsuitable| [SN7406DRG4](https://www.ti.com/lit/ds/symlink/sn7406.pdf?HQS=TI-null-null-digikeymode-df-pf-null-wwe&ts=1599282149626)| 1.34 | 4 | Can only sink 40mA. Will require new layout and increase in chip count as it has less i/o than above. |
| ❌ | Unsuitable | [74HCT245D](https://assets.nexperia.com/documents/data-sheet/74HC_HCT245.pdf) | [$0.69 US](https://www.mouser.com/ProductDetail/Nexperia/74HCT245D653?qs=P62ublwmbi%2FKRO6CQW%252BPyg%3D%3D)  | 4 | VCC is 5v. Datasheet reads input clamping current -20mA  |

Note: as of 2020-08-04 the **SN74LS641-1** is the transceiver suggested when building the PiSCSI.


Some additional parts

| Part| Chip and Datasheet | Cost ($) | Qty needed | Notes |
| - | - |  - |  - |  - | 
| Linear Regulator (for active terminator) | [LM1117SX](https://www.mouser.com/ProductDetail/Texas-Instruments/LM1117SX-ADJ-NOPB?qs=X1J7HmVL2ZFVdHO2uaroKA%3D%3D) | 1.51 | 1 | 800mA LDO |

## Discussion

### Raspberry Pi
The following descriptions are sourced from the RPi's official documentation, but may vary between different versions of the RPi (0, 1, 2, 3, 4, etc).

The documentation on the Raspberry Pi's GPIO pins [is here](https://www.raspberrypi.org/documentation/hardware/raspberrypi/gpio/README.md).
> Each of the three banks has its own VDD input pin. On Raspberry Pi, all GPIO banks are supplied from 3.3V. Connection of a GPIO to a voltage higher than 3.3V will likely destroy the GPIO block within the SoC.

While the drive current of the GPIO pins are configurable up to 16mA, the 3.3v supply that powers them [cannot reach the maximum current for all pins](https://www.raspberrypi.org/documentation/hardware/raspberrypi/gpio/gpio_pads_control.md).
> The Raspberry Pi 3V3 supply was designed with a maximum current of ~3mA per GPIO pin. If you load each pin with 16mA, the total current is 272mA. The 3V3 supply will collapse under that level of load.

Simultaneously, [at 3.3v the pins are rated to sink at least 18mA and still meet spec](https://www.raspberrypi.org/documentation/hardware/raspberrypi/gpio/README.md).

### SCSI-2 Bus
The SCSI protocol suggests drivers capable of sinking 48mA. [(1)](#ref-1) You can see in [this example](http://www.interfacebus.com/Glossary-of-Terms-SCSI-interface-schematic.html) of a SCSI interface circuit.

[This reference](https://www.ti.com/lit/an/slla035/slla035.pdf) on SCSI terminators also states
> ... (i)t is the terminator’s job to source as much current as possible during deassertion. This role is restricted by the SCSI specification, however, which limits each terminator to supplying a maximum of 24mA to prevent the line current from exceeding the 48mA current sink limit of the open-collector drivers. (pg 8)

There is also a discussion of the role of passive and active SCSI termination in [this reference](https://www.microsemi.com/document-portal/doc_download/14643-an-1-understanding-the-single-ended-scsi-bus) (see pg 10).

See [section 5.4 of the SCSI-2 standard](https://www.staff.uni-mainz.de/tacke/scsi/SCSI2-05.html)

    5.4.1 Single-ended alternative
    All signals not defined as RESERVED, GROUND, or TERMPWR shall be terminated at both ends of 
    the cable. The implementor may choose one of the following two methods to terminate each end
    (see figures 9 and 10):

    a) The termination of each signal shall consist of 220 ohms (+/-5%) to the TERMPWR line and 
       330 ohms (+/-5%) to ground. Using resistors with +/-1% tolerance improves noise margins.
    b) The termination of each signal shall meet these requirements:
        1) The terminators shall each supply a characteristic impedance between 100 ohms and 
           132 ohms.
        2) The terminators shall be powered by the TERMPWR line and may receive additional power
           from other sources but shall not require such additional power for proper operation 
           (see 5.4.3).
        3) The current available to any signal line driver shall not exceed 48 mA when the driver
           asserts the line and pulls it to 0.5 V d.c. Only 44.8 mA of this current shall be 
           available from the two terminators.
        4) The voltage on all released signal lines shall be at least 2.5 V d.c. when the 
           TERMPWR line is within specified values (see 5.4.3).
        5) These conditions shall be met with any legal configuration of targets and initiators
           as long as at least one device is supplying TERMPWR. 


    5.4.1.1 Output characteristics
    All signals shall use open-collector or three-state drivers. Each signal driven by an SCSI
    device shall have the following output characteristics when measured at the SCSI device's 
    connector:
        VOL (low-level output voltage)  = 0.0 to 0.5 V d.c. at 48 mA sinking (signal assertion)
        VOH (high-level output voltage) = 2.5 to 5.25 V d.c. (signal negation) 

    5.4.1.2 Input characteristics
    SCSI devices with power on shall meet the following electrical characteristics on each 
    signal (including both receivers and passive drivers):
        VIL (low-level input voltage)   = 0.0 V d.c. to 0.8 V d.c. (signal true)
        VIH (high-level input voltage)  = 2.0 V d.c. to 5.25 V d.c. (signal false)
        IIL (low-level input current)   = -0.4 mA to 0.0 mA at VI = 0.5 V d.c.
        IIH (high-level input current)  = 0.0 mA to 0.1 mA at VI = 2.7 V d.c.
        Minimum input hysteresis        = 0.2 V d.c.
        Maximum input capacitance       = 25 pF (measured at the device connector
                                          closest to the stub, if any, within the
                                          device) 

    It is recommended that SCSI devices with power off also meet the above IIL and IIH 
    electrical characteristics on each signal.
    To achieve maximum noise immunity and to assure proper operation with complex cable 
    configurations, it is recommended that the nominal switching threshold be approximately 1.4 V. 


### PiSCSI
From [the v1.6 schematic](https://github.com/piscsi/piscsi/blob/master/hw/rascsi_1p6/rascsi_din.sch.pdf), the following signals need to be bidirectional:

> DP, D0, D1, D2, D3, D4, D5, D6, D7

Similarly, the following signals are **from** the RPi **to** the SCSI bus:

> BSY, MSG, C_D, REQ, I_O

For SCSI-2, it seems that the drivers should be open-collector/open-drain drivers (ie: they can pull the bus down to ground, and the termination on the bus will pull back high.) 

Finally, these are the signals **to** the RPi **from** the SCSI bus:

> ATN, ACK, RST, SEL

They should probably be Schmitt-trigger inputs on the SCSI bus side. See the "Single-Ended SCSI" section of [this document](https://www.ti.com/lit/an/slla035/slla035.pdf); specifically page 8 of the PDF.

    2.85v Typical SCSI Open-Circuit Voltage
    2.5v SCSI Minimum Output Voltage for Deasserted Signal
    2v SCSI Minimum Input Voltage for Deasserted Signal
    ...
    0.8v Maximum Input Voltage for Asserted Signal
    0.5v SCSI Maximum Output Voltage for Asserted Signal
    0.2v Typical Driver-Asserted Signal

From [the 2.x schematic](https://github.com/piscsi/piscsi/blob/master/hw/rascsi_2p1/rascsi_2p1_sch.pdf), all signals are bidirectional, switched on three different signals.

Switched by `PI-DTD`:

> DP, D0, D1, D2, D3, D4, D5, D6, D7

Switched by `PI-TAD`:

> BSY, MSG, C_D, REQ, I_O

Switched by `PI-IND`:

> ATN, ACK, RST, SEL



# Detailed discusison/comparison

## 74xx series logic parts

[Wikipedia list of 74xx logic parts](https://en.wikipedia.org/wiki/List_of_7400-series_integrated_circuits#74x200_%E2%80%93_74x299)

|Part number	| Units	| Description	| Input	| Output	| Pins	| Datasheet|
| ------------- | ----- | ------------- | ----- | ------------- | ----- | ---------|
| 74x125	| 4	| quad bus buffer, negative enable		| 		| three-state	| 14	| SN74LS125A |
| 74x126	| 4	| quad bus buffer, positive enable		| 		| three-state	| 14	| SN74LS126A |
| 74x245	| 8	| octal bus transceiver, non-inverting outputs	| Schmitt trigger | three-state	| 20	| SN74LS245 |
| 74x641	| 1	| octal bus transceiver, non-inverting outputs	|		| open-collector| 20	| SN74LS641 |

## Logic Families

[Texas Instruments Logic guide](https://www.ti.com/lit/sg/sdyu001ab/sdyu001ab.pdf)

LS, LVTH, LVT, AHCT, F, AHC, ALS, F, ABT, HCT, 

|  | Families      | Voltage| Process  | Bus-Hold | Series Damping Resistors | IOFF F (Partial Power Down)| Schmitt Triggers | Overvoltagetolerant Inputs | Power-off Output Disable  | Power-up 3-State |
| -- | ----------- | ------ | -------- |---|---|---|---|---|---|---|
| ❓ |ABT		| 5	 | Bi-CMOS  | X | X |   |   |   | X | X |
| ❓ |AHC		| 3.3, 5 | CMOS     |   |   |   |   | X | X |   |
| ❓ | AHCT/HCT	| 5	 | CMOS     |   |   |   |   | X | X |   |
| ❓ | ALS		| 5	 | Bi-Polar |   |   |   |   |   |   |   |
| ❓ | F		| 5	 | Bi-Polar |   | X |   |   |   |   |   |
| ✅ | LS		| 5	 | Bi-Polar |   |   |   |   |   |   |   |
| ❌ | LVT/LVTH *	| **3.3** | Bi-CMOS  | X | X | X |   |   | X | X |


* LVT/LVTH: The original LVT devices had the bus-hold feature. The LVTH replacements for these devices not only have bus hold, but also
have the High-Impedance State During Power Up and Power Down feature





## What about NTS0104?

# Notes

<a name="ref-1">(1)</a> [Comment by `saybur`](https://68kmla.org/forums/index.php?app=forums&module=forums&controller=topic&id=30399&page=7&tab=comments#comment-646496)
