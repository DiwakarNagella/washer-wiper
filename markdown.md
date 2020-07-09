Diagnostic Server for Common Data Identifiers - VOL_DIDServer
========


## Table of Contents
**[Overview](#Overview)**<br>
**[Module Initialization](#Module-Initialization)**<br>
**[Global Functions](#Global-Functions)**<br>
**[Internal Functions](#Internal-Functions)**<br>
**[Interfaces](#Interfaces)**<br>
**[Internal Data](#Internal-Data)**<br>
**[Configuration Data](#Configuration-Data)**<br>
**[Calibration Data](#Calibration-Data)**<br>
**[Version History](#Version-History)**<br>

-----------------------------

## Overview



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



### Module Inputs

| No.	| Variable			 | Description 		| Data Type	 	 | Init Value   | Dimension |
|:---	| :---:              | :--:             |:---:        	 | :--:         | ---:      |
|		| 			         | 			        |				 | 			    |			|
|		| 			         | 			        |				 | 			    |			|
### Module Outputs

| No.	| Variable			 | Description 		| Data Type	 	 | Init Value   | Dimension |
|:---	| :---:              | :--:             |:---:        	 | :--:         | ---:      |
|		| 			         | 			        |				 | 			    |			|
|		| 			         | 			        |				 | 			    |			|


## Internal Data



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