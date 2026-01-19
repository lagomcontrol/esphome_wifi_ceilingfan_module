# Ventair Skyfan DC - ESPHome Implementation

ESPHome configuration for the Ventair SkyFan DC ceiling fan Tuya module (SKYAPPCM). This project replaces the cloud-dependent firmware with local control via ESPHome, enabling full integration with Home Assistant and other home automation platforms.

## Overview

This project provides a complete ESPHome implementation for the Ventair Skyfan DC ceiling fan, which features:-
- 6-speed DC motor fan control
- Reversible fan direction
- Integrated LED light with adjustable brightness (5 steps)
- Adjustable color temperature (3 steps)
- Full bidirectional communication so remote works and feeds back to Home Assistant
- All controls are mapped to native HA UI elements
      
- ## Hardware
  - ESP32-C3-SuperMini (esp32-c3-devkitm-1)
  - Custom Adaptor PCB
                     
- ## Features
- ### Fan Control
  - Fan on/off control 
  - Fan Speeds ( 6 Steps )
  - Forward and reverse direction control
- ### Light Control
  - Light on/off control 
  - Brightness ( 5 Steps ) 
  - Color Temperature ( 3000K / 4000K / 5000K )

- ## Technical Details
I wanted all controls to map to HA native Fan & Light UI elements without relying on secondaray dropdowns. However becuase of how the Datapoint's work on this fan, we have to intercept all calls with lambda functions to map HA control values to the Tuya MCU values.

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
