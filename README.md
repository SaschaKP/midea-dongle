
# Midea WiFi Dongle - v3

This repo is a complete rework of [Rene Klootwijk's repository](https://github.com/reneklootwijk/mideahvac-dongle). So credits for the initial hardware study and design go to him!

I've made a lot of changes to the board:
* the board will fit inside the original spacer, occuping the original space, but without casing
* all pads can be soldered with hot-air gun and soldering paste, they are slightly larger for that purpose in mind
* it uses an ESP32 C6 and the software for making it work with this dongle (esphome) can be found [in my repository](https://github.com/SaschaKP/esphome-midea-direct)
* Converted the KiCad project to KiCad 9

For this particular repository you can use an ESP32 C6 MINI (WT0132C6-S5) that can be used as a drop-in replacement for ESP-12F

That's what the board now looks like:
![How it looks](https://github.com/SaschaKP/midea-dongle/blob/main/images/3d_model.png?raw=true)
![Real Object DIY](https://github.com/SaschaKP/midea-dongle/blob/main/images/dongle-diy.png?raw=true)

## PCB and Parts
* The buttons are 3x4mm in size. Height is up to your liking. Can easily be found on AliExpress:
![Buttons](https://github.com/SaschaKP/midea-dongle/blob/main/images/buttons.png?raw=true)
* Specs of the USB jack, can also be found on AliExpress:
![USB Jack](https://github.com/SaschaKP/midea-dongle/blob/main/images/usb-jack.png?raw=true)
* LDO Caps (C1 & C2) can be either tantalum or ceramic: Officially should be tantalum, but ceramic work just fine. 
* Remember that the WT0132C6-S5 (ESP32 C6 MINI) is interchangeable with ESP-12F or ESP-07 which offers an external antenna:
![Boards with ESP-07 and ESP-12F](https://github.com/SaschaKP/midea-dongle/blob/main/images/esp-07-12.jpg?raw=true)

I **highly** recommend taking a look at the iBOM file that can also be found in the "production-files" folder. It makes sourcing the parts and soldering so much easier!

## Flashing
Flashing the ESP can be done using any USB-to-UART adapter. I recommend getting an USB-A-socket cable with open ends, so you can crimp a dupont at the open end.
So TX from the dongle goes to RX on the UART adapter and RX from the dongle goes to TX on the UART adapter. Set the UART adapter to 5V. Yes, it is safe. You will **not** burn the ESP in this case! The board has two mosfets that will switch the pins to 3v3.
Now how to actually flash the board:
 1. Create a new device under "ESPHome Builder" in Home Assistant. Choose `ESP32 C6 devkitm` as board
 2. You can find an example config under "esphome". Edit the config in ESPHome builder and substitute the placeholders and potentially the board.
 3. Install and download.
 4. Now open [ESPHome Web](https://web.esphome.io)
 5. Connect the UART adapter to your PC, but not the dongle just yet!
 6. Hold the "PRG" button on the dongle and keep holding it!
 7. Now connect the dongle to the UART adapter.
 8. Click "Connect" on ESPHome Web, select the UART adapter, click "Install", select the bin you've just built and downloaded and flash it.
 9. As soon as it says "Erasing" or "Flashing", you can release the "PRG" button.
 10. Wait  for it to be installed and it will show up in your Wi-Fi and under "Devices" in Home Assistant
