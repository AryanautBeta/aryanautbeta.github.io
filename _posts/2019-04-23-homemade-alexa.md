---
title: "DIY Alexa"
date: "2019-04-23"
category: category-1
tags: 
  - "alexa"
  - "diy"
  - "how-to-make-alexa-at-home"
  - "step-by-step"
image: "/images/2019/img_0253-1.jpg"
---

## Introduction

Hello everyone! My first project of the year was to build an Alexa device using a raspberry pi computer. After around three weeks, it is finally working!

## How it works

It works on the cloud based service called the Alexa Voice Service (AVS) which is provided by **Amazon Developer** a platform for selling, testing and building applications in the amazon app store. The AVS can be provided to anyone with a developer account.

## Making Alexa

Parts:

- Raspberry Pi 3b+
- AUX cable
- USB microphone
- LED ring light (I used a ring light of 16 LEDs)
- Speaker Hat (optional)
- I2C amplifier (optional)
- Bluetooth speaker or any speaker than can be connected using an AUX cable

**Alexa Installation**

The Alexa Voice Service cannot be just installed and expected to work immediately. Even its installation itself is a complex process. The AVS comes as a .git file from this github [link](https://github.com/alexa/avs-device-sdk).

I had to create a few folders inside the raspberry pi and install a few dependencies. For more information on which dependencies and folders use this [link](https://github.com/alexa/avs-device-sdk/wiki/Raspberry-Pi-Quick-Start-Guide).

I used the command `cmake` to open up the .git file and spread its contents into the folders. I populated those files with more contents from the .git file using the command `make` . The second process of populating is called building and is a very long process. Get familiar with this term because if you're like me, you will have to this process several times.

After 4 million rebuilds, 6 memory card wipes, 4 deletions of the project files and 26 repetitions of my hour long music playlist, the build files were finally written. The final part of the installation was the file config.json which contained the client id and client secret of the developer account. This file has to be downloaded from the developer site and moved into the raspberry pi. I put it in my home directory for simplicity. Then the setup command is run and the initialisation script is started. The script opens up the SampleApp which is an application that runs alexa. This application is not like usual applications since it runs in the command line.

<p align="center">
<img src='/images/2019/screenshot-from-2019-04-23-08-39-17.png'>
</p>

The startup file is in the following directory if anyone is interested:

```
/home/pi/sdk-folder/sdk-source/avs-device-sdk/tools/Install
```

Now alexa is running fine.

**Audio**

Audio was a big problem for me. Initially I had to use the Raspberry Pi Zero which had no headphone jack. So I connected an I2S amplifier and the speaker hat which worked fine bu for some reason after installing alexa, the speaker stopped working. Then my dad and I built a small filter circuit and connected it to a headphone jack.

<p align="center">
<img src='/images/2019/img_5339.jpg'>
</p>

The filter circuit

The headphone jack was plugged into a bluetooth speaker which initially seemed to do the trick. But again after alexa installation, it stopped working. So instead of the Pi Zero, we used a Raspberry Pi 3b+ as mentioned earlier since it has a headphone jack and filter circuit built into it. Now the audio was working perfectly with the bluetooth speaker and the AUX cable even after installation.

The final step was to bring in the I2C (not I2S) amplifier and connect it to the speaker hat from earlier and the audio still worked! However the audio sounded like someone speaking through a fan while driving a truck. In other words it was too distorted.

In the end we used the bluetooth speaker and the cable rendering the speaker hat and the amplifier as a showpiece.

**Lights**

The lights are in my opinion a key for the fully built alexa. I used the WS2812 lED ring light with 16 RGB LEDs. They were programmed using python. What the file does is that it reads the command line to find out whether alexa is listening, speaking, thinking, idle etc. The file is run in the command line using the command `python nameoffile.py` in the command line. I've provided the file at the bottom of this post. What the file does is when it detects a particular aspect of Alexa's behavior, it lights up the LEDs in a particular way. Now Alexa is nearly complete.

## Conclusion

Alexa is now built with all kinds of capabilities. Using the Alexa app, home devices can be connected to it. Alexa Skills can be built to do custom tasks such as "Connect to GPIO pin 10" or "Turn on the TV". I've not built any myself but will probably do so.

Building the alexa was one of the greatest things I've done this year.

That's all for now!

<p align="center">
<img src='/images/2019/img_0253-1.jpg'>
</p>

Live Long and Prosper.

## Links and Files

[AVS .git file](https://github.com/alexa/avs-device-sdk)

[Quick Start Guide](https://github.com/alexa/avs-device-sdk/wiki/Raspberry-Pi-Quick-Start-Guide)

Download the code for the lights as a .zip file from [here](https://github.com/Aryanaut/AlexaPi)

For more about [raspberry pi](https://medium.freecodecamp.org/beginners-guide-to-raspberry-pi-6e55080fdaaf):
