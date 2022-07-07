---
title: MQTT with ExpressJs
description: Setup a MQTT broker and a web server using Express to communicate with it.
image_url: https://assets.emqx.com/images/f984e17ca21ac4b99653a9b666dc537b.png
---

# Using MQTT With Express.js
This documentation covers what I had learnt while setting up MQTT with an Express server built using NodeJS. For this project we had written a script to detect a bot (hardware) and continuously track it using [YOLO](https://pjreddie.com/darknet/yolo/).

## Python Code

The camera will keep detecting the bot and track it, when the bot reaches its sticker the camera should run a post request in Python.

The script for the python script is as follows -
```py
import requests
endpoint = 'http://localhost:3000/send-mqtt'
data = {
    'message': 'Right'
}
r = requests.post(url=endpoint, data=data)
```
If one is connecting via another device they have to simply replace `localhost` with the IP address of the device the server is being run on.

IP of the server can be found by typing in `ipconfig` in Windows and scrolling to the `IPv4` section.

**Note - If the script gives an error saying the module requests is not found just run `pip install requests`**.

## The Server
The broker used for sending messages is **mosquitto**. The url is as follows: `mqtt://test.mosquitto.org`. The following server is open to anyone hence sensitive messages should be avoided.

### Using NodeJs
The first steps involve installing Node itself from their website [here](https://nodejs.dev/).

After Node is setup in a new folder run the following line of code:
`npm init`

Fill in all the details or just keep hitting enter till a `package.json` file is formed.

Proceed to install the **express, body-parser and mqtt** packages by using the following command:
`npm i express body-parser mqtt`

If somehow this command fails install each separately in the following format: `npm i <package name>`

### Server Code
```js
var express = require("express");
var bodyParser = require("body-parser");
var app = express();
var mqttHandler = require("./mqtt_handler");

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

var mqttClient = new mqttHandler();
mqttClient.connect();

// Routing
app.post("/send-mqtt", function (req, res) {
  mqttClient.sendMessage(req.body.message);
  res.status(200).send("Message sent to mqtt");
});

var server = app.listen(3000, function () {
  console.log("App running on port.", server.address().port);
});
```
### MQTT Handler
```js
const mqtt = require("mqtt");

class MqttHandler {
  constructor() {
    this.mqttClient = null;
    this.host = "mqtt://test.mosquitto.org";
    this.username = "YOUR_USER"; // mqtt credentials if these are needed to connect
    this.password = "YOUR_PASSWORD";
  }

  connect() {
    // Connect mqtt with credentials (in case of needed, otherwise we can omit 2nd param)
    this.mqttClient = mqtt.connect(this.host);
    // , { username: this.username, password: this.password }
    // Mqtt error calback
    this.mqttClient.on("error", (err) => {
      console.log("An error has occured: ", err);
      this.mqttClient.end();
    });

    // Connection on success
    this.mqttClient.on("connect", () => {
      console.log(`Mqtt client connected`);
    });

    // Mqtt subscriptions
    this.mqttClient.subscribe("mytopic", { qos: 0 });

    // Logging a message when it arives
    this.mqttClient.on("message", function (topic, message) {
      if (!message.toString().startsWith("32333")) {
        console.log(message.toString());
      }
    });

    this.mqttClient.on("close", () => {
      console.log(`mqtt client disconnected`);
    });
  }

  // Sends a mqtt message to topic: mytopic
  sendMessage(message) {
    this.mqttClient.publish("mytopic", message);
  }
}

module.exports = MqttHandler;
```