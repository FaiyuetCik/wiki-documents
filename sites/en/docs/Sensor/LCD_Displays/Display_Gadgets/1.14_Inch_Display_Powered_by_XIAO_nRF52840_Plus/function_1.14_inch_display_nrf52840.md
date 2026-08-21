---
description: Standalone function-level demos for each onboard peripheral of the 1.14 Inch Display Powered by XIAO nRF52840 Plus. Covers screen, IMU, PDM microphone, buttons, battery, and Grove I2C.
title: Onboard Peripheral Usage
keywords:
  - XIAO
  - nRF52840
  - Display
  - LCD
  - Function
  - 1.14
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /function_1.14_inch_display_nrf52840
sku: 100069374
sidebar_label: Function
sidebar_position: 2
last_update:
  date: 08/12/2026
  author: FaiyuetCik
---

# Onboard Peripheral Usage

This page collects standalone function-level demos for each onboard peripheral of the 1.14 Inch Display. Each section is self-contained — you can pick the one that matches your use case without reading through the others.

:::note
All demos in this page require **Seeed nRF52 Boards (1.1.13)** as described in [Getting Started](/getting_started_1.14_inch_display_nrf52840). Additionally, install the following libraries.
:::

- **Library Manager** — go to **Sketch > Include Library > Manage Libraries...**, search for and install:

<div class="table-center">
  <table align="center">
    <tr><th>Library</th><th>Search Keyword</th><th>Author</th><th>Required by</th></tr>
    <tr><td><strong>Seeed Arduino LSM6DS3</strong></td><td><code>Seeed Arduino LSM6DS3</code></td><td>Seeed Studio</td><td>IMU demos</td></tr>
  </table>
</div>

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
- **Seeed_GFX** is Seeed Studio's fork of TFT_eSPI with pre-configured XIAO board presets. Each sketch's `driver.h` selects `BOARD_SCREEN_COMBO 75` with `USE_XIAO_TFT_DISPLAY_BOARD`, which provides the ST7789 driver and pin mapping — the 135×240 resolution is set by the `TFT_eSPI tft(135, 240)` constructor in each sketch. This library is different from **GFX Library for Arduino** (by Moon On Our Nation) used in the Dashboard.
- The 1.14 Display has **no touch controller, no SD card slot**, so no touch or SD libraries are needed.
:::

## Screen Display — GraphicTest

This demo runs a full graphics benchmark on the 1.14-inch ST7789 IPS panel (135×240), covering color bars, lines, rectangles, circles, triangles, rounded rectangles, text, and a pixel gradient. Use it to verify that the screen is wired correctly and that all draw calls work as expected.

**Code location:** `code/Function/114_nRF52840/xiao_nrf52840_114_graphictest/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_nRF52840/xiao_nrf52840_114_graphictest" target="_blank" rel="noopener noreferrer">
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

**Step 1.** Open `xiao_nrf52840_114_graphictest.ino` in Arduino IDE.

**Step 2.** Select **Tools > Board > Seeed nRF52 Boards > Seeed XIAO nRF52840 Plus** and the correct **Port**.

**Step 3.** Click **Upload**.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud). You should see timing output for each test:

```
LCD width: 135
LCD height: 240
Color bars: 333.98 ms
Lines: 1031.25 ms
Fast lines: 471.68 ms
Rectangles: 375.98 ms
Filled rectangles: 1170.90 ms
Circles: 447.27 ms
Triangles: 567.38 ms
Round rectangles: 397.46 ms
Text: 437.50 ms
Pixel gradient: 1657.23 ms
Graphic test finished.
```

On the screen, you will see each test pattern displayed for about one second before the next one starts. When all tests complete, a "Finished" screen appears.

### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_function_graphictest.gif" style={{width:500, height:'auto'}}/></div>

After the sketch runs through all patterns, the screen shows a "Finished" message. Reset the board to run the test again.

---

## IMU

The 1.14 Inch Display features an onboard 6-axis IMU (LSM6DS3) connected via I2C on D4/D5. The motion interrupt line on **D14** supports hardware wake-up and gesture detection.

Both demos below use the LSM6DS3 at I2C address **0x6A**.

<a id="imu-quicksand"></a>

### Demo 1: Electronic Quicksand

This demo turns the screen into an interactive fluid simulation — golden sand particles that flow and settle according to gravity, as measured by the onboard 6-axis IMU. Tilt the board and the sand shifts direction in real time.

**Code location:** `code/Function/114_nRF52840/xiao_nrf52840_114_electronic_quicksand/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_nRF52840/xiao_nrf52840_114_electronic_quicksand" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The simulation uses a **22×40 occupancy grid** overlaid on the 135×240 screen, where each cell is 6×6 pixels. Around **150 particles** are placed in the grid, each with a position, velocity, and a golden color gradient.

The IMU is read via I2C (D4/D5) using the Seeed Arduino LSM6DS3 library at address `0x6A`. Raw acceleration values are low-pass filtered and used to derive a gravity vector. When you tilt the board:

1. **Gravity vector updates** — accelerometer data is smoothed with an exponential moving average to avoid jitter.
2. **Particle velocity** — each particle accelerates in the direction of the gravity vector, with damping and a per-particle mobility factor based on its depth in the flow.
3. **Cell occupancy** — particles deeper in the flow (closer to the "bottom" relative to gravity) have reduced mobility, creating a realistic packing effect.
4. **Differential rendering** — only cells where particles moved into or out of are redrawn, minimizing SPI traffic and keeping the animation smooth.

Particles near the surface flow freely (higher mobility); particles buried deeper pack tightly (lower mobility) — mimicking how real sand behaves.

### Running the Demo

**Step 1.** Open `xiao_nrf52840_114_electronic_quicksand.ino` in Arduino IDE.

**Step 2.** Select the board and port, then click **Upload**.

**Step 3.** Once uploaded, the screen fills with golden particles at the bottom. Tilt the board in different directions — the sand flows as if pulled by gravity.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud) to confirm initialization:

```
=== Electronic Quicksand 1.14 ===
imu.begin=0
```

### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_function_quicksand.gif" style={{width:500, height:'auto'}}/></div>

The golden sand particles flow smoothly as you tilt the board. When held flat, the sand settles at the bottom of the screen. Rotate the board 90 degrees and the sand flows to the new "bottom" within a second.

---

### Demo 2: Raise to Wake

This demo implements a **screen sleep/wake system** driven by the IMU's built-in motion interrupt on **D14**. The screen automatically turns off (backlight off + nRF52 system ON sleep) after a configurable idle period, and wakes instantly when you pick up or move the device.

**Code location:** `code/Function/114_nRF52840/xiao_nrf52840_114_wakeup/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_nRF52840/xiao_nrf52840_114_wakeup" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The demo uses the LSM6DS3's **embedded wake-up event detector** — a hardware feature that monitors accelerometer data internally and asserts the INT1 pin (routed to D14 on this board) when motion exceeds a configurable threshold. This means the MCU does not need to poll the accelerometer continuously.

**IMU configuration (LSM6DS3):**

<div class="table-center">
  <table align="center">
    <tr><th>Register</th><th>Value</th><th>Purpose</th></tr>
    <tr><td><code>CTRL1_XL</code></td><td><code>0x40</code></td><td>Accelerometer @ 104 Hz, ±2g</td></tr>
    <tr><td><code>TAP_CFG</code></td><td><code>0x80</code></td><td>Enable embedded interrupts</td></tr>
    <tr><td><code>WAKE_UP_THS</code></td><td><code>0x05</code></td><td>Wake-up threshold (medium-low sensitivity)</td></tr>
    <tr><td><code>WAKE_UP_DUR</code></td><td><code>0x00</code></td><td>No duration filter (responsive wake)</td></tr>
    <tr><td><code>MD1_CFG</code></td><td><code>0x20</code></td><td>Route wake-up to INT1</td></tr>
  </table>
</div>

**Sleep/wake flow:**

1. **Active state** — screen is on, backlight at full brightness, UI refreshes every 250 ms with real-time IMU data. A countdown timer shows seconds remaining until auto-sleep.
2. **Auto-sleep** — after the idle timeout, the sketch turns off the backlight, displays a "Sleeping... Pick up device to wake" message, and enters nRF52 System ON sleep (low-power mode with RAM retention). The IMU wake interrupt on D14 was already configured at startup, so motion detection remains active during sleep.
3. **Wake-up** — when the user picks up the board, the IMU detects motion and asserts D14 HIGH. The nRF52840 exits sleep, re-initializes the LCD and IMU, and the UI is fully redrawn.

**Manual test buttons:**

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td>USR1</td><td>D6</td><td>Force sleep</td></tr>
    <tr><td>USR2</td><td>D7</td><td>Force wake</td></tr>
  </table>
</div>

### Running the Demo

**Step 1.** Open `xiao_nrf52840_114_wakeup.ino` in Arduino IDE, select the board and port, and click **Upload**.

**Step 2.** The screen shows a dashboard with power state, motion data, and a countdown timer. Let the board sit still — it will automatically enter sleep after the idle period.

**Step 3.** Pick up the board or shake it gently — the screen wakes immediately.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud) to observe the sleep/wake transitions:

```
LCD: 135x240
[IMU] Seeed LSM6DS3 begin=0
[IMU] D14 wake interrupt OK
[BOOT] done. Screen should be on.
[WAKE] reason=IMU_D14 wakeCount=1 sleptMs=3568 sleepLoops=0
[SLEEP] screen off, entering System ON sleep
[SLEEP] loops=1 D14=0 awake=N
[WAKE] reason=IMU_D14 wakeCount=2 sleptMs=1378 sleepLoops=439
```

### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_function_wakeup.gif" style={{width:500, height:'auto'}}/></div>

The screen displays real-time motion data while awake. After the idle period of stillness, the screen goes dark and the nRF52840 enters low-power sleep. Pick up the device and the screen restores instantly, with the wake counter incremented.

---

## Microphone

The 1.14 Inch Display features the same PDM digital microphone as the 1.47" version, connected to the same pins:

<div class="table-center">
  <table align="center">
    <tr><th>Pin</th><th>Signal</th><th>Function</th></tr>
    <tr><td>D0</td><td>PDM_CLK</td><td>PDM clock output to microphone</td></tr>
    <tr><td>D1</td><td>MIC_DATA</td><td>PDM data input from microphone</td></tr>
  </table>
</div>

### Demo: Voice Bar

This demo visualizes the PDM microphone's real-time audio input as a dynamic equalizer-style waveform and a segmented volume bar. Speak, clap, or blow into the onboard microphone and watch the bars react instantly.

**Code location:** `code/Function/114_nRF52840/xiao_nrf52840_114_voice_bar/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_nRF52840/xiao_nrf52840_114_voice_bar" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

#### How It Works

The sketch uses the nRF52840's PDM peripheral via the `PDM` library (bundled with Seeed nRF52 Boards) at 16 kHz, single channel. The ISR (`onPDMdata`) captures raw PDM samples into a 256-sample ring buffer and computes the peak amplitude.

The screen is divided into three zones:

<div class="table-center">
  <table align="center">
    <tr><th>Zone</th><th>Position</th><th>Description</th></tr>
    <tr><td><strong>Waveform</strong></td><td>Top (y=30–95)</td><td>27-bar equalizer visualizer. Raw samples are down-sampled and drawn as symmetric bars around a center baseline. Waveform color is driven by the same smoothed volume as the volume bar and percentage label — green (&lt;50%), yellow (50–90%), red (&gt;90%).</td></tr>
    <tr><td><strong>Percentage</strong></td><td>Middle</td><td>Large numeric volume percentage (0–100%), color-coded green (&lt;50%), yellow (50–90%), red (&gt;90%).</td></tr>
    <tr><td><strong>Volume Bar</strong></td><td>Bottom (y=130–225)</td><td>10-segment bar (green/yellow/red gradient). Updates with smoothed volume from the PDM peak.</td></tr>
  </table>
</div>

**Signal processing:**

1. **PDM ISR** — `onPDMdata()` fires at ~62 Hz (16000 / 256). It reads raw samples, computes the peak magnitude, and down-samples into 27 bins for the waveform visualizer.
2. **Normalization** — peak values below 10 are treated as silence. Values above 1500 saturate to 100%. In between, linear mapping produces a 0.0–1.0 volume level.
3. **Exponential smoothing** — the displayed volume is smoothed with a 20% mix factor (`SMOOTH = 0.20`) to avoid jitter. During silence, the volume decays at 6% per frame.
4. **Differential rendering** — the volume bar and percentage label are only redrawn when the value changes, minimizing SPI traffic.

#### Running the Demo

**Step 1.** Open `xiao_nrf52840_114_voice_bar.ino` in Arduino IDE.

**Step 2.** Select **Tools > Board > Seeed nRF52 Boards > Seeed XIAO nRF52840 Plus** and the correct **Port**.

**Step 3.** Click **Upload**.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud). You should see:

```
[MIC] ready
```

**Step 5.** Speak, clap, or blow into the microphone. The waveform and volume bar respond in real time. The percentage label changes color as the volume increases.

#### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_function_voice_bar.gif" style={{width:500, height:'auto'}}/></div>

When silent, the waveform is flat and the volume bar is empty (0%). Speak into the microphone and the equalizer bars animate while the volume bar fills up from green through yellow to red. The percentage label updates in real time.

---

## Grove I2C

The 1.14 Inch Display features a dedicated **Grove I2C connector** that exposes D4 (SDA) and D5 (SCL) on a standard 4-pin Grove socket (GND / 3V3 / SDA / SCL). Unlike the 1.47" version where D4/D5 are additionally shared with the touch controller, the 1.14" display shares D4/D5 only with the onboard IMU (it has no touch controller).

<div class="table-center">
  <table align="center">
    <tr><th>Grove Pin</th><th>XIAO Pin</th><th>Notes</th></tr>
    <tr><td>GND</td><td>GND</td><td>Common ground</td></tr>
    <tr><td>3V3</td><td>3V3</td><td>3.3V power output</td></tr>
    <tr><td>SDA</td><td>D4</td><td>I2C data — shared with onboard IMU</td></tr>
    <tr><td>SCL</td><td>D5</td><td>I2C clock — shared with onboard IMU</td></tr>
  </table>
</div>

:::note
D4/D5 are shared between the Grove connector and the onboard IMU. The IMU is at address `0x6A`. When connecting an external I2C device, make sure it does not conflict with this address.
:::

### Demo: Mech Keycap Counter

This demo turns the Grove I2C connector into a button counter using the **Grove Mech Keycap** (SKU 111020049). Press the keycap and the on-screen counter increments from 0 to 9, then wraps back to 0 with a color-coded progress bar.

**Code location:** `code/Function/114_nRF52840/xiao_nrf52840_114_counter/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/114_nRF52840/xiao_nrf52840_114_counter" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

#### Hardware Setup

Plug the Grove Mech Keycap directly into the **Grove I2C connector** on the display board. The keycap uses the following wiring:

<div class="table-center">
  <table align="center">
    <tr><th>Grove Wire</th><th>Color</th><th>XIAO Pin</th><th>Keycap Signal</th></tr>
    <tr><td>SCL</td><td>Yellow</td><td>D5</td><td>SIG (button)</td></tr>
    <tr><td>SDA</td><td>White</td><td>D4</td><td>NC (LED, not used)</td></tr>
    <tr><td>VCC</td><td>Red</td><td>3V3</td><td>Power</td></tr>
    <tr><td>GND</td><td>Black</td><td>GND</td><td>Ground</td></tr>
  </table>
</div>

:::note
Although the connector is labeled "I2C," this demo reads the keycap button through **analog voltage detection** on D5 — not through I2C communication. When pressed, the keycap pulls D5 to VCC, causing a voltage jump the ADC detects.
:::

#### How It Works

**Button detection via ADC** — the sketch samples D5 with `analogRead()` at startup to calibrate a baseline (~624 when not pressed). When the keycap is pressed, D5 connects to VCC and the ADC reading jumps to ~941. A press is registered when the ADC exceeds `baseline + 150` with a 60 ms debounce window.

**Display layout:**

<div class="table-center">
  <table align="center">
    <tr><th>Element</th><th>Description</th></tr>
    <tr><td><strong>Title</strong></td><td>"COUNTER" with "Press Mech Keycap" subtitle</td></tr>
    <tr><td><strong>Number</strong></td><td>Large centered digit (0–9), font size 8. Color transitions from green (0) through yellow to red (9) — a heat-map gradient using <code>color565(r, g, 0)</code>.</td></tr>
    <tr><td><strong>Progress bar</strong></td><td>Horizontal bar near the bottom. Filled portion grows with each press from 0/9 to 9/9, colored to match the digit.</td></tr>
    <tr><td><strong>Hint</strong></td><td>Bottom label: "press key: 0 - 9"</td></tr>
  </table>
</div>

**Counter logic:**
- `g_count` increments on each press (`0 → 1 → ... → 9 → 0`)
- `drawAll()` only redraws when the count changes (differential rendering)
- Serial monitor prints ADC, baseline, and count every 500 ms for debugging

#### Running the Demo

**Step 1.** Open `xiao_nrf52840_114_counter.ino` in Arduino IDE.

**Step 2.** Select **Tools > Board > Seeed nRF52 Boards > Seeed XIAO nRF52840 Plus** and the correct **Port**.

**Step 3.** Click **Upload**.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud). You should see:

```
[BTN] D5 base=623  threshold=773
ADC=623  base=623  max=623  cnt=0
ADC=624  base=623  max=626  cnt=0
ADC=622  base=623  max=626  cnt=0
...
```

**Step 5.** Press the Mech Keycap. The counter increments from 0 to 9 and the progress bar fills. Each press is logged to the serial monitor:

```
...
ADC=623  base=623  max=944  cnt=1
>>> PRESS! ADC=942  count=2
>>> PRESS! ADC=941  count=3
>>> PRESS! ADC=940  count=4
>>> PRESS! ADC=940  count=5
ADC=624  base=623  max=944  cnt=5
...
```

#### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/114_nRF52840Plus_function_counter.gif" style={{width:500, height:'auto'}}/></div>

The screen shows a large colored digit that increments with each keycap press. The progress bar at the bottom fills proportionally. At count 9, the next press wraps back to 0. The digit and bar color shift smoothly from green (low) to red (high).

---

## User Buttons

The 1.14 Inch Display has **three physical push buttons** connected to the XIAO nRF52840 Plus. All three buttons have external **1 KΩ pull-up resistors** on the board, so you can configure the corresponding pins as `INPUT` (no internal pull-up needed):

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Logic</th><th>Silkscreen Label</th><th>Breakout Pad</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Active-low (pressed = LOW)</td><td>USR1</td><td>U1</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Active-low (pressed = LOW)</td><td>USR2</td><td>U2</td></tr>
    <tr><td><strong>USR3</strong></td><td>D19</td><td>Active-low (pressed = LOW)</td><td>USR3</td><td>U3</td></tr>
  </table>
</div>

### Reading Buttons

With the external 1 KΩ pull-up already on the board, you can read the buttons with a simple direct read:

```cpp
const int USR1 = D6;
const int USR2 = D7;
const int USR3 = D19;

void setup() {
  // External 1K pull-up on the board — no internal pull-up needed.
  pinMode(USR1, INPUT);
  pinMode(USR2, INPUT);
  pinMode(USR3, INPUT);
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
  pinMode(D6, INPUT);
  pinMode(D7, INPUT);
  pinMode(D19, INPUT);
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
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Cycle screen brightness (100% → 75% → 50% → 25% → 100%)</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Toggle screen off / restore to last brightness</td></tr>
    <tr><td><strong>USR3</strong></td><td>D19</td><td>Toggle header title between "Hello,XIAO!" and "Seeed"</td></tr>
  </table>
</div>

The button breakout pads (labeled U1, U2, and U3 on the board) mirror D6, D7, and D19 respectively, allowing you to connect external buttons if desired.

---

## Battery Voltage Detection

The 1.14 Inch Display includes an onboard battery voltage measurement circuit connected to the XIAO nRF52840 Plus.

### nRF52840 Plus Battery Measurement

Unlike the ESP32-S3 version which uses a single ADC pin for voltage measurement only, the nRF52840 Plus uses **three GPIO pins** to form a complete battery monitoring system:

<div class="table-center">
  <table align="center">
    <tr><th>Signal</th><th>nRF52840 Pin</th><th>Function</th></tr>
    <tr><td><code>READ_BAT</code></td><td><strong>P0.14</strong></td><td>Battery voltage divider enable. Active-low — set LOW to enable the divider, then release to HIGH (high-impedance) to save power.</td></tr>
    <tr><td><code>VBAT_ADC</code></td><td><strong>PIN_VBAT</strong> (AIN7 / P0.31)</td><td>Analog input reading the divided battery voltage.</td></tr>
    <tr><td><code>CHG</code></td><td><strong>P0.17</strong></td><td>Charging status indicator. Active-low — reads LOW when a charger is connected and the battery is charging.</td></tr>
  </table>
</div>

This three-pin design gives the nRF52840 Plus several advantages over the ESP32-S3 version:
- **Battery percentage** — the known LiPo discharge curve is used to calculate a 0–100% value.
- **Charging detection** — the `~CHG` pin reports real-time charging status from the charger IC.
- **Low-power operation** — the voltage divider can be disabled via P0.14 when not sampling to save power.

### Reading Battery Voltage

```cpp
const int READ_BAT_PIN = 14;   // P0.14, active-low divider enable
const int CHG_PIN      = 17;   // P0.17, active-low charging status
const float DIVIDER_RATIO = (1000.0f + 510.0f) / 510.0f; // ≈ 2.96 (nominal; factory firmware uses 499 kΩ → ≈ 3.004)
const float ADC_FULL_SCALE = 3.6f;  // nRF52840 ADC reference
const int ADC_MAX = 4095;           // 12-bit ADC

void setup() {
  analogReadResolution(12);
  pinMode(CHG_PIN, INPUT_PULLUP);   // CHG is active-low open-drain
  Serial.begin(115200);
}

void readBattery() {
  // Enable divider (active-low): drive P0.14 LOW
  pinMode(READ_BAT_PIN, OUTPUT);
  digitalWrite(READ_BAT_PIN, LOW);
  delay(30); // let the divider settle

  // Read ADC (discard first samples for accuracy)
  for (int i = 0; i < 6; i++) { analogRead(PIN_VBAT); delay(2); }
  uint32_t sum = 0;
  for (int i = 0; i < 16; i++) { sum += analogRead(PIN_VBAT); delay(2); }

  // Disable divider: release P0.14 to high-impedance (INPUT)
  pinMode(READ_BAT_PIN, INPUT);

  uint16_t raw = sum / 16;
  float vadc = (raw * ADC_FULL_SCALE) / ADC_MAX;
  float vbat = vadc * DIVIDER_RATIO;
  bool charging = (digitalRead(CHG_PIN) == LOW); // LOW = charging

  Serial.print("VBAT: "); Serial.print(vbat);
  Serial.print("V, Charging: "); Serial.println(charging ? "Yes" : "No");
}
```

:::note
The nRF52840 Plus uses an **internal** 1 MΩ / 510 kΩ voltage divider (nominal ratio ≈ 2.96) connected to `PIN_VBAT` (P0.31). The factory firmware calibrates the low-side resistor to 499 kΩ (ratio ≈ 3.004) for a more accurate reading. This is built into the XIAO nRF52840 Plus module itself, not the display board. The P0.14 enable pin is **active-low**: drive it LOW to enable the divider, then release it to high-impedance (INPUT) to minimize quiescent current drain when the battery is not being measured.
:::

### Battery Percentage Calculation

The nRF52840 Plus converts the measured voltage to a battery percentage using a LiPo discharge lookup table:

```cpp
int voltageToPercent(float v) {
  if (v >= 4.20) return 100;
  if (v >= 4.10) return 90;
  if (v >= 4.00) return 80;
  if (v >= 3.92) return 70;
  if (v >= 3.85) return 60;
  if (v >= 3.79) return 50;
  if (v >= 3.72) return 40;
  if (v >= 3.66) return 30;
  if (v >= 3.58) return 20;
  if (v >= 3.50) return 10;
  return 0;
}
```

---

## Resources

- **[GitHub]** [XIAO Display Board Demo Code](https://github.com/Seeed-Projects/Display-Gadgets) — all Function demos are in the `code/Function/114_nRF52840/` directory
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
