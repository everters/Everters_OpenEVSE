# Open EVSE -- Eergy
This is a modified version of the OpenEVSE board re-worked by Eergy.

The goal is to make OpenEVSE production easier and cheaper by manifacturing with parts sourced from LCSC and board made by JLCPCB.

Additionally, AC filter and a simplified GFCI circuitry (meant to be used with self contained GFCI filter such as the WA RCM 14-03) have been built in the design.  

## How to use

At editor, Click the document icon on the topbar, via "Document" > "Open" > "EasyEDA Source", and select json file, then open it at the editor.


## How to install firmware

Once your board is mnifactured and all components have been soldered in place, you can transfer the firmware to the Atmel microcontroller on the board. You will need a AVR ISP programmer like the one sold here: https://www.amazon.de/gp/product/B07Y3B8H91/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

As you program the Atmel for the first time remember to set the speed of the programmer to a lower speed. In the particular model of programmer linked above you will need to solder the contacts for a jumper in correspondence of JP3 and apply that jumper to the programmer.

### Firmware snapshot
The snapshot included in this repo was obtained here:

The current firmware can be found in this repo. There are three versions of the firmware reported here:
- Original version compiled on the 27th of August 2020 
- Open energy monitor version
- Open energy monitor threephase version

These files are thre three files with .hex extension you can find in the repo

### Commands to install firmware

More information on how to install firmware can be found here: https://openevse.dozuki.com/Guide/How+to+Load+OpenEVSE+Firmware+(WinAVR)/7

```
avrdude -c USBasp -p m328p -U lfuse:w:0xFF:m -U hfuse:w:0xDF:m -U efuse:w:0x05:m
avrdude -c USBasp -p m328p -V -U flash:w:open_evse.hex
avrdude -c USBasp -p m328p -V -U eeprom:w:eeprom_24.bin -V
```
