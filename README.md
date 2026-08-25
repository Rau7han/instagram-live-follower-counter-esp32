# Instagram Live Follower Counter (ESP32 + WS2812B)

A real-time Instagram follower counter built with **ESP32** and a **32x8 WS2812B LED matrix**.

![Project preview](https://github.com/user-attachments/assets/20576f80-a876-407c-a6e4-d360d134c9aa)

## Features
- Live polling from Instagram Graph API (`followers_count`)
- Animated mechanical-style digit rolling
- 2 / 4 / 6 digit layout transitions based on follower count
- Startup animation and catch-up logic for count changes
- WiFi reconnect handling with retry intervals
- Config template to keep credentials out of git history

## Repository Structure
- `/instagram_live_follower_counter_esp32.ino` → main ESP32 firmware
- `/Config.h.example` → copy to `Config.h` and set your credentials

## Hardware
- ESP32 dev board
- WS2812B matrix (32x8 / 256 LEDs)
- 5V external power supply (sized for LED current)
- Common GND between ESP32 and LED supply

## Wiring
- **LED data pin** → ESP32 GPIO **13**
- **LED VCC** → 5V power supply
- **LED GND** → power supply GND + ESP32 GND

## Setup
1. Open this project in Arduino IDE.
2. Install required libraries:
   - **FastLED**
   - ESP32 board package
3. Copy config template:
   - `Config.h.example` → `Config.h`
4. Edit `Config.h`:
   - `CFG_WIFI_SSID`
   - `CFG_WIFI_PASSWORD`
   - `CFG_INSTAGRAM_ACCESS_TOKEN`
5. Select your ESP32 board and COM port.
6. Upload firmware.

## Instagram Token Notes
- Use an access token that works with:
  - `https://graph.instagram.com/me?fields=followers_count&access_token=YOUR_TOKEN`
- If token is not configured, firmware will skip Instagram polling and print a serial warning.

## Runtime Behavior
- On first valid API response, display initializes with a startup flip animation.
- Device keeps polling Instagram in the background even while display animations run.
- Poll interval and retry interval can be tuned inside the firmware constants.

## Important
- Never commit real credentials.
- Keep `Config.h` local (already ignored by `.gitignore`).
