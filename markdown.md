Diagnostic Server for Common Data Identifiers - VOL_DIDServer
========


## Overview
Module provides the


## Module Initialization



## Global Functions

### VOL_DIDServer_Init

#### Arguments
	 - Void
#### Returntype
	 - Void
	
#### Description
	
+ During Power-on-reset OR when the CRC is not valid Set the following to default values
		vehicleMode - VehicleMode_NotAvailable
		ambAirTemp -  AAT_NA_MAX
		totalDistance - TOTAL_VEHICLE_DISTANCE_HIGH_RES_DBC_DEFAULT
		utcTime - UTC_NOT_AVAILABLE
      
+ Update the CRC of m_noInitVars  
	
+ Set the Diagnostic default session

   	

### Global Function2


## Internal Functions

### fillPartNumber

#### Arguments
	- uint8** pDestPtr 
	- const uint8 IdType
	- const uint8* partNumber
#### Returntype
	- void
#### Description
	
	Copy the partNumber into the destination location

### Internal Function2

## Interfaces



### Application Software Identification and Build Version

| Module ID			| Part Number			| Build Version    | Description	 | 
|:---				|:---:              	| :--:             | ---:        	 | 
|UFBL_MODULE_ID		|BOOTLOADER_PARTNUMBER	|None 			   |				 |
|MSW_MODULE_ID		|MSW_PARTNUMBER			|BUILD_VERSION_MSW |				 | 
|CSW_MODULE_ID		|Part number			|None			   |				 | 
		
### Application Data Identification and Buid ID

| Module ID			| Part Number				  | Build Version    | Description	 														 | 
|:---				|:---:              		  | :--:             | ---:        	 														 | 
|APP_MODULE_ID		|DATASET_PARTNUMBER			  |DATASET_BUILD_ID  |Data set - Configuration parameters									 |
|APP_MODULE_ID		|POSTBUILD_PARTNUMBER		  |POSTBUILD_BUILD_ID|Post build data area for Software Configuration						 | 
|APP_MODULE_ID		|SOUND_PARTNUMBER			  |None			     |Data area to handle the Sound on IC									 |
|APP_MODULE_ID		|DWM_CONFIGURATION_PARTNUMBER |None			     |Dynamic Window manager data area to handle the pixel data.Valid for IC.| 


## ECU Hardware Number



| No.	| Variable			 | Description 		| Data Type	 	 | Init Value   | Dimension |
|:---	| :---:              | :--:             |:---:        	 | :--:         | ---:      |
|		| 			         | 			        |				 | 			    |			|
|		| 			         | 			        |				 | 			    |			|


## Configuration Data



| No.	| Parameter			 | Description 		| Data Type	 	| Value 		| Dimension |
|:---	| :---:              | :--:             |:---:         	| :--:          | ---:      |
|		| 			         | 			        |				| 			    |			|
|		| 			         | 			        |				| 			    |			|	


## Calibration Data



| No.	| Parameter			 | Description 		| Data Type	 	| Value 		| Dimension |
|:---	| :---:              | :--:             |:---:         	| :--:          | ---:      |
|		| 			         | 			        |				| 			    |			|
|		| 			         | 			        |				| 			    |			|	

## ENUMs



| No.	| Variable			 | Description 		| 
|:---	| :---:              | --:              |
|		| 			         | 			        |
|		| 			         | 			        |

## Version History


1.0.0 (Date):

+	Changed the init function 

	**NOTE**: This change affects the initialization behaviour of the module.