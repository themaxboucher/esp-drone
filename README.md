## Control App

The most reliable mobile controller I found for this setup was **LiteWing**.

- [App Store](https://apps.apple.com/us/app/litewing/id6751232172)
- [Google Play](https://play.google.com/store/search?q=litewing&c=apps)

The adjustable trim allows you to correct drift during hover without modifying PID parameters.

## Firmware Setup & Flashing (macOS)

The ESP-FLY tutorial uses Windows for flashing. Below are the steps I followed to set up ESP-IDF and flash the firmware on macOS.

### 1. Install ESP-IDF

Install **ESP-IDF v5.0.7** following Espressif’s official [macOS setup instructions](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/linux-macos-setup.html).

After installation, your ESP-IDF directory path should something look like:

```
~/esp/esp-idf-v5.0.7
```

### 2. Activate ESP-IDF Environment

```bash
# Navigate to ESP-IDF directory
cd ~/esp/esp-idf-v5.0.7

# Load environment variables
source export.sh
```

### 3. Clone this Repository

```bash
git clone https://github.com/themaxboucher/esp-drone.git
cd esp-drone
```

### 3. Build the Firmware

```bash
idf.py build
```

### 4. Flash the Firmware

```bash
idf.py -p <PORT> flash monitor
```

Replace `<PORT>` with the serial device associated with the ESP32 USB connection.

To list available ports:

```bash
ls /dev/cu.*
```

Flashing uploads the compiled firmware to the ESP32 and opens a serial monitor for debugging output.

## Attribution

This project is based on the original **ESP-Fly** platform and firmware ecosystem.

### Original Project & Tutorial

- YouTube Tutorial (Max Imagination):  
  https://www.youtube.com/watch?v=V_mZsiZcy7s

- Elektor Article: _ESP-FLY – The Smallest ESP32 Drone You Can Build_  
  https://www.elektormagazine.com/labs/esp-fly-the-smallest-esp32-drone-you-can-build

### Firmware Base

- `esp-drone` open-source firmware by Espressif Systems:  
  https://github.com/espressif/esp-drone

### Flight Control Ecosystem

- Crazyflie open-source drone platform (control architecture reference):  
  https://www.bitcraze.io/crazyflie/

## License

This project inherits the GPL-3.0 license from the original `esp-drone` firmware.

See the `LICENSE` file for details.
