# homebridge-alexa Version 2 - Home Skill Based

[![NPM Downloads](https://img.shields.io/npm/dm/homebridge-alexa.svg?style=flat)](https://npmjs.org/package/homebridge-alexa)

![Icon](https://github.com/NorthernMan54/alexaAwsBackend/blob/master/skillPublish/homebridge-alexa-108.png?raw=true)

Enable Amazon Alexa access to you homebridge controlled devices and accessories.  Full support for all Amazon Alexa devices, including the echo 2nd Generation and software based solutions.  Uses an Amazon smart home skill based approach for integration between HomeBridge and Amazon Alexa.  ( I have stopped using my previous version based on a custom version of HomeBridge, as Amazon is no longer supporting the integration interface I was using on newer Alexa devices, like the Echo 2nd generation. )

* Supports multiple homebridge instances running on your network.
* Auto-discovery of multiple Homebridge's
* Supports devices of homekit Service type Lightbulb, Outlet, Fan, Fan2, Temperature Sensor, Window Coverings and Switch.
* Includes support for brightness and colour.
* This plugin does not have any devices or accessories that are visible from Homekit, and does not need to be added on the Home app.
* The plugin does not need to be installed in your 'main' homebridge instance.  It can be installed in any 'Homebridge' instance in your setup
* Enables control from non-hardware based alexa devices like Invoxia Triby, and AlexaPI.

## New features with Version 2

* Support for color bulbs
* Support for Window coverings/blinds
* Support for Temperature Sensors
* Support for Fan2 aka Dyson fans
* Support for more than 100 accessories
* Support for generation 2 Echo's and other Alexa devices not supported with the original version

Alexa device names are the same as the homebridge device names.

This only supports accessories connected via a homebridge plugin, any 'Homekit' accessories are not supported, and will never be supported.

# Voice commands supported

* Alexa, discover devices
* Alexa, turn on _______
* Alexa, turn off _______
* Alexa, set ______ to 50
* Alexa, what is the temperature in the ______
* Alexa, dim ________
* Alexa, brighten ________
* Alexa, turn _______ red

# Installation of homebridge-alexa

Alexa Home Skill configuration

1. An account to link your Amazon Alexa to HomeBridge needs to created on this website https://homebridge.cloudwatch.net.  This account will be used when you enable the home skill in the Alexa App on your mobile, and in the configuration of the plugin in homebridge.

2. Search for the homebridge skill on the Alexa App/Web site, and link you Amazon account to the account you created above.

Plugin Installation

The setup of the plugin is very straight forward, and requires enabling insecure mode of each homebridge instance you want to control from Alexa.

3. All homebridge instances that you want to control from Alexa need to run in insecure mode with -I included on the command line.  How you make this change will depend on your installation of homebridge, and how you start homebridge.  If you start from the command line, it would look like this:

```
homebridge -I
```

If your using systemd to manage homebridge, the -I is added to the file /etc/default/homebridge in the line, HOMEBRIDGE_OPTS ie.

```
# Defaults / Configuration options for homebridge
# The following settings tells homebridge where to find the config.json file and where to persist the data (i.e. pairing and others)
HOMEBRIDGE_OPTS=-I

# If you uncomment the following line, homebridge will log more
# You can display this via systemd's journalctl: journalctl -f -u homebridge
#DEBUG=
```

If you have multiple homebridge options, the -I should be listed first. ie

```
HOMEBRIDGE_OPTS=-I -U /var/homebridge
```

4. The setup of homebridge-alexa is similar to other plugins, except it doesn't have any devices in the Home app;-)  I'm just reusing the runtime and configuration file management. And it only needs to installed once if you have multiple homeridge's installed.  It will auto-discover and connect to others instances.

```
sudo npm install -g homebridge-alexa
```

5. Login and password in the config.json, are the credentials you created earlier for the https://homebridge.cloudwatch.net website.   This only needs to be completed for one instance of homebridge in your environment, it will discover the accessories connected to your other homebridges automatically.

6. Restart homebridge, and ask Alexa to discovery devices.

# Upgrading from the previous, non skill based version of homebridge-alexa

If you had installed the previous version of homebridge-alexa with the special version of homebridge and HAP-NodeJS, it can disabled without reinstalling homebridge.  You can disable it by removing the configuration parameter ssdp from your config.json.  This will disable the previous version.

```
"ssdp": 1900
```

Also please have Alexa forget all your old devices.


# config.json

```
"platforms": [
  {
    "platform": "Alexa",
    "name": "Alexa",
    "username": "....",
    "password": "...."
  }
],
```

## Required parameters

* username - Login created for the skill linking website https://homebridge.cloudwatch.net
* password - Login created for the skill linking website https://homebridge.cloudwatch.net

## Optional parameters

* pin - If you had changed your homebridge pin from the default of "pin": "031-45-154" ie

```
"platforms": [
  {
    "platform": "Alexa",
    "name": "Alexa",
    "username": "....",
    "password": "....",
    "pin": "031-45-155"
  }
],
```

# Issues, Questions or Problems

* I have started recording troubleshooting tips here based on issues seen by the community [Troubleshooting](Troubleshooting.MD).

* I have created a slack channel at (https://homebridgeteam.slack.com/messages/hap-alexa/) to troubleshoot issues not on the troubleshooting page.

* If you need to log an issue, please include a DEBUG log with your issue.

```
DEBUG=alexa* homebridge -I
```

## Known Issues

* All homebridge PIN's in your setup need to be set to the same value.

# Previous version of homebridge-alexa

* The old version is still available and the instructions for installation can be found [here.](V1_README.md).

# Roadmap

See https://github.com/NorthernMan54/homebridge-alexa/issues/52

# Credits

* Ben Hardill - For the inspiration behind the design.
* Chrisx9 - German translation
* Tait Brown - HomeSkill Icon
* ozno - Recommendation for the bonjour MDNS implementation
