# Setting Up Ubuntu

This tutorial is made from what I learnt during my experience of setting up Ubuntu on my virtual machine as well as dual booting. If you are interested in knowing how to setup Ubuntu on VMware the tutorial is right under this paragraph. To setup for dual boot you'd find it below the VMware setup instructions.

## VMware

Install the VMware Workstation first from the website (one can optionally get the keys from GitHub and get the Pro version for free).

Download the Ubuntu iso (in my case Windows) on the host machine which can be found on the official Ubuntu site.

Open VMware and create new VM followed by these steps:

- Will install OS later
- `Linux - Ubuntu 64bit`
- Name the VM whatever you like
- Give it at least 40GB and it stays in split
- Customize Hardware:- 4GB RAM minimum, Cores - 4, New CD/DVD => Select iso image, Finish
- Play VM => Software update download and install
- Install Ubuntu
- Minimal Install (If preferred you can go for the other one but I did not require that)
- Check the "Install third party checkbox"
- Erase and install Ubuntu (don't worry your data on your host PC will not be affected if this option is clicked)

Rest steps are easy and configurable on your own.

Let it install, it takes some time and on completion a success message is shown. Once that is done a prompt to restart the VM will be shown and you are done! 

To sync Ubuntu's calendar with your Google Calendar you can login with Google too!


### Some Fixes I had To Search For

1. In the minimalist version the codecs for audio was missing so you have to install ffmpeg using sudo from the CLI.
2. To activate the camera from VMware, when on full screen mode hover to the top and find the camera icon near the notes and right click on it. This will present a option to Enable the camera. Wait for some time and if it gives an error try again. On your second or third try it should work after giving a prompt. 
3. Use the update command to find for updates and upgrade to upgrade the packages.


## Dual Boot (Windows)

Some pre-requisites for doing this include -

- A good USB flash drive (4 GB minimum to install)
- [Balena Etcher](https://www.balena.io/etcher/) installed on Windows
- The latest Ubuntu `.iso` file downloaded and ready

Once you have the above mentioned items ready all you have to do is fire up Balena with the USB plugged in to your device. Balena will automatically detect your USB. On rare circumstances if Balena does not detect your USB, you should check if the USB is being detected by your device first.

A **FLASH** option should appear when everything is ready. Flashing takes some time and once done you are good to go!

Head over to Windows and search for **Disk Management** and create a new partition to install Ubuntu in. A minimum of 40GB is recommended, although I had allocated 100GB. 

Note - The steps mentioned below are for Dell devices, your BIOS menu and settings may be different so do refer their documentations if the need be. Although the steps mentioned below shouldn't defer depending on device.

The following steps have to be done in order to dual boot Ubuntu - 

- Reboot your device and when it is just about to startup press `F12` or whichever shortcut takes you into `BIOS` mode.
- Once into `BIOS` mode, in *Boot Menu* or in *Boot Devices* you will find your USB device name mentioned. Click on that and wait for the screen to load.
- Once the Ubuntu screen loads click on `Install Ubuntu`.
- Select `Normal Installation` and you can then optionally install third-party software for graphics etc.
- This step is the most important step of all. When the option of `Installation Type` is asked, click on `Something else`, find for your partition allocated for Ubuntu in the GUI. In the popup select `Primary` as the type of partition, set the use as `Ext4 journaling file system` and finally the mount point should be set as `/`. Verify if the `Windows Boot Manager` has the type `efi` and then go ahead and click on **Install Now**.
- The next few steps are self-explanatory and the installation should now take place.

Now on rebooting your device you shall notice that a bootloader called GRUB starts up. On selecting `Ubuntu`, `Ubuntu` shall load and on selecting `Windows Boot Manager` Windows will load.

### Issues Faced In Dual Boot

One major issue faced when installing Ubuntu on Dell was that I had to turn off RST.

![Error Image](https://res.cloudinary.com/practicaldev/image/fetch/s--HmcbQ6-A--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/3opvjmf0c8bj7k6yylek.png)

[This](https://dev.to/lakshmiwarrier/dual-booting-windows-10-and-ubuntu-20-04-with-rst-issue-fixed-4le8) article provides a great solution to fix the issue. However if you lazy to read the article here are the steps to fix the issue -

- Open CMD in Windows (`Run as administrator`) and type in `bcdedit /set {current} safeboot minimal` 
![Command Image](https://res.cloudinary.com/practicaldev/image/fetch/s--mNMByZgU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/nyyj81pvyv70ld73hhun.png)
- Go into BIOS setup and search for `SATA mode` and change the current setting from whatever it was to `AHCI`. A frightening question can be asked: `All existing data stored on the drives will be erased when resetting the controller mode. Do you want to proceed? [Yes] [No]` just click on `Yes` without worrying. Press `F10` and it will save and exit from `BIOS Setup`. 
- The computer will startup in `safe boot mode`. Open CMD and type the following - `bcdedit /deletevalue {current} safeboot`
![Second CMD Image](https://res.cloudinary.com/practicaldev/image/fetch/s--v09mfloh--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/mq28k2149ug3j4qoxl7n.PNG)

And done! Your Ubuntu should start without any issues now!

### Personal Setup

 - [Spotify](https://github.com/abba23/spotify-adblock) without ads :)
 - [Grub](https://github.com/AdisonCavani/distro-grub-themes) themes.
 - [KDE Connect](https://kdeconnect.kde.org/) to connect it with your phone.
 - [Gnome Tweaks](https://itsfoss.com/gnome-tweak-tool/)