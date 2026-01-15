
# GreenSeedling Core – Scope 1 Architecture

This document provides a complete **architecture overview for Scope 1** of the GreenSeedling Core grow box controller.  
It defines **subsystems, control loops, sensor-actuator relationships, data flow, wiring, safety interlocks, and state machine**.

---

## 1. System Overview

**Scope 1 Subsystems:**

| Subsystem               | Purpose |
|-------------------------|---------|
| Microcontroller         | Core processing and control |
| Power Monitoring        | 220V AC input, 12V/5V/3.3V DC rails |
| Environmental Sensors   | Air temperature, relative humidity, lux sensor |
| Soil & Water Sensors    | Soil temperature, soil moisture, water reservoir level |
| Actuators               | Soil heating, air heating/cooling, fan, water pump, white grow light |
| Camera                  | Live view and timelapse recording |
| Safety & Alarms         | Visual and audible alarms, interlocks |
| User Interface          | Home Assistant integration or web UI |
| Logging                 | Measurement and event logging for all sensors and control outputs |

---

## 2. Control Loop Diagram

**Mermaid diagram (render locally in VS Code or other Markdown editor with Mermaid plugin):**

\`\`\`mermaid
graph TD
  %% Sensors
  SoilTemp[Soil Temperature Sensor]
  SoilMoist[Soil Moisture Sensor]
  AirTemp[Air Temperature Sensor]
  AirRH[Relative Humidity Sensor]
  Lux[Lux Sensor]
  WaterLevel[Water Reservoir Level]
  FanRPM[Fan RPM Sensor]

  %% Controllers
  SoilTempCtrl[Soil Temperature Controller]
  SoilMoistCtrl[Soil Moisture Controller]
  AirTempCtrl[Air Temperature Controller]
  AirRHCtrl[Air Humidity Controller]
  LightCtrl[Light Controller]
  FanCtrl[Fan Controller]

  %% Actuators
  SoilHeater[Soil Heater]
  WaterPump[Water Pump]
  AirHeater[Air Heater]
  AirCooler[Air Cooler]
  Atomizer[Air Moisture Atomizer]
  WhiteLight[White Grow Light]
  Fan[Fan]

  %% Control Loops
  SoilTemp --> SoilTempCtrl --> SoilHeater
  SoilMoist --> SoilMoistCtrl --> WaterPump
  AirTemp --> AirTempCtrl --> AirHeater
  AirTemp --> AirTempCtrl --> AirCooler
  AirRH --> AirRHCtrl --> Atomizer
  Lux --> LightCtrl --> WhiteLight
  FanRPM --> FanCtrl --> Fan

  %% Safety Interlocks
  WaterLevel -.-> WaterPump
\`\`\`

---

## 3. System Architecture / Data Flow

\`\`\`mermaid
graph LR
  Sensors[Environmental & Soil Sensors] --> MCU[Microcontroller]
  MCU --> Actuators[Soil Heater, Water Pump, Fan, Light, Atomizer]
  MCU --> Logs[Measurement & Event Logging]
  MCU --> UI[Home Assistant / Web UI]
  UI --> User[Grower / Operator]
  MCU --> Camera[Camera Module]
  Camera --> UI
  MCU --> Safety[State Machine & Alarms]
  Safety --> Actuators
  Safety --> UI
\`\`\`

---

## 4. Wiring & Connectivity (Scope 1)

- AC input → DC power supply → MCU & actuators
- Shielded cables for sensors
- Relays/MOSFETs for high-current actuators
- Safety interlocks: pump disabled on low water, heater disabled on over-temp
- Camera connection to MCU

> **Placeholder:** Add actual wiring diagrams and GPIO assignments here (Mermaid or PNG/SVG).

---

## 5. Safety Interlocks & State Machine

| State | Description |
|-------|-------------|
| HOLD  | Controller idle; no actuators active |
| RUN   | Normal operation; control loops active |
| ALARM | Unsafe condition detected; all actuators disabled |
| STOP  | Manual stop; safe state enforced |

**Rules:**  
- Start in **HOLD** mode  
- **ALARM** disables all outputs  
- Manual override only if safe  
- Full recovery requires confirmation  

---

## 6. Documentation Notes

- Track wiring changes, calibration offsets, and control loop tuning  
- Include images/screenshots for wiring, sensors, actuators, and camera setup  
- Future Scope 2+ enhancements will extend this architecture  

---

## 7. Next Steps

1. Replace ASCII/placeholders with proper diagrams  
2. Define PID/threshold parameters for controllers  
3. Add GPIO assignments for all sensors/actuators  
4. Add camera wiring & timelapse setup  
5. Keep architecture synced with Scope 1 build guide
