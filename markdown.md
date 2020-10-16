Diagnostic Server for Common Data Identifiers - VOL_DIDServer
========


## Overview
Module provides static and dynamic diagnostic data to Diagnostic Communication Manager and Diagnostic Event Manager when requested.   

![Introduction](images/Overview.png)

## Dynamic data provided by the Module:

The safestringlib is based on the Safe C Library from Cisco and Intel(https://github.com/intel/safestringlib)
It includes replacement for C Library functions which are not safe to use. 
This library is made available under the MIT Open Source License.
The library functions will be part of C11 standard.
Out of many library functions, only memcpy_s()is used and modified.
There might me other functions included in future.
memcpy_s() function returns nonzero error codes and triggers callback fucntions in case of exceptions.
In the modified version function only returns error codes (no callbacks) 
Always copy source to destination using memmove function 
which is the only solution if there is an overlap between source and destination.
In the modified version, bytes are copied normally (no memmove).
