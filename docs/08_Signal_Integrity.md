# Signal Integrity

## 1. Introduction

The USB 3.1 Gen 1 to Gigabit Ethernet Adapter contains multiple high-speed digital interfaces whose performance depends heavily on PCB layout.

This document summarizes the signal integrity considerations adopted during the design process to ensure reliable operation of the USB SuperSpeed, RGMII, and Gigabit Ethernet interfaces.

The focus is on practical implementation decisions rather than theoretical analysis.

---

# 2. High-Speed Interfaces

The following interfaces were treated as signal integrity critical.

| Interface | Requirement |
|------------|-------------|
| USB 3.1 SuperSpeed | Controlled impedance differential routing |
| RGMII | Timing-controlled parallel interface |
| Ethernet MDI | Controlled impedance differential routing |
| 25 MHz Crystal | Low-noise clock routing |

Each interface imposes different routing constraints and therefore required separate design considerations.

---

# 3. Controlled Impedance Routing

Controlled impedance routing was implemented wherever required by the interface specification.

Target impedances:

| Interface | Target |
|-----------|---------|
| USB SuperSpeed | 90 Ω Differential |
| Ethernet MDI | 100 Ω Differential |

The PCB stack-up and routing geometry were selected accordingly.

---

# 4. Differential Pair Routing

Differential pairs were routed together throughout the design.

The routing objectives included:

- Constant spacing
- Parallel routing
- Equal electrical length within each pair
- Minimal discontinuities
- Smooth corner transitions
- Reduced via usage

Maintaining pair symmetry minimizes differential skew and preserves signal quality.

---

# 5. Return Current Paths

High-speed signals always require a low-impedance return path.

To support this:

- Continuous ground planes were maintained beneath critical routing.
- Plane discontinuities beneath high-speed traces were avoided.
- Reference plane transitions were minimized.

These practices reduce return path inductance and improve signal integrity.

---

# 6. USB SuperSpeed

The USB SuperSpeed interface received particular attention due to its operating frequency.

Routing considerations included:

- Short differential routing
- Controlled impedance
- Minimal stubs
- Minimal vias
- Continuous reference plane
- Isolation from switching regulators and clock circuitry

---

# 7. RGMII Interface

Although RGMII operates at lower frequencies than USB SuperSpeed, it is significantly more sensitive to timing mismatch.

Routing emphasized:

- Short trace lengths
- Length matching
- Reduced skew
- Consistent reference plane
- Clean routing between MAC and PHY

Maintaining timing relationships across the bus was prioritized over routing convenience.

---

# 8. Ethernet Differential Routing

The four MDI differential pairs between the PHY and MagJack were routed according to Gigabit Ethernet layout recommendations.

Routing objectives included:

- 100 Ω differential impedance
- Constant pair spacing
- Minimal pair skew
- Smooth routing
- Short path to the MagJack

---

# 9. Clock Signal Integrity

The 25 MHz reference crystal is one of the most sensitive portions of the design.

To minimize clock degradation:

- The crystal was placed adjacent to the PHY.
- Clock traces were kept short.
- Routing was kept symmetrical.
- High-speed routing was kept away from the oscillator circuitry.

These measures improve oscillator stability and reduce susceptibility to external noise.

---

# 10. Power Integrity

Signal integrity is closely related to power quality.

To reduce supply-induced noise:

- Local decoupling capacitors were placed adjacent to every active device.
- Bulk capacitance was provided near the regulators.
- Low-impedance power distribution was maintained throughout the PCB.

A stable power network reduces supply ripple and improves high-speed communication reliability.

---

# 11. Crosstalk Reduction

PCB routing was organized to minimize electromagnetic coupling between unrelated signals.

This included:

- Maintaining spacing between high-speed interfaces.
- Avoiding long parallel runs where unnecessary.
- Separating clock routing from switching power circuitry.
- Keeping sensitive analog sections away from noisy digital signals.

---

# 12. Layer Stack-Up

Signal integrity was a major factor in selecting the four-layer PCB stack-up.

```
Layer 1 : High-Speed Signals

Layer 2 : Continuous Ground Plane

Layer 3 : Power Plane

Layer 4 : Remaining Signals
```

This arrangement provides:

- Stable reference planes
- Controlled impedance
- Improved return current paths
- Reduced electromagnetic emissions

---

# 13. Verification

The PCB layout was reviewed to verify:

- Differential pair continuity
- Differential impedance constraints
- Pair polarity
- Length matching
- Ground plane continuity
- Crystal routing
- High-speed component placement

These reviews were completed prior to manufacturing.

---

# 14. Summary

Signal integrity considerations influenced nearly every stage of the PCB design.

Particular attention was given to:

- Controlled impedance routing
- Differential pair routing
- Return current paths
- RGMII timing
- Clock placement
- Power integrity
- Crosstalk reduction

These practices contribute to reliable operation of the USB and Gigabit Ethernet interfaces while improving overall robustness of the design.

---

# Related Documents

- 03_USB_Subsystem.md
- 04_Ethernet_Subsystem.md
- 05_Power_Architecture.md
- 07_PCB_Design.md