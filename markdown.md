Fault Event gateway module maintains and broadcasts Active faults within the ECU
========


## Overview
Module maintains the Active Fault list for various Diagnostic Events using data structures and Broadcasts Active faults periodically and it is allowed to do that only when the vehicle mode is either RUNNING or PRE-RUNNING and also depends on the parameter DWMVehicleModes. 

![Introduction](images/Overview.png)

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

### DEM Use Case  
## Initialization Behaviour:
This modules needs to be initialized only after DEM is initialized.
Module creates a Fault List (using Linked List) for various Diagnostic events as defined by DEM configuration Dem_Cfg_GlobalPrimaryFirst() and Dem_Cfg_GlobalPrimaryLast().
Fault entry is made for only those events for which the DTC status bit 'Failed" is set.

## Runtime Behaviour:
This modules updates the Fault list with new active faults as requested by DEM for those events with DTC status bit 'Failed' changes from 0 to 1. For those Events for which the DTC status bit 'Failed' changes from 1 to 0, and if the event is already captured in the Fault list, it will be removed from the List.

Fault list can store only NUM_DTC (Constant) number of faults in the list and once the list fills up then the last entry would be the FAULT_List_FULL DTC.

This modules broadcasts only 2 Active faults periodically to RTE.

If there are any new Events, then DEM informs this module about the new event status to be updated in the fault list.
