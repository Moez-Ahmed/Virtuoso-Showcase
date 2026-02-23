# 6T SRAM Cell Design & Analysis in Cadence Virtuoso

## Overview

Static Random-Access Memory (SRAM) is a six-transistor memory cell primarily used in cache memory, register files, and other performance-critical storage. Each bit is held by a pair of cross-coupled inverters, where state is maintained through active feedback — no periodic refresh is required, unlike DRAM. SRAM remains volatile, however; any stored data is lost when power is removed.

<p align="center">
  <img width="604" alt="6T SRAM Cell Schematic" src="https://github.com/user-attachments/assets/4e841d09-728b-47e5-ad3e-35cc13dfc036" />
</p>

The 6T cell consists of three transistor pairs, each with a distinct role:

| Transistor Pair | Label | Role |
|---|---|---|
| Pull-Up (PMOS) | PU | Pulls the storage node to V<sub>DD</sub> — maintains the high state |
| Pull-Down (NMOS) | PD | Pulls the storage node to GND — maintains the low state |
| Access (NMOS) | AX | Pass gates controlled by the wordline — connects the cell to the bitlines during read/write |

---

## SRAM Operation

### Hold

When the wordline (WL) is low, both access transistors are off and the cell is isolated from the bitlines. The cross-coupled inverters reinforce each other through positive feedback, holding the stored value indefinitely as long as V<sub>DD</sub> is supplied.

### Read

The wordline fires high, turning on both access transistors. Both bitlines (BL and BL̄) are precharged to V<sub>DD</sub> before the read. Once the access transistors open, the storage nodes begin to discharge one bitline through the pull-down path while the other remains high. A small differential voltage develops across BL and BL̄, which a sense amplifier detects and resolves into a full logic level.

> **Read stability concern:** During a read, the access transistor and pull-down transistor form a voltage divider at the storage node holding '0'. If this intermediate voltage rises above the trip point of the opposing inverter, the cell can flip — this is a **destructive read**. This is directly governed by the **cell ratio (CR = PD/AX)**.

### Write

The wordline fires high and write drivers force BL and BL̄ to opposite rails. The write driver must be strong enough to overpower the feedback loop and flip the cell. The access transistor works with the write driver against the pull-up transistor of the side being written low.

> **Write-ability concern:** If the pull-up transistor is too strong relative to the access transistor, the write driver cannot pull the internal node low enough to trip the opposing inverter, and the write fails. This is governed by the **pull-up ratio (PR = PU/AX)**.

---

## Static Noise Margin (SNM)

The Static Noise Margin quantifies how much DC noise voltage the cell can tolerate at its internal nodes before the state flips. It is extracted by plotting the voltage transfer characteristics (VTCs) of the two cross-coupled inverters against each other — forming a **butterfly curve** — and measuring the side of the largest square that fits inside the smaller lobe.

A larger SNM means greater noise immunity and a more robust cell.

### Hold SNM

- **Condition:** WL = 0 (access transistors off, cell isolated).
- **What it measures:** The inherent stability of the cross-coupled inverter pair without any external disturbance.
- **Expectation:** This is the best-case SNM. The butterfly curve should be wide and symmetrical, yielding the largest noise margin of the three modes.

<!-- Hold SNM butterfly curve image placeholder -->
<!-- <p align="center"><img width="500" alt="Hold SNM" src="" /></p> -->

### Read SNM

- **Condition:** WL = 1, bitlines precharged (simulates a read access).
- **What it measures:** How much noise the cell can tolerate during a read without flipping. The voltage divider formed by AX and PD raises the low-side storage node, compressing the butterfly curve.
- **Expectation:** Read SNM is significantly lower than hold SNM. A poor cell ratio leads to a collapsed or negative read SNM, meaning the cell cannot be read without risk of corruption.

<!-- Read SNM butterfly curve image placeholder -->
<!-- <p align="center"><img width="500" alt="Read SNM" src="" /></p> -->

### Write SNM

- **Condition:** WL = 1, one bitline driven to 0 (simulates a write).
- **What it measures:** The ability of the write driver to upset the cell. Unlike read and hold, a *smaller* write SNM (or a collapsed butterfly curve) actually indicates **easier writing**. If the write SNM is too large, the cell is too stable to be written.
- **Note:** Write margin is sometimes characterized separately as **Write Trip Point (WTP)** or **Write Noise Margin (WNM)** rather than by the butterfly method, depending on the methodology.

<!-- Write SNM butterfly curve image placeholder -->
<!-- <p align="center"><img width="500" alt="Write SNM" src="" /></p> -->

---

## Transistor Sizing & Design Trade-offs

Proper sizing of PU, PD, and AX transistors is critical because read stability and write-ability impose **opposing constraints** on the access transistor strength.

### Cell Ratio (CR) — Read Stability

$$CR = \frac{W_{PD} / L_{PD}}{W_{AX} / L_{AX}}$$

- A **higher CR** (stronger pull-down relative to access) keeps the internal '0' node low during a read, improving read SNM.
- Typical target: CR ≥ 1.2–2 depending on the process and voltage.
- Trade-off: increasing PD width costs area.

### Pull-Up Ratio (PR) — Write-ability

$$PR = \frac{W_{PU} / L_{PU}}{W_{AX} / L_{AX}}$$

- A **lower PR** (weaker pull-up relative to access) makes it easier for the write driver to pull the node low and flip the cell.
- Typical target: PR ≤ 1.
- Trade-off: weakening PU too much degrades hold SNM and increases leakage sensitivity.

### The Fundamental Tension

| Want | Requires | Conflicts with |
|---|---|---|
| Strong read stability | Weak AX or strong PD | Write-ability (need strong AX to write) |
| Easy write | Strong AX or weak PU | Read stability (strong AX worsens read SNM) |
| Good hold stability | Strong PU and PD | Area, write-ability |

The designer must find a sizing sweet spot where all three margins are acceptable. This is typically done through parametric sweeps in simulation — varying W<sub>PD</sub>, W<sub>PU</sub>, and W<sub>AX</sub> and plotting the resulting SNMs to identify the viable design space.

---

## Simulation Details

- **Tool:** Cadence Virtuoso (Schematic & ADE)
- **Process:** <!-- Add your PDK/process node here, e.g. GPDK 45nm -->
- **V<sub>DD</sub>:** <!-- e.g. 1.0V -->
- **Analysis:** DC sweeps for butterfly curves, transient simulations for read/write verification

---

## Results

*Results and butterfly curve plots to be added as simulations are completed.*

---

## References

- Weste & Harris, *CMOS VLSI Design: A Circuits and Systems Perspective*
- Rabaey, Chandrakasan & Nikolić, *Digital Integrated Circuits*
- Seevinck, List & Lohstroh, "Static-Noise Margin Analysis of MOS SRAM Cells," *IEEE JSSC*, 1987
