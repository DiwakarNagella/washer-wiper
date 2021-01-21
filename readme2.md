VOL_FaultEventGateway
========

# Overview

* Module acts as a gateway for the Diagnostic Fault status.
* Responsible to collect DTC information from the DEM.
* Periodically sends Diagnostic Fault Status of Active Faults and ECU alive status to DiagnosticWarningManager.
 
## Usecases

### Receiving DTC information

* Active DTCs with warning indicator bit set to true are collected from DEM just before each transmission. 

#### Related Requirements

* LD_Req-5622 v5

#### Integration Notes

TBD

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

### Maximum number of DTCs

* DTCs that can be periodically (100ms) sent will be limited to 30.
* This is to fulfill an overall requirement of presenting DWM related messages to the driver within 3 seconds. 
* When the number of DTCs that are periodically sent reaches 29, this component is responsible to set a DTC on its own.
* The purpose of this DTC is to inform the system that this ECU has too many DTCs set and that the maximum limit is reached.
* This specific DTC set by this component is the last DTC of the 30 DTCs handled by this component.
* There might be more than 30 DTCs set and active in the DEM, but this component will only send the 30 first DTCs.

#### Related Requirements

* LD_Req-21508 v1

#### Integration Notes

TBD

### Initialization Behaviour

* Upon initialization of this component the specific DTC (number 30) shall be reported as TestPassed to the DEM in order
to clear the previous fault.


## More Information

### Technical References
Refer Vector technical references for functionality, API and configuration of BSW Module.

The following documents were referred which can be found in ECU SIP.

* TechnicalReference_Dem.pdf

### SEWS

See the actual version used in ContainerInfo.xml, convenience link to version [3.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=14461)
