# Ventair Skyfan DC - ESPHome Implementation

ESPHome configuration for the Ventair SkyFan DC ceiling fan Tuya module (SKYAPPCM). This project replaces the cloud-dependent firmware with local control via ESPHome, enabling full integration with Home Assistant and other home automation platforms.

## Overview

This project provides a complete ESPHome implementation for the Ventair Skyfan DC ceiling fan, which features:
- - 6-speed DC motor fan control
- - Reversible fan direction
- - Integrated LED light with adjustable brightness (5 steps)
- - Adjustable color temperature (3 steps)
- - Full bidirectional communication so remote works and feeds back to Home Assistant
- - All controls are mapped to native HA UI elements
       
- ## Hardware
- - ESP32-C3-SuperMini (esp32-c3-devkitm-1)
- - Custom Adaptor PCB
                     
- ## Features
- ### Fan Control
- - 6-speed operation with optimized speed mapping
- - Forward and reverse direction control
- - Power on/off control
- - Bidirectional sync with remote control       
- ### Light Control
- - On/Off
- - Brightness ( 5 Steps ) 
- - Color Temperature ( 3000K / 4000K / 5000K )
