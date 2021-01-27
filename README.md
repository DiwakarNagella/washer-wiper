# VOL_DebugServer

## Overview

Debug server module provides the following ECU internal debug data when requested using corresponding DIDs:

* Application Network Status/ISS status (DID P1F2A)
* CPU load (chassis ECUs VOL_CPULOAD_X1A2D or CFG_ZYNQ)
* Trigger reset (chassis ECUs)
* Error counters (DID P1M4R)
* Reset info for snapshots (P1VLE)
* Build info (legacy, DID P1EGB)

P1EGD is a multiplexed DID used for debug purpose.
It is introduced before X-DIDs were allowed in production SW.
Most functionality has been moved to specialized DIDs.
Much of the functionality depends on the target ECU.
Documentation for P1EGD is available in the source file.

## Use cases

### P1EGD - Debug Info DID

This will enable adding and removing of special functionality.
Most functionality will be disabled from default dataset or parameters in production.
Configure the debug server to be in the preferred state to read the data.

* Reset the CPU load counters and CPU load data.
* Possible to force generate the following types of MCU resets for CHASSIS
  ECUS while the debug server is in reset state (only write to DID,
  sets DTC D1AD0_49 and D1AD0_94).
    1. Controlled reset
    2. OS error reset
    3. Other exception resets related to unaligned memory,
       illegal instruction and data write

#### Related requirements

Internal testing

#### Integration notes

TBD

### CPU load measurement

* Chassis ECUs (MPC): Cpu load is measured in a periodic 10ms task and only for
  a specified period which is selected from X1A2D address parameter.
* Smoothing factor for cpu load is selected from X1AWT address parameter.
* CPU load functionality is disabled from default dataset
  or parameters in production.

The reading of the cpu load is done using the DID P1EGD.
For ZYNQ, the implementation is separate from the debug server.

#### Related requirements

Internal testing.

#### Integration notes

For chassis ECUs: Requires a counter in the idle loop.

### P1EGB - BuildVersionInfo

Read the Development internal version information like build version,
build time etc.

#### Related requirements

Legacy, possibly used in V3 tests though.

#### Integration notes

Requires generation of build_info.h.

### P1F2A - Application Network Status

* Only ISS status (transimtted in AnmMsg_ECUName_ISS, for ex: ISS is Backbone2)
  doesn't give any info about which ANW users are active.
* This service provides the following info:
    1. Number of active users (Corresponding to ANW) in the local ECU.
    2. ISS(Communication Networks) status.
    3. ANW/ISS user info in an ECU, 
	     with information if the ECU keeps the networks active.

#### Related requirements

* Requirements related to ISS REQ-ISS_11/01,REQ-ISS_11/01,REQ-ISS_18/01,
  REQ-ISS_20/01,REQ-ISS_24/01,REQ-ISS_XX/01,REQ-ISS_36/01 are tested

#### Integration notes

Connect service ports of ISSM to request the active Application Network Users.

### P1VLE - ExtendedResetInfo

* For ZYNQ based ECUs, this service provides ECU last reset type(reason).
* For CHASSIS ECUS
    1. It provides last reset type,minimum free stack and task ID at reset.
    2. Exception register values for resets related to unaligned memory,
       illegal instruction, data write.
    3. Exception register values for unhandled IRQ reset 
	     and Software Watchdog reset.
    4. Stored Os error information

#### Related requirements

No formal requirements, used to debug production ECUs.

#### Integration notes

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

No formal requirements, used to debug production ECUs.

## More Information

### Technical References

For functionality, API and configuration of the AUTOSAR BSW module, refer
Vector technical references which can be found in ECU SIP.

The following documents were referred.

* TechnicalReference_Issm.pdf

### SEWS

* See the actual version used in `ContainerInfo.xml`,convenience link to version [6.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=26026).
