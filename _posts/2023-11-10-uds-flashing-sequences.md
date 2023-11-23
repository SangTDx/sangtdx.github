---
layout: post
title: Firmware Over-The-Air in Automotive
date: 2023-11-10 00:00:00
categories: [automotive]
tags: [automotive]
last_modified_at: 2023-11-10
---

# ECU Reprogramming Requirements Specification Based on UDS

**Author: https://sangtdx.github.io/**

**Reference Documents**

 - ISO 14229-1--2013 Road vehicles - Unified Diagnostic Services
   (UDS)Part 1
 - ISO 15765-2--2016 Road vehicles – Diagnostics on CAN – Part 2
 - ISO 15765-2--2016 Road vehicles – Diagnostics on CAN – Part 3

**Terms and definitions**
The following terms and definitions for the standard.
Cyclic Redundancy Check（CRC）
Electronic Control Unit（ECU）
Electrically Erasable Programmable Read Only Memory （EEPROM）
Negative Response Code（NRC）
Unified Diagnostic Services（UDS）
Transport Protocol （TP）
Service Identifier （SID）
Data Identifier （DID）
Separation Time Minimum（STmin）
Micro Controller Unit （MCU）
Boot Loader（Bootloader）

# Introduction
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

# 4. Process terminology
<figure>
  <img src="/assets/img/blogs/automotive/Flashing Sequences/memory.png" alt="memory map of a reprogrammable ECU">
  <figcaption>memory map of a reprogrammable ECU</figcaption>
</figure>

# References
[https://www.autosar.org/fileadmin/standards/R20-11/CP/AUTOSAR_EXP_FirmwareOverTheAir.pdf](https://www.autosar.org/fileadmin/standards/R20-11/CP/AUTOSAR_EXP_FirmwareOverTheAir.pdf)