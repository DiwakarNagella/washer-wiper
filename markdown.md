# VOL_FaultEventGateway (FEG)

## Overview

* The FEG keeps active DTC in a list and sends the DTCs to the DiagnosticWarningManager periodically.
* This also functions as an alive signal.
* Dem updates the DTC list when the status for a DTC is changed.

## Usecases

### List with active DTCs

* Dem uses a callback whenever the status for a DTC changes so that FEG can update the internal list.
* When the number of DTCs that are periodically sent reaches 29 which is considered as list is full.
* If the list gets full, FEG discards DTCs and creates a DTC(D1BR9_68) to inform the cluster that there is an overflow.
* During initialization, the DTC(D1BR9_68) is reported as TestPassed to the DEM in order to clear the previous fault.
* This specific DTC set by this component is the last DTC of the 30 DTCs handled by this component.
* There might be more than 30 DTCs set and active in the DEM, but this component will only send the 30 first DTCs.

#### Related Requirements

* LD_Req-5622 v5
* LD_Req-21508 v1 - DTCs are limited to 30 to fulfill the requirement of presenting DWM related messages to the driver within 3 seconds.

#### Integration Notes

* DTCs configured in Dem with the WIB bit set (set by default by SEWS).
* SEWS container with the DTC
* Service port GeneralEventInfo (GetDTCOfEvent & GetEventStatus) connected to Dem
* FEG needs to be initialized after the DEM is initialized.
* Connect Serverice port of DEM to report D1BR9_68.

### Send Diagnostic Fault Status

* The FEG cycles the internal list and initiates sending every 100 ms.
* If there are no active faults, the signal is empty (the signal is used as a heartbeat too).
* Note that the signal database will send the signal every 100 ms when it has been changed, otherwise the Com stack sends every 1000 ms to reduce bus load.

#### Related Requirements

* LD_Req-5623 v7

#### Integration Notes

Connect DiagFaultStat signal

### Configurability and Vehicle modes

* P1BDU parameter is used to check the vehicle mode validity of Diagnostic Warning Manager.
* This module broadcasts the fault status only during those modes where Diagnostic Warning Manager is active.
* Default vehicle modes are Running and Pre-running

#### Related Requirements

* LD_Req-7627 v2
* LD_Req-5625 v4

#### Integration Notes

TBD

## More Information

### Technical References

Refer Vector technical references for functionality, API and configuration of BSW Module.

The following documents were referred.

* TechnicalReference_Dem.pdf (which can be found in ECU SIP)
* Send DiagnosticFaultStatus, Read DTC, Vehicle Mode system specifications from Reg. no. 50269231 (LDS_FCIOM)

### SEWS

See the actual version used in ContainerInfo.xml, convenience link to version [3.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=14461)
