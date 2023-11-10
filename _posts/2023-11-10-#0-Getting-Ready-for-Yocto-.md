---
layout: post
title: 00 - Getting Ready for Yocto Project
date: 2023-11-10 00:00:00
categories: [yocto]
tags: [yocto, beagleBone]
last_modified_at: 2023-11-10
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