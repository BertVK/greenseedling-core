# GreenSeedling Core – Scope 1 (V1) Specification

## Purpose

Scope 1 delivers a **fully functional, safe, and documented grow box controller**.  
It is designed to be **shipped as a physical product** and serve as the basis for later upgrades.

---

## 1. Observability

### Environmental
- Air temperature
- Relative air humidity
- Light intensity (lux)
- Camera (live view + basic timelapse)

### Soil & Water (Closed Loop)
- Soil temperature
- **Soil moisture**
- **Water reservoir level**

### Power & System
- 220V AC input presence
- 12V / 5V / 3.3V DC rail voltages

---

## 2. Control Loops

### Climate
- Air heating
- Air cooling
- Fan airflow control (PWM)

### Soil & Water
- Soil heating
- **Water pump for soil moisture**
  - Automatically controlled to reach soil moisture setpoint
  - **Pump disabled if water reservoir is low**
- Closed-loop feedback ensures safe operation at all times

### Lighting
- White grow light (single channel)

---

## 3. Safety & Alarms

### Environmental
- Air temperature out-of-range
- Soil temperature out-of-range

### Soil & Water
- Low water reservoir level
- Pump inhibited on low water

### Electrical & Mechanical
- DC voltage out-of-range
- Fan RPM failure
- Light failure (lux feedback)

### Alerts
- Visual alarm
- Audible alarm

---

## 4. User Interface

- **Primary interface** (choose one):  
  - Home Assistant integration  
  - Web UI served by controller

### Screens
- Live overview of all measurements
- Manual setpoints:
  - Air temperature
  - Soil temperature
  - Soil moisture
- Alarm overview
- Camera view & timelapse

---

## 5. Logging

- Measurements logging
- Control output logging
- Event logging (alarms, state transitions)

---

## 6. Documentation & Versioning

- All future changes must be **tracked in Git**
- Feature additions outside Scope 1 must be clearly marked as Scope 2 or higher
- Control loops and alarms must always be **validated before firmware release**
- Recipes and automation features are **not included in Scope 1**

---

## 7. Next Steps

- Implement initial hardware prototype according to Scope 1
- Validate sensor readings and control loops
- Document build process, wiring, BOM, and calibration steps
- Begin firmware development for Scope 1 functionality
