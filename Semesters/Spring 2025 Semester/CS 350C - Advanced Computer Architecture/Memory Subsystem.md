## Device Level

Recall the basic organization of a DRAM device, from the [[Main Memory]] lecture.

Bits of data are stored on a 1T1C (1 transistor 1 capacitor) cell. The capacitance is extremely small, about 20 femto farads. There is parasitic resistance, so slowly the capacitor will leak and discharge. For this reason, the capacitor must also be periodically refreshed, the interval of which is directly proportional to temperature.

## Sense Amplifiers


## Access Steps in DRAM Devices

1. Sense bit values of cells in a row, open the row.
2. Restore values. Perform reads or writes on the opened row.
3. Pre-charge sense amplifiers, close the row.

Voltage mode sense amps.

### Step 1: Sense

Start with $EQ=0$

### Step 2a: Restore and Read

Activate chip select (CS, much like UART) to connect amplified value to the output. 

Restore the value from the capacitor to its original state: keep the wordline active and maintain the voltages on the bitlines for a minimum period of time ($t_{\text{ras}}$).  After this time, the row can be closed with a pre-charge operation.

Need to wait for values to stabilize on the bitlines before reading or writing—this is called $t_{\text{RCD}}$.

### Step 2b: Write to an Active Row

Wordline and chip select stay asserted. In addition, Write Enable (WE) is enabled, this activates the transistor that controls access to the write buffer of the bitline. The $\text{input}$ and $\neg \text{input}$ signals update the stored value in the cell. This takes $t_{\text{WR}}$ to finish, and the row is pre-charged after.

### Step 3: Pre-charge Sense Amplifiers

This needs to happen between row activations. CS, WE, wordline, all de-asserted. EQ is active. This sets both bitlines to $\frac{V_{DD}}{2}$: this is a metastable condition that will be changed by the small charge from the capacitor and amplified using the feedback loop in step 1 The row precharge time $t_{RP}$ is the amount of time needed to pass for the bitlines to be set to $\frac{V_{DD}}{2}$.