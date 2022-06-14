# PiVPN Setup
PiVPN is a **self hosted VPN service** one can install on the Raspberry Pi. This service is light and serves both OpenVPN or Wireguard depending on the user's choice. This tutorial will show the steps in installing PiVPN with a **Wireguard** configuration.

## How is this different from any other tutorial?
The initial setup is no different from all other references but here we use Wireguard along with **IPv6** to setup the server. Most of the times one cannot get a static IPv4 address to setup a PiVPN, IPv6 fixes that issue for these cases as 99% of the time it remains static. Incase your ISP changes your IPv6, well, its time to switch to a different one.

Yes some may say one can use a DDNS service but honestly its up-to you. My ISP did not allow me to port forward on my IPv4 address but IPv6 had no such restrictions. Hence this tutorial covers IPv6.

## Installing the software
**A small pre-requisite** : Already have [Pi-hole](https://pi-hole.net/) installed as you can pass all your queries through the Pi-hole.

> Instead of browser plugins or other software on each computer, install Pi-hole in one place and your entire network is protected.

Once Pi-hole is setup all you have to do is run the script to install PiVPN

```bash
curl -L https://install.pivpn.io | bash
```
An automatic installation of PiVPN should take place and just go through with the installation GUI. There will be one part where you will be asked to input your **static IPv4 address**. In that just hit enter and move on, we will be making changes to that later!

After it is installed, in your terminal with your favorite editor (nano or vim) edit the Wireguard configuration file -

```bash
sudo nano /etc/pivpn/wireguard/setupVars.conf
```

Your end result should be something like this -

```bash
PLAT=Debian
OSCN=bullseye
USING_UFW=0
IPv4dev=wlan0
IPv6dev=wlan0
install_user=root
install_home=/home/root
VPN=wireguard
pivpnPORT=51820
pivpnDNS1=some.dns.com
pivpnDNS2=
pivpnHOST="[YOUR IPV6 ADDRESS]"
INPUT_CHAIN_EDITED=0
FORWARD_CHAIN_EDITED=0
INPUT_CHAIN_EDITEDv6=0
FORWARD_CHAIN_EDITEDv6=0
pivpnPROTO=udp
pivpnMTU=1420
pivpnDEV=wg0
pivpnNET=10.53.171.0
subnetClass=24
pivpnforceipv6route=1
pivpnforceipv6=1
pivpnenableipv6=1
pivpnNETv6="fd11:5ee:bad:c0de::"
subnetClassv6=64
ALLOWED_IPS="0.0.0.0/0, ::0/0"
UNATTUPG=1
INSTALLED_PACKAGES=(grepcidr bsdmainutils iptables-persistent wireguard-tools qrencode unattended-upgrades)

```
### A Few Tips
- In the above options put your IPV6 (in *pivpnHOST*) inside the square brackets for it to work.
- The *pivpnDNS1* should be automatically configured to your pi-hole address, if not, then manually configure it.
- Edit *install_user* and *install_home* to your user and home directory respectively.
- **Mainly** ensure *pivpnforceipv6* and *pivpnenableipv6* are set to 1.

Now just run
```bash
pivpn -add
```
to add your client to the list of devices

AND
```bash
pivpn -qr
```
To generate a QR code for mobile devices

Your PiVPN should be good to go! Make sure to make changes to your UFW configurations to allow UDP traffic through the inputted port (by default is 51820).