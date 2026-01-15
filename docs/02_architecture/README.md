# GreenSeedling Core – Architecture Overview

This document provides a high-level view of the **Scope 1 architecture** for the GreenSeedling Core grow box controller.  
It defines **subsystems, control loops, sensor-actuator relationships, and data flows**.  
Detailed diagrams, wiring schematics, and notes are included as placeholders to be filled in as the project progresses.

---

## 1. System Overview

**Scope 1 Subsystems:**

| Subsystem | Purpose |
|-----------|---------|
| Microcontroller | Core processing and control |
| Power Monitoring | 220V AC input, 12V/5V/3.3V DC rails |
| Environmental Sensors | Air temperature, relative humidity, lux |
| Soil & Water Sensors | Soil temperature, soil moisture, water reservoir |
| Actuators | Soil heating, air heating/cooling, fan, water pump, white grow light |
| Camera | Live view and timelapse |
| Safety & Alarms | Visual and audible alarms, interlocks |
| User Interface | Home Assistant or web interface |

## Scope 1 Control Loops
<Mermaid Control Loop Diagram Block>
```mermaid
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

---

## 2. Control Loop Diagram (Scope 1)

[Air Temperature Sensor] → [PID Controller] → [Air Heater / Cooler]
[Soil Moisture Sensor] → [Controller] → [Water Pump] → [Soil]
[Soil Temperature Sensor] → [Controller] → [Soil Heater]
[Lux Sensor] → [Controller] → [White Grow Light]
[Fan RPM Sensor] → [Controller] → [Fan PWM]
[Water Reservoir Level] → [Pump Interlock]


## System Architecture / Data Flow
<Mermaid System Architecture Block>

**Explanation:**
- Sensors feed the controllers  
- Controllers drive actuators  
- Dashed arrow (`-.->`) shows safety interlock (WaterPump disabled if reservoir low)  

GitHub will render this as a clean **flowchart**.  

---

## 2️⃣ System Architecture / Data Flow Diagram (Mermaid)

```markdown
```mermaid
graph LR
  %% Sensors
  Sensors[Environmental & Soil Sensors] --> MCU[Microcontroller]

  %% Actuators
  MCU --> Actuators[Soil Heater, Water Pump, Fan, Light, Atomizer]

  %% Logging
  MCU --> Logs[Measurement & Event Logging]

  %% User Interface
  MCU --> UI[Home Assistant / Web UI]
  UI --> User[Grower / Operator]

  %% Camera
  MCU --> Camera[Camera Module]
  Camera --> UI

  %% Safety
  MCU --> Safety[State Machine & Alarms]
  Safety --> Actuators
  Safety --> UI

---

## 3. Data Flow

1. **Sensors → Microcontroller**
   - All sensor readings are collected at regular intervals.
   - Minimum polling frequency: 1 Hz for fast control loops (soil moisture, temperature).
2. **Microcontroller → Control Outputs**
   - Actuators are updated based on control loops and safety checks.
3. **Microcontroller → User Interface**
   - Measurement logs, alarms, and camera feeds are sent to Home Assistant or web interface.
4. **Logging**
   - Sensor readings, actuator commands, and alarm events are stored for historical analysis.

---

## 4. Wiring & Connectivity (Scope 1)

- **Power**
  - AC → DC power supply → microcontroller and actuators
  - Ensure separate traces for high-current devices
- **Sensors**
  - Connect using shielded cables for analog/digital signals
  - Pull-up resistors where required (e.g., DS18B20)
- **Actuators**
  - Use relays or MOSFETs suitable for voltage/current rating
  - Interlocks prevent operation when unsafe (water low, over-temp)
- **Communication**
  - Ethernet / WiFi / optional Zigbee

> Placeholder: Include wiring diagram images here.

---

## 5. Safety Interlocks & State Machine

**States:**

| State | Description |
|-------|-------------|
| HOLD | Controller idle; no actuators active |
| RUN | Normal operation; control loops active |
| ALARM | Unsafe condition detected; all actuators disabled |
| STOP | Manual stop; safe state enforced |

**Rules:**
- Controller starts in **HOLD** mode
- **ALARM** triggers disable all control outputs
- Manual override allowed only if safe
- Full recovery requires user confirmation

---

## 6. Documentation Notes

- Use this page to track:
  - Wiring changes
  - Control loop tuning
  - Sensor calibration offsets
  - Safety interlocks added
- Future Scope 2+ enhancements (recipes, multi-channel lighting, CO₂) will extend this architecture diagram.

---

## 7. Next Steps

- Replace ASCII diagrams with **Mermaid or draw.io visuals**
- Add **wiring schematics and PCB layouts**
- Define **PID / control loop parameters** for all sensors
- Add **camera wiring and timelapse diagram**
- Keep architecture synced with `/docs/01_scope_1_v1/GETTING_STARTED.md`
