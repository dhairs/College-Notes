## Design
****
**Every board has a specific purpose (PDU for power, VCU for vehicle controls, etc.)**

**Harness built around the needs of each microcontroller/board. NOT built around the sensor placements themselves**

BSPD MANDATED

LOOK AT CAR IN CAD AND SEE COOLANT SENSORS/ETC AND RELEVANT BOARDS/LOCATIONS OF ITEMS THAT WE NEED TO BE USING TO SENSE
#### PDU

**In's**:
- 24V Power

**Out's**:
- Radiator 24V
- Brake Light 24V
- Battery Fans 24V
- Accessory 24V
- Pump 24V
- Shutdown Circuit

**CAN**:
**In's**
- PDU Cooling
- Brake Light
- Buzzer
- PDU Params (?)

**Out's**
- Thermals
- PDU IMU Accel
- PDU IMU Gyro
- LV Battery
- PDU Currents 1
- PDU Currents 2
- PDU Status

#### HVC
**In's**:
- isoSPI (BMBs)

**Out's**:


**CAN**:
**In's**
- HVC Params (?)

**Out's**
- AMS and IMD
- Pack Status
- HVC IMU Accel
- HVC IMU Gyro
- CCS Info
- Fan RPMs
- Cell Voltages
- Cell Temps
- Contactor State

#### VCU
**In's**:
- CAN

**Out's**:
- 3.3V
- 5V

**CAN**:
**In's**
- Inverter Temp Data 1 
- Inverter Temp Data 2
- Inverter Motor Positions
- Inverter Current
- Inverter Voltage
- Inverter State
- Inverter Faults
- Inverter Torque Timer
- Inverter High Speed Message
- Inverter Parameter Response
- AMS and IMD
- Pack Status
- HVC IMU Accel
- HVC IMU Gyro
- CCS Info
- Fan RPMs
- Cell Voltages
- Cell Temps
- Contactor State
- Thermals
- PDU IMU Accel
- PDU IMU Gyro
- LV Battery
- PDU Currents 1
- PDU Currents 2
- PDU Status
- FR Wheelspeed
- FR IMU Accel
- FL Wheelspeed
- FL IMU Accel
- BR Wheelspeed
- BR IMU Accel
- BL Wheelspeed
- BL IMU Accel

**Out's**
- HVC Params
- PDU Params
- Unsprung Params
- Dash Params
- Inverter Torque Command
- Inverter Parameter Request
- Brake Light
- Buzzer
- PDU Cooling
- HVC Cooling
- Dash Info 1
- Dash Info 2

#### Inverter
**In's**:
- 24V power

**Out's**:
- Power to motor (?)

**CAN:**
**In's**
- Inverter Torque Command
- Inverter Parameter Request

**Out's**:
- Inverter Temp Data 1
- Inverter Temp Data 2
- Inverter Motor Positions
- Inverter Current
- Inverter Voltage
- Inverter State
- Inverter Faults
- Inverter Torque Timer
- Inverter High Speed Message
