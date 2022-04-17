# Monitoring Raspberry Pi With Dashboard

One of the interesting things one can do with their RaspberryPi is setting up a monitoring dashboard. For this we use **Grafana** (a dashboard service), **InfluxDB** (the database) and **collectd** (a metric collection service).

## Updating and Upgrading

Down to your basics, update and upgrade your system first

```bash
sudo apt update && sudo apt upgrade
```

## InfluxDB

Installing InfluxDB

```bash
sudo apt install influxdb influxdb-client
```

### Fiddling with Configuration

```bash
sudo nano /etc/influxdb/influxdb.conf
```

The values of the directories are going to be changed to `tmp` so that values are stored in RAM.

End result should look like this

```conf
[meta]
dir = "/tmp/influxdb/meta"

# ABRIDGED

[data]
dir = "/tmp/influxdb/data"
wal-dir = "/tmp/influxdb/wal"
```

Now we will bind our data to localhost only.

```conf
[http]
enabled = true
bind-address = "127.0.0.1:8086"
```

Changing collectd configuration

```conf
[[collectd]]
enabled = true
port = 25826
database = "collectd_db"
typesdb = "/usr/share/collectd/types.db"
```

Done! Now we will run the following code to enable and start InfluxDB

```bash
sudo systemctl enable influxdb
sudo systemctl start influxdb
```

If you now run `influx` in your terminal you should see it work!

Run these commands
```sql
CREATE DATABASE collectd_db
CREATE RETENTION POLICY "twentyfour_hours" ON "collectd_db" DURATION 24h REPLICATION 1 DEFAULT
```

"**twentyfour_hours** is the name of the policy, should you want to delete it later. the **REPLICATION** directive is only relevant for clustered systems but must be set nonetheless. Here, we only want one copy of our data.

Press **CTRL + D** to exit the influx prompt, and start with the next step."

## collectd

Installing collectd - 

```bash
sudo apt install collectd collectd-utils
```

Once again, open the configuration file `/etc/collectd/collectd.conf` and ensure the following settings are not commented out:
(Usually they aren't commented out but just check)

```
Hostname "microserver314"

Interval 60
LoadPlugin syslog
LoadPlugin cpu
LoadPlugin cpufreq
LoadPlugin df
LoadPlugin disk
LoadPlugin entropy
LoadPlugin interface
LoadPlugin irq
LoadPlugin load
LoadPlugin memory
LoadPlugin network
LoadPlugin processes
LoadPlugin swap
LoadPlugin thermal
LoadPlugin users
```

What does all this mean??
The individual plugin report:

1. cpufreq: the CPU frequency
2. df: available disk space
3. entropy: available entropy for (pseudo) random number generation
4. interface: transmitted and received bytes on the network interfaces
5. irq: number of times the interrupt handler of the OS has been called
6. load: CPU load averages
7. memory: available and used main memory
8. network: write data to network servers
9. processes: number of processes and their state
10. swap: size and usage of the swap partition
11. thermal: CPU temperature
12. users: number of logged in users (via SSH, …)


Now that the plugins are loaded, we must configure some of them individually:

```
<Plugin df>
# This will ignore uninteresting file systems
# to keep our DB from cluttering
    FSType rootfs
    FSType sysfs
    FSType proc
    FSType devpts
    FSType tmpfs
    FSType fusectl
    FSType cgroup
    Ignore Selected true
</Plugin>

<Plugin "syslog">
# Skip messages with info label
    LogLevel "warning"
</Plugin>
```

Finally, we must tell collectd where to write all the data. We will set it to the host and port of InfluxDB’s collectd listener:

```
<Plugin "network">
    Server "127.0.0.1" "25826"
</Plugin>
```

Finally making it work!

```bash
sudo systemctl enable collectd
sudo systemctl start collectd
```

### Testing The Data
```bash
influxdb
```
```sql
USE collectd_db
SELECT * FROM processes_value WHERE ("type_instance" = 'sleeping') ORDER BY time DESC LIMIT 1
```
If you get an output you are good to go!

## Grafana
Finally we install the dashboard
To add the Grafana APT key to your Raspberry Pi’s keychain, run the following command
```bash
curl https://packages.grafana.com/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/grafana-archive-keyrings.gpg >/dev/null
```
With the key added, we can now safely add the Grafana repository to our Pi’s list of packages sources.

Use the following command on your Raspberry Pi to add the repository to the list.

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana-archive-keyrings.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

Finally updating our Pi
```bash
sudo apt update
```

And installing it
```bash
sudo apt install grafana
```

Enabling and starting the Grafana service
```bash
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

Now open Grafana using your host IP address and on port *3000*. The password and username for the dashboard is **admin**.

Note - Do not like port 3000 or another service is utilizing it? Change the port in `/etc/grafana/grafana.ini` you have to change in `/usr/share/grafana/conf/defaults.ini`.

Remove the semicolon in `/usr/share/grafana/conf/defaults.ini` and chance the port! You're good to go!


# Finally
1. Open Grafana and if not prompted, head to settings (the gear icon) and click on **Data Sources**
2. Add the data source as InfluxDB as given below

![Top Page](https://cdn.discordapp.com/attachments/456482075307016192/965186519646216253/unknown.png)
![Bottom Page](https://cdn.discordapp.com/attachments/456482075307016192/965192157235384340/unknown.png)

Done! Now just save and test! If it works you are 95% done!

## Getting the beautiful output

Head over to the **+** sign and **Import** [this](https://ch-st.de/assets/posts/raspberry-pi-grafana-influxdb-collectd/dashboard.json) and you shall now be seeing an output!