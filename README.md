# ESP32 Marauder - Double Barrel 5G (BW16) User Manual 

![Alt text](Assets/images/front.with.Flipper.jpg)
![Alt text](Assets/images/Back.with.description.jpg)
![Alt text](Assets/images/standalone.Bruce.with.description.jpg)
![Alt text](Assets/images/top.jpg)
![Alt text](Assets/images/right.jpg)
![Alt text](Assets/images/left.jpg)

> [!NOTE]
> - Batch 2 units will be available to order on [Tindie](https://www.tindie.com/products/honeyhoneytrading/esp32-marauder-double-barrel-5g/) from 11 August 2025, and will ship out on Monday, 18 August 2025.
> - Latest Update: 09 August 2025 by Jay & Anson @ Honey Honey Team - fixing mirror error on GPS setting, 2nd batch availablility and hardware update on the refresher.  
> - Second update: 19 June 2025 by Anson @ Honey Honey Team
> - First version: 17 June 2025 by John @ Honey Honey Team
> - All procedures and descriptions related to the Flipper Zero herein were validated using Momentum Firmware, version < MNTM-010 30-04-2025 >.




<br/>


## What is ESP32 Marauder - Double Barrel 5G? 
First of all, what is the [ESP32 Marauder Double Barrel](https://github.com/HoneyHoneyTeam/ESP32-Marauder-Double-Barrel)? 

"Double Barrel" refers to the fact that the device runs two sperated Marauders simultaneously. The first Marauder features a 2.8-inch screen, an onboard 800mAh battery, GPS, and a microSD card slot. The second Marauder is connected to and controlled by the Flipper Zero.

Due to limitations of the this particular ESP32 chipset, the Marauder currently supports only 2.4 GHz Wi-Fi. However, recent developments with the BW16 Kit / RTL8720DN chipset have shown promising results to 5GHz Wifi. This is exactly what we have implenmented on the 5G cousin of the Double Barrel. 

<br/>

## Specification of the ESP32 Marauder Double Barrel 5G


- **The first Marauder comes with:**
	- ESP32 chipset with an external antenna,
	- A 2.8-inch touch screen,
	- An 800mAh embedded battery, 
	- Onboard GPS access
	- Micro SD card slot, for updating firmware and data storage
	- For Batch one unit, 4pin GPIO (3.3V/Tx/Rx/Gnd)
 	- From Batch Two, 4Pins GPIO have been replaced by USB-C port 
  	- This part of the device can funcation as a standalone device (i.e., you can use it without Flipper Zero).
   	- The hardware version of this marauder is V6

- **The BW16 / RTL8720DN chipset is controlled by the Flipper Zero, it comes with**
  	- BW16 / RTL8720DN chipset with an external antenna
  	- Dual-Band 5Ghz + 2.4Ghz scanning, de-authentication
  	- For Batch one Unit: 4pins GPIO 4pin GPIO (3.3V/Tx/Rx/Gnd) for firmware update, or switch different firmware
  	- From Batch Two, 4Pins GPIO have been replaced by USB-C port 
  	- FAP <Flipper App Package> installation is needed, aka copying the FAP into Flipper SD card
  	- More info regarding the funcationality, please check <How to upgrade BW16 firmware > section of this manual

- **Others:**
	- USB-C Ports for onboard battery charging (A).
 	- CC1101 Chipset(433 MHz), supporting up to 10 dB output per antenna.
  	- GPS Chipset. GPS data is accessible to both Marauders.
  	- Four Antennas: 2 x 3 dB for Wi-Fi (Dual Marauder), 1 x 1 dB for GPS, and 1 x 3 dB for SubGhz 433 MHz.
  	- Toggle on the left for switching GPS power supply ( either by Flipper or device battery)
  	- Full 3D-Printed Enclosure/Case is also included.


<br/>

![Alt text](Assets/images/In.Comparison.png)

## Pre-flight Check / Settings Before First Use 

> [!NOTE]
> All our products are thoroughly checked and configured prior to shipping. While most of our products are plug-and-play, a few specific settings need to be adjusted on your Flipper Zero to ensure proper communication with the Double Barrel 5G.

<br/>

### SubGhz <433mhz>
- **No initial setup is required for SubGhz chipset detection**. The Flipper Zero automatically recognizes an external SubGhz chipset when it connect to The Double Barrel 5G. 
- To confirm if the Flipper Zero is using the external SubGhz chipset, or to switch to it manually:
	1. On your Flipper Zero, navigate to the main menu.
	2. Go to: **Sub-Ghz** -> **Radio Settings** -> **Module**.
	3. Select **External**."
- The SubGhz part of the Double Barrel is fully functional even the first marauder is in OFF mode


<br/>

### 1st Set Marauder / Standalone section (The one with 2.8inch Touch Screen)

- No initial setup is required
- Turn ON or OFF via the switch located on the right side of the Double Barrel / (labeled <**D**>)
- If you would like to update the firmware, please remeber to download **V6 version** of the firmware BIN file

<br/>

### The BW16 part

- The BW16 part use UART 15 and 16 for communicating with Flipper, hence it is necessary to switch from the default 13 & 14 GPIO to 15 & 16.
	1. On your Flipper Zero, navigate to the main menu.
	2. Go to: **Momentum** -> **Protocols** -> **GPIO Pins** -> **ESP32/8266 UART**.
	3. Select **Extra 15, 16**.

- Then, The FAP file need to copy into Flipper SD card, as showed in the following. 
	1. Download the FAP file from [here](Assets/5G.fap) (Right Click and Save AS)
 	2. Copy the file into <**you SD card/Apps/GPIO**> directory. You could do so via a Micro SD card reader, or via qFlipper App. 
  	3. Put the SD card back into Flipper, and you should be able to find an APP call **5G wifi Deauth** in through Flipper manual **APPS** -> **GPIO** -> **5G wifi deauth**
  	   
<br/>

### GPS

- To use the GPS function of Double Barrel 5G via the Flipper Zero, please see the steps below.
  	1. Set the **bottom switch** on the left side of the Double Barrel 5G (labeled <**C**>) to the **DOWN** position.
		- UP position: GPS is powered by the Double Barrel's onboard 800mAh battery.
  		- DOWN position: GPS is powered by the Flipper Zero's battery.
  	2. On your Flipper Zero, navigate to the main menu.
	3. Go to: **Momentum** -> **Protocols** -> **GPIO Pins** -> **NWEA GPS UART**.
	4. Select **Extra 15, 16**.
	5. If **ESP32/8266 UART** setting is also set as **Extra 15, 16**, please change to **Default 13, 14**. The reason is that only one function can use UART pins 15 and 16 at a time. If both the ESP32 and the GPS are set to use UART 15 and 16, it may cause a functional conflict.
	6. For testing purpose, Go to **Apps** -> **GPIO** -> **[NMEA]GPS**.
	7. Acquiring a GPS signal might take up to a minute. The exact time depends on your location and how open or obstructed the sky is.


<br/>

## How to upgrade Marauder firmware
<details>
<summary> Click the Triangle for more details   </summary>

### 1st Set Marauder (The one with 2.8inch Touch Screen)

1. Take the Micro SD card from the Double Barrel and connect to an PC / Laptop / Mac / whatever

2. Download the **V6** firmware file, which is usual inclued < **_new_hardware.bin/_v6.bin** > in the name, from [Marauder website](https://github.com/justcallmekoko/ESP32Marauder/releases).
   
3. **PLEASE PLEASE PLEASE double check which version of Marauder you have downladed and used. 
   
4. When you have checked the bin file, copy the file to the Micro SD card and rename it as< **update.bin** >. Then, insert the Micro SD card back into the Marauder Unit.

5. Please double-check that you have downloaded the correct file and verify its size to ensure it wasn't corrupted during the download process. Using the wrong or a corrupted firmware file may brick the device. If that happen, pleases check [this tutorial of how to revive / recovery the device](https://github.com/HoneyHoneyTeam/ESP-Programmer-for-Slim-Jim-Double-Barrel-Double-Barrel-5G). 
   
6. Turn on the Marauder Unit, Navigating menu as following: < **Device** > => < **Update firmware** > => < **SD Update** > => < **Yes** >. In rare cases, Marauder may repeatedly show that the firmware file is corrupted and exit the update process shortly, no matter how many times you try. We suggest using a new microSD card in such cases.
   
7. In a minute, The unit should restart itself and you are golden.

</details>
</br>

## How to switch firmware for the standalone section, such as from Marauder to Bruce, or vice versa
<details>
<summary> Click the Triangle for more details</summary>


**Notes: Based on our testing (18.June.2025), Bruce firmware can be load into the standalone section of Double Barrel / Double Barrel 5G. but it is still a bit buggy, and not 100% of Bruce funcationality is fully supported, which is understandable**

1. [An ESP32 programmer](https://github.com/HoneyHoneyTeam/ESP-Programmer-for-Slim-Jim-Double-Barrel-Double-Barrel-5G) is included in the package. Connecting the programmer to the GPIO port located in the lower-right corner of the device, as shown in the following picture.

![Alt text](https://github.com/HoneyHoneyTeam/ESP-Programmer-for-Slim-Jim-Double-Barrel-Double-Barrel-5G/blob/main/Assets/images/GPIO.Double.jpg)

2. Using Google Chrome, go to [Bruce.Computer website](https://bruce.computer/flasher). At the bottom of the page, select '**Latest Release**' -> '**Custom Boards**' -> '**Marauder V4 or V6**' -> '**Install**'
   
3. After that, while **holding down the boot button** (Marked as 2) on the back of the device using a pin or the metal stylus included with the Double Barrel, **connect** the ESP32 programmer to your PC's USB port. This will put the device into bootloader/download mode, as shown in the following picture.

![Alt text](https://github.com/HoneyHoneyTeam/ESP-Programmer-for-Slim-Jim-Double-Barrel-Double-Barrel-5G/raw/main/Assets/images/bootDouble.jpg)
   
4. If everything is set up correctly, you should be able to select the COM port from the prompt window on the Bruce website. The website will handle the rest of the process automatically.
   
5. After about a minute, the website should indicate that the process is complete. You can then disconnect the device—now it's time to explore!

6. What happen if you like to reverse back to Marauder Firmware? Check [this tutorial](https://github.com/HoneyHoneyTeam/ESP-Programmer-for-Slim-Jim-Double-Barrel-Double-Barrel-5G)


</details>
</br>

## How to upgrade BW16 firmware 
<details>
<summary> Click the Triangle for more details</summary>
<br/>
1. When we shipped out the Double Barrel 5G, the BW16 was pre-loaded with one of the 5G firmware versions. This firmware is compatible with the FAP call [5G WiFi deauth](https://github.com/HoneyHoneyTeam/ESP32-Marauder-Double-Barrel-5G/blob/main/Assets/5G.fap).

2. Regarding the effectiveness and functionality of the BW16 kit on 5G WiFi networks: it works and is quite effective. However, its functionality is limited to scanning and deauthentication. There may be other binaries or firmware options available, such as Evil Portal or CLI support, but due to time constraints and limited manpower, we haven't been able to test them all. That said, we believe the open-source community will likely develop additional tools, as around 90% of the code is compatible and reuseable.

3. If you would like to explore more on the 5G side of the business, you could load BW16 with [delfyrtl firmware and its compatiable flipper APP](https://github.com/gorebrau/delfyRTL) 

4. **The Delfyrtl GitHub page has a clear description of how to load the firmware, but we will be updating our own version of the loading procedure soon. Please check back in a few days for the latest instructions.  - 19.06.2025 by Anson**

</details>

<br/>

## Could the Double Barrel 5G work with other Flipper Zero firmware, rather than Momentum?

<details>
<summary> Click the Triangle for more details</summary>
<br/>
We believe the 5G FAP is compatible with most firmware versions.

However, there is one caveat. When we checked the latest Unleashed firmware (as of 10 July 2025), we were unable to locate the UART setting for changing the ESP32/8266 GPIO pins (from the default 13/14 to 15/16) in the Unleashed documentation. It’s possible this setting is referred to differently in the Unleashed firmware.

We worked around this by first using a Flipper running the Momentum firmware, where we configured the GPIO pins to 15/16. Then, we used the web installer to flash the Unleashed firmware (version 081). In this case, the update process preserved the existing GPIO configuration.

If you’re planning to use Unleashed with the Double Barrel 5G, this could be one way to get it working.

</details>

<br/>

## What we shipout unit with Marauder 1.4.6，even the latest Marauder is 1.8.2 or further - Update at 09 August 2025?

<details>
<summary> Click the Triangle for more details</summary>
<br/>

The only reason is that Marauder changed how the touchscreen works after version 1.4.6.

In 1.4.6, it functions like a normal touchscreen.

After 1.4.6, the touchscreen is divided into three sections, and each section acts as one big button:
	
 	Top → UP
    Middle → ENTER
    Bottom → DOWN

This change was confusing and counter-intuitive for new users at first, and many thought the device was malfunctioning — which led to a flood of tech support requests.

For that reason, we ship units with version 1.4.6 by default.

That said, you’re free to upgrade or downgrade the Marauder at any time, as long as you download the V6 version of the firmware.

</details>

<br/>

## What is the main difference between Batch one machine and Batch two units - Update at 09 August 2025?

<details>
<summary> Click the Triangle for more details</summary>
<br/>

The only main difference is that the 4-pin GPIO connector has been replaced with a USB-C port. This means users can now use a standard USB-C data cable, rather than a specific refresher tool, to enter the chipset’s bootloader mode.

As a result, the refresher is no longer required for reviving the device or upgrading the firmware.

</details>

<br/>


## Our official shop if you would like to support us.  
1. [ESP32 Marauder - Double Barrel 5G via Tindie](https://www.tindie.com/products/39064/)
2. [ESP32 Marauder - Double Barrel via Tindie](https://www.tindie.com/products/38768/)
3. [Our official site](https://honeyhoneylab.com/)
4. [Tindie](https://www.tindie.com/stores/honeyhoneytrading/)
5. ~~[ETSY Shop](https://www.etsy.com/au/shop/HoneyHoneyTrading)~~

<br/>

## Warrenty and Tech Support

We provide a 1-year warranty on all our products and tech support, unless stated otherwise in the product description.

FYI, our [Etsy](https://www.etsy.com/au/shop/HoneyHoneyTrading) shop is no longer in operation. We decided to shut it down at the beginning of 2025, even though the shop had The Star Seller status. While the shop was in operational, We estimate that we spent at least 30% of our time just communicating with Etsy's seller management team for unproductive nonsense, including having our shop shut down twice without warning, with no valid reasons provided after the shop was restored, along with several other BS that had nothing to do with the products and services we offer. 

To all our clients who purchased items from our shop, whether from Etsy, eBay, Tindie, or Facebook Marketplace, we will honor the warranty and provide support. Please feel free to email us at Support@honeyhoneylab.com. or [Whatsapp](https://wa.me/61452559581) 

<br/>

## FAQ 

## Credibility
- Credit of Marauder Firmware goes to <ins>@JustCallmeCoco</ins>
- Credit of delfyRTL goes to [gorebrau](https://github.com/gorebrau/delfyRTL)
- Credit of Bruce firmware goest to [Bruce.computer](https://bruce.computer/) 

<br/>

## Metadata / keywords / about for bots ##
flipper zero, flipper, wifi board, marauder,5G wifi, bw16, network security, esp32, cc1101, nrf24, subghz, 2.4ghz, wifi, GPS
