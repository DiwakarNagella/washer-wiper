Diagnostic Server for Common Data Identifiers - VOL_DIDServer
========
graph TD
    Start --> Stop

## Overview
Module provides static and dynamic diagnostic data to Diagnostic Communication Manager and Diagnostic Event Manager when requested.   

![Overview](/doc/images/Overview.png)

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
| CBReadData_UTCTimeStamp_First_Day                           | CSDataServices_UTCTimeStamp_Day     | ReadData()                  |             |
| CBReadData_UTCTimeStamp_First_Hour                          | CSDataServices_UTCTimeStamp_Hour    | ReadData()                  |             |
| CBReadData_UTCTimeStamp_First_Minutes                       | CSDataServices_UTCTimeStamp_Minutes | ReadData()                  |             |
| CBReadData_UTCTimeStamp_First_Month                         | CSDataServices_UTCTimeStamp_Month   | ReadData()                  |             |
| CBReadData_UTCTimeStamp_First_Seconds                       | CSDataServices_UTCTimeStamp_Seconds | ReadData()                  |             |
| CBReadData_UTCTimeStamp_First_Year                          | CSDataServices_UTCTimeStamp_Year    | ReadData()                  |             |
| CBReadData_UTCTimeStamp_Latest_Day                          | CSDataServices_UTCTimeStamp_Day     | ReadData()                  |             |
| CBReadData_UTCTimeStamp_Latest_Hour                         | CSDataServices_UTCTimeStamp_Hour    | ReadData()                  |             |
| CBReadData_UTCTimeStamp_Latest_Minutes                      | CSDataServices_UTCTimeStamp_Minutes | ReadData()                  |             |
| CBReadData_UTCTimeStamp_Latest_Month                        | CSDataServices_UTCTimeStamp_Month   | ReadData()                  |             |
| CBReadData_UTCTimeStamp_Latest_Seconds                      | CSDataServices_UTCTimeStamp_Seconds | ReadData()                  |             |
| CBReadData_UTCTimeStamp_Latest_Year                         | CSDataServices_UTCTimeStamp_Year    | ReadData()                  |             |
| DataServices_CHANO_Data_CHANO_ChassisId                     | DataServices_CHANO_Data_CHANO       | ReadData()                  |             |
| DataServices_P1AFR_Data_P1AFR_OutdoorTemperature            | DataServices_P1AFR_Data_P1AFR       | ReadData()                  |             |
| DataServices_P1AFS_Data_P1AFS_Odometer                      | DataServices_P1AFS_Data_P1AFS       | ReadData()                  |             |
| DataServices_P1AFT_Data_P1AFT_VehicleMode                   | DataServices_P1AFT_Data_P1AFT       | ReadData()                  |             |
| DataServices_P1ALA_Data_P1ALA_ECUHardwareNumber             | DataServices_P1ALA_Data_P1ALA       | ReadData() ReadDataLength() |             |
| DataServices_P1ALB_Data_P1ALB_SystemNameOrEngineType        | DataServices_P1ALB_Data_P1ALB       | ReadData()                  |             |
| DataServices_P1ALP_Data_P1ALP_ApplicationDataId             | DataServices_P1ALP_Data_P1ALP       | ReadData() ReadDataLength() |             |
| DataServices_P1ALQ_Data_P1ALQ_ApplicationSoftwareId         | DataServices_P1ALQ_Data_P1ALQ       | ReadData() ReadDataLength() |             |
| DataServices_P1B1O_Data_P1B1O_BootSWIdentifier              | DataServices_P1B1O_Data_P1B1O       | ReadData()                  |             |
| DataServices_P1DIH_Data_P1DIH_activeDiagnosticSessionDataId | DataServices_P1DIH_Data_P1DIH       | ReadData()                  |             |
| DataServices_VINNO_Data_VINNO_VIN                           | DataServices_VINNO_Data_VINNO       | ReadData()                  |             |
| DataServices_P1OLT_Data_P1OLT_BuildVersionInfo              | DataServices_P1OLT_Data_P1OLT       | ReadData()                  |             |
| DataServices_P1Q82_Data_P1Q82_DescriptionFileSha256         | DataServices_P1Q82_Data_P1Q82       | ReadData()                  |             |
| DataServices_P1URK_Data_P1URK_BuildIds                      | DataServices_P1URK_Data_P1URK       | ReadData() ReadDataLength() |             |


## Required C/S Ports:

| Port               	| Interface                	| C/S Operation                                                                                        	| Description 	|
|--------------------	|--------------------------	|------------------------------------------------------------------------------------------------------	|-------------	|
| LINMaster_Services 	| VOL_LINMaster_Services_I 	| RequestAllSlaveSnSnPn() FetchNoOfLinSlaves() FetchAllSlaveSnSnPnServerStatus() FetchAllSlaveSnSnPn() 	|             	|

## Required S/R Ports:

| Port                        	| Interface                     	| DataType 	| Description 	|
|-----------------------------	|-------------------------------	|----------	|-------------	|
| AmbientAirTemperature       	| AmbientAirTemperature_I       	|          	|             	|
| DayUTC                      	| DayUTC_I                      	|          	|             	|
| HoursUTC                    	| HoursUTC_I                    	|          	|             	|
| MinutesUTC                  	| MinutesUTC_I                  	|          	|             	|
| MonthUTC                    	| MonthUTC_I                    	|          	|             	|
| SecondsUTC                  	| SecondsUTC_I                  	|          	|             	|
| YearUTC                     	| YearUTC_I                     	|          	|             	|
| VehicleMode                 	| VehicleMode_I                 	|          	|             	|
| TotalVehicleDistanceHighRes 	| TotalVehicleDistanceHighRes+I 	|          	|             	|


## Address Parameters Required Ports:

| Parameter                   	| Init Value 	| Description	|
|-----------------------------	|-------------	|-------------	|
| P1C54_FactoryModeActive     	|      0       	|		|
| VINNO_VIN                   	|             	|		|
| X1CJT_EnableCustomDemCfgCrc 	|             	|		|
| CHANO_ChassisId             	|             	|		|


## Mode Switch Ports (Required):

| Port                        	| Interface                   	| Mode Declarations                  	|
|-----------------------------	|-----------------------------	|------------------------------------	|
| DcmDiagnosticSessionControl 	| DcmDiagnosticSessionControl 	| DEFAULT_SESSION, EXTENDED_SESSION  	|
| Switch_ESH_ModeSwitch       	| BswM_MSI_ESH_Mode           	| STARTUP, WAKEUP, POSTRUN, SHUTDOWN 	|


## Usecases:

| Func()-->                    	|                    			|           Description       			|
|-----------------------------	|-----------------------------	|------------------------------------	|
| 								| Func()-->					 	| 									  	|
| 						       	| 					           	| 	Func()-->	

			|


| Diagnostic Tester -->        	|    --------------->	|          DCM   	|   ---------------> | VOL_DIDServer |
|-----------------------------	|----------------------	|-----------------------|--------------------|----------------| 										
