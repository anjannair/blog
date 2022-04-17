# Running Scripts On Boot

Sometimes one may wish to run scripts at boot. I looked at a lot of solutions including crontab but the only solution that worked for me was `systemd`. This can be done for all Linux systems but since I did this on the Raspberry Pi I have included it here.

## Getting started

We will be creating a `.service` file in `/usr/lib/systemd/system`.

This will be followed by `sudo nano /etc/systemd/system/discord-webhook.service`. In the file you will include the following lines of code

```service
[Unit]
Description=Discord Webhook IP sender

[Install]
WantedBy=multi-user.target

[Service]
ExecStart=python /bin/main.py
Type=simple
User=pi
Group=pi
WorkingDirectory=/bin
Restart=on-failure
```

Once done hit **Ctrl+X** followed by **Y** and **Enter**

Before actually starting the service you may want to ensure that you have the `main.py` code. Here is the code (you may change it to your needs)

Run this - `sudo nano /bin/main.py`

```py
import socket
import requests
import urllib.request

webhookURL = '<webhook url>'
hostname = socket.gethostname()
external_ipv6 = urllib.request.urlopen('https://v6.ident.me').read().decode('utf8')
external_ipv4 = urllib.request.urlopen('https://v4.ident.me').read().decode('utf8')


data = {
    'username': 'Server IP Webhook',
    'embeds': [{
        'title': 'Server started!',
        'description': hostname + '\n' + 'IPV6' + ': ' + '`' + external_ipv6 + '`'  + '\n\n' + 'IPV4 ' + ':'  + '`' + external_ipv4 + '`',
    }]
}

result = requests.post(webhookURL, json = data)

try:
    result.raise_for_status()
except:
    pass
```

1. Run `sudo systemctl daemon-reload`
2. Run `sudo systemctl start discord-webhook.service` (if there is an output then your code is functioning successfully!)
3. Finally `sudo systemctl enable discord-webhook.service`

And you're good to go! Your script will now run at startup!

Credits - [StackOverFlow](https://stackoverflow.com/a/38484205)