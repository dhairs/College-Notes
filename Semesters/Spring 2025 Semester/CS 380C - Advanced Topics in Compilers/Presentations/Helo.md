Hello, CAN setup should be straightforward now!!!!!!!!!!!!

Longhorn Lib setup on [Notion](https://www.notion.so/lhrelectric/Longhorn-Lib-Setup-2025-18ee26707bba806cbc81e65fa6b64689?pvs=4) is updated with the setup instructions and the [CAN sheet](https://utexas.sharepoint.com/:x:/r/sites/ENGR-LonghornRacing/_layouts/15/Doc.aspx?sourcedoc=%7BE4600CD1-8229-483C-8B61-D76BD54DD0D5%7D&file=2025%20Data%20Flow.xlsx&action=default&mobileredirect=true&DefaultItemOpen=1%3Fweb%3D1) has *most* CAN packets listed. Some are still missing, will update when those are there but they shouldn't cause major changes. 

Follow the “Using the Specified CAN IDs for Communication” part of the notion page to set up sending packets with IDs.

All the CAN packets, precisions, and byte arrays are now auto generated and included with `night_can.h`. Use them so that if the CAN IDs ever update, your code should be fine.

For example:

| CAN ID | CAN ID Binary | From | To  | Packet Info | Frequency (Hz) | Data Length Code (DLC) | Quantity | Data[0]                            | Data[1] | Data[2]                           | Data[3] | Data[4]                            | Data[5] | Data[6]                           | Data[7] |
| ------ | ------------- | ---- | --- | ----------- | -------------- | ---------------------- | -------- | ---------------------------------- | ------- | --------------------------------- | ------- | ---------------------------------- | ------- | --------------------------------- | ------- |
| 0x101  | 100000001     | VCU  | Pi  | GPS         | 10             | 8                      | 1        | GPS Rear Longitude (int16, 0.001º) |         | GPS Rear Latitude (int16, 0.001º) |         | GPS Rear Speed (uint16, 0.001 m/s) |         | GPS Rear Heading (uint16, 0.001º) |         |
Will have the following corresponding definitions in the night_can library:

```c
// Packet: GPS  
#define GPS_ID 257  
#define GPS_DLC 8  
#define GPS_FREQ 100  
#define GPS_QUANTITY 1  
  
#define GPS_REAR_LONGITUDE_BYTE 0  
#define GPS_REAR_LONGITUDE_PREC 0.001f  
#define GPS_REAR_LONGITUDE_LENGTH 2  
#define GPS_REAR_LONGITUDE_TYPE int16_t  
  
#define GPS_REAR_LATITUDE_BYTE 2  
#define GPS_REAR_LATITUDE_PREC 0.001f  
#define GPS_REAR_LATITUDE_LENGTH 2  
#define GPS_REAR_LATITUDE_TYPE int16_t  
  
#define GPS_REAR_SPEED_BYTE 4  
#define GPS_REAR_SPEED_PREC 0.001f  
#define GPS_REAR_SPEED_LENGTH 2  
#define GPS_REAR_SPEED_TYPE uint16_t  
  
#define GPS_REAR_HEADING_BYTE 6  
#define GPS_REAR_HEADING_PREC 0.001f  
#define GPS_REAR_HEADING_LENGTH 2  
#define GPS_REAR_HEADING_TYPE uint16_t  
  
// End Packet: GPS
```

You can define the new packet with this:

```c
NightCANPacket gpsPacket = CAN_create_packet(GPS_ID, GPS_FREQ, GPS_DLC);
```

And you can make functions around this to access and update values:

```c
void updateRearLongitude(float newLong) {
	CAN_writeFloat(GPS_REAR_LONGITUDE_TYPE, &gpsPacket, GPS_REAR_LONGITUDE_BYTE, newLong, GPS_REAR_LONGITUDE_PREC);
}
```

This way, you don't have to worry about changing precisions or data ordering if any of that changes. If the packet's contents themselves change, you will need to update your code.

The same goes for receiving data.