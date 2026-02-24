# Virtuoso-Showcase
This Repository will simply be a journal of the most exciting work I've done with Cadence Virtuoso. The idea is to document and analyze my work to better understand the semiconductor design process. **I am working through this repo as of 2/24/2026 - I have added information on SRAM but expect to add the rest of the results by mid march**

Talking repo structure: Each folder contains a writeup on each memory type, to access a write-up for a specific device access the .md file

| Memory Type | Description | Tool | Process |
|---|---|---|---|
| SRAM + Peripherals | 6T cell with sense amplifier, precharge, and write driver; implemented in a 1kb array; schematic -> layout -> DRC/LVS -> PEX with post-layout performance comparison | Cadence Virtuoso | gpdk045 |
| DRAM + Peripherals | 1T1C cell with peripheral support circuits; implemented in a 1kb array; schematic -> layout -> DRC/LVS -> PEX with post-layout performance comparison | Cadence Virtuoso | gpdk045 |
| Gain Cell + Peripherals | 3T Gain Cell with peripheral support circuits; implemented in a 1kb array; schematic -> layout -> DRC/LVS -> PEX with post-layout performance comparison | Cadence Virtuoso | gpdk045 |
| FeCAP | Verilog-A behavioral model of a ferroelectric capacitor with an anti-ferroelectric/ferroelectric/anti-ferroelectric sandwich structure | Verilog-A, Sentaurus TCAD | — |




| Circuit | Key Specs & Design Decisions | Tool | Process |
|---|---|---|---|
| Sense Amplifiers | Three topologies implemented and compared: gated diode, voltage latch, and current mirror sense amplifier; analysis covers input-referred offset, regeneration speed, and noise sensitivity; topology selection rationalized against SRAM read SNM budget and bitline swing requirements | Cadence Virtuoso | gpdk045 |
| Folded Cascode OTA | Designed to target specifications for DC gain, unity gain bandwidth, and phase margin; bias network sized for headroom across corners; AC analysis includes gain/phase Bode plots and stability verification; schematic → layout → DRC/LVS → PEX with post-layout AC performance comparison | Cadence Virtuoso | gpdk045 |
| 8-bit SAR ADC | Comparator designed as a dynamic latch with kickback noise mitigation; capacitive DAC sized for unit capacitor matching and linearity; control logic implemented for successive approximation sequencing; performance characterized via DNL/INL plots and FFT-based SNDR/ENOB analysis; schematic → layout → DRC/LVS → PEX with post-layout linearity comparison | Cadence Virtuoso | gpdk045 |
| Integer-N PLL | Sub-blocks designed and characterized independently — VCO with Kvco extraction, charge pump with current mismatch analysis, PFD with dead zone evaluation, and loop filter sized from target bandwidth and phase margin; closed-loop analysis covers lock time, phase noise, and reference spur rejection; schematic → layout → DRC/LVS → PEX | Cadence Virtuoso | gpdk045 |

