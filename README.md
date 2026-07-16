# USB 3.1 Gen 1 to Gigabit Ethernet Adapter

A custom 4-layer PCB implementing a USB 3.1 Gen 1 to Gigabit Ethernet adapter based on the **Microchip LAN7801** USB-to-Ethernet controller and the **KSZ9031RNX** Gigabit Ethernet PHY.

The project focuses on producing a manufacturable hardware design by following industry-standard practices for high-speed PCB layout, power distribution, signal integrity, and Ethernet design.

---

## Project Objectives

- Design a production-quality USB 3.1 Gen 1 to Gigabit Ethernet adapter.
- Implement a complete RGMII-based Ethernet subsystem.
- Develop a reliable multi-rail power architecture.
- Follow high-speed PCB design guidelines for USB and Gigabit Ethernet.
- Produce fabrication-ready design files with zero ERC/DRC violations.

---

## Hardware Overview

| Component | Description |
|-----------|-------------|
| LAN7801 | USB 3.1 Gen 1 to Gigabit Ethernet Controller |
| KSZ9031RNX | Gigabit Ethernet PHY |
| 93LC56 | External configuration EEPROM |
| USB Type-C | USB Interface |
| RJ45 MagJack | Ethernet Connector with Integrated Magnetics |
| TLV76733 | 3.3V LDO |
| TPS7A0212 | 1.2V LDO |

---

## System Architecture

```
USB Type-C
      │
      ▼
+--------------+
|   LAN7801    |
+--------------+
      │
     RGMII
      │
      ▼
+--------------+
| KSZ9031RNX   |
+--------------+
      │
 Ethernet MDI
      │
      ▼
 RJ45 MagJack
```

---

## Repository Structure

```text
.
├── Hardware/
│   ├── Schematic/
│   ├── PCB/
│   ├── Libraries/
│   └── Manufacturing/
│
├── Docs/
│   ├── Project_History.md
│   ├── System_Architecture.md
│   ├── Power_Architecture.md
│   ├── Ethernet_Subsystem.md
│   ├── USB_Subsystem.md
│   ├── PCB_Design.md
│   └── Debugging.md
│
├── Datasheets/
│
├── Images/
│
└── README.md
```

---

## Current Project Status

| Stage | Status |
|--------|--------|
| Component Selection | Completed |
| Schematic Design | Completed |
| PCB Placement | Completed |
| PCB Routing | Completed |
| ERC | Passed |
| DRC | Passed |
| Manufacturing Outputs | In Progress |
| Hardware Validation | Pending |

---

## Design Highlights

- 4-layer PCB stack-up
- Controlled impedance routing
- USB differential pair routing
- Gigabit Ethernet differential routing
- Dedicated power planes
- Multi-stage power regulation
- External EEPROM configuration
- RGMII interface between MAC and PHY
- ESD and signal protection provisions

---

## Documentation

Detailed design discussions and engineering decisions are maintained separately under the **Docs** directory.

These documents describe:

- Architecture
- Design decisions
- Power subsystem
- PCB layout methodology
- Signal integrity considerations
- Manufacturing preparation
- Debugging history

The README intentionally provides only a high-level overview.

---

## Future Work

- PCB fabrication
- Assembly
- Hardware bring-up
- USB enumeration verification
- Ethernet link validation
- Throughput testing
- Compliance verification

---

## License

Project license to be added.