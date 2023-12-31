---
layout: post
title: ECU Reprogramming Based on UDS (EU-Ver)
date: 2023-11-10 00:00:00
categories: [automotive]
tags: [automotive]
last_modified_at: 2023-11-10
---

# ECU Reprogramming Requirements Specification Based on UDS

**Author: https://sangtdx.github.io/**

**Reference Documents**

 - ISO 14229-1--2013 Road vehicles - Unified Diagnostic Services
   (UDS) Part 1
 - ISO 15765-2--2016 Road vehicles – Diagnostics on CAN – Part 2
 - ISO 15765-2--2016 Road vehicles – Diagnostics on CAN – Part 3

**Terms and definitions**
The following terms and definitions for the standard.
- Cyclic Redundancy Check（CRC）
- Electronic Control Unit（ECU）
- Electrically Erasable Programmable Read Only Memory （EEPROM）
- Negative Response Code（NRC）
- Unified Diagnostic Services（UDS）
- Transport Protocol （TP）
- Service Identifier （SID）
- Data Identifier （DID）
- Separation Time Minimum（STmin）
- Micro Controller Unit （MCU）
- Boot Loader（Bootloader）

# 1. Introduction
A reprogrammable ECU contains at least Bootloader. A complete ECU is typically composed
of Bootloader and application. During normal ECU operation, the application software is
executed. Bootloader can be activated when a diagnostic device sends a specific diagnostic
service request to ECU or if the application is invalid in the system.

<figure>
  <img src="/assets/img/blogs/automotive/Flashing Sequences/memory.png" alt="memory map of a reprogrammable ECU">
  <figcaption>memory map of a reprogrammable ECU</figcaption>
</figure>

Application software and Bootloader software occupy a dedicated area of Flash memory
as depicted in the Figure1. Either Bootloader or application is executed, the RAM memory
of the system can be fully used by both software packages.

The Bootloader software uses the diagnostic services of UDS as protocol for download
communication. Therefore, the Bootloader has got a communication stack of CAN(FD) driver,
transport layer and a subset of the UDS protocol layer.

# 2. Flash EEPROM Reprogramming Requirements

### 2.1 Requirements for non-reprogrammable ECUs

In order to operate reprogrammable and non-reprogrammable ECUs together in one network,
non-reprogrammable ECUs shall support the diagnostic services specified in6.3.2 except the
DiagnosticSessionControl –programmingSession request.
If a non-reprogammable ECU receives a DiagnosticSessionControl –programmingSession
($10 $02) it shall send the negative response code $12(subFunctionNotSupported).

### 2.2 General Requirements
The system shall be able to enter the Bootloader on request from normal operating mode
or if no ECU application software is available.

The system can be reprogrammed in the event of a failed reprogramming (short circuit,
open circuit) or interrupted, timeout or reset, Flash erasure incomplete, or invalid
application.

The system shall execute Bootloader codeif the application code is missing, invalid or
corrupt.

A system executing Bootloader code must not disturb normal communication on the network.

All ECUs connected to the network shall disable their normal message transmission after
they received a disable normal message transmission request. Normal communication shall be
enabled on all ECUs after an explicit request to enable normal communication, after return
to the default session and after a PowerOn/Reset.

All ECUs connected to the network shall disable their DTC settings after they received
a request to disable fault code setting. Fault code setting shall be enabled on all ECUs
after an explicit request to enable fault code setting, after return to the default session
and after a PowerOn/Reset.

After all download data has been transferred, the integrity of the programmed data
shall be ensured by a verification routine. Therefore, an explicit check value shall be
provided to be compared against the value calculated on the ECU.

If a watchdog is used in the ECU, it shall be served during the complete Flash
reprogramming sequence.

It must be ensured that the Bootloader software has the ability to recover under
abnormal conditions such as a dead loop.

A programming dependency check shall be performed after download if more than one
module can be reprogrammed on the system.

In order to reduce power consumption when an ECU application is not valid, Bootloader
should also support sleep and wakeup function.

### 2.3 Resource Requirements

The Flash memory consumption of the Bootloader must be kept to minimum since the
available Flash memory of an ECU is shared by application and Bootloader.

### 2.4 Security Requirements

Before a reprogramming procedure is started, the security access service shall be
passed successfully.

Critical parts of the Flash driver code (erase and write) can not be permanently stored
inside the ECU and should be downloaded to RAM during reprogramming(software interlock).
This avoids accidental tampering with Flash in the normal operating mode of the ECU.

The Bootloader software shall be stored in a protected memory area (software and/or
hardware protection).

The Bootloader should set the ECU input and output ports to a safe state to prevent
damage to the ECU and the vehicle.

### 2.5 Download Of Flash Data

**2.5.1 Addressing**

The addressing scheme for download data is based on a linear address space. Due to
differences in the underlying microcontroller platforms ,it may be necessary for the
Bootloader to perform address translation while operating Flash.

**2.5.2 Erasing Of Flash Memory**

Flash devices require that Flash memory is erased before it is reprogrammed. Any Flash
cell must not be reprogrammed without a previous erase procedure.

**2.5.3 Flash Programming Conditions**

Before the Flash reprogramming procedure is started, programming conditions must be
checked. A reprogrammed ECU may be in a condition that does not permit reprogramming. In
this case, reprogramming must be rejected. The check for Flash programming conditions
shall be performed when the ECU receives the RoutineControl($31) –
“checkProgrammingPreconditions($02$03)” service request.
For example:
> Flash programming conditions require the vehicle speed to be less than 3km/h and ECU
is in a normal working voltage state.

### 2.6 Programming Counter
The Bootloader software shall count the number of programming event for each logical
block. When RoutineControl ($31 $01 $FF00) is requested, Bootloader should check the programming counter of the related logic block referring to the request of erasing addressand size. If the programming counter exceeds a predefined value, the current erase routine request must be denied.If erasing successfully, the programming counter of each logic block should only be increased by one.

# 3. ECU FBL Software Architecture
### 3.1 Functional Overview
The Bootloader software is subdivided into several functional blocks

<figure>
  <img src="/assets/img/blogs/automotive/Flashing Sequences/functional-block.png" alt="Functional blocks of the Bootloader">
  <figcaption>Functional blocks of the Bootloader</figcaption>
</figure>

 - **Bootloader Application Framework**: The Bootloader application framework provides the boot procedure and the time base handling for the Bootloader components.
 - **Bootloader Application**: This module permits supplier-specific code in order to support system specific implementations.
 - **Bootloader Download State Handler**: Controls the states of the download sequence and the Flash programming.
 - **Diagnostics Protocol**: This module provides all diagnostic services needed for the download procedure.
 - **Transport Protocol** : Transport Layer protocol stack to support segmented transmission of diagnosis/ download data.
 - **Watchdog Driver**: Provide system abnormal restart function.
 - **Security Module**: The security module provides implementations required for the security access service and the verification of the download.
 - **Flash Driver**: The Flash driver provides routines for Flash erasing and programming.
 - **EEPROM Driver**: The EEPROM driver provides routines for EEPROM erasing and programming.
 - **CAN(FD)/ ETH Driver**: Providing the CAN(FD)/ ETH message reception and transmission functions.

### 3.2 Flash Memory Partitioning
**3.2.1 Physical Flash Sectors**

The Bootloader shall take into account that the underlying Flash technology determines
the minimum number of bytes that must be erased all at once. This size is called a physical
Flash sector. The memory area of a Flash device usually is divided into several Flash
sectors.

**3.2.2 Physical Flash Pages**

The Bootloader shall take into account that the underlying Flash technology determines
the minimum number of bytes that must be programmed all at once. This size is called a
physical Flash page.

**3.2.3 Logical Blocks**

The logical block is a logical division of Flash data, and the ECU's Flash data may be
divided into multiple logical blocks. From the application point of view these are the
minimum units that can be individually erased and/or reprogrammed. Each logical block can
be erased and reprogrammed independently from others. The basic motivation for Flash
partitioning is to avoid reprogramming of the complete Flash memory when only a certain
part of the application software or calibration data has changed.

The partition that is occupied by the Bootloader is called boot block and cannot be
reprogrammed. The contents of a logical block can be determined by the ECU supplier and
can consist of code, data or both.

Logical blocks must be aligned to physical Flash sectors. That means that a block shall
start at a physical Flash sector and shall comprise an integer number of Flash sectors. This
requirement makes sure that each logical block can be erased and reprogrammed individually
without affecting other blocks, logical blocks must not overlap, and they must not share
one common physical Flash sector.

Logical blocks must not be nested. There is at least one logical block in a ECU.
The file format of the download file is recommended as S19, Hex, Mot (optional). If it
is a Bin file，it must use the uniform format of the header, which should be located at
beginning of each Bin file.

**3.2.4 Segment**

A segment must reside inside of the address range of the current logical block.

The start address of the segment must be aligned to an integer multiple of the Flash
physical page . For example,if the Flash physical page is 4 bytes, then the starting
address must be an integer multiple of 4.

<figure>
  <img src="/assets/img/blogs/automotive/Flashing Sequences/segmentation.png" alt="Segmentation of logical block data">
  <figcaption>Segmentation of logical block data</figcaption>
</figure>

**3.2.5 Configuration**

* Configuration 1

ECU Flash memory with the Bootloader code in the
protected memory area and one logical block 0（contains application code and calibration
data） in the reprogrammable area. The complete logical block 0 can only be erased and
reprogrammed at once.

* Configuration 2

ECU Flash memory with the Bootloader code in the
protected memory and several logical blocks in the protected area. Logical Block 1 contains
only the calibrated data, so the logical block 1 can be reprogrammed separately when the
content is changed.

<figure>
  <img src="/assets/img/blogs/automotive/Flashing Sequences/logical_blocks.png" alt="Configuration of logical blocks">
  <figcaption>Configuration of logical blocks</figcaption>
</figure>

# References
[https://www.autosar.org/fileadmin/standards/R20-11/CP/AUTOSAR_EXP_FirmwareOverTheAir.pdf](https://www.autosar.org/fileadmin/standards/R20-11/CP/AUTOSAR_EXP_FirmwareOverTheAir.pdf)