---
description: Standalone function-level demos for each onboard peripheral of the 0.96 Inch Display Powered by XIAO nRF52840 Plus. Covers screen, IMU, PDM microphone, buttons, and battery.
title: Onboard Peripheral Usage
keywords:
  - XIAO
  - nRF52840
  - Display
  - LCD
  - Function
  - 0.96
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /function_0.96_inch_display_nrf52840
sku: 100063377
sidebar_label: Function
sidebar_position: 2
last_update:
  date: 08/21/2026
  author: FaiyuetCik
createdAt: '2026-08-13'
updatedAt: '2026-08-24'
url: https://wiki.seeedstudio.com/function_0.96_inch_display_nrf52840/
---

# Onboard Peripheral Usage

This page collects standalone function-level demos for each onboard peripheral of the 0.96 Inch Display. Each section is self-contained — you can pick the one that matches your use case without reading through the others.

:::note
All demos in this page require **Seeed nRF52 Boards (1.1.13)** as described in [Getting Started](/getting_started_0.96_inch_display_nrf52840). Additionally, install the following libraries.
:::

The four demos on this page use **two different graphics libraries**, so install both:

- **Library Manager** — go to **Sketch > Include Library > Manage Libraries...**, search for and install:

<div class="table-center">
  <table align="center">
    <tr><th>Library</th><th>Search Keyword</th><th>Author</th><th>Required by</th></tr>
    <tr><td><strong>GFX Library for Arduino</strong></td><td><code>GFX Library for Arduino</code></td><td>Moon On Our Nation</td><td>GraphicTest, Quicksand, Wake</td></tr>
    <tr><td><strong>Seeed Arduino LSM6DS3</strong></td><td><code>Seeed Arduino LSM6DS3</code></td><td>Seeed Studio</td><td>Quicksand, Wake</td></tr>
  </table>
</div>

- **Seeed_GFX (Manual Installation)** — only the **Flash Recorder** demo uses this library. It is not available in Library Manager and must be installed manually:

:::note
Seeed_GFX's nRF52840 processor includes `Seeed_Arduino_FS.h` when `SMOOTH_FONT` is enabled (the default). Install **Seeed Arduino FS** from the Library Manager (search "Seeed Arduino FS") or from [Seeed-Studio/Seeed_Arduino_FS](https://github.com/Seeed-Studio/Seeed_Arduino_FS) — otherwise the Flash Recorder demo fails to compile with `Seeed_Arduino_FS.h: No such file or directory`.
:::

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Studio/Seeed_GFX/archive/a2de1abca0597c202193f22d01e9fa35d1ff613b.zip" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> Download Seeed_GFX</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

**Step 1.** Click the button above to download `Seeed_GFX` as a ZIP file (pinned to a fixed commit so the tutorial stays reproducible). Alternatively, clone the repository from [Seeed-Studio/Seeed_GFX](https://github.com/Seeed-Studio/Seeed_GFX).

**Step 2.** In the Arduino IDE, go to **Sketch > Include Library > Add .ZIP Library...** and select the downloaded ZIP. The IDE reads `library.properties` and installs it into the correct `Seeed_GFX` folder automatically — you do not need to rename the extracted folder. (To install manually instead, unzip the archive and rename the extracted folder to `Seeed_GFX` before placing it in `Documents/Arduino/libraries/`.)

**Step 3.** Restart the Arduino IDE so the new library is detected.

:::tip
- **Why two graphics libraries?** The screen/IMU demos use **Arduino_GFX** (from *GFX Library for Arduino*) with software SPI, while the Flash Recorder demo uses **Seeed_GFX** (Seeed Studio's fork of TFT_eSPI). The two are different libraries and are not interchangeable.
- The nRF52840's **hardware SPI is not compatible** with this 0.96-inch ST7789 panel, so the screen demos use **software SPI**.
- The 0.96 Display has **no touch controller and no SD card slot**, so no touch or SD libraries are needed.
:::

## Getting the Demo Code

Every demo on this page lives in the [Display-Gadgets](https://github.com/Seeed-Projects/Display-Gadgets) repository. Each demo is a folder that contains the `.ino` sketch **together with a `driver.h` configuration file** — both are required to compile, so always grab the whole folder rather than copying the `.ino` source from the GitHub web view.

**Option A — Download the repository as a ZIP (recommended):**

1. Open [github.com/Seeed-Projects/Display-Gadgets](https://github.com/Seeed-Projects/Display-Gadgets) and click **Code > Download ZIP**, then extract the archive anywhere convenient.
2. Navigate into `code/Function/` and open the folder shown in each demo's **Code location** line. For example, the GraphicTest demo for this board lives in `code/Function/096_nRF52840/xiao_nrf52840_096_graphictest/`.
3. **Double-click the `.ino` file** to open it in the Arduino IDE. Keep the `.ino` and `driver.h` together in the same folder — the IDE relies on them being side-by-side.

**Option B — git clone:**

```sh
git clone https://github.com/Seeed-Projects/Display-Gadgets.git
```

Then open the demo's `.ino` file from the cloned `code/Function/...` folder.

## Screen Display — GraphicTest

This demo runs a full graphics benchmark on the 0.96-inch ST7789 IPS panel (80×160), covering color bars, lines, rectangles, circles, triangles, rounded rectangles, text, and a pixel gradient. Use it to verify that the screen is wired correctly and that all draw calls work as expected.

**Code location:** `code/Function/096_nRF52840/xiao_nrf52840_096_graphictest/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/096_nRF52840/xiao_nrf52840_096_graphictest" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The sketch initializes the ST7789 IPS panel via Arduino_GFX using **software SPI**, then runs through ten graphics primitives in sequence, measuring the execution time of each one via `micros()` and printing the result to the serial monitor.

The key LCD configuration:

- **Chip select:** D2
- **Data/command:** D3
- **SPI clock:** D8
- **SPI data (MOSI):** D10
- **Reset:** D17
- **Backlight:** D18 (PWM-capable)

The ST7789 panel is initialized with `rotation = 2`, `invertDisplay(true)`, and a column offset of 24 (`col_offset = 24`, `row_offset = 0`). Because hardware SPI is incompatible with this panel, all draws go through `Arduino_SWSPI`.

:::note
**Color order (BGR panel).** This 0.96-inch panel physically swaps the red and blue channels. The demo aliases colors accordingly (e.g. a wire-level red `0xF800` appears blue on screen). If you write your own drawing code, use the demo's color aliases or account for the BGR order — otherwise reds and blues will appear swapped.
:::

### Running the Demo

**Step 1.** Open `xiao_nrf52840_096_graphictest.ino` in Arduino IDE.

**Step 2.** Select **Tools > Board > Seeed nRF52 Boards > Seeed XIAO nRF52840 Plus** and the correct **Port**.

**Step 3.** Click **Upload**.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud). You should see timing output for each test:

```
=== XIAO nRF52840 Plus 0.96 graphic test ===
LCD: 80x160
Color bars: 284.18 ms
Lines: 1220.70 ms
Fast lines: 331.05 ms
Rectangles: 263.67 ms
Filled rects: 834.96 ms
Circles: 356.45 ms
Triangles: 440.43 ms
Round rects: 302.73 ms
Text: 297.85 ms
Pixel gradient: 1388.67 ms
Graphic test finished.
```

On the screen, you will see each test pattern displayed for about one second before the next one starts. When all tests complete, a "Done! All tests OK" screen appears.

### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_nRF52840Plus_function_graphictest.gif" style={{width:500, height:'auto'}}/></div>

After the sketch runs through all patterns, the screen shows a "Done!" message. Reset the board to run the test again.

---

## IMU

The 0.96 Inch Display features an onboard 6-axis IMU (**LSM6DS3**) connected via I2C on D4/D5. The motion interrupt line on **D14** supports hardware wake-up and gesture detection.

Both demos below use the LSM6DS3 at I2C address **0x6A**.

<a id="imu-quicksand"></a>

### Demo 1: Electronic Quicksand

This demo turns the screen into an interactive fluid simulation — golden sand particles that flow and settle according to gravity, as measured by the onboard 6-axis IMU. Tilt the board and the sand shifts direction in real time.

**Code location:** `code/Function/096_nRF52840/xiao_nrf52840_096_electronic_quicksand/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/096_nRF52840/xiao_nrf52840_096_electronic_quicksand" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### How It Works

The simulation uses a **13×26 occupancy grid** overlaid on the 80×160 screen, where each cell is 6×6 pixels. Around **65 particles** are placed in the grid, each with a position, velocity, and a golden color gradient.

The IMU is read via I2C (D4/D5) using the Seeed Arduino LSM6DS3 library at address `0x6A`. Raw acceleration values are low-pass filtered and used to derive a gravity vector. When you tilt the board:

1. **Gravity vector updates** — accelerometer data is smoothed with an exponential moving average to avoid jitter.
2. **Particle velocity** — each particle accelerates in the direction of the gravity vector, with damping and a per-particle mobility factor based on its depth in the flow.
3. **Cell occupancy** — particles deeper in the flow (closer to the "bottom" relative to gravity) have reduced mobility, creating a realistic packing effect.
4. **Differential rendering** — only cells where particles moved into or out of are redrawn, minimizing SPI traffic and keeping the animation smooth on the small panel.

Particles near the surface flow freely (higher mobility); particles buried deeper pack tightly (lower mobility) — mimicking how real sand behaves.

### Running the Demo

**Step 1.** Open `xiao_nrf52840_096_electronic_quicksand.ino` in Arduino IDE.

**Step 2.** Select the board and port, then click **Upload**.

**Step 3.** Once uploaded, the screen fills with golden particles at the bottom. Tilt the board in different directions — the sand flows as if pulled by gravity.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud) to confirm initialization:

```
LCD w=80 h=160
=== Electronic Quicksand 0.96 ===
imu.begin=0
```

### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_nRF52840Plus_function_quicksand.gif" style={{width:500, height:'auto'}}/></div>

The golden sand particles flow smoothly as you tilt the board. When held flat, the sand settles at the bottom of the screen. Rotate the board 90 degrees and the sand flows to the new "bottom" within a second.

---

### Demo 2: Raise to Wake

This demo implements a **screen sleep/wake system** driven by the IMU's built-in motion interrupt on **D14**. The screen automatically turns off (backlight off + nRF52 system ON sleep) after a configurable idle period, and wakes instantly when you pick up or move the device.

**Code location:** `code/Function/096_nRF52840/xiao_nrf52840_096_wakeup/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/096_nRF52840/xiao_nrf52840_096_wakeup" target="_blank" rel="noopener noreferrer">
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
    <tr><td><code>CTRL3_C</code></td><td><code>0x44</code></td><td>Block data update (BDU) + auto-increment</td></tr>
    <tr><td><code>CTRL1_XL</code></td><td><code>0x40</code></td><td>Accelerometer @ 104 Hz, ±2g</td></tr>
    <tr><td><code>TAP_CFG</code></td><td><code>0x80</code></td><td>Enable embedded interrupts</td></tr>
    <tr><td><code>WAKE_UP_THS</code></td><td><code>0x05</code></td><td>Wake-up threshold (medium-low sensitivity)</td></tr>
    <tr><td><code>WAKE_UP_DUR</code></td><td><code>0x00</code></td><td>No duration filter (responsive wake)</td></tr>
    <tr><td><code>MD1_CFG</code></td><td><code>0x20</code></td><td>Route wake-up to INT1</td></tr>
  </table>
</div>

**Sleep/wake flow:**

1. **Active state** — screen is on, backlight at full brightness, UI refreshes every 250 ms with real-time IMU data.
2. **Auto-sleep** — after 8 seconds of inactivity, the sketch turns off the backlight, displays a "Sleep — Move to wake" message, and enters nRF52 System ON sleep (low-power mode with RAM retention). The IMU wake interrupt on D14 was already configured at startup, so motion detection remains active during sleep.
3. **Wake-up** — when the user picks up the board, the IMU detects motion and asserts D14 HIGH. The nRF52840 exits System ON sleep, turns the backlight back on, and redraws the UI — the LCD and IMU keep their state because System ON sleep retains RAM.

**Manual test buttons:**

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td>USR1</td><td>D6</td><td>Force sleep</td></tr>
    <tr><td>USR2</td><td>D7</td><td>Force wake</td></tr>
  </table>
</div>

### Running the Demo

**Step 1.** Open `xiao_nrf52840_096_wakeup.ino` in Arduino IDE, select the board and port, and click **Upload**.

**Step 2.** The screen shows a compact dashboard with power state, motion data, and a countdown. Let the board sit still — it will automatically enter sleep after 8 seconds.

**Step 3.** Pick up the board or shake it gently — the screen wakes immediately.

**Step 4.** Open **Tools > Serial Monitor** (115200 baud) to observe the boot and sleep/wake transitions:

```
=== XIAO nRF52840 Plus 0.96 IMU Wake Demo ===
[LCD] OK 0.96 ST7789 80x160
[IMU] LSM6DS3 begin=0
[IMU] CTRL1_XL    = 0x40
[IMU] TAP_CFG     = 0x80
[IMU] MD1_CFG     = 0x20
[IMU] WAKE_UP_THS = 0x05
[IMU] D14 wake interrupt OK
[IMU] D14 pin state = 0
[BOOT] done. Screen should be on.
[SLEEP] screen off, entering System ON sleep
[SLEEP] loops=1 D14=0 awake=N
[SLEEP] loops=1025 D14=0 awake=N
[WAKE] D14 pin HIGH (polled)
[WAKE] src=0xA
[WAKE] reason=IMU_D14 wakeCount=8 sleptMs=4142 sleepLoops=1936 wakeSrc=0xA
[WAKE] src=0x0
```

The `sleptMs`, `sleepLoops`, and `wakeSrc` fields vary depending on how long the board slept and what gesture triggered the wake.

### Expected Result

<div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_nRF52840Plus_function_wakeup.gif" style={{width:500, height:'auto'}}/></div>

The screen displays real-time motion data while awake. After 8 seconds of stillness, the screen goes dark and the nRF52840 enters low-power sleep. Pick up the device and the screen restores instantly, with the wake counter incremented.

---

## Microphone & Audio — Flash Recorder

This demo turns the 0.96 Inch Display into a tiny voice recorder. Press USR1 to capture a short clip from the onboard PDM microphone into the nRF52840's internal flash filesystem, then press USR2 to play it back through an external I2S amplifier.

The 0.96 Display's PDM microphone connects to the same pins as the other XIAO display boards:

<div class="table-center">
  <table align="center">
    <tr><th>Pin</th><th>Signal</th><th>Function</th></tr>
    <tr><td>D0</td><td>PDM_CLK</td><td>PDM clock output to microphone</td></tr>
    <tr><td>D1</td><td>PDM_DATA</td><td>PDM data input from microphone</td></tr>
  </table>
</div>

**Code location:** `code/Function/096_nRF52840/xiao_nrf52840_096_flash_record/`

<div class="github_container" style={{textAlign: 'center'}}>
    <a class="github_item" href="https://github.com/Seeed-Projects/Display-Gadgets/tree/main/code/Function/096_nRF52840/xiao_nrf52840_096_flash_record" target="_blank" rel="noopener noreferrer">
    <strong><span><font color={'FFFFFF'} size={"4"}> View on GitHub</font></span></strong>
    <svg aria-hidden="true" focusable="false" role="img" className="mr-2" viewBox="-3 10 9 1" width={16} height={16} fill="currentColor" style={{textAlign: 'center', display: 'inline-block', userSelect: 'none', verticalAlign: 'text-bottom', overflow: 'visible'}}><path d="M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.12 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1.28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.46.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.53.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z" /></svg>
    </a>
</div><br />

### Hardware Setup

The playback side needs an external I2S amplifier. The demo is written for the **MAX98357A** breakout, wired to the 0.96 Display's I2S test pads:

<div class="table-center">
  <table align="center">
    <tr><th>XIAO Pin</th><th>I2S Signal</th><th>MAX98357A</th></tr>
    <tr><td>D11</td><td>I2S_SD (data out)</td><td>DIN</td></tr>
    <tr><td>D12</td><td>I2S_SCK (bit clock)</td><td>BCLK</td></tr>
    <tr><td>D13</td><td>I2S_WS (word select)</td><td>LRC</td></tr>
  </table>
</div>

:::note
The 0.96 Display does **not** have an SD card slot, so this demo records into the nRF52840's **internal flash filesystem** (InternalFS) instead. InternalFS is only about 28 KB, which limits the clip to ~1.4 seconds at 8 kHz — shorter than the ESP32-S3 versions, whose LittleFS is much larger.
:::

### How It Works

**Recording (USR1):**

1. The sketch starts the PDM peripheral at **8 kHz, single channel** and captures raw samples into a 11200-sample buffer (≈ 1.4 s, ≈ 22 KB of PCM) through an ISR (`onPdmData`).
2. A progress screen shows the recording percentage and elapsed time in real time.
3. When the buffer is full, the sketch prepends a 44-byte WAV header and writes the file `/REC_RAW.WAV` to InternalFS.

**Playback (USR2):**

1. The WAV is loaded back from InternalFS.
2. The sketch drives the nRF52840's I2S peripheral in **master mode** with a 64× ratio (≈ 8 kHz LRCK), sending 16-bit stereo frames to the MAX98357A at **0.75× gain** (each mono sample is duplicated to both channels).
3. A double-buffer (ping-pong) scheme keeps the audio stream uninterrupted until the clip ends.

**Buttons:**

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td>USR1</td><td>D6</td><td>Record a new clip (overwrites the previous one)</td></tr>
    <tr><td>USR2</td><td>D7</td><td>Play back the saved clip</td></tr>
  </table>
</div>

### Running the Demo

**Step 1.** Open `xiao_nrf52840_096_flash_record.ino` in Arduino IDE.

**Step 2.** Select **Tools > Board > Seeed nRF52 Boards > Seeed XIAO nRF52840 Plus** and the correct **Port**.

**Step 3.** Click **Upload**.

**Step 4.** The screen shows the "Recorder" idle screen. Press **USR1** — a red "REC" progress bar fills as it records. When done, it saves the WAV and returns to the idle screen.

**Step 5.** Press **USR2** — the clip plays through the connected MAX98357A speaker, with the screen showing "Playing...".

### Expected Result

<!-- TODO: Add flash_record GIF -->
<!-- <div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/Display_Gadgets/imgs/096_nRF52840Plus_function_flash_record.gif" style={{width:500, height:'auto'}}/></div> -->

After pressing USR1, the red progress bar fills to 100% and the clip is saved. Pressing USR2 plays the recording back through the MAX98357A. Recording again with USR1 overwrites the previous clip. The recording is lost when the board is reset.

---

## User Buttons

The 0.96 Inch Display has **two physical push buttons** connected to the XIAO nRF52840 Plus:

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Logic</th><th>Silkscreen Label</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Active-low (pressed = LOW)</td><td>USR1</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Active-low (pressed = LOW)</td><td>USR2</td></tr>
  </table>
</div>

:::note
Unlike the 1.14 Inch Display, the 0.96 Display has **no third button** (no USR3 on D19). It also has no dedicated button breakout pads.
:::

### Reading Buttons

The onboard demos configure the buttons with the internal pull-up:

```cpp
const int USR1 = D6;
const int USR2 = D7;

void setup() {
  pinMode(USR1, INPUT_PULLUP);
  pinMode(USR2, INPUT_PULLUP);
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
}
```

### Debounce with Interrupts

For responsive, debounced button handling without blocking the main loop, you can use pin-change interrupts:

```cpp
volatile bool btn1Flag = false;
volatile bool btn2Flag = false;

void btn1Isr() { btn1Flag = true; }
void btn2Isr() { btn2Flag = true; }

void setup() {
  pinMode(D6, INPUT_PULLUP);
  pinMode(D7, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(D6), btn1Isr, FALLING);
  attachInterrupt(digitalPinToInterrupt(D7), btn2Isr, FALLING);
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
}
```

### Default Behavior in the Factory Dashboard

In the preloaded factory firmware, the buttons are mapped as follows (you can override these in your own code):

<div class="table-center">
  <table align="center">
    <tr><th>Button</th><th>Pin</th><th>Action</th></tr>
    <tr><td><strong>USR1</strong></td><td>D6</td><td>Cycle screen brightness (100% → 75% → 50% → 25% → 100%)</td></tr>
    <tr><td><strong>USR2</strong></td><td>D7</td><td>Toggle screen backlight ON/OFF</td></tr>
  </table>
</div>

When the screen is off (toggled via USR2), pressing USR2 again restores it to the previous non-zero level.

---

## Battery Voltage Detection

The 0.96 Inch Display relies on the XIAO nRF52840 Plus module's built-in battery monitoring. There is **no dedicated battery ADC pin on the display board** (D16 is NC) — battery voltage is measured through the module's internal divider.

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
#include <nrf.h>

const int READ_BAT_PIN = 14;   // P0.14, active-low divider enable
const int CHG_PIN      = 17;   // P0.17, active-low charging status
const float DIVIDER_RATIO = (1000.0f + 510.0f) / 510.0f; // ≈ 2.96 (nominal; factory firmware uses 499 kΩ → ≈ 3.004)
const float ADC_FULL_SCALE = 3.6f;  // nRF52840 ADC reference
const int ADC_MAX = 4095;           // 12-bit ADC

void setup() {
  analogReadResolution(12);

  // Configure CHG as an input with internal pull-up (active-low open-drain).
  nrf_gpio_cfg_input(CHG_PIN, NRF_GPIO_PIN_PULLUP);

  // Release the divider enable pin to high-impedance when not measuring.
  NRF_P0->DIRCLR = (1UL << READ_BAT_PIN);

  Serial.begin(115200);
}

void readBattery() {
  // Enable the divider (active-low): drive P0.14 LOW.
  NRF_P0->OUTCLR = (1UL << READ_BAT_PIN);
  NRF_P0->DIRSET = (1UL << READ_BAT_PIN);
  delay(30); // let the divider settle

  // Read ADC (discard first samples for accuracy)
  for (int i = 0; i < 6; i++) { analogRead(PIN_VBAT); delay(2); }
  uint32_t sum = 0;
  for (int i = 0; i < 16; i++) { sum += analogRead(PIN_VBAT); delay(2); }

  // Disable divider: release P0.14 to high-impedance.
  NRF_P0->DIRCLR = (1UL << READ_BAT_PIN);

  uint16_t raw = sum / 16;
  float vadc = (raw * ADC_FULL_SCALE) / ADC_MAX;
  float vbat = vadc * DIVIDER_RATIO;
  bool charging = (NRF_P0->IN & (1UL << CHG_PIN)) == 0; // LOW = charging

  Serial.print("VBAT: "); Serial.print(vbat);
  Serial.print("V, Charging: "); Serial.println(charging ? "Yes" : "No");
}
```

:::note
The `~CHG` pin is read through the nRF52840's **raw GPIO registers** (`nrf_gpio_cfg_input()` and `NRF_P0->IN`) instead of `digitalRead()`. In the Arduino API, pin numbers follow the board package's mapping, where `digitalRead(17)` actually reads **P0.07** (the 6D IMU's I2C data line) rather than P0.17. The constants `14` and `17` here are **raw Nordic P0.x pin numbers** (P0.14 and P0.17), which is exactly what the register calls expect.
:::

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

- **[GitHub]** [XIAO Display Board Demo Code](https://github.com/Seeed-Projects/Display-Gadgets) — all Function demos are in the `code/Function/096_nRF52840/` directory
- **[PDF]** [Schematic — 0.96 Inch Display (XIAO nRF52840 Plus)](https://github.com/Seeed-Projects/Display-Gadgets/tree/main/schematics/0.96_Inch_Display_Powered_by_XIAO_nRF52840_Plus/Schematic)

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
