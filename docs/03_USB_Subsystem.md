# USB Subsystem

## 1. Introduction

The USB subsystem provides the primary communication interface between the host computer and the adapter.

In addition to transferring Ethernet frames, the USB interface also supplies power to the entire system through the USB Type-C connector.

This document describes the implementation of the USB subsystem, including the connector, protection circuitry, power entry, and interface to the LAN7801 controller.

---

# 2. Objectives

The USB subsystem was designed to achieve the following objectives:

- Reliable USB 3.1 Gen 1 communication
- Stable power delivery from USB VBUS
- Compliance with USB Type-C device connection requirements
- Protection against ESD events
- Controlled impedance routing for SuperSpeed differential pairs
- Seamless integration with the LAN7801 controller

---

# 3. USB Architecture

```
                 USB Host
                     │
                     │
                     │
                     ▼
          ┌─────────────────────┐
          │ USB Type-A Connector│
          └─────────────────────┘
                     │
      ┌──────────────┼──────────────┐
      │              │              │
      ▼              ▼              ▼
    VBUS         USB Data      Configuration
                    │             Channel
                    │
                    ▼
          ┌─────────────────────┐
          │      LAN7801        │
          └─────────────────────┘
```

---

# 4. USB Type-A Connector

The USB Type-A connector serves as the interface between the host computer and the adapter.

Its functions include:

- Receiving USB SuperSpeed signals
- Receiving USB 2.0 signals
- Supplying system power through VBUS

The connector is implemented as a USB device interface.

---

# 5. USB Data Path

The SuperSpeed differential pairs are routed directly between the USB Type-A connector and the LAN7801.

Primary routing objectives included:

- Controlled differential impedance
- Continuous reference plane
- Minimal via count
- Length matching within each differential pair
- Smooth routing without unnecessary discontinuities
- Isolation from noisy switching circuits

Signal integrity was prioritized during placement and routing.

---

# 6. USB 2.0 Interface

The USB 2.0 differential pair is routed alongside the SuperSpeed interface.

Although Gigabit Ethernet communication utilizes the SuperSpeed interface, USB 2.0 remains necessary for:

- Device enumeration
- Backward compatibility
- Standard USB operation

The routing follows standard differential pair design practices.

---


# 7. Power Entry

System power is obtained directly from the USB VBUS supply.

VBUS serves as the primary input to the onboard power distribution network.

Subsequent voltage regulation generates the required operating voltages for the remaining subsystems.

The power architecture is discussed separately in **Power_Architecture.md**.

---

# 8. Protection Circuitry

To improve robustness, the USB interface includes protection against external electrical disturbances.

Protection features include:

- ESD protection for high-speed data lines
- ESD protection for Configuration Channel pins
- Protection of VBUS input
- Proper grounding strategy for transient current dissipation

Component placement minimizes the distance between the connector and protection devices.

---

# 9. PCB Layout Considerations

The USB interface imposes strict layout requirements.

Key design considerations include:

## Component Placement

- LAN7801 positioned close to the USB connector
- Short SuperSpeed routing paths
- Minimal signal discontinuities

## Differential Pair Routing

- Controlled impedance
- Constant spacing
- Length matching
- No unnecessary stubs
- Reduced via usage

## Reference Plane

The SuperSpeed pairs are routed above a continuous ground reference plane to maintain impedance and provide a low-inductance return path.

## Return Current

High-speed return currents are allowed to flow directly beneath their associated signal traces by avoiding interruptions in the reference plane.

---

# 10. Verification

The USB subsystem was reviewed for:

- Connector pin assignments
- Differential pair continuity
- Differential pair polarity
- Power connectivity
- ESD device placement
- CC resistor implementation
- ERC compliance
- PCB DRC compliance

---

# 11. Summary

The USB subsystem provides both communication and power entry for the adapter.

Its implementation emphasizes:

- Reliable high-speed communication
- Controlled impedance routing
- Proper Type-C device configuration
- Robust protection against external disturbances
- Clean integration with the LAN7801 controller

Together with the Ethernet subsystem, it forms the primary communication path of the adapter.

---

# Related Documents

- 01_System_Architecture.md
- 02_Component_Selection.md
- 04_Ethernet_Subsystem.md
- 05_Power_Architecture.md
- 07_PCB_Design.md
