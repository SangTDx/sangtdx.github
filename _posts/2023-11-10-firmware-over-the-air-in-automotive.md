---
layout: post
title: Firmware Over-The-Air in Automotive
date: 2023-11-10 00:00:00
categories: [automotive]
tags: [automotive]
last_modified_at: 2023-11-10
---

### What is the Firmware Over-the-Air (FOTA)?

* The FOTA application allows vehicle ECU firmware to be updated in the background. The FOTA gateway is physically connected with in-vehicle networking and has the ability to communicate with ECUs capable of FOTA updating; and it is typically the controller that performs firmware updating management for the whole vehicle.

* A typical FOTA system consists of three components:
  * FOTA server: responsible for the management of vehicle software release, and optionally to customize updates for every vehicle client based on OEM policies
  * FOTA client: application responsible for communication with a backend server and updating campaign management for all the other ECUs in the vehicle. Typically runs on FOTA gateway.
  * FOTA agent: application that performs final updating of firmware for ECUs during run-time. It sometimes also runs on FOTA gateway to support self-updating.


