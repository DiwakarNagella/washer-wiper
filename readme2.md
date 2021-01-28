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
* Engine Type (DID P1ALB)
* Build ID (DID P1URK)
* Boot Software Identification (DID P1B1O)
* Outdoor Temperature (DID P1AFR)
* Total Vehicle Distance (DID P1AFS)
* Vehicle Mode (DID P1AFT)
* Active Diagnostic Session (DID P1DIH)
* UTC TimeStamp

P1B1O is an optional did for development purpose.
Not supported by Volvo tester

## Usecases

### Dynamic data

The following parameters are read periodically from RTE and stored locally
along with calculated CRC.
DEM uses callback functions to read DTC snapshot/Extended data.
DCM reads the data when requested from external tool with corresponding DIDs:

*   Outdoor Temperature (DTC snapshot data)
*   Total Vehicle Distance (DTC snapshot data). The odometer value of distance
    driven since the assembly of the vehicle.
*   Vehicle Mode (DTC snapshot data)
*   UTCTimeStamp (DTC Extended Diagnostic Data)

Active Diagnostic Session is updated by diagnostic session control
mode machine. This is an optional DID not supported by VOLVO tester.

#### Related Requirements

* REQ-DIR-15 v6
* REQ-DIR-27 v4

#### Integration notes

* Service ports connected to DEM and DCM
* connect RTE ports for signals
* SEWS2 parameters are assigned to Application SWC containers

### ECU hardware identification

This service provides vehicle Manufacturer ECU Hardware number which includes 
* HW module ID
* HW Partnumber
* HW Serial number
* Sub node info (serial number and slave node part number for LIN Slaves)
  1. Number of Sub modules depends on number of LIN slave nodes
     configured in LIN Manager.
  2. Requests LIN manager service for slave node information and waits for
     the server to respond back.
  3. If LIN manager doesn't respond within the timeout, this module returns
     the ECU H/W info without LIN slave information.

ECU HW part number and HW serial number are stored in flash memory and
available in all diagnostic sessions.

#### Related Requirements

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
* SEWS2 parameters are assigned to Application SWC containers.
* Connect service ports of VOL_LINManger for slave info.

### SystemNameOrEngineTypeDataIdentifier

System Name uniquely identifies the Node name of the ECU in the network,
and provides information on the main vehicle function of the node.
Values for Node Family, Node Type and Node Position are assigned 
according to definition on SEWS2

#### Related Requirements

* REQ-RW-32 v2

#### Integration notes

* Requires manufacturing info.h for ZYNQ based ECUs
* Requires linker_symbols.h for symbols
* SEWS2 parameters assigned

### Vehicle identification

Returns vehicle identification number. The data connected to this identifier
can be configured using address based parameter code VINNO.
Available in only default and Extended diagnostic sessions

#### Related Requirements

* REQ-RW-33 v5
* REQ-OBD-115 v1 
* REQ-EOALP-18 v1

#### Integration notes

Connect Address parameter Rte_AddrPar_0x2F_VINNO

### Chassis identification

Returns VOLVO proprietary chassis-id. The data connected to this identifier
can be configured using address based parameter code CHANO.
Available in only default and Extended diagnostic sessions.

#### Related Requirements

* REQ-RW-33 v5

#### Integration notes

Connect Address parameter Rte_AddrPar_0x2F_CHANO

### Application Software identification

Returns number of application software modules (Bootloader, MSW and CSW) and 
their identities (Part number, Module ID and Build version).
For ZYNQ based ECUs, bitstream partnumber is used for CSW module. 

#### Related Requirements

* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1
* REQ-RW-33 v5

#### Integration notes

* Requires generation of build_info.h.
* Requires linker_symbols.h for symbols

### Application data identification

Returns Number of application data modules present in the ECU
and their part numbers.
Dataset and post build data by default for all ECUS.
Sound data and Diagnostic Warning Manager configuration
data part numbers for IC.

#### Related Requirements

* REQ-SS-19 v3
* REQ-SS-11 v1
* REQ-SS-42 v1
* REQ-RW-33 v5

#### Integration notes

Requires generation of build_info.h.

### Build ID

#### Related Requirements


#### Integration notes


### Boot Software Identification


#### Related Requirements


#### Integration notes

## More Information

### Technical References
For functionality, API and configuration of the AUTOSAR BSW module, refer
Vector technical references which can be found in ECU SIP.
The following documents were referred.

* TechnicalReference_Dem.pdf
* TechnicalReference_Dcm.pdf

### SEWS

See the actual version used in ContainerInfo.xml, convenience link to version
[10.0](https://sews.volvo.net/Sews2/ViewData/ViewContainerData.aspx?ContainerId=27734).
