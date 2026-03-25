---
id: safety-interlocks
name: Safety Interlocks
description: Implement safety interlocks and protective mechanisms to prevent equipment damage and ensure safe control system operation.
category: Research
requires: []
examples:
  - How do I implement a safety cutoff for my control loop?
  - Show me a pattern for applying safety limits to sensor data.
---

# Safety Interlocks for Control Systems

## Overview

Safety interlocks are protective mechanisms that prevent equipment damage and ensure safe operation. In control systems, the primary risks are output saturation and exceeding safe operating limits.

## Instruction
- Perform a critical pre-control check to verify that sensor readings are within physical bounds and not NaN or infinite.
- Identify and define the absolute safety limits (Maximum and Minimum) for both measurements and control outputs.
- Implement a "Check BEFORE Output" logic where safety conditions are evaluated immediately before any control command is sent.
- Trigger an emergency cutoff (setting output to a safe minimum) whenever a critical threshold is breached.
- Maintain a structured safety log recording the timestamp, measurement, and the specific event that triggered an interlock.
- Utilize output clamping to ensure that manual or automated commands never exceed the hardware's safe operating range.

## When to Use
- When designing or implementing control logic for laboratory hardware, heating systems, or mechanical actuators.
- When establishing protective mechanisms to prevent system saturation or catastrophic equipment damage.
- When performing risk assessments and configuring automated safety monitoring for industrial processes.

## Output
- Functional safety logic patterns and code snippets for interlock implementation.
- Configuration summaries for safety thresholds and emergency response behaviors.
- A checklist of precautions for pre-control sensor validation and safety event logging.

## Pre-Control Checklist

Before starting any control operation:

1. **Verify sensor reading is reasonable**
   - Not NaN or infinite
   - Within physical bounds

2. **Check initial conditions**
   - Measurement should be at expected starting point
   - Output should start at safe value

3. **Confirm safety limits are configured**
   - Maximum limit threshold set
   - Output clamping enabled


## Best Practices

1. **Defense in depth**: Multiple layers of protection
2. **Fail safe**: When in doubt, reduce output
3. **Log everything**: Record all safety events
4. **Never bypass**: Safety code should not be conditionally disabled
5. **Test safety**: Verify interlocks work before normal operation
