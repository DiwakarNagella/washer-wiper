# VOL_DebugServer

## Overview

Debug server module provides the following ECU internal debug data when requested using corresponding DIDs
   * CPU load
   * Application Network Status/ISS status
   * Extended reset info
   * Error counters
	
## Usecases

### P1EGD - Debug Info Write data DID

* This will enable adding and removing of special functionality.
* Most functionality will be disabled from default dataset or parameters in production.
* Configure the debug server to be in the preffered state to read the data.
* Reset the CPU load counters and CPU load data.
* Possible to force Generate the following types of MCU resets for CHASSIS 
  ECUS while the debug server is in reset state.
   1. Controlled reset
   2. OS error reset
   3. Other exception resets related to unalligned memory, illegal instruction and data write
* Reset causes DTC D1AD0_49 and D1AD0_94 to be set

#### Related requirements

TBD

#### Integration Notes

TBD

### P1EGD - Debug Info Read data DID

* Responds with the state of debug server.
* While in Configure state, it returns only the CPU load measure period 
  selected from X1A2D address parameter.
* While in Data Read and Reset state returns min,max and average CPU Load.

#### Related requirements

TBD

#### Integration Notes

TBD

### CPU load measurement

* Cpu load is measured in a periodic 10ms task and only for a specified period 
  which is selected from X1A2D address parameter.
* Smoothing factor for cpu load is selected from X1AWT address parameter.
* CPU load functionality is disabled from default dataset or parameters in production.

#### Related requirements

TBD

#### Integration Notes

TBD

### P1EGB - BuildVersionInfo

Read the Development internal version information like build version, build time etc.

#### Related requirements

TBD

#### Integration Notes

TBD

### P1F2A - Application Network Status

* Only ISS status (transimtted in AnmMsg_ECUName_ISS, for ex: ISS is Backbone2)
  does't give any info about which ANW users are active.
* This service provides the following info:
    1. Number of active users (Corresponding to ANW) in the local ECU.
    2. ISS(Communication Networks) status. 
    3. ANW/ISS user info in an ECU, with information if the ECU keeps the networks active.
    
#### Related requirements

* Requirements related to ISS REQ-ISS_11/01,REQ-ISS_11/01,REQ-ISS_18/01,
  REQ-ISS_20/01,REQ-ISS_24/01,REQ-ISS_XX/01,REQ-ISS_36/01 are tested

#### Integration Notes

Connect service ports of ISSM to request the active Application Network Users.

### P1VLE - ExtendedResetInfo

* For ZYNQ based ECUs, this service provides ECU last reset type(reason).
* For CHASSIS ECUS
    1. It provides last reset type,minimum free stack and task ID at reset.
    2. Exception register values for resets related to unalligned memory, 
       illegal instruction, data write.
    3. Exception register values for unhandled IRQ reset and Software Watchdog reset.
    4. Stored Os error information
    
#### Related requirements

TBD

#### Integration Notes

TBD

### P1M4R - Error counters

* This service provides the following stored error counters info:
    1. RAM error counter updated each time due to for example ECC errors.
    2. ROM error counter updated each time due to NvM time out (60 s).
    3. Reset counter that includes software resets and Hardware resets
       except WDG supervised entity resets.
    4. Software error counters

#### Related requirements

TBD

#### Integration Notes

TBD

## More Information

### Technical References

  For functionality, API and configuration of the AUTOSAR BSW module, refer
  Vector technical references which can be found in ECU SIP.
  
  The following documents were referred.
* TechnicalReference_Issm.pdf

### SEWS

* See the actual version used in `ContainerInfo.xml`,convenience link to version [6.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=26026).

