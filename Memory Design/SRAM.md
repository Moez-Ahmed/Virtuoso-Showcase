SRAM is a 6 transistor memory device primarily used in cache memory. Each bit is held by two cross-coupled inverters (6T cell) , state is maintained by active feedback

Both inverters hold state indefinitely as long as power is supplied so no refresh is needed, however, these devices are still volatile. Losing power corrupts any data stored

<img width="604" height="288" alt="Image" src="https://github.com/user-attachments/assets/4e841d09-728b-47e5-ad3e-35cc13dfc036" />

SRAM Operation:
Reading - Requires the Wordline fires, both access transistors open, the stored voltage appears on BL and BL̄ — a small differential develops

Writing - Requires the Wordline fires, write drivers force BL and BL̄ to opposite rails, overpowering the weak feedback inverters and flipping the cell state

One key reason why SRAM is used within memory systems is its stability and speed.

