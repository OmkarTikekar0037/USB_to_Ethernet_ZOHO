# System Architecture

## 1. Introduction

This document describes the overall hardware architecture of the USB 3.1 Gen 1 to Gigabit Ethernet Adapter.

The design is partitioned into multiple functional subsystems, each responsible for a specific task in the data path, power distribution, or device configuration.

Understanding the interaction between these subsystems is essential before studying their individual implementations.

---

# 2. System Overview

The adapter converts USB 3.1 Gen 1 data received from the host computer into Gigabit Ethernet frames that can be transmitted over a standard RJ45 interface.

At the highest level, the system consists of the following major functional blocks:

- USB Interface
- USB-to-Ethernet Controller
- Gigabit Ethernet PHY
- Ethernet Magnetics
- EEPROM Configuration Memory
- Clock Generation
- Power Distribution Network
- Status Indicators

---

# 3. High-Level Block Diagram

```

                 USB HOST
                     │
                     │
             USB 3.1 Gen 1
                     │
                     ▼
        ┌──────────────────────┐
        │      USB Type-C      │
        └──────────────────────┘
                     │
                     ▼
        ┌──────────────────────┐
        │       LAN7801        │
        │ USB Ethernet MAC     │
        └──────────────────────┘
                     │
                  RGMII
                     │
                     ▼
        ┌──────────────────────┐
        │     KSZ9031RNX       │
        │ Gigabit Ethernet PHY │
        └──────────────────────┘
                     │
             Differential Pairs
                     │
                     ▼
        ┌──────────────────────┐
        │    RJ45 MagJack      │
        │  Integrated Magnetics│
        └──────────────────────┘
                     │
                Ethernet Cable

```

---

# 4. Functional Subsystems

## 4.1 USB Interface

The USB interface provides communication between the adapter and the host computer.

Its responsibilities include:

- USB SuperSpeed communication
- USB device detection
- Power input from VBUS
- Data transfer to the LAN7801 controller

The USB interface serves as the entry point for both system power and data.

---

## 4.2 Ethernet Controller

The LAN7801 acts as the central controller of the adapter.

Its primary responsibilities include:

- USB protocol handling
- Ethernet MAC implementation
- Packet buffering
- DMA operations
- Interface with external EEPROM
- Communication with the Gigabit PHY through RGMII

It forms the bridge between the USB subsystem and the Ethernet subsystem.

---

## 4.3 Ethernet PHY

The KSZ9031RNX performs physical layer processing required for Gigabit Ethernet communication.

Responsibilities include:

- RGMII interface
- 1000BASE-T physical layer
- Clock recovery
- Auto-negotiation
- Auto MDI/MDI-X
- Differential signal transmission and reception

The PHY converts digital Ethernet frames into electrical signals suitable for transmission through twisted-pair Ethernet cable.

---

## 4.4 Ethernet Magnetics

The RJ45 MagJack provides:

- Isolation transformer
- Common-mode noise rejection
- Differential signal coupling
- Cable interface

This stage electrically isolates the PCB from the external Ethernet network while preserving signal integrity.

---

## 4.5 EEPROM

An external EEPROM stores device configuration parameters required during LAN7801 initialization.

Typical information includes:

- USB descriptors
- Vendor information
- Product identification
- MAC address
- Configuration options

The controller loads these parameters during startup.

---

## 4.6 Clock Generation

Stable clock sources are required for reliable operation of both the controller and PHY.

The clock subsystem provides timing references necessary for:

- USB operation
- Ethernet operation
- PHY synchronization
- Internal PLL operation

Clock quality directly affects communication reliability.

---

## 4.7 Power Distribution

The adapter derives all operating voltages from the USB VBUS supply.

Separate regulated rails are generated for:

- Digital I/O
- Analog circuitry
- Core logic

The power architecture is discussed in detail in **Power_Architecture.md**.

---

# 5. Data Flow

The data path through the adapter is illustrated below.

```

USB Host
    │
    ▼
USB Type-C
    │
    ▼
LAN7801
    │
 RGMII Interface
    │
    ▼
KSZ9031RNX
    │
 Ethernet MDI
    │
    ▼
RJ45 MagJack
    │
    ▼
Ethernet Network

```

The reverse path follows the same sequence in the opposite direction for received Ethernet frames.

---

# 6. Power Flow

The power distribution network begins at the USB connector.

```

USB VBUS
    │
    ▼
Primary Regulation
    │
    ├────────► 3.3 V Rail
    │
    └────────► 1.2 V Rail

```

Each subsystem receives power from the appropriate regulated supply according to its operating requirements.

---

# 7. Reset Architecture

Proper initialization requires all major devices to enter a known state after power application.

The reset network ensures:

- Stable power rails before initialization
- Predictable startup sequence
- Reliable device configuration
- Proper PHY initialization

Reset sequencing is discussed in the subsystem documentation where applicable.

---

# 8. Configuration Interfaces

Several auxiliary interfaces are used internally within the design.

| Interface | Purpose |
|------------|---------|
| USB 3.1 | Host communication |
| RGMII | LAN7801 ↔ KSZ9031RNX |
| MDIO/MDC | PHY register configuration |
| Microwire | EEPROM communication |
| Differential Ethernet | Physical Ethernet interface |

Each interface is described in detail within its respective subsystem document.

---

# 9. Design Philosophy

The system architecture emphasizes:

- Functional partitioning
- Independent subsystem verification
- Short critical signal paths
- Reliable power delivery
- Manufacturable PCB layout
- Maintainable hardware organization

This modular organization simplified schematic development, PCB layout, and design verification throughout the project.

---

# 10. Related Documents

The following documents expand each subsystem in detail:

- USB_Subsystem.md
- Ethernet_Subsystem.md
- Power_Architecture.md
- EEPROM.md
- PCB_Design.md
- Signal_Integrity.md
- Manufacturing.md