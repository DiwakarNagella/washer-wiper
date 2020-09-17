Fault Event gateway module maintains and broadcasts Active faults within the ECU
========


## Overview
Module maintains the Active Fault list for various Diagnostic Events using data structures and Broadcasts Active faults periodically and it is allowed to do that only when the vehicle mode is either RUNNING or PRE-RUNNING.    

![Introduction](images/Overview.png)

## Dynamic data provided by the Module:

Module Initializes the following dynamic data to their default values and periodically updates the data as Read from RTE (received from corresponding SWCs,CAN/ On board Sensors) and check if it is valid. Only Valid signals are considered.
Data is protected with CRC.


| Data				| Init Value			|  Description	 |
|:---				|:---:              	|  :---:        	 | 
|UTCTimeStamp		|UTC_NOT_AVAILABLE		 | Default value - 0xFF				 |
|OutdoorTemperature	|AAT_NA_MAX			 |Default value - 65535				 | 
|Odometer status	|TOTAL_VEHICLE_DISTANCE_HIGH_RES_DBC_DEFAULT			|Default value - 0xffffffffu				 | 
|Vehicle Mode		|VehicleMode_NotAvailable		|				 | 



## Static data provided by the Module:


### Application Software Identification and Build Version

| Module ID			| Part Number			| Build Version    | Description	 |
|:---				|:---:              	| :--:             | :---:        	 | 
|UFBL_MODULE_ID		|BOOTLOADER_PARTNUMBER	|None 			   |Bootloader Software				 |
|MSW_MODULE_ID		|MSW_PARTNUMBER			|BUILD_VERSION_MSW |Application Software				 | 
|CSW_MODULE_ID		|Part number			|None			   |optional module				 | 
		
### Application Data Identification and Buid ID

| Module ID			| Part Number				  | Build Version    | Description	 														 | 
|:---				|:---:              		  | :--:             | :---:        	 														 | 
|APP_MODULE_ID		|DATASET_PARTNUMBER			  |DATASET_BUILD_ID  |Data set - Configuration parameters									 |
|APP_MODULE_ID		|POSTBUILD_PARTNUMBER		  |POSTBUILD_BUILD_ID|Post build data area for Software Configuration						 | 
|APP_MODULE_ID		|SOUND_PARTNUMBER			  |None			     |Data area to handle the Sound data on IC								 |
|APP_MODULE_ID		|DWM_CONFIGURATION_PARTNUMBER |None			     |Dynamic Window manager data area to handle the pixel data.Only valid for IC.| 


### ECU Hardware Number

| Module ID			| Part Number				  | Serial Number    | Sub Module info	 | 
|:---				|:---:              		  | :--:             | :---:        	 | 		 
|HW_MODULE_ID		|HARDWARE_PARTNUMBER		  |HARDWARE_SERIAL_NO  |SUB_HW_MODULE_ID,Sub node Part number,Sub node serial number |

ECU hardware number includes the above information along with Sub node (LIN Slave) information. It is assumed that VOL_DIDServer module is running on ECU which implements LIN Master server.
Number of Sub modules depends on number of LIN slave nodes configured in that LIN cluster. Then the Hardware Number includes ID, Part number and Serial number of those many LIN Slaves apart from the main ECU hardware details.

## The following Section provides the details about ports and interfaces
## Provided C/S Ports:

| Port                                                        | Interface                           | C/S Operation               | Description |
|-------------------------------------------------------------|-------------------------------------|-----------------------------|-------------|
|CBStatusDTC_DemCallbackDTCStatusChanged                      | CallbackDTCStatusChange		    | DTCStatusChanged()          | Used by DEM to update the Event dtc status |


## Required C/S Ports:

| Port               	| Interface                	| C/S Operation        			| Description 	|
|--------------------	|--------------------------	|---------------------------------------|-------------	|
| GeneralEvtInfo 	| GeneralDiagnosticInfo 	|GetEventStatus(), GetDTCOfEvent() 	| Used only during module Init|
|Event_D1BR9_68_VOL_FaultEventGateway_ListFull |DiagnosticMonitor |SetEventStatus() | Used to inform DEM about Fault List status     |

## Provided S/R Ports:

| Port                        	| Interface                     	| DataType 	| Description 	|
|-----------------------------	|-------------------------------	|----------	|-------------	|
| DiagFaultStat                 	| DiagFaultStat_I                 	| DiagFaultStat         	|   Broadcast fault information    	|

## Required S/R Ports:

| Port                        	| Interface                     	| DataType 	| Description 	|
|-----------------------------	|-------------------------------	|----------	|-------------	|
| VehicleMode                 	| VehicleMode_I                 	| VehicleMode_T         	|   Received by CAN    	|


## Address Parameters Required Ports:

| Parameter                   	| Init Value 	| Description		|
|-----------------------------	|-------------	|-----------------------|
| P1BDU_DWMVehicleModes     	|      0       	|			|


## Mode Switch Ports (Required):

| Port                        	| Interface                   	| Mode Declarations                  	|
|-----------------------------	|-----------------------------	|------------------------------------	|
| Switch_ESH_ModeSwitch       	| BswM_MSI_ESH_Mode           	| STARTUP, WAKEUP, POSTRUN, SHUTDOWN 	|


## Usecases:

### DCM Use Case  
Diagnostic Communication Manager can Read the following data From VOL_DIDServer component. However Diagnostic Data Write services are not part of this module.

* ChassisId - Using DataServices_CHANO_Data_CHANO_ChassisId_ReadData() Parameter Port interface 


| Diagnostic Tester         	|    	|          DCM   		|    | VOL_DIDServer |
|-----------------------------	|----------------------	|-----------------------|--------------------|------------| 
|    RDBID 22 01 00		|	                     					|	Call DataServices_CHANO_Data_CHANO_ChassisId_ReadData()	|			    		 |	Reads Data from Address Parameter and returns back the response			|	


* OutdoorTemperature - Using DataServices_P1AFR_Data_P1AFR_OutdoorTemperature_ReadData() C/S interface   


| Diagnostic Tester         	|    	|          DCM   		|    | VOL_DIDServer |
|-----------------------------	|----------------------	|-----------------------|--------------------|------------| 
|    RDBID 22 11 02		|	                     					|	Call DataServices_P1AFR_Data_P1AFR_OutdoorTemperature_ReadData()	|			    		 |	Reads Data periodically from RTE and Updates local copy after validation and returns back as Diag response to DCM			|	


* VehicleMode - Using DataServices_P1AFT_Data_P1AFT_VehicleMode_ReadData() C/S interface     


| Diagnostic Tester         	|    	|          DCM   		|    | VOL_DIDServer |
|-----------------------------	|----------------------	|-----------------------|--------------------|------------| 
|    RDBID 22 11 00		|	                     					|	Call DataServices_P1AFT_Data_P1AFT_VehicleMode_ReadData()	|			    		 |	Reads Data periodically from RTE and Updates local copy after validation and returns back as Diag response to DCM			|	


* DataServices_P1ALA_Data_P1ALA_ECUHardwareNumber_ReadData() C/S interface


| Diagnostic Tester         	|    	|          DCM   		|    | VOL_DIDServer |
|-----------------------------	|----------------------	|-----------------------|--------------------|------------| 
|    RDBID 22 F1 91		|	                     					|	Call DataServices_P1ALA_Data_P1ALA_ECUHardwareNumber_ReadData()	|			    		 |	Reads Data from Memory and returns back the response ***			|	

### DEM Use Case  
Diagnostic Event Manager Needs UTC Time stamp information, Vehicle mode, Odometer status and Outside air temperature that might be part of Snapshot data for various DTCs 
DEM uses C/S ports to access the data.
