# How to switch from Windows to ElementaryOS
Ensure you download the *.iso* file from their [website](https://elementary.io/). Scroll down to the download section, if you wish to pay you can pay else click on custom and enter the amount as 0. Once that is done the download will be initiated.

### The Installation
The same instructions are mentioned on their installation guide over [here](https://elementary.io/docs/installation#installation). Be sure to check the specifications required for the USB flash drive as well as the system.

### Flashing
Once the image file is downloaded Etcher does the magic. The process takes some time so hold tight.

### Booting
The device used to install Elementary in my case was Dell hence on booting **F12** was enough to enter Boot Mode. Once you are in boot mode the USB should be visible in the options on the left (varies per device). Click on it and viola!

If you are booting from the EOS image for the first time let it run a file check. Once the check is done a basic setup screen will pop-up. Select the clear drive option and wait for some time.

(Optionally the demo mode can be tried on first to check how your device suits with EOS)

After the initial setup is done and an account is setup you are ready to go!!

NOW THE NEXT TIME YOU POWER ON YOUR DEVICE IT SHOULD AUTOMATICALLY START EOS!

(Side note - You can eject the USB and remove it now)

## Initial tips and tricks
 - Firefox or your preferred browser can be installed from [FlatHub](https://flathub.org/home). All major apps can be found there.
 - The weird close and maximize button can be tweaked too using this package - https://github.com/pantheon-tweaks/pantheon-tweaks
 - In settings I noticed the **Location** permission is on by default, one can fix that by switching it off.
 - Desktop folders has an app called DesktopFolder which can usually be installed using the AppCentre but it has not been optimized for EOS6 hence a pull request fixing the error can be found here - https://github.com/spheras/desktopfolder/pull/328 (as of October 2021).