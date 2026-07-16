# Power Architecture

## 1. Introduction

The power architecture provides regulated supply rails for every subsystem of the adapter, beginning with the 5 V supplied through the USB Type-C connector.

The design emphasizes:

- Stable voltage regulation
- Low-noise power distribution
- Proper subsystem isolation
- Reliable startup
- Adequate local decoupling
- Manufacturable PCB layout

The power network was designed to satisfy the requirements of both the LAN7801 controller and the KSZ9031RNX Gigabit Ethernet PHY while maintaining good signal integrity throughout the board.

---

# 2. Power Overview

The entire adapter is powered directly from the USB VBUS supply.

```

                USB VBUS (5 V)
                       │
                       ▼
             +------------------+
             |    3.3 V LDO     |
             +------------------+
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
    LAN7801       KSZ9031RNX      EEPROM
      I/O             I/O
                       │
                       ▼
              +------------------+
              |    1.2 V LDO     |
              +------------------+
                       │
         ┌─────────────┴─────────────┐
         ▼                           ▼
   LAN7801 Core             KSZ9031RNX Core

```

The design uses a cascaded regulation approach where the 3.3 V rail supplies the lower-voltage regulator required for the core logic.

---

# 3. Supply Rails

## 3.1 USB VBUS (5 V)

The USB connector provides the primary power source for the board.

This rail serves as the input to the onboard voltage regulation circuitry and is not distributed directly to digital logic.

Primary responsibilities:

- System power input
- Regulator input supply

---

## 3.2 3.3 V Rail

The 3.3 V rail supplies the I/O circuitry and supporting peripherals.

Typical loads include:

- LAN7801 I/O
- KSZ9031RNX I/O
- EEPROM
- Supporting logic

This rail also serves as the input source for the 1.2 V regulator.

---

## 3.3 1.2 V Rail

The 1.2 V rail powers the internal core logic of the major integrated circuits.

Typical loads include:

- LAN7801 Core
- KSZ9031RNX Core
- Internal digital logic

Because these circuits switch at high frequency, particular attention was given to local decoupling and power plane integrity.

---

# 4. Power Tree

```

                    USB VBUS
                        │
                        ▼
                 3.3 V Regulator
                        │
      ┌─────────────────┼─────────────────┐
      │                 │                 │
      ▼                 ▼                 ▼
 LAN7801 I/O      KSZ9031 I/O        EEPROM
      │
      ▼
               1.2 V Regulator
                        │
        ┌───────────────┴───────────────┐
        ▼                               ▼
   LAN7801 Core                  KSZ9031 Core

```

Separating the I/O and core supplies reduces supply noise while allowing each voltage rail to operate within its required specification.

---

# 5. Decoupling Strategy

Power integrity depends heavily on proper local energy storage.

Each major integrated circuit includes multiple decoupling capacitors positioned close to its supply pins.

The objectives are:

- Supply transient current locally
- Reduce voltage ripple
- Minimize supply impedance
- Suppress high-frequency switching noise

Where multiple supply pins exist, each supply pin is locally decoupled according to the manufacturer recommendations.

---

# 6. Bulk Capacitance

In addition to local decoupling, bulk capacitors are placed on the primary supply rails.

These capacitors provide:

- Low-frequency energy storage
- Startup stability
- Load transient support

Bulk capacitance complements the local high-frequency decoupling network.

---

# 7. Power Distribution

Power routing was performed with the following priorities:

- Low impedance
- Short current paths
- Wide power traces where appropriate
- Continuous power planes
- Minimal voltage drop

Sensitive analog supplies were routed separately from noisy digital switching paths wherever practical.

---

# 8. Ground Strategy

A continuous ground plane forms the primary return path for all circuitry.

The ground system provides:

- Low return impedance
- Stable voltage reference
- Improved signal integrity
- Reduced electromagnetic emissions

Ground plane discontinuities beneath high-speed interfaces were avoided.

---

# 9. Startup Considerations

Reliable startup depends on all regulated rails reaching stable operating conditions before normal device operation begins.

The design considers:

- Regulator stabilization
- Power rail sequencing
- Device reset timing
- EEPROM availability during initialization

These factors ensure predictable system initialization after USB connection.

---

# 10. PCB Layout Considerations

Power distribution strongly influenced component placement.

Major layout practices include:

## Regulator Placement

Voltage regulators are positioned close to their primary loads to reduce supply path impedance.

---

## Decoupling Placement

Each decoupling capacitor is placed adjacent to its associated supply pin.

The routing between capacitor and IC supply pin is kept as short as practical.

---

## Power Plane Usage

Dedicated copper regions are used to distribute regulated supplies.

This reduces:

- IR drop
- Supply inductance
- Power distribution impedance

---

## Via Usage

Power vias are placed close to decoupling capacitors and supply pins to provide efficient current flow between PCB layers.

---

# 11. Verification

The power subsystem was verified for:

- Supply connectivity
- Regulator output routing
- Decoupling placement
- Power plane continuity
- Ground continuity
- ERC compliance
- DRC compliance

Particular attention was given to ensuring that every supply pin was connected to the correct voltage rail.

---

# 12. Design Philosophy

The power architecture follows three fundamental principles:

- Generate only the voltages required by the system.
- Deliver each voltage through a low-impedance distribution network.
- Decouple every active device as close to the load as possible.

These principles improve reliability, simplify debugging, and contribute to stable operation during high-speed communication.

---

# Related Documents

- 01_System_Architecture.md
- 02_Component_Selection.md
- 03_USB_Subsystem.md
- 04_Ethernet_Subsystem.md
- 06_EEPROM.md
- 07_PCB_Design.md