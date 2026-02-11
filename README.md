# OLED I2C Demo

Short description
- Simple Arduino sketch that initializes an SSD1306 128x64 I2C OLED and prints static text. Intended for development using CLion on Windows with `arduino-cli` integration.

## Version of IDE
- IDE: CLion `2025.3.2` (Windows)

## Code overview
- Location: `src/main.cpp`
- Behavior: constructs an `Adafruit_SSD1306` object, initializes the display using the defined I2C address, prints three lines of text in `setup()`. `loop()` is a placeholder for runtime code.
- Important constants:
  - `SCREEN_WIDTH = 128`
  - `SCREEN_HEIGHT = 64`
  - `OLED_ADDRESS = 0x3C`
- Key fix: ensure `display.begin(SSD1306_SWITCHCAPVCC, OLED_ADDRESS)` is used (avoid hardcoded `12`), and use `-1` as constructor reset pin if the module lacks a reset line.

## Libraries
- `Adafruit_SSD1306`
- `Adafruit_GFX`
- `Wire`
- Arduino core for your target board (e.g. `arduino:avr` for Uno family)

## Dependencies / Tooling
- `arduino-cli` (installed and added to `%PATH%`)
- CMake (for CLion integration)
- CLion `2025.3.2` (Windows)
- Board core package for your board (install via `arduino-cli core install <core>`)

## Components & Wiring (SSD1306 I2C OLED)
- Module: SSD1306 128x64 (I2C)
- Typical wiring (Arduino Uno R4 or similar):
  - OLED VCC -> 3.3V or 5V (check module)
  - OLED GND -> GND
  - OLED SDA -> SDA (board)
  - OLED SCL -> SCL (board)
- I2C address: commonly `0x3C` (verify with an I2C scanner)
- If the module has no reset pin, construct the display object with `-1` for reset to avoid passing the address as a pin.

## Build & Upload (quick)
- Compile:
  - `arduino-cli compile --fqbn <your_board_fqbn> <path-to-sketch>`
- Upload:
  - `arduino-cli upload -p COM3 --fqbn <your_board_fqbn> <path-to-sketch>`
- CLion: add `CMakeLists.txt` with custom targets that run the above `arduino-cli` commands, then run the `arduino_compile` / `arduino_upload` targets.

## Troubleshooting
- Run an I2C scanner to confirm the OLED address.
- If `display.begin(...)` fails:
  - Check wiring (VCC/GND/SDA/SCL).
  - Ensure correct I2C address (use `OLED_ADDRESS` constant).
  - Use `-1` for reset in constructor if module lacks reset pin.
  - Confirm library versions (`Adafruit_SSD1306`, `Adafruit_GFX`).
- Serial debugging: initialize `Serial.begin(9600)` and print meaningful messages.

## Software requirements
- Windows (development machine)
- CLion `2025.3.2`
- `arduino-cli` in `%PATH%`
- CMake
- Arduino board drivers (if required)

## Hardware requirements
- Microcontroller board (e.g. Arduino Uno R4)
- SSD1306 I2C OLED 128x64 module
- USB cable for board
- Jumper wires / breadboard (if applicable)

## Author
- GitHub: `subhasini123`

## Notes
- Replace placeholders like `<your_board_fqbn>` and `COM3` with your actual board FQBN and port before building/uploading.
- Keep `OLED_ADDRESS` consistent across constructor/init calls to avoid initialization issues.
