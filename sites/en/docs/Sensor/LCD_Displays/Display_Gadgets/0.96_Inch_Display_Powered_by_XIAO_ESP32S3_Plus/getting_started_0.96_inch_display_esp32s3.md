---
description: Getting Started with 0.96 Inch Display Powered by XIAO ESP32-S3 Plus.
title: Getting Started with 0.96 Inch Display Powered by XIAO ESP32-S3 Plus
keywords:
  - XIAO
  - ESP32-S3
  - Display
  - LCD
  - 0.96
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /getting_started_0.96_inch_display_esp32s3
sku: 100037468
sidebar_label: Getting Started
sidebar_position: 1
type: gettingstarted
last_update:
  date: 08/19/2026
  author: FaiyuetCik
createdAt: '2026-08-20'
updatedAt: '2026-08-24'
url: https://wiki.seeedstudio.com/getting_started_0.96_inch_display_esp32s3/
---

# Getting Started with 0.96 Inch Display Powered by XIAO ESP32-S3 Plus

<div class="table-center">
  <table align="center">
    <tr><th>0.96 Inch Display (XIAO ESP32-S3 Plus)</th></tr>
    <!-- TODO: Replace with actual product hero image (096_ESP32S3Plus_display_hardware_hero.jpg) -->
    <tr><td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png" style={{width:100, height:'auto'}}/></div></td></tr>
    <tr><td><div class="get_one_now_container" style={{textAlign: 'center'}}>
        <a class="get_one_now_item" href="#" target="_blank">
            <strong><span><font color={'FFFFFF'} size={"4"}> Get One Now 🖱️</font></span></strong>
        </a>
    </div></td></tr>
  </table>
</div>

## Introduction

The 0.96 Inch Display is a compact expansion board powered by the XIAO ESP32-S3 Plus. It combines an 80×160 IPS color LCD, an onboard PDM microphone, a 6-axis IMU, two user buttons, I2C and I2S expansion pads, and battery voltage sensing in a form factor designed for small connected devices.

The ESP32-S3 Plus adds Wi-Fi and Bluetooth connectivity, making the board suitable for compact wearables, portable sensor dashboards, keychain gadgets, and wireless IoT prototypes.

<div class="table-center">
  <table align="center">
    <tr><th>Item</th><th>Detail</th></tr>
    <tr><td>Screen</td><td>0.96 inch, ST7789, 80×160, IPS</td></tr>
    <tr><td>Microphone</td><td>PDM digital microphone (D0 clock / D1 data)</td></tr>
    <tr><td>IMU</td><td>LSM6DS3, 3-axis accelerometer + 3-axis gyroscope, I2C address 0x6A (D4/D5), interrupt D14</td></tr>
    <tr><td>Buttons</td><td>USR1 = D6 / USR2 = D7 (2 buttons, active-low)</td></tr>
    <tr><td>I2C breakout</td><td>D4/D5 back-side 4-pin test pad, shared with the onboard IMU</td></tr>
    <tr><td>Battery</td><td>LiPo battery connector; D16 ADC voltage sensing through a 316 kΩ / 160 kΩ divider</td></tr>
    <tr><td>Expansion</td><td>I2C test pad (GND, 3V3, SDA, SCL); I2S breakout (D11, D12, D13)</td></tr>
    <tr><td>Compatibility</td><td>XIAO ESP32-S3 Plus</td></tr>
  </table>
</div>

:::note
This display board is designed for the **XIAO ESP32-S3 Plus**. If you are using the XIAO nRF52840 Plus version, refer to the [0.96 Inch Display Powered by XIAO nRF52840 Plus](/getting_started_0.96_inch_display_nrf52840) guide instead.
:::

:::note
The ESP32-S3 Plus version uses D16 to measure the battery divider voltage. The current Dashboard displays the raw D16 ADC voltage and the calculated external voltage; it does not show a charging-state indicator.
:::

## Hardware Overview

Refer to the following views to identify the connectors and onboard components before connecting expansion hardware.

### Front View

<!-- TODO: Add front view image -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_hardware_front.jpg" style={{width:600, height:'auto'}}/></div> -->

### Back View

<!-- TODO: Add back view image -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_hardware_back.jpg" style={{width:600, height:'auto'}}/></div> -->

### Pin Map

The table below lists the XIAO ESP32-S3 Plus pins used by the display board and its onboard peripherals.

<div class="table-center">
  <table align="center">
    <tr><th>XIAO Pin</th><th>Net Name</th><th>Function Description</th><th>Hardware Connection Notes</th></tr>
    <tr><td>D0</td><td>PDM_CLK</td><td>PDM microphone clock</td><td>Internally connected to the onboard PDM microphone</td></tr>
    <tr><td>D1</td><td>PDM_DATA</td><td>PDM microphone data</td><td>Internally connected to the onboard PDM microphone</td></tr>
    <tr><td>D2</td><td>LCD_CS</td><td>LCD chip select</td><td>Internally connected to the LCD</td></tr>
    <tr><td>D3</td><td>LCD_DC</td><td>LCD data/command select</td><td>Internally connected to the LCD</td></tr>
    <tr><td>D4</td><td>I2C_SDA</td><td>I2C data</td><td>Shared by the onboard IMU and back-side I2C test pad</td></tr>
    <tr><td>D5</td><td>I2C_SCL</td><td>I2C clock</td><td>Shared by the onboard IMU and back-side I2C test pad</td></tr>
    <tr><td>D6</td><td>BTN_USR1</td><td>User button 1</td><td>Active-low; cycles the backlight brightness in the factory Dashboard</td></tr>
    <tr><td>D7</td><td>BTN_USR2</td><td>User button 2</td><td>Active-low; toggles the screen backlight ON/OFF in the factory Dashboard</td></tr>
    <tr><td>D8</td><td>LCD_SCK</td><td>Hardware SPI clock</td><td>Internally connected to the LCD</td></tr>
    <tr><td>D9</td><td>NC</td><td>Not connected</td><td>No physical connection</td></tr>
    <tr><td>D10</td><td>LCD_MOSI</td><td>Hardware SPI data output</td><td>Internally connected to the LCD</td></tr>
    <tr><td>D11</td><td>I2S_SD</td><td>I2S audio data</td><td>Externally exposed to the bottom expansion pad</td></tr>
    <tr><td>D12</td><td>I2S_SCK</td><td>I2S bit clock</td><td>Externally exposed to the bottom expansion pad</td></tr>
    <tr><td>D13</td><td>I2S_WS</td><td>I2S word select</td><td>Externally exposed to the bottom expansion pad</td></tr>
    <tr><td>D14</td><td>IMU_INT</td><td>IMU interrupt</td><td>Internally connected to the LSM6DS3 for motion and double-tap events</td></tr>
    <tr><td>D15</td><td>NC</td><td>Not connected</td><td>No physical connection</td></tr>
    <tr><td>D16</td><td>VBAT_ADC</td><td>Battery voltage sensing</td><td>Connected to the 316 kΩ / 160 kΩ divider. <strong>Do not use externally</strong></td></tr>
    <tr><td>D17</td><td>LCD_RST</td><td>LCD reset</td><td>Internally connected to the LCD</td></tr>
    <tr><td>D18</td><td>LCD_BL_PWM</td><td>LCD backlight control</td><td>Internally connected to the backlight driver circuit</td></tr>
    <tr><td>D19</td><td>NC</td><td>Not connected</td><td>No physical connection</td></tr>
  </table>
</div>

<!-- TODO: Add annotated pinout image -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_pinout.png" style={{width:1000, height:'auto'}}/></div> -->

:::caution
D4 and D5 are shared with the onboard IMU. Any external I2C device connected to the test pad must use a unique address and support 3.3 V logic.
:::

## Getting Started — Dashboard

The factory Dashboard demonstrates the LCD, battery voltage sensing, IMU data, double-tap detection, microphone level, and both user buttons. You can upload it again after testing your own sketches or use it as a reference for application development.

### Software Preparation

You will need the following tools and libraries:

- **Arduino IDE** (version 1.8 or later)

<div class="download_arduino_container" style={{textAlign: 'center'}}>
    <a class="download_arduino_item" href="https://www.arduino.cc/en/software"><strong><span><font color={'FFFFFF'} size={"4"}>Download Arduino IDE</font></span></strong></a>
</div><br />

- **esp32 Boards by Espressif (3.3.11)** — add the following URL to **File > Preferences > Additional Boards Manager URLs**:

```
https://espressif.github.io/arduino-esp32/package_esp32_index.json
```

Then go to **Tools > Board > Boards Manager**, search for **esp32**, and install version **3.3.11**.

- **Required Library** — go to **Sketch > Include Library > Manage Libraries...**, search for and install:

<div class="table-center">
  <table align="center">
    <tr><th>Library</th><th>Search Keyword</th><th>Author</th></tr>
    <tr><td><strong>GFX Library for Arduino</strong></td><td><code>GFX Library for Arduino</code></td><td>Moon On Our Nation</td></tr>
  </table>
</div>

:::note
**GFX Library for Arduino** above is required for the factory Dashboard firmware. The standalone function demos in the [Function](/function_0.96_inch_display_esp32s3) page instead use **Seeed_GFX2** (installed manually as described on that page) — the two libraries are different and not interchangeable.
:::

:::tip
The **Wire** and **WiFi** libraries are included with the esp32 board package and do not require separate installation.
:::

### Download the Dashboard Code

The complete example code is available on GitHub:

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/example/096_ESP32/0715_DashBoard_096_ESP32" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> Download the Code</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

Navigate to `code/example/096_ESP32/0715_DashBoard_096_ESP32/` and open `0715_DashBoard_096_ESP32.ino` in Arduino IDE.

### Upload the Firmware

**Step 1.** Connect the XIAO ESP32-S3 Plus to your computer through USB-C.

**Step 2.** Select **Tools > Board > esp32 > XIAO_ESP32S3_PLUS**.

**Step 3.** Select the correct **Port** under **Tools > Port**.

**Step 4.** Click **Upload**. The sketch will compile and upload to the board.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_dashboard_uploadpage.png" style={{width:1000, height:'auto'}}/></div>

**Step 5.** Open **Tools > Serial Monitor** and set the baud rate to **115200** to view the Dashboard diagnostics.

### Dashboard Overview

After upload, the Dashboard uses a compact layout optimized for the 80×160 display.

**Welcome Header**

The top of the screen shows **"Hello"** and the subtitle **"0.96 Display"**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_dashboard_welcome_header.gif" style={{width:500, height:'auto'}}/></div>

<a id="battery-voltage"></a>

**Battery Voltage**

The **SYSTEM** section displays two live readings:

- **D16** — the voltage measured at the ADC node.
- **Calc** — the calculated external voltage after applying the divider ratio of approximately 2.975.

The divider is `VBAT → 316 kΩ → D16 ADC node → 160 kΩ → GND`. D16 can float when no battery is connected, so treat the values as voltage-sense diagnostics rather than a charging-status indication.

There are three power scenarios:

- **USB-C powered, no battery** — the board is powered via USB-C, no battery connected.
- **Battery only (no USB-C)** — the board runs on battery power, displaying live voltage readings.
- **USB-C + battery** — both connected.

<div class="table-center">
  <table align="center">
    <tr>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_battery_states1.jpg" style={{width:220, height:'auto'}}/></div></td>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_battery_states2.jpg" style={{width:220, height:'auto'}}/></div></td>
    </tr>
    <tr>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_battery_states3.jpg" style={{width:220, height:'auto'}}/></div></td>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_battery_states4.jpg" style={{width:220, height:'auto'}}/></div></td>
    </tr>
  </table>
</div>

**Motion Sensor**

The **MOTION** section displays accelerometer and gyroscope readings from the onboard LSM6DS3. Move, tilt, or rotate the board and observe the values change.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_dashboard_motion.gif" style={{width:500, height:'auto'}}/></div>

**Double-Tap Counter**

The **TAP** counter increments when the LSM6DS3 detects a double-tap gesture. The gesture interrupt is connected to **D14**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_dashboard_double_tap.gif" style={{width:500, height:'auto'}}/></div>

**Microphone Level**

The **MIC** section contains a segmented audio-level meter and a raw peak value. Speak near the onboard PDM microphone to see the meter respond.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_dashboard_mic.gif" style={{width:500, height:'auto'}}/></div>

**User Buttons**

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Dashboard Action</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Cycle backlight brightness (100% → 75% → 50% → 25% → 100%)</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Toggle the LCD backlight ON/OFF</td></tr>
  </table>
</div>

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_ESP32S3Plus_display_dashboard_buttons.gif" style={{width:500, height:'auto'}}/></div>

## FAQ

### The board does not appear in the Tools > Board menu

1. Open **File > Preferences** and add the ESP32 Boards Manager URL:

   ```
   https://espressif.github.io/arduino-esp32/package_esp32_index.json
   ```

2. Open **Tools > Board > Boards Manager**, search for **esp32**, and install version **3.3.11**.
3. Select **Tools > Board > esp32 > XIAO_ESP32S3_PLUS**.

Restart Arduino IDE if the board entry still does not appear.

### Why isn't my screen bright when I plug in the USB-C cable?

The screen backlight may be off. Press the **USR2 (D7)** button to toggle the backlight back on — the display will light up normally.

### How should I hold the board?

Hold the board near the buttons, and do not touch the **XIAO** module. Grip the board by the button area instead.

## Resources

- **[GitHub]** [XIAO Display Board Demo Code](https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/example/096_ESP32/0715_DashBoard_096_ESP32)
- **[PDF]** [Schematic — 0.96 Inch Display (XIAO ESP32-S3 Plus)](https://github.com/Seeed-Projects/Display-Gadgets/tree/main/schematics/0.96_Inch_Display_Powered_by_XIAO_ESP32-S3_Plus/Schematic)

## Tech Support & Product Discussion

Thank you for choosing our products! We are here to provide you with different support to ensure that your experience with our products is as smooth as possible. We offer several communication channels to cater to different preferences and needs.

<div class="table-center">
  <div class="button_tech_support_container">
  <a href="https://forum.seeedstudio.com/" class="button_forum"></a>
  <a href="https://www.seeedstudio.com/contacts" class="button_email"></a>
  </div>

  <div class="button_tech_support_container">
  <a href="https://discord.gg/eWkprNDMU7" class="button_discord"></a>
  <a href="https://github.com/Seeed-Studio/wiki-documents/discussions/69" class="button_discussion"></a>
  </div>
</div>
