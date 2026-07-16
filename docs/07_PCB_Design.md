# PCB Design

## 1. Introduction

This document summarizes the PCB design methodology adopted for the USB 3.1 Gen 1 to Gigabit Ethernet Adapter.

The focus is on the design decisions that directly influenced signal integrity, power integrity, manufacturability, and overall board reliability.

---

# 2. PCB Stack-Up

A four-layer PCB stack-up was selected to satisfy the routing and signal integrity requirements of both USB SuperSpeed and Gigabit Ethernet interfaces.

The adopted stack-up is:

```
Layer 1 : High-Speed Signals
Layer 2 : Continuous Ground Plane
Layer 3 : Power Plane
Layer 4 : Signals
```

### Why a Four-Layer PCB?

The design contains several high-speed interfaces that require continuous reference planes and controlled impedance routing.

Compared to a two-layer PCB, the selected stack-up provides:

- Improved signal integrity
- Lower EMI
- Better return current paths
- Easier impedance control
- Improved power distribution
- Simplified routing

---

# 3. Component Placement

Component placement was completed before routing.

The placement strategy prioritized:

- Short USB routing
- Short RGMII interface
- Short MDI differential pairs
- Proper crystal placement
- Efficient power distribution

Critical devices were placed according to signal flow rather than mechanical convenience.

---

# 4. USB SuperSpeed Routing

The USB SuperSpeed differential pairs were routed directly between the USB Type-C connector and the LAN7801.

Routing objectives included:

- 90 Ω differential impedance
- Continuous ground reference
- Minimal via usage
- Length matching within each pair
- Smooth routing geometry
- Minimal discontinuities

---

# 5. RGMII Routing

The RGMII interface between the LAN7801 and KSZ9031RNX was treated as one of the most timing-sensitive sections of the design.

Layout considerations included:

- Short trace lengths
- Length matching
- Reduced skew
- Continuous reference plane
- Minimal routing detours

---

# 6. Ethernet MDI Routing

The four Ethernet differential pairs were routed from the PHY to the integrated MagJack.

Routing followed Gigabit Ethernet layout recommendations.

Design goals included:

- 100 Ω differential impedance
- Constant pair spacing
- Length matching within each pair
- Smooth routing
- Reduced discontinuities
- Minimal layer transitions

---

# 7. Clock Layout

The 25 MHz reference crystal was placed immediately adjacent to the PHY.

Routing between the PHY and crystal was kept:

- Short
- Symmetrical
- Free from nearby high-speed signals

This minimizes clock noise and improves oscillator stability.

---

# 8. Power Distribution

Power routing emphasized low impedance and clean supply delivery.

The implementation includes:

- Wide power traces where required
- Dedicated power plane
- Local decoupling for every active device
- Bulk capacitance near regulators

---

# 9. Grounding Strategy

A continuous ground plane was maintained beneath all high-speed interfaces.

The ground plane provides:

- Controlled return current paths
- Reduced EMI
- Stable reference for impedance-controlled routing

Plane interruptions beneath critical signals were avoided.

---

# 10. Design Verification

Before manufacturing, the PCB underwent multiple verification stages.

Verification included:

- ERC
- DRC
- Differential pair inspection
- Power connectivity review
- Footprint verification
- Connector orientation review

The objective was to eliminate layout-related issues before fabrication.

---

# 11. Summary

The PCB layout was driven primarily by signal integrity and manufacturability rather than routing convenience.

Particular attention was given to:

- USB SuperSpeed routing
- RGMII timing
- Gigabit Ethernet differential routing
- Power integrity
- Ground reference continuity

The final design is intended to provide a robust hardware platform suitable for fabrication and hardware validation.

---

# Related Documents

- 03_USB_Subsystem.md
- 04_Ethernet_Subsystem.md
- 05_Power_Architecture.md