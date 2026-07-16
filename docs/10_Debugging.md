# Debugging

## 1. Introduction

This document provides a systematic debugging procedure for the USB 3.1 Gen 1 to Gigabit Ethernet Adapter after PCB assembly.

The objective is to isolate hardware faults in a logical order, beginning with the power subsystem and progressing through USB communication, Ethernet initialization, and network functionality.

The recommended approach is to verify one subsystem at a time rather than attempting full system validation immediately after power-up.

---

# 2. Required Equipment

The following equipment is recommended during hardware bring-up:

- Digital Multimeter (DMM)
- Oscilloscope
- USB Protocol Analyzer (optional)
- Ethernet Cable
- Gigabit Ethernet Switch or Router
- Computer with USB 3.x Port
- Bench Power Supply (if external power testing is required)

---

# 3. Debugging Sequence

Hardware should always be verified in the following order:

```
Visual Inspection
        │
        ▼
Continuity Check
        │
        ▼
Power Rails
        │
        ▼
Clock Verification
        │
        ▼
Reset Signals
        │
        ▼
EEPROM Detection
        │
        ▼
USB Enumeration
        │
        ▼
PHY Initialization
        │
        ▼
Ethernet Link
        │
        ▼
Network Communication
```

Skipping intermediate stages may make fault isolation significantly more difficult.

---

# 4. Visual Inspection

Before applying power, inspect the PCB for manufacturing defects.

Verify:

- Component orientation
- Missing components
- Solder bridges
- Lifted pins
- Poor solder joints
- Damaged traces
- Connector alignment

Correct any visible defects before continuing.

---

# 5. Continuity Checks

With the board unpowered:

- Verify there are no shorts between power and ground.
- Check continuity of all power rails.
- Confirm USB VBUS is not shorted.
- Verify Ethernet differential pairs are not shorted.
- Inspect regulator outputs for shorts.

These checks reduce the risk of damaging components during first power-up.

---

# 6. Power Verification

After connecting USB power:

Verify:

- VBUS present
- 3.3 V rail
- 1.2 V rail

Each regulator should reach its nominal output voltage and remain stable.

If any rail is missing or unstable:

- Disconnect power immediately.
- Inspect regulator circuitry.
- Verify component orientation.
- Check surrounding passive components.

Do not proceed until all power rails are operating correctly.

---

# 7. Clock Verification

Using an oscilloscope, verify the presence of the reference clock.

Check:

- Oscillation starts after power-up.
- Stable waveform.
- Expected frequency.
- Clean signal without excessive noise.

If no oscillation is observed:

- Inspect crystal connections.
- Verify load capacitors.
- Confirm regulator outputs.
- Inspect the surrounding layout.

---

# 8. EEPROM Verification

Confirm that the EEPROM is correctly powered and connected.

Verify:

- Supply voltage
- Communication lines
- Device orientation

If the controller cannot read configuration data, USB enumeration may fail or default configuration values may be used.

---

# 9. USB Enumeration

Connect the adapter to a host computer.

Verify:

- Device detection
- Correct Vendor ID
- Correct Product ID
- Successful enumeration
- Driver loading

If enumeration fails:

- Verify USB differential pairs.
- Inspect CC circuitry.
- Confirm EEPROM operation.
- Recheck power rails.
- Inspect the LAN7801 solder joints.

---

# 10. PHY Verification

After successful USB initialization, verify PHY operation.

Check:

- PHY power rails
- Reset signal
- Clock input
- MDIO communication
- Link status

If the PHY does not initialize correctly:

- Verify RGMII routing.
- Inspect strap pins.
- Confirm clock operation.
- Verify regulator outputs.

---

# 11. Ethernet Link Verification

Connect the adapter to a known-good Gigabit Ethernet switch.

Verify:

- Link LED
- Activity LED
- Auto-negotiation
- Link speed

Failure to establish link may indicate:

- PHY configuration issues
- Magnetics problems
- RJ45 soldering defects
- MDI routing faults

---

# 12. Functional Testing

Once a valid Ethernet link is established, perform functional testing.

Recommended tests include:

- IP address acquisition
- Ping test
- File transfer
- Sustained network traffic
- Throughput measurement

Observe the board for any instability during prolonged operation.

---

# 13. Common Symptoms

| Symptom | Possible Cause |
|----------|----------------|
| No Power | USB connector, regulator, short circuit |
| Missing 3.3 V | LDO fault, shorted load |
| Missing 1.2 V | Core regulator fault |
| No Clock | Crystal or oscillator circuitry |
| USB Not Detected | USB routing, CC pins, LAN7801 |
| Enumeration Failure | EEPROM, controller configuration |
| No Ethernet Link | PHY, MagJack, MDI routing |
| Intermittent Link | Signal integrity or soldering issues |

---

# 14. Debugging Philosophy

Always isolate one subsystem before moving to the next.

Avoid making multiple hardware changes simultaneously, as this makes it difficult to identify the true source of a fault.

After every modification:

- Inspect the PCB.
- Repeat continuity checks if necessary.
- Re-verify the affected subsystem before proceeding.

A structured debugging process is significantly more effective than random trial-and-error.

---

# 15. Summary

Successful bring-up depends on verifying the hardware in a logical sequence.

Beginning with the power subsystem and progressing through clocks, configuration memory, USB communication, and Ethernet functionality minimizes debugging time and simplifies fault isolation.

This procedure should be followed whenever a new revision of the hardware is assembled.

---

# Related Documents

- 05_Power_Architecture.md
- 06_EEPROM.md
- 07_PCB_Design.md
- 08_Signal_Integrity.md
- 09_Manufacturing.md