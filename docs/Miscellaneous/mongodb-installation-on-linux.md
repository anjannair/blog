# Installing MongoDB Community on Ubuntu
A small guide to install MongoDB Community on Ubuntu. This guide was created after a minor inconvenience I faced to get the server up and running.

## Getting Started
The starting few steps can be found [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) on their website

Starting the mongodb server - 
```shell
sudo service mongod start
```

Checking the status of the server - 
```shell
sudo systemctl status mongod
```

Stopping the mongodb server - 
```shell
sudo service mongod stop
```

## Error faced
On trying to get the server status I always got the following error - 
`Active: failed (Result: exit-code)`

I tried all the troubleshooting guides until I stumbled on a StackOverflow answer detailing the solution to this
Just do those two commands for temporary solution:

```shell
sudo rm -rf /tmp/mongodb-27017.sock
sudo service mongod start
```

### Cause of the error
For details:

That shall be fault due to user permissions in .sock file, You may have to change the owner to monogdb user.
```shell
chown -R mongodb:mongodb /var/lib/mongodb
chown mongodb:mongodb /tmp/mongodb-27017.sock

```
## Uninstall MongoDB completely

```shell
sudo service mongod stop
sudo apt-get purge mongodb-org*
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb

```