---
title: Imagining Daemons
description: Get to know daemons and what is their functionality on Linux systems.
image_url: https://itsfoss.com/wp-content/uploads/2021/05/demons-800x400.jpg
---

# Daemons
"There's a saying -- 'The devil is at his strongest while we're looking the other way.' Like a program running in the background silently. While we're busy doing other shit. 'Daemons,' they call them. They perform action without user interaction. Monitoring, logging, notifications" - Elliot Alderson

## What Are Daemons?
Pronounced as `day-mons`. Daemons are processes that run in the background. They are usually used to perform tasks that are not directly related to the user. For example, a daemon might be used to monitor a network connection and log the traffic.

## Identifying Your Daemons
A simple way of identifying daemons on your linux system is to run the `pstree` command.

```bash
pstree
```

## Summoning Your Daemons
You can summon your daemons by running the `service` command.

```bash
service <daemon> start
service <daemon> stop
service <daemon> restart
service <daemon> status
```

Want to spin up a daemon?

```bash
sudo systemctl start <daemon>
sudo systemctl stop <daemon>
sudo systemctl restart <daemon>
sudo systemctl status <daemon>
```
Finally using systemd you can manage your daemons. A quick boot up daemon example has already been published by me here - [Running Scripts On Boot](../Hardware/Microprocessor/Raspberry%20Pi%203/Systemd-Reboot.md).

## Final Thoughts
A quick way to identify daemons even includes looking at the suffix of services. If it ends with a `d` it's a daemon.

Examples:

- `mysqld`
- `systemd`
- `httpd`
- `sshd`