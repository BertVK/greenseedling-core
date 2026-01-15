# GreenSeedling Core – Scope 1 Getting Started Guide

This guide walks you through building and validating **Scope 1 of the GreenSeedling Core grow box controller**.  
It covers hardware assembly, firmware preparation, sensor calibration, and basic testing.

---

## 1. Hardware Overview

### Core Components
- Microcontroller board (ESP32 / preferred variant)
- Sensors:
  - Soil temperature
  - Soil moisture
  - Air temperature
  - Relative humidity
  - Lux sensor
  - Camera
  - DC voltage monitors (12V, 5V, 3.3V)
- Actuators:
  - Soil heating element
  - Air heater / cooler (if available)
  - Fan (PWM controlled)
  - Water pump for soil moisture
  - White grow light
- Power:
  - 220V AC input
  - 12V DC output
- Safety:
  - Visual and audible alarms
  - Water level detection

---

## 2. Wiring & Connections

1. **Microcontroller Pinout**
   - Assign GPIO pins for each sensor and actuator according to the `/docs/02_architecture/` block diagram.
   - Ensure **power rails are separated** for high-current devices.

2. **Sensors**
   - Connect soil moisture sensor with water-proof wiring into soil.
   - Connect soil temperature probe (DS18B20 or equivalent).
   - Connect air temperature & humidity sensor (DHT22/BME280 recommended).
   - Connect lux sensor facing canopy lights.
   - Connect camera module to designated microcontroller pins.

3. **Actuators**
   - Wire soil heating element through relay / solid-state switch.
   - Wire fan through PWM-enabled driver.
   - Wire water pump controlled by microcontroller, ensuring **low-level interlock from water reservoir sensor**.
   - Wire white grow light via relay / MOSFET.

4. **Power**
   - Connect AC input to your main power supply or UPS.
   - Verify 12V, 5V, 3.3V rails with a multimeter **before connecting sensors or microcontroller**.

---

## 3. Firmware Setup

1. Install development environment:
   - ESP-IDF (or Arduino IDE if using compatible board)
   - Git clone `greenseedling-core`
2. Open `/firmware` folder (or planned firmware folder structure).
3. Configure:
   - WiFi / network option
   - Initial sensor calibration values
   - Control loop parameters (PID / threshold values)
4. Compile and flash firmware to microcontroller.
5. Power up the controller.

---

## 4. Initial Calibration

1. **Sensors**
   - Soil moisture: record dry and wet readings for min/max thresholds
   - Soil temperature: check against reference thermometer
   - Air temp/humidity: compare with calibrated meter
   - Lux sensor: verify light intensity at canopy level

2. **Actuators**
   - Test each individually:
     - Soil heater responds to setpoint
     - Fan changes speed with PWM input
     - Water pump activates only when reservoir is sufficient
     - Light turns on/off as commanded

---

## 5. Safety Verification

- Check alarms:
  - Low water triggers visual and audible alarm
  - Over-temperature triggers alarm and stops heater
  - DC voltages out of range trigger alarm
- Verify state machine:
  - Controller starts in **Hold mode**
  - Alarm mode disables unsafe outputs
  - Manual override is allowed only if safe

---

## 6. Basic Operation

1. Set soil moisture and air temperature setpoints via interface (Home Assistant or Web UI).
2. Monitor live readings.
3. Activate a short test run:
   - Soil heater and pump respond to setpoints
   - Fan responds to airflow control
   - Light responds to on/off command
4. Verify timelapse camera is recording at default interval.

---

## 7. Logging & Documentation

- All sensor readings and control outputs should appear in logs.
- Record test runs in `/docs/logs/` (CSV or Home Assistant database export).
- Note any anomalies, adjustments, or calibration changes.

---

## 8. Next Steps

- Once basic Scope 1 operation is verified:
  - Document build photos and diagrams in `/docs/03_hardware/`
  - Prepare firmware configuration notes in `/docs/04_firmware/`
  - Begin preparing for **Scope 2 enhancements** (recipes, multi-channel lighting)
