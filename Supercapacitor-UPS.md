# Background

The PiSCSI service caches data in RAM. When power is pulled from a PiSCSI/Raspberry Pi setup, it is possible to lose some or all of this data. In order to allow a graceful shutdown of the PiSCSI service and the Raspberry Pi OS, a USP can be added to the assembly. This way, when power is removed, the Raspberry Pi will have enough saved power to properly shut down.

# Prototype Phase: Dr. Scott M. Baker design

Dr. Scott M. Baker has designed two different UPS versions that will work with the PiSCSI. He has generously made these available on this blog for other people to use. [Tutorial video](https://www.youtube.com/watch?v=j5Bv8r3TVPM).

## Assembly
![image](https://user-images.githubusercontent.com/34318535/165860429-e71abe1e-e8b8-42eb-8194-94afd55ff2b6.png)

For akuker's initial prototype, he started with the [gerber files](https://github.com/sbelectronics/ups/tree/master/gerbers/12v) provided by Dr. Baker. At the time of this writting, ATTiny85 chips are in very short supply. However, I was able to acquire some through [Amazon] in small volumes. (https://smile.amazon.com/gp/product/B06W9JBJJ6/ref=ppx_yo_dt_b_asin_title_o04_s00?ie=UTF8&psc=1) The rest of the parts were ordered from Digikey:
![image](https://user-images.githubusercontent.com/34318535/165860847-f07941f5-336a-48c2-bd18-9706a9f4d247.png)

Note that for my initial prototype, I did not populate all of the connectors. I also did not populate the voltage dividers on the USB port (R15, R16, R17, R18). The "ORK" buck converter used by Dr. Baker was also not available. For one prototype, I used a [7805TV voltage regulator](https://www.sparkfun.com/datasheets/Components/LM7805.pdf). For the other, I bodged in a [LM2596S voltage regulator](https://www.ti.com/lit/ds/symlink/lm2596.pdf?ts=1651114146845&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FLM2596%253Futm_source%253Dgoogle%2526utm_medium%253Dcpc%2526utm_campaign%253Dapp-null-null-GPN_EN-cpc-pf-google-wwe%2526utm_content%253DLM2596%2526ds_k%253DLM2596%2526DCM%253Dyes%2526gclid%253DCj0KCQjw06OTBhC_ARIsAAU1yOUmvCB1WjcI1iKPeRtjK6ZXnT-MiqXwZSRntonhIAZ8ne8dBUrtJYsaAkxREALw_wcB%2526gclsrc%253Daw.ds), which has a higher amperage rating.

## Programming the ATTiny85

For programming the ATTin85, I followed these instructions: https://create.arduino.cc/projecthub/arjun/programming-attiny85-with-arduino-uno-afb829

For me, the pin names were very confusing. Here's my conversion table:

| Arduino Pin  | ATtiny85 Physical Pin | ATtiny85 Logical Pin | UPS Board Name |
| ------------ | --------------------- | -------------------- | -------------- |
| 5v           |  8                    | Vcc                  | +5v            |
| Gnd          |  4                    | Gnd                  | Gnd            |
| Pin 13 (D13) |  7                    | Pin 2                | SCL            |
| Pin 12 (D12) |  6                    | Pin 1                | VIN_Sense      |
| Pin 11 (D11) |  5                    | Pin 0                | SDA            |
| Pin 10 (D10) |  1                    |  Reset               | Reset          |

You'll need to install the [TinyWireS](https://github.com/nadavmatalon/TinyWireS) library following [these instructions](https://www.baldengineer.com/installing-arduino-library-from-github.html).

# "Official" PiSCSI version

For the PiSCSI, akuker will be focusing on the 12v version of Dr. Baker's UPS. A modified version of this is being designed and will be offered in the Tindie store (when it is ready). 