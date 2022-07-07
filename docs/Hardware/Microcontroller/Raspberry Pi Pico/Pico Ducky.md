---
title: Ducky on Raspberry Pi Pico
description: Pico Ducky is a small USB ducky for Raspberry Pi. It is a cheap and easy to use USB ducky which can be used to automate tasks on your system.
image_url: https://hackster.imgix.net/uploads/attachments/1245772/_V7g5cyupUX.blob?auto=compress%2Cformat&w=600&h=450&fit=min 
---

# Pico Ducky aka Bad USB

A Pico Ducky is a USB Rubber Ducky. As defined on the internet as -
"USB Rubber ducky is an HID device that looks similar to a USB Pen drive. It may be used to inject keystroke into a system, used to hack a system, steal victims essential and credential data can inject payload to the victim's computers."

# Getting Started

If you want to skip to the Github Repository [here](https://github.com/dbisu/pico-ducky) is the link.

1. Download the `.uf2` file from [CircuitPython for the Raspberry Pi Pico](https://circuitpython.org/board/raspberry_pi_pico/)

2. Plug the device into a USB port while holding the boot button. It will show up as a removable media device named `RPI-RP2`.

3. Copy the downloaded `.uf2` file to the root of the Pico (`RPI-RP2`). The device will reboot and after a second or so, it will reconnect as `CIRCUITPY`.

4. Download `adafruit-circuitpython-bundle-7.x-mpy-YYYYMMDD.zip` from [here](https://github.com/adafruit/Adafruit_CircuitPython_Bundle/releases/latest) and extract it on your main device (not the Pico).

5. Navigate to `lib` in the recently extracted folder and copy `adafruit_hid` to the `lib` folder in your Raspberry Pi Pico.

6. Click [here](https://raw.githubusercontent.com/dbisu/pico-ducky/main/duckyinpython.py), press CTRL + S and save the file as `code.py` in the root of the Raspberry Pi Pico, overwriting the previous file.

7. Before the next step, let us enter setup mode. To enter setup mode by connecting the pin 1 (`GP0`) to pin 3 (`GND`), this will stop the pico-ducky from injecting the payload in your own machine.
The easiest way to so is by using a jumper wire between those pins as seen bellow.


![Setup Mode](https://github.com/dbisu/pico-ducky/blob/main/images/setup-mode.png?raw=true)


8. Find a script [here](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payloads) or [create your own one using Ducky Script](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Duckyscript) and save it as `payload.dd` in the Pico.

9. Be careful, if your device isn't in [setup mode](#setup-mode), the device will reboot and after half a second, the script will run.


## Enable Disable Mode

If you need the pico-ducky to not show up as a USB mass storage device for stealth, follow these instructions.
1. Enter setup mode.
2. Copy boot.py to the root of the pico-ducky.
3. Copy your payload script to the pico-ducky.
4. Disconnect the pico from your host PC.
5. Connect a jumper wire between pin 18 (`GND`) and pin 20 (`GPIO15`).
6. This will prevent the pico-ducky from showing up as a USB drive when plugged into the target computer. 
7. Remove the jumper and reconnect to your PC to reprogram.
8. The default mode is USB mass storage enabled.