# Project History

## Introduction

This document records the engineering journey of the USB 3.1 Gen 1 to Gigabit Ethernet Adapter project.

Rather than serving as a development log or commit history, this document explains the reasoning behind major design decisions, architectural choices, and the evolution of the hardware throughout the project lifecycle.

Its purpose is to preserve engineering knowledge that would otherwise be lost after the project is completed.

---

# 1. Initial Objective

The objective of this project was to design a custom USB 3.1 Gen 1 to Gigabit Ethernet Adapter PCB capable of providing reliable Gigabit Ethernet connectivity over a USB interface.

The primary deliverable was a fabrication-ready hardware design rather than firmware or software.

From the beginning, emphasis was placed on understanding the complete hardware architecture instead of merely reproducing a reference design.

---

# 2. Design Philosophy

Several principles guided the development of this project.

- Every component should have a defined purpose.
- Every connection should be understood before implementation.
- Datasheets should be treated as the primary source of information.
- Reference designs should be studied, not blindly copied.
- PCB layout should be driven by signal integrity requirements rather than aesthetics.
- The design should remain maintainable and easy to review.

This philosophy significantly increased the design time but resulted in a much deeper understanding of the hardware.

---

# 3. Learning Before Designing

The project began with an extensive study phase.

Instead of immediately creating schematics, each major integrated circuit was studied individually.

Topics included:

- Device architecture
- Pin functions
- Power requirements
- Clock requirements
- Reset sequencing
- Configuration methods
- Interface standards
- Recommended layout practices

Only after understanding these topics was schematic capture started.

---

# 4. System Partitioning

Rather than viewing the adapter as a single PCB, it was divided into several independent functional blocks.

These blocks included:

- USB Interface
- Ethernet Controller
- Gigabit PHY
- Power Supply
- EEPROM
- Clock Generation
- Ethernet Magnetics
- Protection Circuits

Treating each subsystem independently simplified both design and verification.

---

# 5. Schematic Development

The schematic was developed incrementally.

Instead of completing one large schematic, each subsystem was reviewed multiple times before proceeding to the next.

Particular attention was given to:

- Power connections
- Decoupling capacitors
- Pull-up and pull-down resistors
- Strap pins
- Clock circuitry
- Reset circuitry
- Differential pair connectivity

Multiple iterations were performed before considering the schematic complete.

---

# 6. PCB Design

PCB development focused on achieving a layout suitable for high-speed digital communication.

Major considerations included:

- Four-layer stack-up
- Continuous reference planes
- Controlled impedance routing
- Return current paths
- Component placement
- Differential pair matching
- Power integrity
- Manufacturability

Placement was finalized before routing began.

Routing was performed subsystem by subsystem instead of net by net.

---

# 7. Verification

Before manufacturing, every stage of the design underwent verification.

Verification included:

- Electrical Rule Check (ERC)
- Design Rule Check (DRC)
- Net connectivity review
- Power rail verification
- Differential pair inspection
- Decoupling placement review
- Connector orientation verification

The objective was to eliminate preventable manufacturing issues before fabrication.

---

# 8. Current State

At the current stage, the hardware design has reached fabrication readiness.

The remaining work primarily consists of:

- Final manufacturing review
- PCB fabrication
- Assembly
- Hardware bring-up
- Functional validation
- Performance testing

---

# 9. Future Documentation

The remainder of the project documentation expands each subsystem individually.

Separate documents describe:

- System Architecture
- USB Subsystem
- Ethernet Subsystem
- Power Architecture
- PCB Design Methodology
- Signal Integrity Considerations
- Manufacturing Preparation
- Debugging History

Together these documents form the complete engineering record of the project.