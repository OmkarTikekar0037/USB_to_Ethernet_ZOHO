# EEPROM Subsystem

## 1. Introduction

The adapter utilizes an external serial EEPROM to store non-volatile configuration data required by the LAN7801 during system initialization.

Separating configuration data from the controller provides flexibility during manufacturing and allows device-specific parameters to be updated without modifying the hardware.

The EEPROM is accessed automatically by the LAN7801 during the power-up sequence.

---

# 2. Objectives

The EEPROM subsystem was designed to:

- Store permanent device configuration
- Provide USB identification information
- Store Ethernet-related configuration
- Support production programming
- Enable board-specific customization

---

# 3. Architecture

```

                 LAN7801
                     │
         Microwire Serial Interface
                     │
                     ▼
              +--------------+
              |   93LC56     |
              |   EEPROM     |
              +--------------+

```

The EEPROM acts as a non-volatile configuration memory and is not involved in normal Ethernet data transfer.

---

# 4. Stored Information

The EEPROM stores configuration information used during device initialization.

Typical contents include:

- Vendor ID (VID)
- Product ID (PID)
- USB device descriptors
- Manufacturer information
- Product string
- MAC address
- LAN7801 configuration options

The exact EEPROM image is generated according to the project requirements and programmed during manufacturing.

---

# 5. Initialization Sequence

During startup, the LAN7801 checks for the presence of a valid external EEPROM.

If a valid configuration is detected, the controller loads the stored parameters into its internal configuration registers before beginning normal USB operation.

This process is transparent to the host computer.

---

# 6. Interface

Communication between the LAN7801 and the EEPROM occurs through the Microwire serial interface.

The interface provides:

- Read operations during startup
- Configuration data transfer
- Reliable non-volatile storage

Since EEPROM access occurs primarily during initialization, the interface has minimal impact on normal Ethernet operation.

---

# 7. Power Supply

The EEPROM operates from the regulated 3.3 V supply rail.

Local decoupling is provided adjacent to the device to ensure reliable operation during power-up and configuration loading.

---

# 8. PCB Layout Considerations

Although the EEPROM is not a high-speed device, proper placement improves system reliability.

Design considerations include:

## Placement

- Located close to the LAN7801
- Short serial interface traces
- Convenient routing to the controller

---

## Power

- Local decoupling capacitor positioned adjacent to the supply pin
- Short connection to the 3.3 V rail
- Direct connection to the ground plane

---

## Signal Routing

The Microwire interface traces were kept short and free from unnecessary routing complexity.

Because the interface operates at relatively low speed, impedance-controlled routing was not required.

---

# 9. Manufacturing Considerations

The EEPROM is programmed with the required configuration image during board production.

Programming may include:

- USB identification data
- Device configuration
- Factory MAC address
- Customer-specific parameters (if applicable)

This allows identical hardware assemblies to be configured for different production variants without modifying the PCB.

---

# 10. Verification

The EEPROM subsystem was verified for:

- Correct device selection
- Supply connectivity
- Microwire interface continuity
- Decoupling placement
- ERC compliance
- DRC compliance

Additional verification is performed during hardware bring-up by confirming successful configuration loading by the LAN7801.

---

# 11. Summary

Although physically small, the EEPROM plays an essential role during system initialization.

It enables permanent storage of device-specific configuration while keeping the hardware design flexible and suitable for manufacturing.

Because configuration data resides externally, updates can be made without redesigning the PCB or replacing the controller.

---

# Related Documents

- 01_System_Architecture.md
- 02_Component_Selection.md
- 03_USB_Subsystem.md
- 04_Ethernet_Subsystem.md
- 05_Power_Architecture.md
- 07_PCB_Design.md