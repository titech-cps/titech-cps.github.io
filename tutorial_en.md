# M5Stack How-To

M5Stack is an open-source modular toolkit for IoT devices.
This tutorial explains how to set up a development environment for M5Stack on your PC.

-----
## M5Stack and ESP32

### About M5Stack
An M5Stack module is an enclosed device that consists of an ESP32 SoC and several peripheral components, including three buttons, an LCD, and a speaker. 

* Models
  - M5Stack Core Basic
  - M5Stack Core Gray (used in this tutorial)
  - M5Stack Fire
* Processor: ESP32 SoC (see below)
  - CPU: Dual 240MHz LX6
  - Memory: 512KB
* Flash: 4MB
* Peripheral Components
  - ILI9341 320x240 Color TFT LCD
  - Speaker
  - 3 x button
  - MPU9250 9-Axis Motion Sensor (M5Stack Core Gray, M5Stack Fire)
  - CP2104 USB-UART Adapter
  - Li-Po Battery
* Ports
  - USB-C
  - MBUS (GPIO etc.)
  - Grove (I2C)
  - micro-SD
* Size: 54 x 54 x 17 mm
* Weight: 120g
* Web
  - [http://www.m5stack.com](http://www.m5stack.com)
  - [https://github.com/m5stack/M5Stack](https://github.com/m5stack/M5Stack)

### About ESP32

ESP32 is a series of low-cost, low-power SoC microcontrollers with integrated WiFi and Bluetooth capabilities, created and developed by Espressif.  Apart from M5Stack, many ESP32-based modules and development boards are available.

* Processors
  - Dual 160/240MHz Xtensa LX6 (Tensilica)
  - ULP (Ultra Low Power) Co-Processor
* Memory: 520KB SRAM
* Wireless
  - WiFi 802.11 b/g/n (2.4GHz)
  - Bluetooth v4.2 BR/EDR & BLE
* Peripheral I/F
  - 18 x 12bit ADC
  - 2 x 8bit DAC
  - 10 x capacitive touch sensors
  - temperature sensor
  - 4 x SPI
  - 2 x I2S
  - 2 x I2C
  - 3 x UART
  - SD/SDIO/CE-ATA/MMC/eMMC host controller
  - SDIO/SPI slave controller
  - Ethernet MAC I/F
  - CAN bus 2.0
  - 8 x Infrared TX/RX
  - Motor PWM
  - 16 x LED PWM
  - Hall Effect Sensor
  - Ultra low power analog pre-amplifier
* Security
  - IEEE 802.11 WFA, WPA/WPA2 and WAPI
  - Secure boot
  - Flash encryption
  - 1024bit OTP
  - Cryptographic H/W acceleration: AES, SHA-2, RSA, ESS, RNG
* Web
  - [https://www.espressif.com](https://www.espressif.com)
    + [https://www.espressif.com/en/products/hardware/esp32/overview](https://www.espressif.com/en/products/hardware/esp32/overview)
  - [https://github.com/espressif](https://github.com/espressif)
    + [https://github.com/espressif/esp-idf](https://github.com/espressif/esp-idf)
    + [https://github.com/espressif/arduino-esp32](https://github.com/espressif/arduino-esp32)


-----
## Development Environments for M5Stack

### Overview

Tools and libraries required for developing M5Stack applications are as follows.

1. Toolchain (C/C++ Compiler and other utilities)
2. ESP-IDF (official development framework for ESP32 distributed by Espressif)
3. Arduino Core for ESP32 (library for developing applications using Arduino framework)
4. M5Stack Library (library for developing applications that use M5Stack hardware components)

You may chose several options.

* [Arduino IDE](https://www.arduino.cc)
    - Simple GUI-based IDE for [Arduino](https://www.arduino.cc)
    - Toolchain, ESP-IDF and libraries for M5Stack can be easily installed.
* [PlatformIO](https://platformio.org)
    - IDE for developing various devices.
    - Command-line toolset and editor plugins (for Visual Studio Code and Atom) are available
    - Toolchain, ESP-IDF and libraries for M5Stack can be easily installed.
* [ESP-IDF](https://github.com/espressif/esp-idf)
    - Command-line toolset distributed with the official development framework (ESP-IDF)
    - You should install Arduino Core for ESP32 and M5Stack Library as separate components

The rest of this section describes how to install and set up the development environment listed above.
Other options, for example, setting up cloud-based development environments or methods for uploading programs via WiFi are skipped for now.

* First, you need to install USB-UART driver to connect your PC to M5Stack.
* Then, you can choose either of the following: 
    - Arduino IDE
    - PlatformIO
    - ESP-IDF (with command line tools)

### Installing USB-UART Driver

M5Stack is equipped with a Silicon Labs CP2014 USB-UART adapter as the communication interface to the host PC.
Download an appropriate device driver for your PC from the following link and follow the instructions along with the driver.

* [https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

If the device driver is successfully installed, you should be able to find the following USB-serial port when you connect M5Stack to your PC via a USB cable.

* Mac: `/dev/cu.SLAB_USBtoUART`
* Linux: `/dev/ttyUSB0`

You can easily check using shell command `ls /dev/cu.*` or `ls /dev/tty*`.

#### Notes on Cabling

If you cannot find the above port when you connect your PC to the M5Stack device, try to change the orientation of the USB-C plug connected to the device.
USB-C connectors are usually known to be *reversible* (no orientation).
However, the wiring of the USB-C connector on the M5Stack main board may be bit weird and have *orientation*.

Another possible trouble about cabling may occur when you are using a USB-C to USB-C cable. If your PC has only USB-C ports (like recent MacBook or MacBook Pro), you would like to connect to M5Stack using such cables. 
In my experience, a few instances of M5Stack Core have a connection trouble with some USB-C to USB-C cables. In this case, reversing the connector orientation does not help.  When you come across such trouble with your cable, it is better to give up to use the cable and use USB-A to USB-C cable included in the box of M5Stack with a USB-C to USB-A adapter.

-----
### Setting Up Arduino IDE

#### Installation

Download an appropriated Arduino IDE application from the following link and install it in your PC.

* https://www.arduino.cc/en/Main/Software

#### Setting up for M5Stack

You can easily install the required toolchain, framework and libraries using the *board manager* and *library manager* of Arduino IDE.

* In the *Preference* window of Arduino IDE, add the following URL to "Additional Boards Manager URLs".
  - `https://dl.espressif.com/dl/package_esp32_index.json`
* Invoke *Board Manager* from *Tools* menu.
Type `ESP32` into "Filter your search ..." field and then select "esp32 by Espressif Systems" to install the framework and toolchain.
* Invoke *Library Manager* fro *Tools* menu.
Type `M5Stack` into "Filter your search ..." field and then select "M5Stack by M5Stack" to install the required library.
