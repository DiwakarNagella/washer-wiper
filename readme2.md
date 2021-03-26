# VOL_DIDServer

## Overview

DID server module provides the following diagnostic data
when requested using corresponding DIDs:

* Application Software Identification (DID P1ALQ)
* Application Data Identification (DID P1ALP)
* Chassis Identification (DID CHANO)
* Vehicle Identification Number (DID VINNO)
* Description File Sha256 (DID P1Q82)
* ECU Hardware Number (DID P1ALA)
* System Name or Engine Type (DID P1ALB)
* Build ID (DID P1URK)
* Boot Software Identification (DID P1B1O)
* Outdoor Temperature (DID P1AFR)
* Total Vehicle Distance (DID P1AFS)
* Vehicle Mode (DID P1AFT)
* Active Diagnostic Session (DID P1DIH)
* UTC TimeStamp

## Use cases

### Snapshot data

The following parameters are provided for common snapshot data 

* Outdoor Temperature (DID P1AFR)
* Total Vehicle Distance (DID P1AFS). The odometer value of distance
  driven since the assembly of the vehicle.
* Vehicle Mode (DID P1AFT)

#### Related requirements

* REQ-DIR-15 v6

#### Integration notes

* Service ports connected to DEM and DCM
* connect RTE ports for signals

### Extended diagnostic data

UTCTimeStamp data is provided as extended diagnostic data.

#### Related requirements

* REQ-DIR-27 v4

#### Integration notes

* Service ports connected to DEM
* connect RTE ports for signals

### P1DIH - Active Diagnostic Session

Active Diagnostic Session is updated by diagnostic session control
mode machine.

#### Related requirements

* This is an optional DID not required by system specification.

#### Integration notes

* Service port connected to DCM
* connect RTE port for signal

### P1ALA - ECU hardware identification

This service provides vehicle Manufacturer ECU Hardware number which includes
*   HW module ID
*   HW Partnumber
*   HW Serial number
*   Sub node info (serial number and slave node part number for LIN Slaves)
    1.  Number of Sub modules depends on number of LIN slave nodes
        configured in LIN Manager.
    2.  Requests LIN manager service for slave node information and waits for
        the server to respond back.
    3.  If LIN manager doesn't respond within the timeout, this module returns
        the ECU H/W info without LIN slave information.

ECU HW part number and HW serial number are stored in flash memory and
available in extended diagnostic session.

#### Related requirements

* REQ-LNI_verification-2 v2
* REQ-LNI_SN-4 v3
* REQ-LNI_SN-5 v3
* REQ-LNI_SNPN-4 v2
* REQ-LNI_readout-10 v1
* REQ-LNI_readout-1 v1
* REQ-LNI_readout-2 v2
* REQ-LNI_readout-3 v2
* REQ-LNI_readout-7 v2
* REQ-SS-9 v3
* REQ-RW-32 v2

#### Integration notes

* Requires manufacturing_info.h for ZYNQ based ECUs.
* Requires linker_symbols.h for symbols.
* Connect service ports of VOL_LINManger for slave info.

### P1ALB - System name

System Name uniquely identifies the Node name of the ECU in the network,
and provides information on the main vehicle function of the node.
Values for Node Family, Node Type and Node Position are assigned
according to definition in [SEWS2](https://sews.volvo.net/Sews2/ViewData/ViewNode.aspx)

#### Related requirements

* REQ-RW-32 v2

#### Integration notes

* Requires manufacturing info.h for ZYNQ based ECUs
* Requires linker_symbols.h for symbols
* SEWS2 parameters assigned

### VINNO - Vehicle identification

Returns vehicle identification number. The data connected to this identifier
can be configured using address based parameter code VINNO.
Available in extended diagnostic session.

#### Related requirements

* REQ-RW-33 v5
* REQ-OBD-115 v1 
* REQ-EOALP-18 v1

#### Integration notes

Connect Address parameter Rte_AddrPar_0x2F_VINNO

### CHANO - Chassis identification

Returns VOLVO proprietary chassis-id. The data connected to this identifier
can be configured using address based parameter code CHANO.
Available in extended diagnostic session.

#### Related requirements

* REQ-RW-33 v5

#### Integration notes

Connect Address parameter Rte_AddrPar_0x2F_CHANO

### P1ALQ - Application software identification

Returns application software module (Bootloader, MSW and CSW) Part numbers.
For ZYNQ based ECUs, one CSW module may be the bitstream.

#### Related requirements

* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1
* REQ-RW-33 v5

#### Integration notes

* Requires generation of build_info.h.
* Requires linker_symbols.h for symbols

### P1ALP - Application data identification

Returns application data part numbers. It includes 
Dataset and post build data by default for all ECUS.
Sound data and Diagnostic Warning Manager configuration
data for IC.

#### Related requirements

* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1
* REQ-RW-33 v5

#### Integration notes

Requires generation of build_info.h.

###  P1URK - Build ID

P1URK provides the build id along with all the info that is
provided by P1ALP and P1ALQ. Build ID can uniquely identify 
any version of the downloadable software compared to the part-number.

Example: 2.14.0.48-g1d621746

#### Related requirements

* REQ-RW-68 v2

#### Integration notes

* Requires linker_symbols.h for symbols
* Requires generation of build_info.h

### P1Q82 - Description File Sha256

The SHA256 checksum for the description file for the MSW.

#### Related requirements

TBD

#### Integration notes

TBD

### P1B1O - Boot software identification

 An optional did for development purpose. Not supported in production

#### Related requirements

TBD

#### Integration notes

* Requires linker_symbols.h for symbols

## More information

### Technical references

* Refer Vector technical references for functionality,
  API and configuration of BSW Module.
* TechnicalReference_Dem.pdf (which can be found in ECU SIP)
* Vehicle Mode system specifications
* SYS - ReadAndWriteSpecifiction(Reg. no. 50135952)
* ECU Software Structure (Reg. no. 50136492)
* LIN Node Identification and Addressing System Specification, Reg. no. 50136194

### SEWS

See the actual version used in ContainerInfo.xml, convenience link to version
[10.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=27734).
