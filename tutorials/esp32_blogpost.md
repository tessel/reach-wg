---
title: Hello World- ESP32 Firmware
layout: post
created_at: Wed Aug 29 2018
permalink: tutorials/esp32_blogpost
current: blog
author: Arushi
twitter: arushi1803
categories:
- student-posts
---

We’re currently aiming to make our contribution to the Tessel project. Tessel-Reach is a developing concept that we 
recently got introduced to.<br>
It aims at creating a star topology network with a Tessel 2 board as the hub and Reach modules as low power nodes, 
that are currently being configured on an ESP32 Thing.<br><br>
What is a star topology network?<br>
A star topology network consists of several nodes (a node here means any device) connected to a single central node. The central node can talk to all the nodes connected to it. Each node (connected to the central one) can talk only with the central node. So to 
send any message to another node in the network, the node sends a message to central node which transmits to the intended
recipient node.<br>
The latest development on this project was to push a hello world program onto the firmware of ESP32. We began 
by achieving the same, while following the ESP-IDF tutorial (https://docs.espressif.com/projects/esp-idf/en/latest/get-started/) , in order to familiarise ourselves with the 
platform we would be working on.<br>
Connecting the ESP32 module to the laptop was just about plugging it into a USB port via a micro-USB 
cable. But that is not enough to run the module on Windows 10. We need to setup a toolchain so that we can ‘talk’
with the sensor i.e. push code to the sensor and make it do some exciting stuff :D<br>
Here’s how we went about it...<br>
## Step 1
We kick-started the process by setting up the toolchain for the ESP32 module. This took about an hour — first 
downloading, then unzipping the compressed file. The toolchain provided an environment to interact with the ESP32 
module on Windows 10 through minGW32 CLI. IDF_PATH was set as the system environment variable pointing to to the 
‘esp-idf’ folder in esp.<br><br>
You might have noticed we mentioned "toolchain". A toolchain basically compiles the source code into execuatable files
which can be run directly on the device and it consists of a compiler, linker and run-time libraries. In this case, the toolchain
was used to set up terminal and other software to act as an interface for communication with ESP32.<br>
(/img/esp1.png)
## Step 2
The hello world folder loaded into the msys32 folder. We had to the set IDF_PATH correctly. It was initially set 
to the esp folder but it worked only with the esp-idf folder. The path given on the website did not work.<br>
(/img/esp2.png)
## Step 3
We then gave the "make menuconfig" command and selected the serial flash option. Following that, we selected the default
serial port, which did not work. We had to do some hit and trial to figure out the correct port. We tried /dev/ttyUSB0,
/dev/ttyUSB1,…..,/dev/ttyUSB3, /dev/ttyS2 /dev/tty. The device manager in Windows 10 showed the connected port to be
COM3. We googled around and it finally worked at COM3 (/dev/ wasn’t required).<br>
(/img/esp3.png)
## Step 4
The next command we gave was "make flash". We then waited for the process to complete. The sdkconfig file was generated.<br>
(/img/esp4.png)
## Step 5
Upon its completion, this is what we got.<br>
(/img/esp5.png)
## Step 6
We then followed with the command "make monitor". After doing so, the screen showed some garbled characters — so on
referring to the guide again, we set the XTAL frequency to 26 Hz instead of 40 Hz in the component configuration 
menu under the serial flash option ("make menuconfig").<br>
(/img/esp6.png)
## Step 7
The process was finally complete and we got ‘hello world’ up and running on our screen!<br>
(/img/esp7.png)


