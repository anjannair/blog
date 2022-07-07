# VeraCrypt (Cross-Platform)
VeraCrypt is a free and open source encryption software. The software can create a virtual encrypted disk that works just like a regular disk but within a file. It can also encrypt a partition or the entire storage device with pre-boot authentication.

## Installation
This software is available on Mac OSX, Linux and Windows. Just simply download the installation file from their [official site](https://www.veracrypt.fr/en/Home.html). At the time of writing this was their official site.

### For Linux
Since I used Ubuntu my guide will be based on Debian based systems. Just download the Debian/Ubuntu `.deb` package from the website.

Run the command - 

```shell
sudo dpkg -i VeraCrypt_File_Name.deb
```
Replace VeraCrypt_File_Name.deb with the name of your downloaded `.deb` file.

### For Windows
A simple `.exe` installation will work like a charm.

## Setup

- Get your USB stick ready and plug it into your PC. 
- Boot up VeraCrypt and click on the `Create Volume` option.

Two options will load:

1) **Create an encrypted file container**: If this option is used VeraCrypt will create a file which will be used as a virtual mount point. A key point to remember here is that once a size is allocated to the file it cannot be increased nor decreased as opposed to the next option.

2) **Create a non-system partition/drive**: If this option is used VeraCrypt will encrypt your whole drive. The size of the drive is the size that will be available to you.

VeraCrypt suggests option 1 but I would say go for 2 if you do not know how much content you plan to encrypt. In this guide we will be going ahead with option 2.

💡 **Note** - *If you are interested in option 1: Check out [this](https://www.youtube.com/watch?v=4SBWc_cQm-Y) video.*

 - After selecting your encryption type, it is time to select volume type. The options here are quite understandable. Unless you are possessing very sensitive material and your life is at stake go for the **Standard VeraCrypt Volume**.

After selecting your drive aka the USB stick mount location, there are 2 cases here:

1) Your USB stick may be having content already.
2) Your USB stick is empty.

- If your USB stick is empty no worries, in **Volume Creation Mode** select the *Create encrypted volume and format it* option. If your USB stick has content that you want then select the *Encrypt partition in place* option.

- In **Encryption Options** if you know what you are doing change it to your preference. I left it at the default options as that sufficed me.
- **Volume Password** should be something that is strong to avoid dictionary attacks. Usually a unique alphanumeric password should suffice.
- 💡 **This is important**, if you plan to use your USB stick cross-platform, which you will, it is important that in **Format Options** you should select NTFS. Users who encrypted their partition and did not format it may not get this option.

### Final steps

- After all of this is done you will get a interesting window called the **Volume Format**. This will ask you to shake your mouse till a particular bar is full.
- Once done a 'Format' option should be available. Click that and depending on the size of your drive and the speed it could take time. My 64GB USB stick took up-to an hour to encrypt.

On a conclusive note to the setup I would like to say the *Final steps* for those who had content in their volume could be different nevertheless, it isn't rocket science to figure it out. 

## General Use

To now use your volume after it has been encrypted, ensure the device you want to use your volume on has VeraCrypt.

- Open VeraCrypt and click on `Select Device` and select the encrypted volume mount point.
- Select the slot you want it to mount on. On Linux it will show as `1`,`2`,`3`...etc and on Windows it will show as `A`,`B`,`C`...etc.
- Click on `Mount` after selecting the slot and enter your password. Done! Now just navigate to the mount spot and enjoy accessing your files like a normal volume. Once done click on `Dismount`.

## Videos Used As Reference:

1) [How To Use VeraCrypt On Linux](https://www.youtube.com/watch?v=4SBWc_cQm-Y)
   
2) [Linux Tips - Encrypt USB Drive on Windows Linux and MacOS (VeraCrypt)](https://www.youtube.com/watch?v=w0hMYpBpjJM)
   
3) [Hide & Encrypt Your Secret Files With VeraCrypt](https://www.youtube.com/watch?v=xWDXRH1mWHM)