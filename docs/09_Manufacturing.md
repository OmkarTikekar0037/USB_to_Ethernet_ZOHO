# Manufacturing

## 1. Introduction

This document summarizes the manufacturing deliverables and design checks performed prior to PCB fabrication and assembly.

The objective is to ensure that the completed PCB design can be transferred to a PCB manufacturer and assembler without introducing avoidable production errors.

---

# 2. Manufacturing Outputs

The following manufacturing files are generated from the PCB design.

| Output | Purpose |
|----------|----------|
| Gerber Files | PCB fabrication |
| Drill Files | Hole and via locations |
| Bill of Materials (BOM) | Component procurement |
| Pick and Place (Position) File | Automated component assembly |
| Assembly Drawings | Manual and automated assembly reference |

These files collectively describe the physical implementation of the design.

---

# 3. Design Rule Verification

Before releasing the design for manufacturing, the PCB was verified using KiCad's Design Rule Check (DRC).

The review included:

- Minimum trace width
- Minimum spacing
- Via dimensions
- Pad clearances
- Copper-to-edge clearance
- Silkscreen overlap
- Unconnected nets

The objective was to eliminate layout violations prior to fabrication.

---

# 4. Electrical Verification

Electrical Rule Check (ERC) was performed on the schematic before PCB release.

Verification included:

- Power pin connections
- Driver conflicts
- Floating inputs
- Missing connections
- Net consistency
- Component annotation

This ensured consistency between the schematic and PCB implementation.

---

# 5. Footprint Verification

Each component footprint was reviewed against the manufacturer's mechanical drawings.

Verification included:

- Package dimensions
- Pin numbering
- Orientation
- Pad geometry
- Courtyard clearance

Particular attention was given to fine-pitch integrated circuits and the USB Type-A connector.

---

# 6. Assembly Considerations

The PCB layout was developed with automated assembly in mind.

Considerations included:

- Consistent component orientation where practical
- Adequate spacing between components
- Clear reference designators
- Accessible fiducial locations
- Proper polarity markings for polarized components

These practices simplify inspection and reduce assembly errors.

---

# 7. PCB Fabrication Requirements

The PCB was designed for fabrication using the following characteristics:

| Parameter | Value |
|-----------|-------|
| PCB Layers | 4 |
| Surface Finish | ENIG *(or manufacturer selected)* |
| Copper Weight | 1 oz *(unless otherwise specified)* |
| PCB Material | FR-4 |
| PCB Thickness | 1.6 mm *(design target)* |
| Controlled Impedance | Required |

Final fabrication parameters should be confirmed with the selected PCB manufacturer.

---

# 8. Assembly Inspection

Prior to electrical testing, the assembled PCB should be visually inspected for:

- Component orientation
- Missing components
- Solder bridges
- Tombstoned passive components
- Fine-pitch solder quality
- Connector alignment
- Mechanical damage

Any visible defects should be corrected before applying power.

---

# 9. Pre-Power Checks

Before connecting the board to a USB host, the following inspections are recommended:

- Verify power-to-ground resistance
- Check for shorts between supply rails
- Confirm regulator output continuity
- Inspect USB differential pair routing
- Inspect Ethernet differential pair routing
- Verify crystal installation
- Verify EEPROM orientation

These checks reduce the likelihood of damage during first power-up.

---

# 10. Manufacturing Checklist

The following checklist should be completed before releasing the design.

| Item | Status |
|--------|--------|
| ERC Passed | ✓ |
| DRC Passed | ✓ |
| Component Annotation Complete | ✓ |
| Footprints Verified | ✓ |
| BOM Generated | ✓ |
| Pick and Place File Generated | ✓ |
| Gerbers Generated | ✓ |
| Drill Files Generated | ✓ |
| Final Design Review Completed | ✓ |

---

# 11. Revision Control

All manufacturing files should correspond to a single tagged hardware revision.

For each hardware revision, archive:

- Schematic
- PCB layout
- Gerber package
- Drill files
- BOM
- Pick and Place file
- Manufacturing notes

This ensures complete traceability of released hardware.

---

# 12. Summary

The manufacturing package represents the transition from design to physical hardware.

Completing the verification and documentation steps described above reduces fabrication risk, simplifies assembly, and improves the likelihood of successful first-pass hardware bring-up.

---

# Related Documents

- 05_Power_Architecture.md
- 07_PCB_Design.md
- 08_Signal_Integrity.md