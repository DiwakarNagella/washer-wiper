VOL_DIDServer

# Overview

Module provides the following diagnostic data to DCM and DEM when requested:

* Application Software Identification(P1ALQ)
* Application Data Identification(P1ALP)
* Chassis Identification
* Vehicle Identification Number
* DescriptionFileSha256(P1Q82)
* ECU Hardware Number(P1ALA)
* Engine Type(P1ALB)
* Build ID(P1URK)
* Boot Software Identification(P1B1O)
* Outdoor Temperature(P1AFR)
* Total Vehicle Distance(P1AFS)
* Vehicle Mode(P1AFT)
* Active Diagnostic Session(P1DIH)
* UTCTimeStamp

## Usecases

### Snapshot data
 
OutdoorTemperature	
Odometer value (TOTAL_VEHICLE_DISTANCE_HIGH_RES) 
Vehicle Mode		

##### Related Requirements
* REQ-DIR-15 v6  

### Extended data

UTCTimeStamp

##### Related Requirements
* REQ-DIR-27 v4

### Application Software Identification and Build Version

UFBL_MODULE_ID		|BOOTLOADER_PARTNUMBER	|None 			   |Bootloader Software				 |
MSW_MODULE_ID		|MSW_PARTNUMBER			|BUILD_VERSION_MSW |Application Software				 | 
CSW_MODULE_ID		|Part number			|None			   |optional module				 | 

#### Related Requirements
* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1
		
### Application Data Identification and Buid ID


APP_MODULE_ID		|DATASET_PARTNUMBER			  |DATASET_BUILD_ID  |Data set - Configuration parameters									 |
APP_MODULE_ID		|POSTBUILD_PARTNUMBER		  |POSTBUILD_BUILD_ID|Post build data area for Software Configuration						 | 
APP_MODULE_ID		|SOUND_PARTNUMBER			  |None			     |Data area to handle the Sound data on IC								 |
APP_MODULE_ID		|DWM_CONFIGURATION_PARTNUMBER |None			     |Diagnostic Warning Manager configuration | 

#### Related Requirements
* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1

#### ECU Hardware Number

| Module ID			| Part Number				  | Serial Number    | Sub Module info	 | 
|:---				|:---:              		  | :--:             | :---:        	 | 		 
|HW_MODULE_ID		|HARDWARE_PARTNUMBER		  |HARDWARE_SERIAL_NO  |SUB_HW_MODULE_ID,Sub node Part number,Sub node serial number |

* ECU hardware number includes the above information along with Sub node (LIN Slave) information.
* It is assumed that VOL_DIDServer module is running on ECU which implements LIN Master server.
* Number of Sub modules depends on number of LIN slave nodes configured in that LIN cluster.
* Hardware Number includes ID, Part number and Serial number of those many LIN Slaves and main ECU hardware details.
* This module waits for the LIN Master to respond back with LIN slave info untill the timeout.
* If LIN master doesn't respond within the timeout, this module returns the ECU H/W info without LIN slave information.

##### Related Requirements
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
