# Ventair Skyfan DC - ESPHome Implementation

ESPHome configuration for the Ventair Skyfan DC ceiling fan with integrated Tuya module. This project replaces the cloud-dependent Tuya firmware with local control via ESPHome, enabling full integration with Home Assistant and other home automation platforms.

## Overview

This project provides a complete ESPHome implementation for the Ventair Skyfan DC ceiling fan, which features:
- 6-speed DC motor fan control
- - Reversible fan direction (forward/reverse)
  - - Integrated LED light with adjustable brightness
    - - Adjustable color temperature (warm to cool white)
      - - Full bidirectional communication with the Tuya MCU
       
        - ## Hardware
       
        - - **MCU:** ESP32-C3 (esp32-c3-devkitm-1)
          - - **Communication:** UART (9600 baud)
            -   - RX: GPIO21
                -   - TX: GPIO20
                    - - **Status LED:** GPIO8
                     
                      - ## Features
                     
                      - ### Fan Control
                      - - 6-speed operation with optimized speed mapping
                        - - Forward and reverse direction control
                          - - Power on/off control
                            - - Bidirectional sync with remote control
                             
                              - ### Light Control
                              - - CWWW (Cool White / Warm White) LED control
                                - - 5-level brightness adjustment
                                  - - 3 color temperature presets:
                                    -   - Cool (5000K / 200 mireds)
                                        -   - Neutral (4000K / 250 mireds)
                                            -   - Warm (3000K / 333.3 mireds)
                                                - - Zero transition time for instant response
                                                 
                                                  - ## Installation
                                                 
                                                  - ### Prerequisites
                                                  - - ESPHome installed (via Home Assistant or standalone)
                                                    - - ESP32-C3 compatible flashing tool
                                                      - - Access to your WiFi credentials
                                                       
                                                        - ### Configuration Files
                                                       
                                                        - The project consists of two main files:
                                                       
                                                        - 1. **skyfandc.yaml** - Main configuration file
                                                          2. 2. **secrets.yaml** - WiFi and API credentials (template provided)
                                                            
                                                             3. ### Setup Steps
                                                            
                                                             4. 1. Clone this repository or download the configuration files
                                                               
                                                                2. 2. Edit `secrets.yaml` with your credentials:
                                                                   3. ```yaml
                                                                      ssid: your_wifi_ssid
                                                                      password: your_wifi_password
                                                                      domain: .local
                                                                      api_key: your_32_character_api_key
                                                                      fallback_password: your_fallback_ap_password
                                                                      ```

                                                                      3. Flash the ESP32-C3:
                                                                      4. ```bash
                                                                         esphome run skyfandc.yaml
                                                                         ```

                                                                         4. Adopt the device in your ESPHome dashboard
                                                                        
                                                                         5. ### Dashboard Import
                                                                        
                                                                         6. You can also import this configuration directly in the ESPHome dashboard:
                                                                         7. ```
                                                                            github://lagomcontrol/skyfandc_esphome/skyfandc.yaml@main
                                                                            ```

                                                                            ## Usage

                                                                            Once installed and connected, the device exposes two entities:

                                                                            ### Fan Entity
                                                                            - **Name:** SkyFan DC01 Fan
                                                                            - - **Controls:**
                                                                              -   - Power on/off
                                                                                  -   - Speed (1-6)
                                                                                      -   - Direction (forward/reverse)
                                                                                       
                                                                                          - ### Light Entity
                                                                                          - - **Name:** SkyFan DC01 Light
                                                                                            - - **Controls:**
                                                                                              -   - Power on/off
                                                                                                  -   - Brightness (0-100%)
                                                                                                      -   - Color temperature (3000K-5000K)
                                                                                                       
                                                                                                          - ## Technical Details
                                                                                                       
                                                                                                          - ### Tuya Datapoint Mapping
                                                                                                       
                                                                                                          - | Datapoint | Type | Function | Values |
                                                                                                          - |-----------|------|----------|--------|
                                                                                                          - | 1 | bool | Fan Power | true/false |
                                                                                                          - | 3 | int | Fan Speed | 1,6,2,3,4,5 (mapped to speeds 1-6) |
                                                                                                          - | 8 | enum | Fan Direction | 0=forward, 1=reverse |
                                                                                                          - | 15 | bool | Light Power | true/false |
                                                                                                          - | 16 | int | Light Brightness | 0-5 |
                                                                                                          - | 19 | enum | Color Temperature | 0=cool, 1=neutral, 2=warm |
                                                                                                       
                                                                                                          - ### Speed Mapping
                                                                                                       
                                                                                                          - The Tuya module uses a non-sequential speed mapping which is handled automatically:
                                                                                                          - - ESPHome Speed 1 → Tuya value 1
                                                                                                            - - ESPHome Speed 2 → Tuya value 6
                                                                                                              - - ESPHome Speed 3 → Tuya value 2
                                                                                                                - - ESPHome Speed 4 → Tuya value 3
                                                                                                                  - - ESPHome Speed 5 → Tuya value 4
                                                                                                                    - - ESPHome Speed 6 → Tuya value 5
                                                                                                                     
                                                                                                                      - ## Configuration Options
                                                                                                                     
                                                                                                                      - The configuration uses substitutions for easy customization:
                                                                                                                     
                                                                                                                      - ```yaml
                                                                                                                        substitutions:
                                                                                                                          name: skyfandc01
                                                                                                                          friendly_name: SkyFan DC01
                                                                                                                        ```
                                                                                                                        
                                                                                                                        Modify these values to change device names and create multiple instances.
                                                                                                                        
                                                                                                                        ## Home Assistant Integration
                                                                                                                        
                                                                                                                        This device integrates seamlessly with Home Assistant via the ESPHome integration:
                                                                                                                        
                                                                                                                        1. Navigate to Settings → Devices & Services
                                                                                                                        2. 2. Click "Add Integration" and select ESPHome
                                                                                                                           3. 3. Enter the device IP address or hostname
                                                                                                                              4. 4. Enter your API key from secrets.yaml
                                                                                                                                
                                                                                                                                 5. The fan and light will appear as separate entities ready to use in automations, scenes, and dashboards.
                                                                                                                                
                                                                                                                                 6. ## Network Features
                                                                                                                                
                                                                                                                                 7. - **WiFi:** Standard 2.4GHz connection
                                                                                                                                    - - **Web Server:** Built-in web interface on port 80
                                                                                                                                      - - **OTA Updates:** Over-the-air firmware updates supported
                                                                                                                                        - - **Fallback AP:** Captive portal for configuration if WiFi fails
                                                                                                                                          - - **mDNS:** Device discovery via .local domain
                                                                                                                                           
                                                                                                                                            - ## Troubleshooting
                                                                                                                                           
                                                                                                                                            - ### Device won't connect to WiFi
                                                                                                                                            - - Check credentials in secrets.yaml
                                                                                                                                              - - Connect to fallback AP (SkyFan DC01 ESP) and reconfigure
                                                                                                                                                - - Check 2.4GHz WiFi is available
                                                                                                                                                 
                                                                                                                                                  - ### Fan/Light not responding
                                                                                                                                                  - - Verify UART pins (GPIO20/GPIO21)
                                                                                                                                                    - - Check baud rate is set to 9600
                                                                                                                                                      - - Ensure status LED on GPIO8 is functioning
                                                                                                                                                       
                                                                                                                                                        - ### Remote control not syncing
                                                                                                                                                        - - Configuration includes bidirectional datapoint listeners
                                                                                                                                                          - - Remote changes should reflect in Home Assistant immediately
                                                                                                                                                            - - Check UART communication in ESPHome logs
                                                                                                                                                             
                                                                                                                                                              - ## Contributing
                                                                                                                                                             
                                                                                                                                                              - Contributions are welcome! Please feel free to submit issues or pull requests.
                                                                                                                                                             
                                                                                                                                                              - ## License
                                                                                                                                                             
                                                                                                                                                              - This project is open source and available for personal and commercial use.
                                                                                                                                                             
                                                                                                                                                              - ## Credits
                                                                                                                                                             
                                                                                                                                                              - Project maintained by [lagomcontrol](https://github.com/lagomcontrol)
                                                                                                                                                             
                                                                                                                                                              - ## Version
                                                                                                                                                             
                                                                                                                                                              - Current version: 1.0
