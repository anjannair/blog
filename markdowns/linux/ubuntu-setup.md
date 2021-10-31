# Getting Started
Install the VMware Workstation first from the website (One can optionally get the keys from GitHub and get the Pro version).

Install the iso on the host machine (in my case Windows)

Open VMware and create new VM followed by these steps:
- Will install OS later
- Linux - Ubuntu 64bit
- Name the VM
- Give it atleast 40GB and it stays in split
- Customize Hardware:- 4GB RAM minimum, Cores - 4, New CD/DVD => Select iso image, Finish
- Play VM => Software update download and install
- Install Ubuntu
- Minimal Install (If preferred you can go for the other one but not required)
- Check the "Install third party checkbox"

Erase and install Ubuntu

Rest steps are easy and configurable on your own

Let it install, it takes some time but not too much too

Restart

Login now

Enter your Google account if sync is wanted with Ubuntu Calendar
<br><br>

# Some Fixes I had To Search For
1. In the minimalist version the codecs for audio was missing so you have to install ffmpeg using sudo from the CLI.
2. To activate the camera from VMware, when on full screen mode hover to the top and find the camera icon near the notes and right click on it. This will present a option to Enable the camera. Wait for some time and if it gives an error try again. On your second or third try it should work after giving a prompt. 
3. Use the update command to find for updates and upgrade to upgrade the packages.