Few key changes from [[Angelique LV Architecture|Angelique's architecture]].

Motivation: Save weight, space, materials. Streamline debugging hardware.

## Design
****
**Every board can have *multiple* purposes (board closest to pedals can read pedal readings and manage motor output, etc.)**

**Harness built around each sensor and auxiliary device (unsprung boards, inverter, etc.)**


## Ideas
****
1. Remove PDU board
	1. HVC should stay — isoSPI for BMBs
	2. HVC connects to car with can and can control 24V power to rest of the car