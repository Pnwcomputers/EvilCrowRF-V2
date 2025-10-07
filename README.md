# EvilCrowRF-V2

![EvilCrow](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/Logo1.png)

**Idea, development and implementation:** Joel Serna (@JoelSernaMoreno).

**Main collaborator:** Little Satan (https://github.com/LSatan/)

**Other collaborators:** Jordi Castelló (@iordic), Eduardo Blázquez (@_eblazquez), Federico Maggi (@phretor), Andrea Guglielmini (@Guglio95) and RFQuack (@rfquack).

**PCB design:** Ignacio Díaz Álvarez (@Nacon_96), Forensic Security (@ForensicSec) and April Brother (@aprbrother).

**Manufacturer and distributor:** April Brother (@aprbrother).

**Distributor from United Kingdom:** KSEC Worldwide (@KSEC_KC).

The developers and collaborators of this project do not earn money with this. 
You can invite Joel for a coffee to further develop Low-Cost hacking devices. If you don't invite him for a coffee, nothing happens, he will continue developing devices.

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/E1E614OA5)

**Available with April Brother (shipping from China):** 

* Evil Crow RF V2 Tindie: https://www.tindie.com/products/aprbrother/evil-crow-rf-v2-rf-transceiver-rf/
* Evil Crow RF V2 Alibaba: https://www.alibaba.com/product-detail/Evil-Crow-RF2-signal-receiver-with_1600467911757.html 
* Evil Crow RF V2 Aliexpress: https://www.aliexpress.com/item/3256807682636637.html

**Available with SAPSAN Cybersec & Military (shipping from EU, Poland):**

* https://sapsan-sklep.pl/en/products/evil-crow-rf-v2

**Available with KSEC Worldwide (shipping from United Kingdom):**

* Evil Crow RF V2: https://labs.ksec.co.uk/product/evil-crow-rf-v2/
* Evil Crow RF V2 Lite: https://labs.ksec.co.uk/product/evil-crow-rf2-lite/

**Available with Tienda Espía (shipping from Mexico):**

* https://tiendaespia.com.mx/producto/evil-crow-rf-v2-radiofrequency-hacking-device/

**Discord Group:** https://discord.gg/evilcrowrf

# 🚀 Stability and Functionality Updates
The updated firmware in this repository for v1.3.2 has been patched and configured to ensure reliable compilation and stable runtime performance on modern ESP32 environments and current versions of Arduino IDE.

I have resolved critical library version conflicts and optimized the web server's file handling to prevent runtime crashes (HTTP500 errors) and make the web panel fully functional.

### ✅ Key Fixes Implemented
* Fixed Library Conflicts: Resolved the persistent HTTP_METHOD conflicts and the fatal ElegantOTA incompatibility errors that arise when mixing ElegantOTA and ESPAsyncWebServer.
* WDT Stability Fix: Updated the Watchdog Timer (WDT) function signature within force_reset() to match the requirements of the stable ESP32 Core v2.0.14.
* Web Serving Optimized: Replaced inefficient, redundant single-file HTTP_GET handlers with a robust, high-performance serveStatic configuration.
* Web Interface Functional: Fixed the issue where menu links were missing the .html extension (by using an onNotFound fallback) and ensured assets are loaded correctly, making all menu options functional.

**Summary:**

1. Disclaimer
2. Introduction
3. Firmware
	* Installation
	* First steps with Evil Crow RF V2
	* RX Config Example
	* RX Log Example
	* RAW TX Config Example
	* Binary TX Config Example
	* Pushbuttons Configuration
	* Tesla Charge Door Opener
	* URH Parse example
	* OTA Update
	* Wi-Fi Config
	* Power management
	* Other Sketches
4. Evil Crow RF V2 Support

# NOTE

**Currently, the latest version cannot be compiled due to issues with third-party libraries. Rewriting the firmware will take some time.**

**I worked extensively on this to get Evil Crow v2 Working with modern/current Libraries and updated Arduino IDE 1.8**


# Disclaimer

Evil Crow RF V2 is a basic device for professionals and cybersecurity enthusiasts.

We are not responsible for the incorrect use of Evil Crow RF V2.

We recommend using this device for testing, learning and fun :D

**Be careful with this device and the transmission of signals. Make sure to follow the laws that apply to your country.**

![EvilCrowRF](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/evilcrowrfv2.jpg)

# Introduction

Evil Crow RF V2 is a radiofrequency hacking device for pentest and Red Team operations, this device operates in the following radiofrequency bands:

* 300Mhz-348Mhz
* 387Mhz-464Mhz
* 779Mhz-928Mhz
* 2.4GHz

Evil Crow RF V2 has two CC1101 radiofrequency modules, these modules can be configured to transmit or receive on different frequencies at the same time. Additionally, Evil Crow RF V2 has a NRF24L01 module for other attacks.

Evil Crow RF V2 allows the following attacks:

* Signal receiver
* Signal transmitter
* Replay attack
* URH parse
* Mousejacking
* ...

**NOTE:** 

* All devices have been flashed with basic firmware Evil Crow RF V2 before shipping.
* Please do not ask me to implement new functions in this code. You can develop code for Evil Crow RF V2 and send PR with your new code.

# Firmware (v1.3.2 Stable)
The basic firmware allows to receive and transmit signals. You can configure the two radio modules through a web panel via WiFi.

Installation (Optimized Configuration)
Prerequisites (Crucial for Stability)
ESP32 Core: You MUST install and select the ESP32 Core version 2.0.14 in the Boards Manager to avoid library signature conflicts.

Codebase: Use the code in the firmware/v1.3.2/ directory.

The basic firmware allows to receive and transmit signals. You can configure the two radio modules through a web panel via WiFi.

## Installation

1. Install esptool: sudo apt install esptool
2. Install pyserial: sudo pip install pyserial
3. Download and install the latest version of Arduino IDE (v2.3.3): https://www.arduino.cc/en/main/software
4. Download Evil Crow RF V2 1.3.2 Fork: https://github.com/Pnwcomputers/EvilCrowRF-V2 *Use Specifically Firmware v1.3.2
5. SD Card File Preparation
  - Rename File: Ensure the JavaScript file on your SD card (inside the /HTML/ folder) is named lib.js (not javascript.js) to match the HTML page request.
  - Formatting: Format your MicroSD card to FAT32.
  - Index.html Update: Make sure to update the index.html file with "btn3.html" for 'Button Configuration' instead of "btnconfig.html"
  - Copy the relevant SD/HTML and SD/URH folders to the root of the MicroSD card.
6. Open Arduino IDE
7. Download and install the following libraries into your Arduino libraries:
   - ESPAsyncWebServer
   - ElegantOTA
   - ESP32-targz
   - AsyncTCP
8. Go to File - Preferences. Locate the field "Additional Board Manager URLs:" Add "https://espressif.github.io/arduino-esp32/package_esp32_index.json" without quotes. Click "Ok"
9. Select Tools - Board - Boards Manager. Search for "esp32". Install "esp32 by Espressif system version 2.0.14" & Click "Close". *The version is VERY important.
10. Open the EvilCrowRF-V2/firmware/v1.3.2/EvilCrow-RFv2/EvilCrow-RFv2.ino sketch
11. Select Tools:
    * Board - "ESP32 Dev Module".
    * Flash Size - "4MB (32Mb)".
    * CPU Frequency - "80MHz (WiFi/BT)".
    * Flash Frequency - "40MHz"
    * Flash Mode - "DIO"
12. Edit ElegantOTA/src/ElegantOTA.h and chage the following:
* #define ELEGANTOTA_USE_ASYNC_WEBSERVER 0 to #define ELEGANTOTA_USE_ASYNC_WEBSERVER 1

13. Edit AsyncTCP/src/AsyncTCP.h and change the following:
* #define CONFIG_ASYNC_TCP_USE_WDT 1 to #define CONFIG_ASYNC_TCP_USE_WDT 0

14. Upload the code to the Evil Crow RF V2 device
15. Copy the EvilCrowRF-V2/firmware/v1.3.2/SD/HTML folder to a MicroSD card.
16. Copy the EvilCrowRF-V2/firmware/v1.3.2/SD/URH folder to a MicroSD card.

![SD](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/sd.png)

**Notes about SD:** 

* Web server will not load, is a blank page or displays nothing:

Check you have copied the relevant files to the SD card and the SD card is inserted in the Evil Crow RF V2 device. Check you are connected to the Wifi Access Point of the Evil Crow RF V2.

* My files are on the SD card but the web server will not work:

Check your SD card size. It is recommended to use a small card. 32GB or smaller is sufficent for operation. Cards larger than this have been shown to cause issues and not work.

* I cannot access the internet when I am connected to the Evil Crow RF V2:

By default, the Evil Crow operates as an access point. When you connect to it, it has no internet access as it is not connected to the internet. If you need internet at the same time, read the Wi-Fi Config section of this repository to configure Evil Crow RF V2 in STATION mode.

## First steps with Evil Crow RF V2

0. Check & verify you have copied the relevant files to your SD card.
1. Insert the MicroSD card into the Evil Crow RF V2 and connect the device to an external battery or laptop.
2. Visualize the wifi networks around you and connect to the Evil Crow RF V2 (default SSID: Evil Crow RF v2).
3. Enter the password for the wifi network (default password: 123456789).
4. Open a browser and access the web panel (default IP: 192.168.4.1).
5. Go!

**Web Interface Stability Notes:**
* Home Button Functional: The bare root path (/) now loads the index.html file correctly due to an explicit handler placed before serveStatic.
* Full Menu Navigation: All menu links now load their respective HTML pages.
* SD Card Fatal Error: If the web panel does not load and the Serial Monitor (at 115200 baud) shows FATAL ERROR: SD Card initialization failed., the issue is physical (power instability from USB, or a faulty SD card/interface).

![Webpanel](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/webpanel.png)

## RX Config Example

* Module: (1 for first CC1101 module, 2 for second CC1101 module)
* Modulation: (example ASK/OOK)
* Frequency: (example 433.92)
* RxBW bandwidth: (example 58)
* Deviation: (example 0)
* Data rate: (example 5)

![RX](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/rx.png)

**2-FSK NOTES:**

* Evil Crow RF V2 allows 2-FSK (RX/TX) modulation, this is configured for use with CC1101 module 2. Do not use CC1101 module 1 for 2-FSK RX. 

* You can use 2-FSK TX with module 1 or with module 2. 

* Evil Crow RF V2 allows you to receive signals at the same time on two different frequencies, but this does not work correctly if you use 2-FSK. Make sure you use module 2 for 2-FSK RX, while doing this do not use module 1 for anything or you will not receive the 2-FSK signals correctly. 

* You can receive two signals on different frequencies with ASK/OOK.

## RX Log Example

![RXLog](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/rx-log.png)

## RAW TX Config Example

* Module: (1 for first CC1101 module, 2 for second CC1101 module)
* Modulation: (example ASK/OOK)
* Transmissions: (number transmissions)
* Frequency: (example 433.92)
* RAW Data: (raw data or raw data corrected displayed in RX Log)
* Deviation: (example 0)

![TXRAW](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/txraw.png)

## Binary TX Config Example

* Module: (1 for first CC1101 module, 2 for second CC1101 module)
* Modulation: (example ASK/OOK)
* Transmissions: (number transmissions)
* Frequency: (example 433.92)
* Binary Data: (binary data displayed in RX Log)
* Sample Pulse: (samples/symbol displayed in RX Log)
* Deviation: (example 0)

![TXBINARY](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/txbinary.png)

## Pushbuttons Configuration

* Button: (1 for first pushbutton, 2 for second pushbutton)
* Modulation: (example ASK/OOK)
* Transmissions: (number transmissions)
* Frequency: (example 433.92)
* RAW Data: (raw data or raw data corrected displayed in RX Log)
* Deviation: (example 0)

![TXBUTTON](https://github.com/joelsernamoreno/EvilCrowRF-V2/blob/main/images/pushbutton.png)

## Tesla Charge Door Opener

Demo: https://www.youtube.com/watch?v=feNokjfEGgs

## URH Parse example

Demo: https://youtube.com/watch?v=TAgtaAnLL6U

## OTA Update

Demo: https://www.youtube.com/watch?v=YQFNLyHu42A

## WiFi Config

Evil Crow RF V2 is configured in AP mode with a default SSID and password. You can change the mode to STATION or AP, change SSID, change password and change Wi-Fi channel remotely from the web panel.

The changes will be stored in the device, every time you restart Evil Crow RF V2 the new Wi-Fi settings will be applied. If you want to return to the default settings, you can delete the stored Wi-Fi configuration from the web panel.

**NOTE:** When changing the Wi-Fi configuration you have to fill in all the fields correctly, if you do not do this you bricked the device.

## Power Management

1. In normal mode, press push2 + reset, then release reset: Evil Crow RF v2 blinks several times and goes to sleep. 
2. In sleep mode, press push2 + reset, then release reset to wake him up.

Demo: https://www.youtube.com/shorts/K_Qkss6-pEY

**NOTE:** If Evil Crow RF v2 is sleeping and you accidentally press reset, he'll go straight back to sleep. If he isn't asleep and you press reset then he will stay awake too.

## Other Sketches

* Mousejacking: EvilCrowRF-V2/firmware/other/standalone-mousejacking
* ...

# Evil Crow RF V2 Support

* You can ask in the Discord group: https://discord.gg/jECPUtdrnW
* You can open issue or send me a message via twitter (@JoelSernaMoreno).

