---
description: Standalone function-level demos for each onboard peripheral of the 1.14 Inch Display Powered by XIAO ESP32-S3 Plus. Covers screen, IMU, PDM microphone and I2S audio, buttons, and battery voltage detection.
title: Onboard Peripheral Usage
keywords:
  - XIAO
  - ESP32-S3
  - Display
  - LCD
  - Function
  - 1.14
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /function_1.14_inch_display_esp32s3
sku: 100086099
sidebar_label: Function
sidebar_position: 2
last_update:
  date: 08/13/2026
  author: FaiyuetCik
---

# Onboard Peripheral Usage

This page collects standalone function-level demos for each onboard peripheral of the 1.14 Inch Display. Each section is self-contained — you can pick the one that matches your use case without reading through the others.

:::note
All demos in this page require **esp32 Boards by Espressif (3.3.11)** as described in [Getting Started](/getting_started_1.14_inch_display_esp32s3). Additionally, install the following library.
:::

- **Seeed_GFX (Manual Installation)** — this library is not available in Library Manager and must be installed manually:

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Studio/Seeed_GFX" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> Download Seeed_GFX</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

**Step 1.** Click the button above to download the `Seeed_GFX` library as a ZIP file. Alternatively, clone the repository from [Seeed-Studio/Seeed_GFX](https://github.com/Seeed-Studio/Seeed_GFX).

**Step 2.** Place the downloaded folder into your Arduino libraries folder (typically `Documents/Arduino/libraries/` on Windows). The resulting folder structure should be:

```
libraries/Seeed_GFX/
├── library.properties
├── TFT_eSPI.h
├── TFT_eSPI.cpp
├── User_Setup_Select.h
└── ...
```

**Step 3.** Restart the Arduino IDE so the new library is detected.

:::tip
- **Seeed_GFX** is Seeed Studio's fork of TFT_eSPI with pre-configured XIAO board presets. Each sketch's `driver.h` selects `BOARD_SCREEN_COMBO 75` with `USE_XIAO_TFT_DISPLAY_BOARD`, which maps to the correct 135×240 pin layout. This library is different from **GFX Library for Arduino** (by Moon On Our Nation) used in the Dashboard.
- The **IMU** is read directly over I2C (`Wire`) in these demos — no external IMU library is needed. The **PDM microphone** and **I2S output** use the ESP-IDF 5 drivers (`driver/i2s_pdm.h`, `driver/i2s_std.h`) and `LittleFS`, all included with the esp32 board package.
- The 1.14 Display has **no touch controller, no SD card slot**, so no touch or SD libraries are needed.
:::

## Screen Display — GraphicTest

This demo runs a full graphics benchmark on the 1.14-inch ST7789 IPS panel (135×240), covering color bars, lines, rectangles, circles, triangles, rounded rectangles, text, and a pixel gradient. Use it to verify that the screen is wired correctly and that all draw calls work as expected.

**Code location:** `code/Function/114_ESP32/xiao_esp32s3_114_graphictest/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_ESP32/xiao_esp32s3_114_graphictest" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The sketch initializes the ST7789 IPS panel via TFT_eSPI, then runs through ten graphics primitives in sequence, measuring the execution time of each one via `micros()` and printing the result to the serial monitor.

The key LCD configuration is abstracted in `driver.h`:

- **Chip select:** D2
- **Data/command:** D3
- **SPI clock:** D8
- **SPI data (MOSI):** D10
- **Reset:** D17
- **Backlight:** D18 (PWM-capable)

The ST7789 IPS panel on this board requires `invertDisplay(true)` for correct colors (unlike the 1.47" JD9853A which uses `invertDisplay(false)`). No MADCTL fix or JD9853A-specific register tweaks are needed.

### Running the Demo

**Step 1.** Open `xiao_esp32s3_114_graphictest.ino` in Arduino IDE.

**Step 2.** Select **Tools > Board > esp32 > XIAO_ESP32S3_Plus** and the correct **Port**.

**Step 3.** Click **Upload**.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud). You should see the panel size followed by timing output for each test:

```
=== XIAO ESP32-S3 Plus 1.14 graphic test ===
LCD width: 135
LCD height: 240
Color bars: ... ms
Lines: ... ms
Fast lines: ... ms
Rectangles: ... ms
Filled rectangles: ... ms
Circles: ... ms
Triangles: ... ms
Round rectangles: ... ms
Text: ... ms
Pixel gradient: ... ms
Graphic test finished.
```

On the screen, you will see each test pattern displayed for about one second before the next one starts. When all tests complete, a "Graphic / Finished" screen appears with a blue rounded-rectangle border.

### Expected Result

<!-- TODO: Add graphictest GIF -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_ESP32S3Plus_function_graphictest.gif" style={{width:500, height:'auto'}}/></div> -->

After the sketch runs through all patterns, the screen shows a "Graphic / Finished" message with "Reset to rerun" below it. Reset the board to run the test again.

---

## IMU

The 1.14 Inch Display features an onboard **LSM6DS3** 6-axis IMU (3-axis accelerometer + 3-axis gyroscope) connected via I2C on D4/D5 at address **0x6A**. The motion interrupt line on **D14** supports hardware wake-up and gesture detection.

:::note
The onboard IMU is the **LSM6DS3** (confirmed from the board schematic, I2C address `0x6A`). The demo sketches additionally probe for a QMI8658-compatible sensor as a defensive fallback in case of BOM variants, but the shipped 1.14 Inch Display uses the LSM6DS3.
:::

The demos below read the IMU directly over I2C (`Wire`) — no external IMU library is required.

<a id="imu-quicksand"></a>

### Demo 1: Electronic Quicksand

This demo turns the screen into an interactive fluid simulation — golden sand particles that flow and settle according to gravity, as measured by the onboard 6-axis IMU. Tilt the board and the sand shifts direction in real time.

**Code location:** `code/Function/114_ESP32/xiao_esp32s3_114_electronic_quicksand/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_ESP32/xiao_esp32s3_114_electronic_quicksand" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The simulation uses a **22×40 occupancy grid** overlaid on the 135×240 screen, where each cell is 6×6 pixels. Around **150 particles** are placed in the grid, each with a position, velocity, and a golden color gradient.

The IMU is read via I2C (D4/D5). The sketch probes for an IMU at both known addresses — QMI8658 first, then LSM6DS3 — and uses whichever one responds. Raw acceleration values are low-pass filtered and used to derive a gravity vector. When you tilt the board:

1. **Gravity vector updates** — accelerometer data is smoothed with an exponential moving average to avoid jitter.
2. **Particle velocity** — each particle accelerates in the direction of the gravity vector, with damping and a per-particle mobility factor based on its depth in the flow.
3. **Cell occupancy** — particles deeper in the flow (closer to the "bottom" relative to gravity) have reduced mobility, creating a realistic packing effect.
4. **Differential rendering** — only cells where particles moved into or out of are redrawn, minimizing SPI traffic and keeping the animation smooth.

Particles near the surface flow freely (higher mobility); particles buried deeper pack tightly (lower mobility) — mimicking how real sand behaves.

### Running the Demo

**Step 1.** Open `xiao_esp32s3_114_electronic_quicksand.ino` in Arduino IDE.

**Step 2.** Select the board and port, then click **Upload**.

**Step 3.** Once uploaded, the screen fills with golden particles at the bottom. Tilt the board in different directions — the sand flows as if pulled by gravity.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud) to confirm initialization:

```
=== Electronic Quicksand 1.14 ===
[IMU] QMI8658-compatible at 0x6B, WHO=0x05
```
or
```
=== Electronic Quicksand 1.14 ===
[IMU] LSM6-compatible at 0x6A, WHO=0x69
```

### Expected Result

<!-- TODO: Add quicksand GIF -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_ESP32S3Plus_function_quicksand.gif" style={{width:500, height:'auto'}}/></div> -->

The golden sand particles flow smoothly as you tilt the board. When held flat, the sand settles at the bottom of the screen. Rotate the board 90 degrees and the sand flows to the new "bottom" within a second.

---

### Demo 2: Raise to Wake

This demo implements a **screen sleep/wake system** driven by the IMU's built-in wake-up interrupt on **D14**. The screen automatically turns off (backlight off + ESP32 deep sleep) after 8 seconds of inactivity, and wakes instantly when you pick up or move the device.

**Code location:** `code/Function/114_ESP32/xiao_esp32s3_114_wakeup/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_ESP32/xiao_esp32s3_114_wakeup" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The demo uses the LSM6-compatible IMU's **embedded wake-up event detector** — a hardware feature that monitors accelerometer data internally and asserts the INT1 pin (routed to D14 on this board) when motion exceeds a configurable threshold. This means the MCU does not need to poll the accelerometer continuously.

**IMU configuration (LSM6-compatible):**

<div class="table-center">
  <table align="center">
    <tr><th>Register</th><th>Value</th><th>Purpose</th></tr>
    <tr><td><code>CTRL3_C</code></td><td><code>0x44</code></td><td>Enable BDU + auto-increment for block reads</td></tr>
    <tr><td><code>CTRL1_XL</code></td><td><code>0x40</code></td><td>Accelerometer @ 104 Hz, ±2g</td></tr>
    <tr><td><code>CTRL2_G</code></td><td><code>0x40</code></td><td>Gyroscope @ 104 Hz</td></tr>
    <tr><td><code>TAP_CFG</code></td><td><code>0x80</code></td><td>Enable embedded interrupts</td></tr>
    <tr><td><code>WAKE_UP_THS</code></td><td><code>0x05</code></td><td>Wake-up threshold (medium-low sensitivity)</td></tr>
    <tr><td><code>WAKE_UP_DUR</code></td><td><code>0x00</code></td><td>No duration filter (responsive wake)</td></tr>
    <tr><td><code>MD1_CFG</code></td><td><code>0x20</code></td><td>Route wake-up to INT1</td></tr>
  </table>
</div>

**Sleep/wake flow:**

1. **Active state** — screen is on, backlight at PWM 160. IMU data and battery voltage refresh periodically. A countdown timer shows seconds remaining until auto-sleep.
2. **Auto-sleep** — after 8 seconds of no activity, the sketch turns off the backlight, displays a "Sleeping... Pick up device to wake" message, configures D14 as an external wake-up source via `esp_sleep_enable_ext0_wakeup()`, and enters ESP32 deep sleep.
3. **Wake-up** — when the user picks up the board, the IMU detects motion and asserts D14 HIGH. The ESP32 wakes from deep sleep, re-initializes the LCD and IMU, and the UI is fully redrawn.

**Manual test buttons:**

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td>USR1</td><td>D6</td><td>Force sleep</td></tr>
    <tr><td>USR2</td><td>D7</td><td>Force wake</td></tr>
  </table>
</div>

### Running the Demo

**Step 1.** Open `xiao_esp32s3_114_wakeup.ino` in Arduino IDE, select the board and port, and click **Upload**.

**Step 2.** The screen shows a dashboard with power state, motion data, and a countdown timer. Let the board sit still for 8 seconds — it will automatically sleep.

**Step 3.** Pick up the board or shake it gently — the screen wakes immediately.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud) to observe the sleep/wake transitions:

```
=== XIAO ESP32-S3 Plus 1.14 IMU Wake Demo ===
[IMU] LSM6-compatible at 0x6A, WHO=0x69
[WAKE] POWER_ON count=1
sleep in 8s
[WAKE] IMU_D14 count=2
sleep in 8s
```

### Expected Result

<!-- TODO: Add wakeup GIF -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_ESP32S3Plus_function_wakeup.gif" style={{width:500, height:'auto'}}/></div> -->

The screen displays real-time motion data while awake. After 8 seconds of stillness, the screen goes dark and the ESP32-S3 enters deep sleep. Pick up the device and the screen restores within a fraction of a second, with the wake counter incremented.

---

## Microphone & Audio — Flash Recorder

This demo records 5 seconds of audio from the onboard PDM microphone into onboard Flash memory, then plays it back through an external speaker connected to the I2S output. Press one button to record, another to play.

**Code location:** `code/Function/114_ESP32/xiao_esp32s3_114_flash_record/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_ESP32/xiao_esp32s3_114_flash_record" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### Hardware Setup

Playback requires an external **I2S audio amplifier and speaker**. The demo is written for a **MAX98357A** breakout connected to the board's I2S output pads:

<div class="table-center">
  <table align="center">
    <tr><th>I2S Pad</th><th>XIAO Pin</th><th>MAX98357A</th></tr>
    <tr><td>3V3</td><td>3V3</td><td>VIN</td></tr>
    <tr><td>GND</td><td>GND</td><td>GND</td></tr>
    <tr><td>I2S_SD</td><td>D11</td><td>DIN</td></tr>
    <tr><td>I2S_SCK</td><td>D12</td><td>BCLK</td></tr>
    <tr><td>I2S_WS</td><td>D13</td><td>LRC</td></tr>
  </table>
</div>

The I2S pads (3V3, GND, D11, D12, D13) are exposed on the bottom expansion pad group of the display board.

### How It Works

**Recording** — the onboard **PDM (Pulse Density Modulation) digital microphone** is sampled through the ESP32-S3's I2S peripheral configured in PDM RX mode. On ESP-IDF v5 (Arduino core 3.3.11), this uses the new driver API (`driver/i2s_pdm.h`):

<div class="table-center">
  <table align="center">
    <tr><th>Pin</th><th>Signal</th><th>Function</th></tr>
    <tr><td>D0</td><td>PDM_CLK</td><td>PDM clock output to microphone</td></tr>
    <tr><td>D1</td><td>MIC_DATA</td><td>PDM data input from microphone</td></tr>
  </table>
</div>

The microphone is captured at **16 kHz mono** with 4 DMA descriptors of 256 frames each. When you press **USR1**, the sketch samples 5 seconds of audio into a RAM buffer, then writes it to onboard Flash as a WAV file (`/REC_RAW.WAV`) using `LittleFS`.

**Playback** — pressing **USR2** reads the WAV back from Flash and streams it out through the I2S peripheral in standard (Philips) stereo mode on D11/D12/D13. The mono samples are duplicated to both channels with a `0.75×` gain applied to avoid clipping. The amplifier drives a small speaker so you can hear the recording.

**On-screen states:**

<div class="table-center">
  <table align="center">
    <tr><th>State</th><th>Description</th></tr>
    <tr><td><strong>Ready</strong></td><td>"Flash Recorder" title with "USR1: record" and "USR2: play Flash WAV" (or "No saved recording")</td></tr>
    <tr><td><strong>Recording</strong></td><td>"Recording" label, a percentage (e.g. "45%  2/5s"), and a red progress bar</td></tr>
    <tr><td><strong>Saved</strong></td><td>"Done — Saved Flash WAV" confirmation, then returns to Ready</td></tr>
    <tr><td><strong>Playback</strong></td><td>"Playing raw audio" while streaming, then "Finished"</td></tr>
  </table>
</div>

### Running the Demo

**Step 1.** Connect a MAX98357A amplifier and speaker to the I2S pads as described above.

**Step 2.** Open `xiao_esp32s3_114_flash_record.ino` in Arduino IDE, select the board and port, and click **Upload**.

**Step 3.** Press **USR1 (D6)** to record 5 seconds of audio from the onboard microphone. The progress bar fills as it records.

**Step 4.** Press **USR2 (D7)** to play the recording back through the speaker.

:::note
The recording is stored in onboard Flash (`LittleFS`), so it survives a power cycle — you can record once and play it back later. Recording again overwrites the previous file.
:::

### Expected Result

<!-- TODO: Add flash recorder GIF -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_ESP32S3Plus_function_flash_record.gif" style={{width:500, height:'auto'}}/></div> -->

Press USR1 and the screen shows a recording progress bar. After 5 seconds it confirms the WAV was saved. Press USR2 and the audio plays through the connected speaker while the screen shows the playback status.

---

## User Buttons

The 1.14 Inch Display has **three physical push buttons** connected to the XIAO ESP32-S3 Plus:

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Logic</th><th>Silkscreen Label</th><th>Breakout Pad</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Active-low (pressed = LOW)</td><td>USR1</td><td>U1</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Active-low (pressed = LOW)</td><td>USR2</td><td>U2</td></tr>
    <tr><td><strong>USR3</strong></td><td>D19</td><td>Active-low (pressed = LOW)</td><td>USR3</td><td>U3</td></tr>
  </table>
</div>

### Reading a Button

The buttons use the XIAO's internal pull-up resistors. A simple non-blocking read looks like this:

```cpp
const int USR1 = D6;
const int USR2 = D7;
const int USR3 = D19;

void setup() {
  pinMode(USR1, INPUT_PULLUP);
  pinMode(USR2, INPUT_PULLUP);
  pinMode(USR3, INPUT_PULLUP);
  Serial.begin(115200);
}

void loop() {
  if (digitalRead(USR1) == LOW) {
    Serial.println("USR1 (D6) pressed");
    delay(200); // simple debounce
  }
  if (digitalRead(USR2) == LOW) {
    Serial.println("USR2 (D7) pressed");
    delay(200);
  }
  if (digitalRead(USR3) == LOW) {
    Serial.println("USR3 (D19) pressed");
    delay(200);
  }
}
```

### Debounce with Interrupts

For responsive, debounced button handling without blocking the main loop, you can use pin-change interrupts:

```cpp
volatile bool btn1Flag = false;
volatile bool btn2Flag = false;
volatile bool btn3Flag = false;

void btn1Isr() { btn1Flag = true; }
void btn2Isr() { btn2Flag = true; }
void btn3Isr() { btn3Flag = true; }

void setup() {
  pinMode(D6, INPUT_PULLUP);
  pinMode(D7, INPUT_PULLUP);
  pinMode(D19, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(D6), btn1Isr, FALLING);
  attachInterrupt(digitalPinToInterrupt(D7), btn2Isr, FALLING);
  attachInterrupt(digitalPinToInterrupt(D19), btn3Isr, FALLING);
}

void loop() {
  if (btn1Flag) {
    btn1Flag = false;
    delay(30); // debounce settling time
    if (digitalRead(D6) == LOW) {
      // handle USR1 press
    }
  }
  if (btn2Flag) {
    btn2Flag = false;
    delay(30);
    if (digitalRead(D7) == LOW) {
      // handle USR2 press
    }
  }
  if (btn3Flag) {
    btn3Flag = false;
    delay(30);
    if (digitalRead(D19) == LOW) {
      // handle USR3 press
    }
  }
}
```

### Default Behavior in the Factory Dashboard

In the preloaded factory firmware, the buttons are mapped as follows (you can override these in your own code):

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Cycle screen brightness (100% → 75% → 50% → 25% → 0% → 100%)</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Toggle screen off / restore to last brightness</td></tr>
    <tr><td><strong>USR3</strong></td><td>D19</td><td>Toggle header title between "Hello,XIAO!" and "Seeed"</td></tr>
  </table>
</div>

The button breakout pads (labeled U1, U2, and U3 on the board) mirror D6, D7, and D19 respectively, allowing you to connect external buttons if desired.

---

## Battery Voltage Detection

The 1.14 Inch Display includes an onboard battery voltage measurement circuit. The ESP32-S3 Plus reads the LiPo battery voltage through a voltage divider on D16.

### ESP32-S3 Plus Battery Measurement

<div class="table-center">
  <table align="center">
    <tr><th>Signal</th><th>ESP32-S3 Pin</th><th>Function</th></tr>
    <tr><td><code>BAT_ADC</code></td><td><strong>D16</strong></td><td>Analog input reading the divided battery voltage. Internally connected to a voltage divider circuit (316K / 160K). <strong>Do not use this pin externally.</strong></td></tr>
  </table>
</div>

**Voltage divider ratio:** R1 = 316 kΩ, R2 = 160 kΩ → **Divider ratio = (316 + 160) / 160 ≈ 2.975**

:::note
Unlike the nRF52840 Plus version which can detect charging status and calculate battery percentage, the ESP32-S3 Plus version displays live voltage readings rather than percentage or charging state.
:::

### Reading Battery Voltage

The ESP32-S3's 12-bit ADC reads the voltage at the ADC node (after the voltage divider). Multiply by the divider ratio to get the actual battery voltage:

```cpp
const int BAT_ADC_PIN = D16;
const float DIVIDER_RATIO = (316.0 + 160.0) / 160.0; // ≈ 2.975
const float ADC_FULL_SCALE = 3.3;   // ESP32-S3 ADC reference
const int ADC_MAX = 4095;            // 12-bit ADC

void setup() {
  analogReadResolution(12);
  Serial.begin(115200);
}

void readBattery() {
  // Discard first few samples for accuracy
  for (int i = 0; i < 8; i++) { analogRead(BAT_ADC_PIN); delay(2); }

  uint32_t sum = 0;
  for (int i = 0; i < 32; i++) {
    sum += analogRead(BAT_ADC_PIN);
    delay(2);
  }

  uint16_t raw = sum / 32;
  float vadc = (raw * ADC_FULL_SCALE) / ADC_MAX;
  float vbat = vadc * DIVIDER_RATIO;

  Serial.print("D16: "); Serial.print(vadc);
  Serial.print("V, Battery: "); Serial.print(vbat);
  Serial.println("V");
}
```

The circuit provides a continuous live-sense reading: `VBAT → 316K → ADC node (D16) → 160K → GND`.

---

## Resources

- **[GitHub]** [XIAO Display Board Demo Code](https://github.com/Seeed-Projects/Display-Gadgets) — all Function demos are in the `code/Function/114_ESP32/` directory
- **[PDF]** [Schematic — 1.14 Inch Display (XIAO ESP32-S3 Plus)](https://github.com/Seeed-Projects/Display-Gadgets/tree/main/schematics/1.14_Inch_Display_Powered_by_XIAO_ESP32-S3_Plus/Schematic)

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
