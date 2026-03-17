---
id: embedded-systems
name: Embedded Systems
description: Design and implement embedded firmware with reliable hardware interaction, timing control, and resource constraints in mind.
category: Development
requires: ["target mcu or soc", "firmware feature requirements", "peripheral and timing constraints"]
examples:
  - "Design firmware architecture for this sensor + BLE embedded product on STM32."
  - "Review this embedded driver flow for ISR timing, memory use, and failure handling."
---

# Embedded Systems

Build robust embedded systems by combining hardware-aware design with testable firmware patterns.

## When to Use

- You are building firmware for MCU/SoC targets.
- You need guidance on peripheral control, timing, and power/resource management.

## Workflow

1. Define hardware constraints, memory budget, and real-time requirements.
2. Plan firmware layers (drivers, middleware, application logic).
3. Design interrupt/DMA/timer interactions and failure recovery behavior.
4. Validate power, latency, and reliability tradeoffs.
5. Provide hardware-in-loop testing and debugging checklist.

## Output

- Firmware architecture guidance
- Timing and reliability recommendations
- Validation checklist for embedded testing
