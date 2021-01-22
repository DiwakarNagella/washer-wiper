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

* Need Dem eventIds to request DTC status from DEM (generated DEM configuration)
* Connect service ports of DEM to get these event status and dtcs.
* FEG needs to be initialized after the DEM is initialized.
* Connect Serverice port of DEM to report D1BR9_68.

### Send Diagnostic Fault Status

* When there are one or more DTCs that are active, fault information shall be sent with a periodicity of 100ms.
* Sends out the status of 2 Active faults each time.
* If there are no active faults, then only the ECU address is sent in the signal as alive status.

#### Related Requirements

* LD_Req-5623 v7

#### Integration Notes

TBD

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

The following documents were referred which can be found in ECU SIP.

* TechnicalReference_Dem.pdf

### SEWS

See the actual version used in ContainerInfo.xml, convenience link to version [3.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=14461)
