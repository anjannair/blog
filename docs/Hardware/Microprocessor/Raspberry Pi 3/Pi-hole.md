---
title: Pi-hole with Raspberry Pi 3
description: Setup a Raspberry Pi 3 to be a Pi-hole server for your network and block ads and trackers.
image_url: https://howchoo.com/media/nt/uw/mt/the-pi-hole-logo.png?width=1440&auto=webp&quality=70
---

# Pi-hole Using Raspberry Pi 3
A pi-hole is basically a black-hole for internet ads. The project is an open source ad blocking software at the DNS level.

## Installing Pi-hole
The easiest way of installing Pi-hole is by running the following script
```bash
curl -sSL https://install.pi-hole.net | bash
```

The script will do everything to install the software and convert your Raspberry Pi into a pi-hole.

Once done, you can open the web interface of the pi-hole. The web interface is simple to understand and easy to setup too.

Finally before moving on we set the DNS of our router to the IP address of our pi-hole.

## Ad-lists
To add lists apart from the one used at setup we go to *Group Management*>*Adlists*

My preferred lists are - 

1) Normal Hosts - https://v.firebog.net/hosts/static/w3kbl.txt
   
2) Adguard List - https://v.firebog.net/hosts/AdguardDNS.txt
   
3) EasyList - https://v.firebog.net/hosts/Easylist.txt
   
4) Privacy - https://v.firebog.net/hosts/Easyprivacy.txt
   
5) Windows Spyware - https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt
   
6) Anti-Malware List - 	https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt
   
7) Threat Intel by OSINT - https://osint.digitalside.it/Threat-Intel/lists/latestdomains.txt
   
8) Adult sites - https://blocklistproject.github.io/Lists/porn.txt

You can add all this together by adding the URLs separated by space. After doing so make sure to update the *Gravity* list by running `pihole -g` command or by heading to *Tools* and *Update Gravity*. This downloads the list and updates it.

## DNS over HTTPS (DOH)
To setup DNS over HTTPS on your pi-hole we use the docs given in the official website [here](https://docs.pi-hole.net/guides/dns/cloudflared/).

**Note** - Go with the manual method as the automatic did not work for me.