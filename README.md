# Memory-Showcase
This Repository will simply be a journal of the most exciting memory work I've done with Cadence Virtuoso. The idea is to document and analyze my work to better understand the semiconductor design process. **I am working through this repo as of 2/24/2026 - I have added information on SRAM but expect to add the rest of the results by mid march**

Talking repo structure: Each folder contains a writeup on each memory type, to access a write-up for a specific device access the .md file

| Memory Type | Description | Tool | Process |
|---|---|---|---|
| SRAM + Peripherals | 6T cell with sense amplifier, precharge, and write driver; implemented in a 1kb array; schematic -> layout -> DRC/LVS -> PEX with post-layout performance comparison | Cadence Virtuoso | gpdk045 |
| DRAM + Peripherals | 1T1C cell with peripheral support circuits; implemented in a 1kb array; schematic -> layout -> DRC/LVS -> PEX with post-layout performance comparison | Cadence Virtuoso | gpdk045 |
| Gain Cell + Peripherals | 3T Gain Cell with peripheral support circuits; implemented in a 1kb array; schematic -> layout -> DRC/LVS -> PEX with post-layout performance comparison | Cadence Virtuoso | gpdk045 |
| FeCAP | Verilog-A behavioral model of a ferroelectric capacitor with an anti-ferroelectric/ferroelectric/anti-ferroelectric sandwich structure | Verilog-A, Sentaurus TCAD | — |














As all of the above are made using gpdk045, an example of SRAM designed using finfets would be added later
