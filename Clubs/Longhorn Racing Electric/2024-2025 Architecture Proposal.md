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
2. 22 Gauge wire to all fans
	1. Each fan on average pulls ~1W — At max speed assume RAD fans ~10W
	2. Current needed is 15W (leeway) / 24V $\approx$ 0.625A. Very comfortable for 22 gauge until ~50 ft.
		1. Assuming the 3.3V and 10A fans, we can still use 22 AWG up to ~25 ft. More than enough for the fans
3. 