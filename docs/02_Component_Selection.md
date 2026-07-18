# Component Selection

## 1. Introduction

This document summarizes the major components used in the USB 3.1 Gen 1 to Gigabit Ethernet Adapter and their roles within the overall system architecture.

The objective is to document the purpose of each component and the considerations that influenced its selection. Since several devices were specified as part of the project requirements, this document focuses primarily on system integration rather than evaluating alternative solutions.

---

# 2. Primary Components

| Component | Function |
|-----------|----------|
| LAN7801 | USB-to-Gigabit Ethernet Controller |
| KSZ9031RNX | Gigabit Ethernet PHY |
| 93LC56 | External Configuration EEPROM |
| USB Type-A Plug | USB Interface |
| RJ45 MagJack | Ethernet Connector with Integrated Magnetics |
| TLV76733 | 3.3 V Voltage Regulator |
| TPS7A0212 | 1.2 V Voltage Regulator |
| 25 MHz Crystal | System Clock Source |

---

# 3. LAN7801

## Role

The LAN7801 serves as the primary controller of the adapter.

It performs:

- USB device communication
- Ethernet MAC functions
- Packet buffering
- DMA operations
- External EEPROM access
- RGMII communication with the PHY

As this device was specified by the project requirements, the hardware architecture was developed around its interface and design recommendations.

---

# 4. KSZ9031RNX Gigabit PHY

## Role

The KSZ9031RNX provides the physical layer required for Gigabit Ethernet communication.

It interfaces directly with the LAN7801 through the RGMII bus and converts digital Ethernet frames into differential electrical signals suitable for transmission over twisted-pair Ethernet cable.

### Selection Considerations

The device integrates several features that simplify PCB implementation, including:

- Native RGMII interface
- Integrated termination resistors
- Auto-negotiation
- Auto MDI/MDI-X
- Clock skew adjustment
- Extensive configuration through MDIO

These capabilities reduce external component count while providing flexibility during hardware bring-up.

---

# 5. 93LC56 EEPROM

## Role

The EEPROM stores non-volatile configuration data required during controller initialization.

Typical stored information includes:

- USB descriptors
- Vendor ID
- Product ID
- Device configuration
- MAC address

Separating configuration from the controller allows firmware-independent customization of the hardware.

---

# 6. USB Type-C Connector

## Role

The USB Type-C connector provides:

- USB SuperSpeed interface
- USB 2.0 compatibility
- System power input
- Mechanical connection to the host

The connector follows the standard USB Type-C implementation required for USB device operation.

---

# 7. RJ45 MagJack

## Role

The RJ45 connector integrates both the Ethernet connector and the required isolation magnetics.

Its responsibilities include:

- Galvanic isolation
- Common-mode noise suppression
- Differential signal coupling
- External cable connection

Using an integrated MagJack reduces routing complexity and minimizes external magnetic components.

---

# 8. Voltage Regulators

## 8.1 TLV76733

Provides the regulated 3.3 V supply used by:

- LAN7801 I/O
- KSZ9031RNX I/O
- EEPROM
- Supporting circuitry

### Selection Considerations

- Low output noise
- Stable regulation
- Suitable output current
- Compact footprint
- Good transient response

---

## 8.2 TPS7A0212

Provides the regulated 1.2 V rail required for internal core supplies.

### Selection Considerations

- Low-noise output
- Excellent line regulation
- Small PCB footprint
- Stable operation with ceramic capacitors

---

# 9. 25 MHz Crystal

A precision 25 MHz crystal provides the reference clock required for Ethernet operation.

Clock stability directly influences:

- PHY synchronization
- PLL operation
- Ethernet timing
- Reliable link establishment

Special attention was given to crystal placement and routing during PCB layout.

---

# 10. Passive Components

Although passive components are individually simple, they play a critical role in overall system reliability.

The design includes:

- Power supply decoupling capacitors
- Bulk capacitors
- Pull-up resistors
- Pull-down resistors
- Bias resistors
- Filtering components
- Termination resistors where required

Passive component values were selected according to the recommendations provided in the respective device datasheets.

---

# 11. Design Considerations

Component selection throughout the project emphasized:

- Compatibility between subsystems
- Availability of documentation
- PCB layout simplicity
- Manufacturability
- Electrical reliability
- Long-term maintainability

Wherever possible, the design follows the reference recommendations published by the component manufacturers while maintaining a layout optimized for this specific application.

---

# 12. Related Documents

Additional information regarding the implementation of these components can be found in:

- 03_USB_Subsystem.md
- 04_Ethernet_Subsystem.md
- 05_Power_Architecture.md
- 06_EEPROM.md
- 07_PCB_Design.md
