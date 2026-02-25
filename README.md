# ESP32 WiFi Micro Drone

**"Bumble Bee"** 🐝 is a palm-sized ESP32-based WiFi quadcopter built on the ESP-Fly platform and powered by the Espressif [`esp-drone`](https://github.com/espressif/esp-drone) firmware.

![IMG_5006](https://github.com/user-attachments/assets/64b22a95-8172-48ec-a266-67a1b20c1d60)

This project involved:

- 🔬 Assembling and soldering a complete micro quadcopter platform
- 💻 Building and flashing firmware using ESP-IDF
- 😩 Debugging hardware and firmware integration issues
- 🎮 Configuring and validating WiFi flight control

## 🔧 Hardware

**Core Components:**

- **Seeed Studio XIAO ESP32-S3** — main flight controller (WiFi + processing)
- **Custom PCB** — integrates the MPU6050 IMU and MOSFET motor drivers
- **4x brushed coreless motors** — driven directly from the onboard MOSFETs
- **LiPo battery (220 mAh)** — onboard power source
- **3D printed frame** — supports motors and electronics

![IMG_4997](https://github.com/user-attachments/assets/68ece96f-53ce-48f2-b10c-7a918c23d1ee)

## 💻 Firmware

The firmware is based on the open-source `esp-drone` project from Espressif Systems.

It includes:

- Real-time flight control loop  
- Sensor fusion from IMU  
- PID stabilization control  
- WiFi command interface  
- PWM motor signal generation  
- FreeRTOS-based task scheduling  

## 📱 Control App

The most reliable mobile controller I found for this setup was **LiteWing**.

- [App Store](https://apps.apple.com/us/app/litewing/id6751232172)
- [Google Play](https://play.google.com/store/search?q=litewing&c=apps)

It connects directly to the ESP32 over WiFi and provides stable throttle and attitude control. The feature that made a big difference was **adjustable trim**. This allowed correction of small drift during hover without modifying PID parameters.

## 🛠 Firmware Setup & Flashing (macOS)

The ESP-FLY tutorial focuses on Windows for flashing. Below are the steps I followed to set up ESP-IDF and flash the firmware on macOS.

### 1️⃣ Install ESP-IDF

Install **ESP-IDF v5.0.7** following Espressif’s official [macOS setup instructions](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/linux-macos-setup.html).

After installation, your ESP-IDF directory path should something look like:

```
~/esp/esp-idf-v5.0.7
```

### 2️⃣ Activate ESP-IDF Environment

```bash
# Navigate to ESP-IDF directory
cd ~/esp/esp-idf-v5.0.7

# Load environment variables
source export.sh
```


### 3️⃣ Clone this Repository

```bash
git clone https://github.com/themaxboucher/esp-drone.git
cd esp-drone
```


### 4️⃣ Build the Firmware

```bash
idf.py build
```


### 5️⃣ Flash the Firmware

```bash
idf.py -p <PORT> flash monitor
```

Replace `<PORT>` with the serial device associated with the ESP32 USB connection.

To list available ports:

```bash
ls /dev/cu.*
```

Flashing uploads the compiled firmware to the ESP32 and opens a serial monitor for debugging output.


## 🙏 Attribution

This project is based on the original **ESP-Fly** platform and firmware ecosystem.

### Original Project & Tutorial
- 🎥 YouTube Tutorial (Max Imagination):  
  https://www.youtube.com/watch?v=V_mZsiZcy7s

- 📖 Elektor Article: *ESP-FLY – The Smallest ESP32 Drone You Can Build*  
  https://www.elektormagazine.com/labs/esp-fly-the-smallest-esp32-drone-you-can-build

### Firmware Base
- 🧠 `esp-drone` open-source firmware by Espressif Systems:  
  https://github.com/espressif/esp-drone

### Flight Control Ecosystem
- 🚁 Crazyflie open-source drone platform (control architecture reference):  
  https://www.bitcraze.io/crazyflie/

---

This repository documents the hardware assembly, firmware configuration (macOS ESP-IDF environment), system tuning, and validation work built on top of these open-source resources.

## 📜 License

This project inherits the GPL-3.0 license from the original `esp-drone` firmware.

See the `LICENSE` file for details.

