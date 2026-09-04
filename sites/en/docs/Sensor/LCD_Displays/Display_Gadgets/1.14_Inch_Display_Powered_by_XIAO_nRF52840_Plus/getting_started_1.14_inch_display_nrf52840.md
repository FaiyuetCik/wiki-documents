---
description: Getting Started with 1.14 Inch Display Powered by XIAO nRF52840 Plus.
title: Getting Started with 1.14 Inch Display Powered by XIAO nRF52840 Plus
keywords:
  - XIAO
  - nRF52840
  - Display
  - LCD
  - 1.14
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /getting_started_1.14_inch_display_nrf52840
sku: 100069374
sidebar_label: Getting Started
sidebar_position: 1
type: gettingstarted
last_update:
  date: 08/20/2026
  author: FaiyuetCik
createdAt: '2026-08-11'
updatedAt: '2026-08-21'
url: https://wiki.seeedstudio.com/getting_started_1.14_inch_display_nrf52840/
---

# Getting Started with 1.14 Inch Display Powered by XIAO nRF52840 Plus

<div class="table-center">
  <table align="center">
    <tr><th>1.14 Inch Display (XIAO nRF52840 Plus)</th></tr>
    <tr><td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_hardware_hero.jpg" style={{width:600, height:'auto'}}/></div></td></tr>
    <tr><td><div class="get_one_now_container" style={{textAlign: 'center'}}>
        <a class="get_one_now_item" href="#" target="_blank">
            <strong><span><font color={'FFFFFF'} size={"4"}> Get One Now 🖱️</font></span></strong>
        </a>
    </div></td></tr>
  </table>
</div>

## Introduction

The 1.14 Inch Display is an expansion board designed for the XIAO series, powered by the XIAO nRF52840 Plus. It features a 135×240 IPS color LCD, onboard PDM microphone, 6-axis IMU (LSM6DS3-compatible), Grove I2C connector, three user buttons, and battery power management with percentage display — all integrated into a compact form factor.

This combination makes it an ideal platform for wearable devices, compact sensor nodes, portable instruments, and IoT prototyping where space is at a premium.

<div class="table-center">
  <table align="center">
    <tr><th>Item</th><th>Detail</th></tr>
    <tr><td>Screen</td><td>1.14 inch, ST7789, 135×240, IPS</td></tr>
    <tr><td>Microphone</td><td>PDM digital microphone (D0 CLK / D1 DATA)</td></tr>
    <tr><td>IMU</td><td>LSM6DS3, 3-axis accelerometer + 3-axis gyroscope, I2C (D4/D5), interrupt D14</td></tr>
    <tr><td>Buttons</td><td>USR1 = D6 / USR2 = D7 / USR3 = D19 (3 buttons, active-low)</td></tr>
    <tr><td>Grove I2C</td><td>D4/D5 breakout (shared with onboard IMU; standard Grove I2C connector)</td></tr>
    <tr><td>Battery</td><td>LiPo battery connector, voltage measurement with percentage display and charging status detection</td></tr>
    <tr><td>Expansion</td><td>I2C breakout (GND, 3V3, SDA, SCL); Button breakout (U1, U2, U3); I2S breakout (3V3, GND, D11, D12, D13); Test pad (D15 / TP11); SWD (DIO, CLK, RST, GND)</td></tr>
    <tr><td>Compatibility</td><td>XIAO nRF52840 Plus</td></tr>
  </table>
</div>

:::note
This display board is designed for the **XIAO nRF52840 Plus**. If you are using the XIAO ESP32-S3 Plus version, please refer to the [1.14 Inch Display Powered by XIAO ESP32-S3 Plus](/getting_started_1.14_inch_display_esp32s3) guide instead.
:::

## Hardware Overview

Before we start, refer to the following images to understand the physical layout of the 1.14 Inch Display.

### Front View

<!-- TODO: Add front view image (114_nRF52840Plus_display_hardware_front.jpg) -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_hardware_front.jpg" style={{width:600, height:'auto'}}/></div> -->

### Back View

<!-- TODO: Add back view image (114_nRF52840Plus_display_hardware_back.jpg) -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_hardware_back.jpg" style={{width:600, height:'auto'}}/></div> -->

### Pin Map

The 1.14 Inch Display breaks out all XIAO nRF52840 Plus pins. The table below lists every pin, its net name on the display board, its function, and how it is connected to onboard peripherals.

<div class="table-center">
  <table align="center">
    <tr><th>XIAO Pin</th><th>Net Name</th><th>Function Description</th><th>Hardware Connection Notes</th></tr>
    <tr><td>D0</td><td>PDM_CLK</td><td>PDM digital microphone clock</td><td>Internally connected to PDM Mic</td></tr>
    <tr><td>D1</td><td>MIC_DATA</td><td>PDM digital microphone data</td><td>Internally connected to PDM Mic</td></tr>
    <tr><td>D2</td><td>LCD_CS</td><td>Screen chip select signal</td><td>Internally connected to LCD driver IC</td></tr>
    <tr><td>D3</td><td>LCD_DC</td><td>Screen data/command switch</td><td>Internally connected to LCD driver IC</td></tr>
    <tr><td>D4</td><td>SDA</td><td>I2C data bus</td><td>Bus sharing: internally connected to IMU; externally exposed to Grove I2C connector</td></tr>
    <tr><td>D5</td><td>SCL</td><td>I2C clock bus</td><td>Bus sharing: internally connected to IMU; externally exposed to Grove I2C connector</td></tr>
    <tr><td>D6</td><td>BTN_A</td><td>Physical button A (left)</td><td>Internally connected to front-left microswitch with external 1 KΩ pull-up. Externally exposed as U1 test pad</td></tr>
    <tr><td>D7</td><td>BTN_B</td><td>Physical button B (right)</td><td>Internally connected to front-right microswitch with external 1 KΩ pull-up. Externally exposed as U2 test pad</td></tr>
    <tr><td>D8</td><td>SCK</td><td>Hardware SPI clock</td><td>Internally connected to LCD driver IC</td></tr>
    <tr><td>D9</td><td>NC</td><td>Floating (reserved)</td><td>No physical connection</td></tr>
    <tr><td>D10</td><td>MOSI</td><td>Hardware SPI data output</td><td>Internally connected to LCD driver IC</td></tr>
    <tr><td>D11</td><td>I2S_SD</td><td>Audio data output</td><td>Externally exposed to bottom expansion pad</td></tr>
    <tr><td>D12</td><td>I2S_SCK</td><td>Audio bit clock</td><td>Externally exposed to bottom expansion pad</td></tr>
    <tr><td>D13</td><td>I2S_WS</td><td>Audio word select</td><td>Externally exposed to bottom expansion pad</td></tr>
    <tr><td>D14</td><td>IMU_INT</td><td>IMU motion hardware interrupt</td><td>Internally connected to 6-axis IMU for asynchronous wake-up</td></tr>
    <tr><td>D15</td><td>NC</td><td>Reserved test point</td><td>Bare copper test pad reserved on PCB</td></tr>
    <tr><td>D16</td><td>NC</td><td>Floating (reserved)</td><td>No physical connection</td></tr>
    <tr><td>D17</td><td>LCD_RST</td><td>Screen soft reset</td><td>Internally connected to LCD driver IC</td></tr>
    <tr><td>D18</td><td>LCD_BL</td><td>Screen backlight control</td><td>Internally connected to backlight driver circuit</td></tr>
    <tr><td>D19</td><td>BTN_C</td><td>Physical button C (side)</td><td>Internally connected to side microswitch with external 1 KΩ pull-up. Externally exposed as U3 test pad</td></tr>
  </table>
</div>

<!-- TODO: Add annotated pinout image (114_nRF52840Plus_display_pinout.png) -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_pinout.png" style={{width:1000, height:'auto'}}/></div> -->

## Getting Started — Dashboard

The product ships with a **Factory Dashboard** firmware preloaded, which demonstrates all onboard peripherals: screen display, IMU data, microphone, Grove I2C scan, and battery monitoring. The steps below walk you through setting up the development environment and re-flashing this firmware — useful if you want to restore the factory demo after experimenting with your own code, or use it as a starting point for your own projects.

### Software Preparation

You will need the following tools and libraries:

- **Arduino IDE** (version 1.8 or later)

<div class="download_arduino_container" style={{textAlign: 'center'}}>
    <a class="download_arduino_item" href="https://www.arduino.cc/en/software"><strong><span><font color={'FFFFFF'} size={"4"}>Download Arduino IDE</font></span></strong></a>
</div><br />

- **Seeed nRF52 Boards (1.1.13)** — add the following URL to **File > Preferences > Additional Boards Manager URLs**:

```
https://files.seeedstudio.com/arduino/package_seeeduino_boards_index.json
```

Then go to **Tools > Board > Boards Manager**, search for **Seeed nRF52** and install version **1.1.13**.

- **Required Libraries** — go to **Sketch > Include Library > Manage Libraries...**, search for and install the following:

<div class="table-center">
  <table align="center">
    <tr><th>Library</th><th>Search Keyword</th><th>Author</th></tr>
    <tr><td><strong>GFX Library for Arduino</strong></td><td><code>GFX Library for Arduino</code></td><td>Moon On Our Nation</td></tr>
    <tr><td><strong>SparkFun LSM6DS3</strong></td><td><code>SparkFun LSM6DS3</code></td><td>SparkFun</td></tr>
  </table>
</div>

:::note
**GFX Library for Arduino** above is only required for the factory Dashboard firmware. If you are working with the standalone function demos in the [Function](/function_1.14_inch_display_nrf52840) page, install **Seeed_GFX2** (from [Seeed-Studio/Seeed_GFX2](https://github.com/Seeed-Studio/Seeed_GFX2)) instead — the two libraries are different and not interchangeable.
:::

### Download the Dashboard Code

The complete example code is available on GitHub:

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> Download the Code</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

Navigate to `code/example/114_nRF52840/0715_DashBoard_114_nRF52840/` and open `0715_DashBoard_114_nRF52840.ino` in Arduino IDE.

### Upload the Firmware

**Step 1.** Connect the XIAO nRF52840 Plus to your computer via the USB-C port.

**Step 2.** In Arduino IDE, select the board:
- **Tools > Board > Seeed nRF52 Boards > Seeed XIAO nRF52840 Plus**

**Step 3.** Select the correct **Port** under **Tools > Port**.

**Step 4.** Click the **Upload** button (→). The firmware will compile and upload to the board.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_uploadpage.png" style={{width:1000, height:'auto'}}/></div>

:::note
If you encounter upload issues, double-click the reset button to enter bootloader mode. The USR LED will breathe in red and a **NRF52BOOT** drive will appear on your computer, indicating the board is in bootloader mode.
:::

### Dashboard Overview

Once uploaded, the factory Dashboard lights up the screen and demonstrates every onboard peripheral through a unified interface. Here is what each area shows and how to interact with it:

**Welcome Banner**

At the top of the screen, **"Hello,XIAO!"** is displayed in large green text, with a subtitle reading **"1.14 Inch Display"** in cyan below it. This static banner appears on boot — if you see it without artifacts or tearing, the LCD is working correctly.

Pressing <strong>USR3 (D19)</strong> toggles the header text between <strong>"Hello,XIAO!"</strong> and <strong>"Seeed Studio"</strong>. Due to the 135 px display width, the second title is abbreviated to <strong>"Seeed"</strong> on screen.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_welcome_banner.gif" style={{width:500, height:'auto'}}/></div>

**Battery**

The **BAT** section inside the **SYS** card shows a battery icon, percentage, and a charging indicator. There are three scenarios:

- **USB-C powered, no battery** — displays **"USB PWR"** in red.
- **Battery only (no USB-C)** — displays the battery icon with the percentage (e.g. **"85%"**).
- **USB-C + battery** — same as above, plus a yellow lightning bolt ⚡ icon indicating the battery is charging. There is a switch on the board to toggle battery power mode on or off.

<div class="table-center">
  <table align="center">
    <tr>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_battery_states1.jpg" style={{width:220, height:'auto'}}/></div></td>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_battery_states2.jpg" style={{width:220, height:'auto'}}/></div></td>
    </tr>
    <tr>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_battery_states3.jpg" style={{width:220, height:'auto'}}/></div></td>
      <td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_battery_states4.jpg" style={{width:220, height:'auto'}}/></div></td>
    </tr>
  </table>
</div>

**I2C Scan**

Also inside the **SYS** card, the **I2C** line shows the result of a periodic I2C bus scan. It displays the number of detected I2C devices followed by the lowest address. By default it shows the onboard 6-axis IMU — **"1 0x6A"**.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_i2c_scan.jpg" style={{width:500, height:'auto'}}/></div>

**Motion Sensor**

The **MOTION** card streams 6-axis IMU data over I2C. Accelerometer readings (X/Y/Z) and gyroscope readings (X/Y/Z) are shown as multi-line text. Pick up the board and tilt or shake it — the values change according to the direction of movement.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_motion.gif" style={{width:500, height:'auto'}}/></div>

**Double-Tap Counter**

The **"Tap"** counter at the top-right of the MOTION card tracks double-tap gestures. Firmly tap the board twice in quick succession (like a mouse double-click) and the counter increments by 1. This uses the LSM6DS3's built-in double-tap detection on the D14 interrupt line.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_double_tap.gif" style={{width:500, height:'auto'}}/></div>

**Microphone Level**

The **MIC LEVEL** card displays a VU-style audio meter — a segmented horizontal bar that grows and shrinks with the ambient sound volume. In a quiet room the bar stays empty or nearly so. Speak into the onboard PDM microphone or blow on it, and the bar fills up, turning orange then red at high volume levels. The raw peak value is printed below the bar for debugging.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_mic.gif" style={{width:500, height:'auto'}}/></div>

**Button & Backlight Control**

The **BACKLIGHT** card at the bottom shows the current brightness percentage and the three push-button mappings:

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Short press: cycle brightness through <strong>100% → 75% → 50% → 25% → 100%</strong></td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Short press: <strong>toggle screen off / restore to last brightness</strong></td></tr>
    <tr><td><strong>USR3</strong></td><td>D19</td><td>Short press: <strong>toggle header title between "Hello,XIAO!" and "Seeed"</strong></td></tr>
  </table>
</div>

When the screen is off (toggled via USR2), pressing USR2 again restores it to the previous non-zero level.

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_display_dashboard_button.gif" style={{width:500, height:'auto'}}/></div>

## FAQ

### What if the upload fails or the board is not detected?

Double-click the reset button on the XIAO nRF52840 Plus. The USR LED will breathe in red and a drive named **NRF52BOOT** will appear on your computer. Drag the compiled `.uf2` file onto the **NRF52BOOT** drive. The board will program itself and reset automatically.

### Can I hot-plug I2C devices while the dashboard is running?

No — we strongly recommend **against hot-plugging** devices on the I2C interface while the dashboard is running. Always power off the board before connecting or disconnecting anything on the Grove I2C connector or the SDA/SCL breakout pads. Hot-plugging can hang the I2C bus.

## Resources

- **[GitHub]** [XIAO Display Board Demo Code](https://github.com/Seeed-Projects/Display-Gadgets) — Dashboard code is in `code/example/114_nRF52840/`
- **[PDF]** [Schematic — 1.14 Inch Display (XIAO nRF52840 Plus)](https://github.com/Seeed-Projects/Display-Gadgets/tree/main/schematics/1.14_Inch_Display_Powered_by_XIAO_nRF52840_Plus/Schematic)

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
