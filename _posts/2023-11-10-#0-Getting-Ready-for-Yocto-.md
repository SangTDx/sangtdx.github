---
layout: post
title: 00 - Getting Ready for Yocto Project
date: 2023-11-09 00:00:00
categories: [yocto]
tags: [yocto, beagleBone]
last_modified_at: 2023-11-09
---

### Your Workstation Setup

<figure>
  <img src="/assets/img/blogs/yocto/Your_Workstation_Setup.png" alt="Your Workstation Setup">
  <figcaption>Your Workstation Setup</figcaption>
</figure>

### Host Environment

* Depending on the Host System used, make sure that you have installed all
required packages to run Yocto

* Ubuntu
```bash
sudo apt-get install gawk wget git-core diffstat unzip texinfo \
build-essential chrpath libsdl1.2-dev xterm curl
```

* For Virtual Machine setups, set the minimal memory size to 1GB and minimal
disk size to 32GB

* Install the repo tool from google
```bash
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

### Embedded Linux Reference Model
<figure>
  <img src="/assets/img/blogs/yocto/Embedded-Linux-Reference-Model.png" alt="Embedded Linux Reference Model">
  <figcaption>Embedded Linux Reference Model</figcaption>
</figure>

### Build System – Do We Need It?

* Without a build system, each application has to be built manually, or with help
from a custom script
* We need to find a correct toolchain
* We need to configure and build each package and application by hand
* For each package/application in the file system, we need to figure out the crossdependency, which may involve changing configurations for multiple packages
* If this does not sound painful enough, the next steps involve building a file
system formatted correctly for the chosen form of deployment
* Sharing your work with colleagues is also difficult

###  Yocto Project Governance

* Organized under the Linux Foundation
* Split governance model
* Technical Leadership Team
* Advisory Board made up of participating organizations

<figure>
  <img src="/assets/img/blogs/yocto/member.png" alt="Yocto Member">
  <figcaption>Yocto Member</figcaption>
</figure>

###  What is Yocto Project?
**Yocto is not a Linux distribution. Yocto creates one for you**

* An Open source project with a strong community
* A collection of embedded tools and projects
    * Place for Vendors to release BSPs
    * Application Development Tools (ADT) including Eclipse plug-ins
* Support for ARM, x86, MIPS and Power
* Layer approach enables re-use of software
* Complete build system for Linux OS
    * Latest kernel (LTSI)
    * Toolchain
    * Packages
    * Documentation
* Releases every 6 months

### Yocto Project Releases
**Yocto names its releases, similar to Android** [Releases Links](https://wiki.yoctoproject.org/wiki/Releases)

<figure>
  <img src="/assets/img/blogs/yocto/yocto-releases.png" alt="Yocto Releases">
  <figcaption>Yocto Releases</figcaption>
</figure>

###  The Yocto Project Nomenclature
* BitBake
   * Powerful and flexible build engine
   * Determines dependencies and schedules tasks
* Metadata
  * A structured collection of “recipes” which tell BitBake what to build
  * Organized in layers
* Poky
  * The reference system
  * It is a collection of projects and tools, used to bootstrap a new distribution based on the Yocto Project
* Recipes
  * Describe how to fetch, configure, compile and package an application and images
  * Have a specific syntax.
* Layers
  * Sets of recipes, matching a common purpose. E.g. Freescale i.MX enabling layer

###  Yocto Project

<figure>
  <img src="/assets/img/blogs/yocto/yocto-project.png" alt="Yocto Project">
  <figcaption>Yocto Project</figcaption>
</figure>

###  Poky

<figure>
  <img src="/assets/img/blogs/yocto/yocto-project.png" alt="Poky">
  <figcaption>Poky</figcaption>
</figure>

###  The Yocto Project Workflow

<figure>
  <img src="/assets/img/blogs/yocto/yocto-workflow.png" alt="The Yocto Project Workflow">
  <figcaption>The Yocto Project Workflow</figcaption>
</figure>

### End

let's start Yocto project in next chapter