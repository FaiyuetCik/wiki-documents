---
description: Overview and comparison of the XIAO Display Gadgets series.
title: XIAO Display Gadgets Series
keywords:
  - XIAO
  - Display
  - LCD
  - ESP32-S3
  - nRF52840
image: https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png
slug: /display_gadgets
sidebar_label: Overview
sidebar_position: 0
last_update:
  date: 08/31/2026
  author: FaiyuetCik
createdAt: '2026-08-31'
updatedAt: '2026-08-31'
url: https://wiki.seeedstudio.com/display_gadgets/
---

# XIAO Display Gadgets Series

<div class="table-center">
  <table align="center">
    <tr><th>XIAO Display Gadgets Series</th></tr>
    <!-- TODO: Replace with actual series hero image -->
    <tr><td><div style={{textAlign:'center'}}><img src="https://files.seeedstudio.com/wiki/seeed_logo/logo_2023.png" style={{width:100, height:'auto'}}/></div></td></tr>
    <tr><td><div class="get_one_now_container" style={{textAlign: 'center'}}>
        <a class="get_one_now_item" href="#" target="_blank">
            <strong><span><font color={'FFFFFF'} size={"4"}> Get One Now 🖱️</font></span></strong>
        </a>
    </div></td></tr>
  </table>
</div>

## Introduction

The XIAO Display Gadgets series is a family of compact expansion boards that pair a Seeed Studio XIAO main controller with a small color LCD. Six models are available across three screen sizes — 0.96", 1.14", and 1.47" — and two XIAO controllers — the XIAO nRF52840 Plus and the XIAO ESP32-S3 Plus — ranging from a pocket-friendly 80×160 display to a 172×320 capacitive-touch display with MicroSD storage.

## Product Comparison

| Model | Size | Controller | Resolution | Touch | MicroSD | Buttons | Current (Dashboard) | SKU |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [1.47" Touch Display (nRF52840)](/getting_started_1.47_inch_touch_display_nrf52840) | 1.47" | nRF52840 | 172×320 | ✓ | ✓ | 2 | TODO | 100004242 |
| [1.47" Touch Display (ESP32-S3)](/getting_started_1.47_inch_touch_display_esp32s3) | 1.47" | ESP32-S3 | 172×320 | ✓ | ✓ | 2 | TODO | 100069905 |
| [1.14" Display (nRF52840)](/getting_started_1.14_inch_display_nrf52840) | 1.14" | nRF52840 | 135×240 | — | — | 3 | TODO | 100069374 |
| [1.14" Display (ESP32-S3)](/getting_started_1.14_inch_display_esp32s3) | 1.14" | ESP32-S3 | 135×240 | — | — | 3 | TODO | 100086099 |
| [0.96" Display (nRF52840)](/getting_started_0.96_inch_display_nrf52840) | 0.96" | nRF52840 | 80×160 | — | — | 2 | TODO | 100063377 |
| [0.96" Display (ESP32-S3)](/getting_started_0.96_inch_display_esp32s3) | 0.96" | ESP32-S3 | 80×160 | — | — | 2 | TODO | 100037468 |

*Current is measured while running the Dashboard firmware (unit: mA); values are pending measurement.*

## How to Choose

- **1.47" Touch Display** — choose this if you need a capacitive touchscreen and MicroSD storage, for example for photo frames, SD audio recording, or touch-driven HMI interfaces.
- **1.14" Display** — a mid-size screen with three user buttons and a Grove I2C connector, a good balance between compactness and expandability.
- **0.96" Display** — the smallest form factor, ideal for wearables and space-constrained designs.
- **Controller** — pick the ESP32-S3 variant when you need Wi-Fi and Bluetooth connectivity; pick the nRF52840 variant for a low-power BLE-focused design.

## Shared Features

All six models share the following onboard peripherals:

- PDM digital microphone
- 6-axis IMU (LSM6DS3, 3-axis accelerometer + 3-axis gyroscope)
- Battery voltage detection
- Arduino support (GFX Library for Arduino on all models; Seeed_GFX on the 1.14" and 1.47" Function demos only)

## Getting Started

Each model has its own Getting Started guide and Function reference. Choose a model from the comparison table above to jump to its documentation.
