# WiFi Ceiling Fan ESPHome Module ( with SkyFan DC compatibility )

<b>WARNING: This firmware or it's associated module is not endorsed or approved by Ventair. It’s use will void any warranties you may have with them.
NOTE: To use the OEM Ventair app you must use the factory module. This is for Home Assistant integration only and is not intended to provide OEM functionality.</b>

ESPHome firmware for the WiFi Ceiling Fan module developed to be contatible with the Ventair SkyFan DC ceiling fan range as an alternative to the official module (SKYAPPCM). This project replaces the cloud-dependent module with a local ESP based module via ESPHome, enabling full local integration with Home Assistant.

Fan Speed, Brightness & Color Temperature work with the native HA Light & Fan UI panels.

This module can be bought Plug & Play from here:
https://lagomcontrol.com.au/product/skyfan-esphome

## Overview

This project provides a complete Wifi ESPHome based module intended to be compatible with the Ventair Skyfan DC ceiling fan range:
  - 6-speed DC motor fan control
  - Reversible fan direction
  - Integrated LED light with adjustable brightness (5 steps)
  - Adjustable color temperature (3 steps)
  - Full bidirectional communication so remote works and feeds back to Home Assistant
  - All controls are mapped to native HA UI elements

Functions such as timers or sleep mode are not implemented and assumed handled by Home Assistant.
      
## Hardware
  - ESP32-C3-SuperMini (esp32-c3-devkitm-1)
  - Custom Adaptor PCB
                     
## Features
- ### Fan Control
  - Fan on/off control 
  - Fan Speeds ( 6 Steps )
  - Forward and reverse direction control
- ### Light Control
  - Light on/off control 
  - Brightness ( 5 Steps ) 
  - Color Temperature ( 3000K / 4000K / 5000K )

## Technical Details
I wanted all controls to map to HA native Fan & Light UI elements without relying on secondary dropdowns or external libraries. As a result, because of how the Datapoint's work on this MCU, we have to intercept all calls with lambda functions to map HA control values to the MCU values.

- ### Color Temperature Mapping ( 19 )
  - 0 -> 5000K
  - 1 -> 4000K
  - 2 -> 3000K
- ### Brightness Mapping ( 16 )
  - 1 -> 20%
  - 2 -> 40%
  - 3 -> 60%
  - 4 -> 80%
  - 5 -> 100%
- ### Fan Speed Mapping ( 3 )                                                                                                     
  - 1 -> 16.6%
  - 6 -> 33.3% ( ECO )
  - 2 -> 50.0%
  - 3 -> 66.6%
  - 4 -> 83.3%
  - 5 -> 100%

- ## Credits

Datapoints, Module Pinouts & Inspiration originally from here.
- https://github.com/jeggleston1981/skyfandc

Similar Projects
- https://github.com/Jagomeister/ESPHome-SkyFan-DC
- https://github.com/SirMrDexter/skyfandc
