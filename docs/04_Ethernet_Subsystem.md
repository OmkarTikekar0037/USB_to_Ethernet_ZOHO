# Ethernet Subsystem

## 1. Introduction

The Ethernet subsystem implements the complete physical communication path between the LAN7801 USB-to-Ethernet controller and the external Gigabit Ethernet network.

The subsystem consists of the Ethernet MAC integrated within the LAN7801, the KSZ9031RNX Gigabit Ethernet PHY, the RGMII interface connecting both devices, the Ethernet magnetics, and the RJ45 connector.

Together, these components enable IEEE 802.3 compliant 10 Mbps, 100 Mbps and 1000 Mbps Ethernet communication.

---

# 2. Objectives

The Ethernet subsystem was designed with the following objectives:

- Reliable Gigabit Ethernet communication
- Short and well-controlled RGMII routing
- Stable PHY operation
- Proper clock distribution
- Robust power distribution
- Manufacturable PCB layout
- Compliance with recommended PHY layout practices

---

# 3. Ethernet Architecture

```

                LAN7801
           (Ethernet MAC)
                   │
                   │ RGMII
                   │
                   ▼
            KSZ9031RNX
          Gigabit Ethernet PHY
                   │
         MDI Differential Pairs
                   │
                   ▼
          RJ45 MagJack
      (Integrated Magnetics)
                   │
             Ethernet Cable

```

---

# 4. Ethernet MAC

The Ethernet Media Access Controller (MAC) is integrated within the LAN7801.

Its responsibilities include:

- Ethernet frame generation
- Frame reception
- CRC generation and verification
- Packet buffering
- DMA transfers
- Communication with the USB subsystem

The MAC communicates with the external PHY using the RGMII interface.

---

# 5. Gigabit Ethernet PHY

The KSZ9031RNX performs all Physical Layer (PHY) operations required for Ethernet communication.

Major responsibilities include:

- RGMII interface
- 10BASE-T operation
- 100BASE-TX operation
- 1000BASE-T operation
- Auto-negotiation
- Auto MDI/MDI-X
- Clock recovery
- Line encoding and decoding
- Cable interface

The PHY converts digital Ethernet frames into differential electrical signals suitable for transmission through twisted-pair Ethernet cable.

---

# 6. RGMII Interface

Communication between the LAN7801 and KSZ9031RNX occurs through the Reduced Gigabit Media Independent Interface (RGMII).

Signals include:

- GTX_CLK
- TX_CTL
- TXD[3:0]
- RX_CLK
- RX_CTL
- RXD[3:0]

The interface also includes:

- MDC
- MDIO

for PHY management and configuration.

---

# 7. MDIO Management Interface

The MDIO interface provides software access to the PHY registers.

Typical functions include:

- PHY identification
- Link status monitoring
- Auto-negotiation control
- Speed selection
- Duplex configuration
- Diagnostic information

This interface is intended for configuration and monitoring rather than high-speed data transfer.

---

# 8. Ethernet Magnetics

The RJ45 MagJack integrates the required isolation transformer and common-mode filtering components.

Its primary functions are:

- Galvanic isolation
- Common-mode noise rejection
- Impedance matching
- Differential signal coupling
- External Ethernet connection

The integrated solution simplifies PCB layout while reducing component count.

---

# 9. Clocking

Reliable Ethernet communication depends on accurate clock generation.

The subsystem utilizes a dedicated 25 MHz reference crystal connected to the PHY.

The PHY internally generates the clocks required for Ethernet operation and provides the necessary timing for communication with the MAC.

Proper crystal placement and routing were treated as critical PCB design constraints.

---

# 10. Power Distribution

The Ethernet subsystem utilizes multiple regulated supply rails.

These include:

- PHY Core Supply
- PHY Analog Supply
- PHY I/O Supply

Each supply rail is independently decoupled according to the manufacturer recommendations.

Special attention was given to minimizing noise coupling between analog and digital sections.

---

# 11. PCB Layout Considerations

Because the Ethernet subsystem contains multiple high-speed interfaces, PCB layout significantly influences system performance.

Major design considerations included:

## Component Placement

- PHY placed close to LAN7801
- Short RGMII routing
- Crystal located adjacent to PHY
- Magnetics positioned close to RJ45 connector

---

## RGMII Routing

The RGMII interface was routed with emphasis on:

- Short trace lengths
- Length matching
- Continuous reference planes
- Minimal vias
- Reduced skew

Signal timing requirements were considered throughout routing.

---

## Ethernet Differential Pairs

The four MDI differential pairs between the PHY and MagJack were routed using controlled impedance practices.

Routing objectives included:

- Constant pair spacing
- Length matching within each pair
- Minimal discontinuities
- Smooth routing geometry
- Continuous reference plane

---

## Return Current

Continuous ground reference planes were maintained beneath all high-speed Ethernet signals to provide low-inductance return paths.

Plane splits beneath critical routing were avoided.

---

## Crystal Placement

The reference crystal was positioned immediately adjacent to the PHY.

Routing between the PHY and crystal was kept short and symmetrical to minimize clock noise and improve oscillator stability.

---

# 12. Verification

The Ethernet subsystem underwent verification for:

- RGMII connectivity
- Differential pair polarity
- PHY power rails
- Crystal connections
- MDIO interface
- Strap pin configuration
- Decoupling placement
- Ethernet pair continuity
- ERC compliance
- DRC compliance

---

# 13. Summary

The Ethernet subsystem forms the communication bridge between the LAN7801 controller and the external Ethernet network.

The implementation emphasizes:

- Reliable Gigabit Ethernet communication
- Stable PHY operation
- Proper clock generation
- Controlled impedance routing
- Clean subsystem partitioning
- Manufacturable PCB layout

---

# Related Documents

- 01_System_Architecture.md
- 02_Component_Selection.md
- 03_USB_Subsystem.md
- 05_Power_Architecture.md
- 07_PCB_Design.md