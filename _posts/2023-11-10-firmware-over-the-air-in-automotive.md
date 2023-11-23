---
layout: post
title: Firmware Over-The-Air in Automotive
date: 2023-11-10 00:00:00
categories: [automotive]
tags: [automotive]
last_modified_at: 2023-11-10
---

### 1. What is the Firmware Over-the-Air (FOTA)?

* The FOTA application allows vehicle ECU firmware to be updated in the background. The FOTA gateway is physically connected with in-vehicle networking and has the ability to communicate with ECUs capable of FOTA updating; and it is typically the controller that performs firmware updating management for the whole vehicle.

<figure>
  <img src="/assets/img/blogs/automotive/FOTA/car-fota.png" alt="FOTA in automotive">
  <figcaption>Firmware Over-the-Air</figcaption>
</figure>

* A typical FOTA system consists of three components:
  * FOTA server: responsible for the management of vehicle software release, and optionally to customize updates for every vehicle client based on OEM policies
  * FOTA client: application responsible for communication with a backend server and updating campaign management for all the other ECUs in the vehicle. Typically runs on FOTA gateway.
  * FOTA agent: application that performs final updating of firmware for ECUs during run-time. It sometimes also runs on FOTA gateway to support self-updating.

<figure>
  <img src="/assets/img/blogs/automotive/FOTA/system-block-diagram.png" alt="System Blog Diagram">
  <figcaption>System Blog Diagram - from NXP</figcaption>
</figure>

# 2. Motivation
Due to a growing SW complexity driven by evolving security requirements, distributed and connected functions the need to keep a system in a vehicle up-to-date is continuously increasing. In order to avoid time-consuming and recurring service garage visits because of an upcoming SW update, the SW deployment to fleets shall be orchestrated over-the-air. Different wireless techniques (UMTS, LTE, Bluetooth, WiFi, 5G) can be used to connect the vehicle to a backend/cloud system to provide a capability to download SW to the vehicle. The distribution of the new SW to target ECUs affected by the update is done via vehicle busses as CAN, CAN-FD, Flexray or Automotive Ethernet.

Most ECUs nowadays have an on-board reprogramming capability, which is used in the service garage infrastructure to deploy bugfixes or functional improvements in the field.

This interface, usually a flashbootloader, could also be addressed via an Over-The-Air (OTA) update master ECU in order to install a new SW, when the vehicle is outside of the service garage. In other words, you can realize an over-the-air SW update through the transfer of programming functionalities from an external diagnostic tester into a connected in-car-ECU (OTA-Master). From the perspective of target ECUs, it can be even more transparent, whether the target ECU is conducted via diagnostic tester or OTA-Master.

This approach brings several aspects that are to be considered:

 - During the entire SW update process the target ECU is not operational
   from functional point of view. This usually leads to a down-time of
   the entire vehicle during SW update.
 - In case of distributed functions, where several ECUs must be updated
   in one campaign, the vehicle down-time is even longer compared to a
   single ECU update
 - In case of errors during or after the installation of the new SW a
   re-installation of the previous SW could be initiated and realized
   via OTA-Master. However, this additionally increases the vehicle
   downtime and could finally lead to a situation of functionally
   bricked ECUs.
 - In case a rollback is necessary, all dependent ECUs related to the
   update have to be rolled back as well.
 - The power supply concept and residual capacity of battery shall be
   also taken with care following this approach.

# 3. System Component Terminology
3.1 FOTA Target 
This term applies to all ECUs which are capable to be updated via the FOTA procedure in general.

3.2 FOTA Master
The FOTA Master specifies the instance which handles all software updates with all their related information needed to apply the respective update to the FOTA Target ECU addressed by the FOTA update process.

3.3 (FOTA-) Image
The term Image describes a full downloadable ECU software collection. This shall be regardless if partial, incremental or full featured ECU software is downloaded and installed. Applying a new Image to an ECU will update at least one of the following ECU software parts:

 - Application software  
 - Basic software  
 - Calibration data

3.4 Backend
This identifies the remote instance which provides the FOTA Image to be downloaded into the FOTA Target ECU (e.g. via Wifi, 3G, 4G, 5G, etc.).

3.5 Data Chunk
Data Chunks are data packets, transferred from the FOTA Master ECU to the FOTA Target ECU, containing the raw image data (UDS TransferData service payload). This term is used since the length of each data chunk may vary.

# 4. Process terminology
<figure>
  <img src="/assets/img/blogs/automotive/FOTA/fota-phases.png" alt="FOTA Phases">
  <figcaption>FOTA Phases</figcaption>
</figure>

# References
[https://www.autosar.org/fileadmin/standards/R20-11/CP/AUTOSAR_EXP_FirmwareOverTheAir.pdf](https://www.autosar.org/fileadmin/standards/R20-11/CP/AUTOSAR_EXP_FirmwareOverTheAir.pdf)