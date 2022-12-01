+++
title = "Introduction to Xilinx Software Command-line Tool"
date = "2022-11-30T12:15:11-06:00"
author = "Surej Joseph"
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
+++

# Introduction to Xilinx Software Command-Line Tool (XSCT)

The Xilinx Software Command-line Tool (XSCT) is an interactive and scriptable 
command-line interface to Xilinx software development tools. Basically, it 
allows to perform all of the operations that the Eclipse-based interface of 
Vitis supports but from a shell environment, including:

Creating and managing projects:
* Platform Projects
* Application Projects
* System Projects

Below is a block diagram of a zynq bare metal application from build system 
perspective while using XSCT:

{{< figure  src="./images/block_diagram.svg" 
            title="Zynq Bare-Metal Application Architecture" >}}

Building an Bare-Metal application using XSCT involves:

1. Create platform using the XSA file.
2. Create Domain for the application.
3. Add drivers and libraries to the Domain.
4. Modify Processor or Domain parameters for the application.
5. Generate the platform.
6. Create an application based off Xilinx app templates.
7. Build the app.

The below example details the steps to build Xilinx FSBL using XSCT.

#### Step 1: Create workspace directory for XSCT.

A workspace directory is need to create platform and build the application. 

```bash
mkdir -p ~/xsct/ws
mkdir -p ~/xsct/hardware
source /opt/xilinx/Vitis/2020.2/settings64.sh

cp system.xsa  ~/xsct_ws/hardware
xsct

xsct% setws ~/xsct/ws
```

#### Step 2: Create platform using the XSA.

Hardware specification file (XSA) is generated from Xilinx Vivado. The XSA file
is in zip format containing the bistream, ps7_init .c/.h/.tcl files and hardware
specification in json. To create a platform, XSCT provides _ platform create_
command. This command takes the path to XA file as input:

```bash
xsct% platform create -name zed_platform -hw ~/xsct_ws/hardware/system.xsa
Opening the hardware design, this may take few seconds.
Starting vitis. This could take few seconds...Eclipse:
The Eclipse executable launcher no longer supports running with GTK + 2.x. 
Continuing using GTK+ 3.x.
done

```
```bash
xsct% platform active
bajie_7010_platform
```

#### Step 3: Create Domain to host the application.

