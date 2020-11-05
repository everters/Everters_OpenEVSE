# Open EVSE -- Eergy
This is a modified version of the OpenEVSE board re-worked by Eergy.

The goal is to make OpenEVSE production easier and cheaper by manifacturing with parts sourced from LCSC and board made by JLCPCB.

Additionally, AC filter and a simplified GFCI circuitry (meant to be used with self contained GFCI filter such as the WA RCM 14-03) have been built in the design.  

## Changes

Power supply for the board does not use a double voltage AC-DC power block anymore. The AC-DC power block is now outputting 12V DC which are regulated to 5V using a 7805 IC. This makes the board simpler, less expensive and less sensitive to AC tension fluctuations which may change the secondary tension of the transforme.

GFCI logic has been removed. Open an issue if you still would like to have the old logic for the regular GFCI sensor used in OpenEVSE project.

A filter to make the board compliant with EU regulation has been added. The filter is obtained from here: https://github.com/openenergymonitor/openevse-ac-filter-pcb

Components have been changed in order to fit the requirements of JLCPCB and be sourced via LCSC. Some components could not be found at LCSC but these are mostly through hole components that can be installed later and manually.

Board connectors have been changed with harder to disconnect ones.

## How to use

In the editor, Click the document icon on the topbar, via "Document" > "Open" > "EasyEDA Source", and select json file, then open it in the editor.


## How to install firmware

Once your board is mnifactured and all components have been soldered in place, you can transfer the firmware to the Atmel microcontroller on the board. You will need a AVR ISP programmer like the one sold here: https://www.amazon.de/gp/product/B07Y3B8H91/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

As you program the Atmel for the first time remember to set the speed of the programmer to a lower speed. In the particular model of programmer linked above you will need to solder the contacts for a jumper in correspondence of JP3 and apply that jumper to the programmer.

### Firmware snapshot
The snapshot included in this repo was obtained here: https://github.com/openenergymonitor/open_evse/releases

The current firmware can be found in the repo above and also here. This is version 7.0.2 EU:
- Original open_evse firmware
- Open energy monitor version
- Open energy monitor threephase version

These files are the three files with .hex extension you can find in the repo.

### Commands to install firmware

More information on how to install firmware can be found here: https://openevse.dozuki.com/Guide/How+to+Load+OpenEVSE+Firmware+(WinAVR)/7

```
avrdude -c USBasp -p m328p -U lfuse:w:0xFF:m -U hfuse:w:0xDF:m -U efuse:w:0x05:m
avrdude -c USBasp -p m328p -V -U flash:w:open_evse.hex
avrdude -c USBasp -p m328p -V -U eeprom:w:eeprom_24.bin -V
```
For convenience eeprom_24.bin has been included in the repo.
