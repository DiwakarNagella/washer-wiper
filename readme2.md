# VOL_DIDServer

## Overview

Module acts as a server and provides static and dynamic diagnostic data to DCM and DEM when requested. 
Periodically recieves (from RTE) the following parameters, validates and protects the data with CRC.

* Outdoor Temperature (P1AFR)
* Total Vehicle Distance (P1AFS)
* Vehicle Mode (P1AFT)
* UTCTimeStamp

Provides software build information (ECU SW and data), Vehicle, Chassis and ECU hardware identification data

## Usecases

### Snapshot data
 
The following snapshot data is provided to DEM:

* Outdoor Temperature (P1AFR, 0x1102)
* Total Vehicle Distance (P1AFS, 0x1104). The odometer value of distance driven since the assembly of the vehicle.
* Vehicle Mode (P1AFT, 0x1100)

DEM reads the data using callback functions

#### Related Requirements

* REQ-DIR-15 v6  

#### Integration notes

### Extended data

UTCTimeStamp  which is one of the extended diagnostic data used for all DTCs is provided to DEM.
UTCTimeStamp is collection of various signals like Year, Month, Day, Hour, Minutes and Seconds.
DEM reads the data using callback function.

#### Related Requirements

* REQ-DIR-27 v4

#### Integration notes

### ECU Hardware Number

* ECU hardware number includes the following information along with Sub node (LIN Slave) information.
1 HW_MODULE_ID
2 HARDWARE_PARTNUMBER
3 HARDWARE_SERIAL_NO
4 SUB_HW_MODULE_ID,Sub node Part number,Sub node serial number(LIN Slaves)

* It is assumed that VOL_DIDServer module is running on ECU which implements LIN Master server.
* Number of Sub modules depends on number of LIN slave nodes configured in that LIN cluster.
* This module waits for the LIN Master to respond back with LIN slave info untill the timeout.
* If LIN master doesn't respond within the timeout, this module returns the ECU H/W info without LIN slave information.

#### Related Requirements

* REQ-LNI_verification-2 v2
* REQ-LNI_SN-4 v3
* REQ-LNI_SN-5 v3
* REQ-LNI_SNPN-4 v2
* REQ-LNI_readout-10 v1
* REQ-LNI_readout-1 v1
* REQ-LNI_readout-2 v2
* REQ-LNI_readout-3 v2
* REQ-LNI_readout-7 v2
* REQ-SS-9 v3

#### Integration notes


### Application Software Identification 

Provides the following information about Bootloader, MSW and CSW modules:
* Part number
* Module ID
* Build version

#### Related Requirements

* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1

#### Integration notes
		
### Application Data Identification

Provides the following information about application data:
* DATASET_PARTNUMBER DATASET_BUILD_ID
* POSTBUILD_PARTNUMBER POSTBUILD_BUILD_ID
* SOUND_PARTNUMBER
* Diagnostic Warning Manager configuration data PARTNUMBER

#### Related Requirements
* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1

#### Integration notes

### DCM Use Case  
Diagnostic Communication Manager can request above mentioned diagnostic data along with ChassisId and VIN. 
However Diagnostic Data Write services are not part of this module.

#### Related Requirements
* REQ-OBD-115 v1 - for OBD ECUs
* REQ-EOALP-18 v1 - Non OBD ECUs

## More Information

### Technical References
For functionality, API and configuration of the AUTOSAR BSW module, refer Vector technical references which can be found in ECU SIP. The following documents were referred.

* TechnicalReference_Dem.pdf
* TechnicalReference_Dcm.pdf

### SEWS

See the actual version used in ContainerInfo.xml, convenience link to version [10.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=27734)
