# GreenSeedling Core – Product Foundation

## Product Vision

GreenSeedling Core is a **modular, fully documented indoor grow box controller** designed for hobbyists, educators, and small-scale urban growers.  
Its purpose is to enable **reproducible plant cultivation** while providing transparency in hardware and software design.

**Key principles:**
- **Open and documented**: Every aspect of hardware, firmware, and control logic is publicly available.
- **Safe-by-design**: The system is inherently safe; all alarms, fail-safes, and state machines are implemented to prevent plant or hardware damage.
- **Expandable**: Designed to allow incremental upgrades (recipes, multi-channel lighting, CO₂ enrichment, advanced sensors).
- **Modular and reusable**: Components and control loops can be extended without rewriting the core system.

---

## Non-goals

These are **explicitly excluded in Scope 1** to maintain focus and reliability:
- CO₂ enrichment (planned for Scope 3)
- EC / TDS / pH automation
- Multi-channel lighting beyond white (2700K / 5000K / UV / IR)
- OTA updates (except planned later)
- Zigbee or wireless redundancy beyond initial chosen option

---

## Scope Model Philosophy

1. **Scope 0 — Platform Foundation**
   - Invisible technical layer: state machine, safe states, watchdog, power monitoring
   - No grow-specific features yet

2. **Scope 1 — Essential Grow Control (current phase)**
   - All measured parameters have **closed-loop control where applicable**
   - Minimal viable product: soil moisture, air/soil temp, basic lighting, safety alarms
   - Fully documented and reproducible

3. **Scope 2 — Automated Growth & Recipes**
   - Multi-channel lighting
   - Recipe engine
   - Timelapse automation
   - Air humidification

4. **Scope 3 — Advanced Cultivation**
   - CO₂ control
   - Water EC/TDS/pH
   - Advanced alarms and analytics

5. **Scope 4 — Intelligence & Vision**
   - Flower, leaf, root detection triggers
   - Adaptive recipes
   - Multi-grow orchestration

**Rule:** If a variable is measured, a minimal control loop exists in the same scope.

---

## Design Principles

- **Documentation first:** Specs and architecture are finalized before hardware or firmware implementation.
- **Validation at every step:** Control loops, alarms, and safety features are always defined and tested.
- **Public-first mindset:** Early adopters and hobbyists can build, use, and learn without ambiguity.
- **Phase consistency:** No Scope 2 or 3 features are implemented in Scope 1 hardware without clear separation.
- **Traceable decisions:** Every architectural or design choice is recorded in `/docs/09_decisions/`.

