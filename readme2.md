# VOL_DIDServer

## Overview

DID server module provides the following diagnostic data when requested using corresponding DIDs: 

* Application Software Identification (DID P1ALQ)
* Application Data Identification (DID P1ALP)
* Chassis Identification (DID CHANO)
* Vehicle Identification Number (DID VINNO)
* DescriptionFileSha256 (DID P1Q82)
* ECU Hardware Number (DID P1ALA)
* Engine Type (DID P1ALB)
* Build ID (DID P1URK)
* Boot Software Identification (DID P1B1O)
* Outdoor Temperature (DID P1AFR)
* Total Vehicle Distance (DID P1AFS)
* Vehicle Mode (DID P1AFT)
* Active Diagnostic Session (DID P1DIH)
* UTC TimeStamp

Chassis Identification and Vehicle Identification data is accessed both by using DID and address parameters.
Accessing through only DID is supported in this module. All the DIDs are readonly.

UTC TimeStamp is accessed internally by DEM using callback functions.

Provides software build information (ECU SW and data), Vehicle, Chassis and ECU hardware identification data
SEWS2 parameters are assigned to Application SWC containers
## Usecases

### Dynamic data

The following parameters are read periodically from RTE and stored locally along with calculated CRC.
Accessed by DEM as DTC snapshot data/Extended data and also by DCM when requested from external tool with corresponding DIDs:

*   Outdoor Temperature (DTC snapshot data)
*   Total Vehicle Distance (DTC snapshot data). The odometer value of distance
    driven since the assembly of the vehicle.
*   Vehicle Mode (DTC snapshot data)
*   UTCTimeStamp (DTC Extended Diagnostic Data)

Active Diagnostic Session (P1DIH) is updated when there is a change in the diagnostic session triggered by Diagnostic session control mode machine.

#### Related Requirements

* REQ-DIR-15 v6
* REQ-DIR-27 v4

#### Integration notes

Read by DEM using corresponding callback functions:
DCM reads the data using callback functions when requested
RTE ports for signals

### ECU Hardware Number

This service provides ECU hardware number which includes the following information:
* HW module ID
* HW Partnumber
* HW Serial number
* Sub node info (module id, serial number and slave node part number for LIN Slaves)

HW part number and HW serial number are stored in flash memory.
For both Chassis ECUs and ZYNQ, the corresponding linker files copy this into execution region.
Module reads the data from the RAM address. 

Number of Sub modules depends on number of LIN slave nodes configured in LIN Manager.
Requests LIN manager service for slave node information and waits for the server to respond back.
If LIN manager doesn't respond within the timeout, this module returns the ECU H/W info without LIN slave information.
It also handles reading of serial number
and slave node part number from each node using diagnostic requests.
It is assumed that VOL_DIDServer module is running on ECU which implements LIN Master server.

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

manufacturing info.h
linker_symbols.h

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

Requires generation of build_info.h.

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
