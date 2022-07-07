---
title: Xilinx Setup on Ubuntu
description: Verilog programming using Xilinx Vivado for Linux made easy.
image_url: https://allaboutfpga.com/wp-content/uploads/2020/06/Vivavo-software-link.png
---

# Xilinx Download And Setup In Ubuntu

Xilinx has been one software used to program the FPGA board in Verilog. Currently (at the time of writing) quite funnily this software fails to install in Windows 11 and has some issues installing in Windows 10. Linux however does not fail us here. This tutorial has been picked up from [this](https://www.youtube.com/watch?v=yzEIQLQZYpk) YouTube tutorial but with a few changes.

## First Step

As of 2022 in April the latest version of Xilinx is 14.7. Head over [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/archive-ise.html) and click on 14.7, scroll down to the ISE Design Suite and install the **Full Installer for Linux**. A simple popup to sign-up/in will come up.

## Extract the contents

After the download is complete extract the file using the following command - 

```shell
tar -xvf Xilinx_ISE_DS_Lin_14.7_1015_1.tar
```

This extracts the whole tar file.

## Running The Setup

To further setup the Xilinx software we run the following - 

```shell
sudo ./xsetup
```

This will run the setup!

### Error fixing

During this you may run into an issue which says *libncurses.so.5: cannot open shared object file: No such file or directory*. A fix to this is done by running 

```shell
sudo apt-get install libncurses5 
```

## Next Steps

The next steps are intuitive and can easily be figured out by clicking **Next**

## Finally Running It

Run this command first - 

```shell
source /opt/Xilinx/14.7/ISE_DS/settings64.sh
```

and then just type

```shell
ise
```

in the command line. You are good to go!

### Error I faced

The video mentioned above has a step involving adding the *source..* command to *.bashrc*. This led to errors as well as problems on my bash terminal. So avoid it and follow the step mentioned above.