# VOL_DebugServer

## Overview

* Debug server module provides the following ECU internal debug data when requested using corresponding DIDs<br/>
    -CPU load<br/>
    -Application Network Status/ISS status<br/>
    -Extended reset info<br/>
    -Error counters
	
## Usecases

### P1EGD - Debug Info Write data DID

* Used to configure the debug server to be in the preffered state to read the data.
* Reset the CPU load counters and CPU load data
* Possible to force Generate the following types of MCU resets for CHASSIS ECUS while the debug server is in reset state<br/>
   -- Controlled reset<br/>
   *OS error reset<br/>
   -other exception resets related to illegal instruction and data fetch


#### Related requirements

### P1EGD - Debug Info Read data DID

#### Related requirements

### P1EGB - BuildVersionInfo

DID used to read the Development internal version information like build version, build time etc.

#### Related requirements

TBD

### P1F2A - Application Network Status

#### Related requirements

### P1VLE - ExtendedResetInfo

#### Related requirements

### P1M4R - Error counters

#### Related requirements

## More Information

### Technical References

  For functionality, API and configuration of the AUTOSAR BSW module,<br/> refer Vector technical references which can be found in ECU SIP.
  The following documents were referred.
* TechnicalReference_Issm.pdf

### SEWS

* See the actual version used in `ContainerInfo.xml`,convenience link to version [6.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=26026).

