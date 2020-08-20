Diagnostic Server for Common Data Identifiers - VOL_DIDServer
========


## Overview
Module provides constant and dynamic diagnostic data to Diagnostic Communication manager when requested by Diagnostic tester.   

![Overview](Overview.png)

Module Initializes the dynamic data to their default values and periodically updates the data as received from corresponding SWCs which inturn might receive the data either by CAN or Sensors.

## The following Static data provided by the Module:


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

## Provided C/S Ports:

| Port                                   | Interface                           | C/S Operation | Description |
|----------------------------------------|-------------------------------------|---------------|-------------|
| CBReadData_UTCTimeStamp_First_Day      | CSDataServices_UTCTimeStamp_Day     | ReadData()    |             |
| CBReadData_UTCTimeStamp_First_Hour     | CSDataServices_UTCTimeStamp_Hour    | ReadData()    |             |
| CBReadData_UTCTimeStamp_First_Minutes  | CSDataServices_UTCTimeStamp_Minutes | ReadData()    |             |
| CBReadData_UTCTimeStamp_First_Month    | CSDataServices_UTCTimeStamp_Month   | ReadData()    |             |
| CBReadData_UTCTimeStamp_First_Seconds  | CSDataServices_UTCTimeStamp_Seconds | ReadData()    |             |
| CBReadData_UTCTimeStamp_First_Year     | CSDataServices_UTCTimeStamp_Year    | ReadData()    |             |
| CBReadData_UTCTimeStamp_Latest_Day     | CSDataServices_UTCTimeStamp_Day     | ReadData()    |             |
| CBReadData_UTCTimeStamp_Latest_Hour    | CSDataServices_UTCTimeStamp_Hour    | ReadData()    |             |
| CBReadData_UTCTimeStamp_Latest_Minutes | CSDataServices_UTCTimeStamp_Minutes | ReadData()    |             |
| CBReadData_UTCTimeStamp_Latest_Month   | CSDataServices_UTCTimeStamp_Month   | ReadData()    |             |
| CBReadData_UTCTimeStamp_Latest_Seconds | CSDataServices_UTCTimeStamp_Seconds | ReadData()    |             |
| CBReadData_UTCTimeStamp_Latest_Year    | CSDataServices_UTCTimeStamp_Year    | ReadData()    |             |
|                                        |                                     |               |             |
|                                        |                                     |               |             |
