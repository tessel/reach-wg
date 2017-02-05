**What project did you work on?**

Josh    | Welding controller
------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | Literally a local IOT (13 edisons, 2 pi's, 2 unos, 1 bluno, 2 Tessels, 16 Arduino pro minis, 2 espruinos, tons of tablets and computers, IP cameras, a health center of bluetooth medical devices)
William | Connecting a Tessel to Azure. Use cases = sw that connects with it. A good thing to have built it?
Fang    | Robot machine assembling chips. Build customized robot. Some sort of assembly line. Drag and drop and modules -> takes to production. Humidifier. From software to hardware to production. Design what you need.
Galen   | Childs clock with neopixels. 3d printed a case for the neo-pixels. Websockets - change the clock to set alarms (change the time various)
Abe     | Smartware connected devices. Devices that connect and talk to each other that need simple connectivity.
Jay     | Environmental hackathon - water conservation. A water barrel that could count rain to measure rainfall. Real Time clock.

**What was the end goal of the user (you potentially)?**

Josh    | Replace PLC's
------- | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | To control everything To be able to come into a house and have complete control over all things over a local Cheap (a module, probably many, in every room = expensive)
William | Security in mind. Automated stuff. Workbench controlled by a device. Wifi built in is nice.
Fang    | He's describing Fractal. Drag and drop software -> Drag and drop software -> put this board into this enclosure -> end product. Industry 4.0
Galen   | gpio, webapps, neo-pixels
Abe     | Simple. Not ready for production. Reusability. Magic solution -> node code compiling to an M0.
Jay     | Real Time clock take it to production startup weekend - build it and get it to market

**What are some of the components they used?**

Josh    | gpio, no interest in BLE (aka reach)
------- | ---------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | nrf24
William | Phones, BLE, wifi. I see it as a dev board. Big unwieldy mass. Other things act better as a gateway. Play with some code. LUA is interesting.
Fang    | Literally would talk about anything besides his project
Galen   | Ambient, gpio (neo-pixels)
Abe     | Various, but found it to be an overkill
Jay     |

**Are there any components you needed but weren't there?**

- BLE built in

- GPIO ports (more/less)

- Tessel ports (more/less)

- USB ports

- Ethernet ports

- Type C ports

- Any other ports

Josh    | RJ45 Interest in USB Buttons PID functionality
------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | Components were there but broken into modules. why not have wifi, ble, nrf24, ir all built in?
William | air quality. water soil air.
Fang    | Literally would talk about anything besides his project
Galen   |
Abe     |
Jay     | Real time clock html,css that connects. Controls the mobile app Out of box solution - combination of phonegap and ionic photon - and - edison software people trying to understand it

**We're exploring possibilities with USB modules. Is there a use case there?**

Josh    | Not really. Can see some use cases for other pr
------- | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | Yeah. now we're communicating data over nrf networks
William | Not sure it would be really usefull. Other things. Battery Operated (power envelope). What have you got over a raspi? (watch out for land mines). Battery? You've got umph. everything was to be connected?
Fang    |
Galen   |
Abe     |
Jay     |

**What's your vision for the overall size, shape, form of your final product?**

Josh    | size irrelevant mounting kits (din rail mounts - standard) gpio breakout board (terminal screws) reduce rewire align/modularize headers (<https://www.google.com/search?q=honeywell+hc900&safe=off&espv=2&biw=1309&bih=708&source=lnms&tbm=isch&sa=X&ei=boS1VNb3GoqRyQTMx4DQAg&ved=0CAgQ_AUoAw&dpr=1.1>) shield (<https://www.modmypi.com/piface-digital-2-raspberry-pi-model-b-plus-expansion-board>)
------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | Really small modules (reach-like).
William | Cases might be nice. Stackable shields (it's a good idea - potentially a way to avoid cases). Don't avoid it - there's no reason to - it works Like the idea - future of programming hardware. Likes Fractal. Helps out non-programmers become programmers.
Fang    |
Galen   | small, whack the table -> needs to be reliable stacking shields good? -> remove the wifi (comms board)
Abe     | palm sized battery wearing not shock proof
Jay     | is that easy? wearables? platform to send out a couple of different designs (changeable form factor) decisions about hardware - how will this cost me later?

**Tessel problems!**

Josh    | Reliable communication
------- | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | communication seems to be an issue. Basically wants Reach should allow people to solder headers
William | Do something beyond the CC3000\. Price lower. Give me an embeddable version (Base Tessel - BLE - built it would be great!). Luajit compiled. Construction company - needs wifi, needs to talk to cell network (may or may not have internet), needs to talk to bluetooth (when network is down). Check the forums
Fang    | Industrial (residential, office, medical, agricultural, retail)
Abe     |
Jay     |
Galen   | Mounting Real Time clock (works when power is off - less essential) Speed of refreshing (clean neo-pixels)

**Interests/Thoughts**

Josh    | Node server Custom remote with just what you need rf232/rs485
------- | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Wesley  | Think about wall sockets. One in each socket "essentially we need a system that works independent of the web, but that can talk to the web, so that is the net dies, the wheels don't fall off" reach modules should be small flexible base station
William | Too big. Dev board.
Fang    | Modularized components. Plug and play Sensors. You're doing well. Plug and play SW -> Plug and play HW -> Enclosures -> Production Imagine the possibilities. Really low cost robot manufacturing - don't use human assembly (look at iRobot assembly) Javascript node is really cool! I'm a software guy. I want an easy interface to hardware
Galen   | Even more modular Daisy chain. Modules talking to modules Great community Boilerplates IOS/Android control ( boilerplates - have tons ) Remote DEPLOY seems absolutely necessary MORE Documentation Reliable connection
Abe     | Nice control of LED's (candy board) Python control
Jay     | wrapper that could communicate with our board iconic and phonegap (vs comm through the web) starter app that would get us started with the board - have different things (test different modules on the phone) - source code to have out the box when you get started phonegap (check it out)

**Software/Hardware considerations**

| TinyG CNC - 3D printing
| -----------------------
|

**Segments**

- Industry

  - retail

    - tracking customers

      - What is this?

        - tracking mass movements

        - analytics of customer behavior in store

      - will need to be in a case for testing

      - unobtrusive to customers

      - gpio to try different sensors

      - doesn't need super reliability (Wifi is fine)

      - lots of sensors around

    - interactive displays

      - What is this?

        - e.g. Kinect fits featured clothing on you when you approach

        - iBeacon pushes you a link

        - Changes based on whether you've picked up the goods

      - Cloud connectivity

      - High processing power
      - USB

    - goods tracking

      - What is this?

        - keeping tracking of goods/checkout
        - instantly know what's there

      - No connectivity

      - Underkill

  - manufacturing

    - warehouse

      - What is this?

        - Fix fulfillment
        - Finding parts
        - Path optimization

      - Low cost

      - Fast connectivity
      - Web heavy
      - Hardware - leds

    - robotics

      - What is this?

        - Assembly line jobs
        - Get data about how the jobs are done

      - Ultra reliable

      - High voltage
      - Mounting
      - Big motor control
      - Hazardous environment

    - environment sensing

      - High third party use
      - Sensor heavy
      - Weatherproof but accessible

    - 3D printing

      - Environmental monitoring
      - Network print jobs

    - precision fabrication

  - medical

    - environment sensing
    - patient tracking
    - event tracking/reacting
    - medical data capturing/analysis

  - agricultural

    - animal tracking/monitoring

      - What is this?

        - device that animals can wear to track them
        - records location, health, etc

      - biosensing human-like

      - long range comm v. mesh network
      - "wearable"
      - user interface

    - plant health tracking

      - What is this?

        - A system to track plants and regulate environment

      - high third party use

      - waterproof

    - machine monitoring

      - What is this?

        - Tracking information for the various machines on site
        - Diagnostics on machines (similar to auto case)

      - Size irrelevant

      - gpio heavy
      - hazardous environment

  - auto

    - insurance tracking

      - What is this?

        - tracks information about car to determine insurance

      - zero down time

      - protected/unhackable
      - standard car mounting?
      - high third party use

    - vehicle performance

      - What is this?

        - ability to read car data (oil levels, brake pads, etc)
        - ability to fine tune components

      - really high third party use

      - no wifi, either rf/ble for internal components
      - lots of wiring?
      - user interface sw/hw?

- Makers

  - kickstarter

    - alarm clock

      - What is this?

        - Ambient reactive neo-pixel alarm clock

      - robust hardware/connections

      - hardware interface
      - production ready

    - home automation

      - What is this?

        - Connected devices used to automate tasks

      - Super easy application to what already exists in home

      - USB heavy? (cameras, etc)

    - server

      - What is this?

        - simple node server

      - Literally don't care about hardware

      - Software must be solid
      - great API's
      - great documentation

    - gps tracking

      - What is this?

        - tracks something via GPS

      - mounting

      - sturdy
      - smaller product

    - dog tracker

      - What is this?

        - tracks your dog and what they do
        - provides sw feedback

      - wearable

      - mesh type network
      - access data online

    - boating sensing

      - What is this?

        - diagnose/report problems about boat

      - wet environment

      - user interface HW/SW

    - hydroponics/greenhouse

      - What is this?

        - Monitors/reports/adjusts sensors for plants

      - Base station size irrelevant

      - moist environment **Use cases round II**

- welding controller - connects with other devices to do automatic welding

  - sturdy

    - strong case
    - strong connections

  - modularized connections (no need to rewire)

    - standard port (usb, gpio, tessel, custom?)
    - gpio adaptors?

  - reliable connectivity

    - ethernet
    - good wifi antenna

  - easy hardware interface

    - lcd?
    - buttons/screens/switches

  - heavy gpio use

    - lots of gpio
    - easy processes to know what is what

  - size does not matter

    - sheilds
    - ports
    - all in one

- home automation and networking

  - high connectivity

    - all comms built in (wifi, eth, ble, nrf, ir?)

  - easy already connected sensors (like easily attachable relays)

    - plug and play Reach client.
    - gpio on Reach client?

  - easy sw interface (way to see connected devices)

    - Provided services that work with Tessel (keen, etc)

  - needs connectivity options (usb, etc)

    - shields, modules, best option?

- automating assembly

  - protected from environment

    - reasonable size
    - long & flat v. big and tall?

  - provided sw/hw interface

    - buttons/screens/switches
    - provided services (keen, etc)

  - heavy gpio use?

    - standard gpio connections
    - reliable gpio?

  - plug and play (little to no development needed)

    - it just works
    - simple to understand

- alarm clock

  - sturdy

    - good casing options
    - way to make connection sturdy

  - simple (needs ambient, neo-pixels, and wifi connection)

    - minimized main board
    - simplest possible options
    - build from the ground up (fractal like in this sense)

  - no usb, gpio, ethernet needed

    - simpler options available
    - no overkill
    - baseboard is what then?

  - slim form factor

    - simple board
    - flat design
    - slim

- wearable connected devices

  - low power connected devices

    - mesh networking available
    - batteries heavily used
    - cheap if in a lot of products

  - wearable

    - slim
    - battery powered

  - small

    - built in functionality

  - base station

    - size independent
    - independent of wearable items

  - user interface

    - easy to use via sw or hw

- crop data sharing

  - Kelsey has this contact: <http://photosynq.org/>
  - protected from environment

    - casing really important
    - reliable connections

  - easy sw interface

    - provided services (keen, etc)

  - easy connectivity and documentation

    - plug and play ability

  - heavy gpio use

    - simple way to understand
    - documentation

  - Battery powered

**The future market (2020)**

- advanced medical devices
- factory automation sensors
- industrial robotics
- sensor motes for increased agricultural yield
- automotive sensors
- infrastructure integrity monitoring systems for diverse areas, such as road and railway transportation, water distribution and electrical transmission
