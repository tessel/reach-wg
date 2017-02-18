# Reach Working Group

[![Code of Conduct](https://img.shields.io/badge/%E2%9D%A4-code%20of%20conduct-blue.svg?style=flat)](https://github.com/tessel/project/blob/master/CONDUCT.md)

We're designing Tessel Reach!

> Reach is a remote I/O board for connecting to sensors.
>
> The point of Tessel Reach is to enable low-power internet-connected devices to be programmed in high-level languages - an extension of Tessel into the low-power realm, and a sensible/accessible way to connect many distributed sensor nodes to form a sensor ecosystem.
>
> Tessel and Reach form star network whose origin is Tessel and points are Reach modules. The Tessel 2 is the entry point for the programmer.
>
> Reach modules are low-power sensor nodes placed around a room or environment.

How to get involved:

* **[Read the product design document.](https://github.com/tessel/reach-wg/issues/12)**
* Join #reach-wg on [Tessel slack](//tessel.io/slack)
* Ongoing software / hardware work to come.
* Read the meeting minutes in `meetings/`

## Development Process

Reach is a work in progress. To ship Reach, there are three projects to work on:

### Interaction

**[Read our design for interacting with reach.](https://github.com/tessel/reach-wg/blob/master/INTERACTION.md)** 

How do you interface with a network of sensors? How do you perform autodiscovery? And when talking to a sensor, what is the API like to control its I/O interfaces? We're investigating these questions by designing an API proposal that we can eaasily prototype and test in a few common scenarios.

*Next steps:*

* [ ] [Collect user studies in the folder `case-studies/`. (Submit a PR and contribute your project!)](https://github.com/tessel/reach-wg/issues/11)
* [ ] [Design an API that allows for star network topology over BLE or Wifi.](https://github.com/tessel/reach-wg/issues/13)
* [ ] Describe how module code would interact with Reach over this network.
* [ ] Prototype these interactions on a high level, e.g. using two or more Tessels to begin with.
* [ ] Identify milestones for implementation, including "shipping" milestones and "advanced" milestones to follow.

### Firmware

**[Read the getting started instructions.](https://github.com/tessel/reach-wg/blob/master/firmware-esp32/README.md)**

See the `firmware-esp32/` folder for source code and instructions on how to run Reach's firmware.

We want to build a realtime firmware that can handle asynchronous radio communication, enter and wake from low power sleep modes, can handle a novel protocol design communicating with T2, and which exposes the full range of I/O. We are currently prototyping with the ESP32 architecture:

* We recommend using the [Sparkfun ESP32 Thing](https://www.sparkfun.com/products/13907) with a corresponding [tutorial](https://learn.sparkfun.com/tutorials/esp32-thing-hookup-guide). (You can also choose another dev kit like the [DevKitC from Adafruit](https://www.adafruit.com/products/3269), with some adjustments to your setup.)
* We use the [esp-idf](https://github.com/espressif/esp-idf) development environment (make sure to use v2.0 or a v2.0 release candidate.)

*Next steps:*

* [x] <s>[Add a "hello world" to `firmware-esp32/` that can be built out of this repo.](https://github.com/tessel/reach-wg/issues/14)</s>
* [x] <s>[Write a guide for getting started with an ESP32 Thing.](https://github.com/tessel/reach-wg/issues/17)</s>
* [ ] [Make our firmware able to talk I2C and be testable (e.g. with a module and a logic analyzer).](https://github.com/tessel/reach-wg/issues/18)
* [ ] [Identify which RTOS (or otherwise) is required for the ESP32.](https://github.com/tessel/reach-wg/issues/20)
* [ ] Make our firmware able to talk Wifi and be testable.
* [ ] Make our firmware able to talk BLE and be testable.
* [ ] Implement an end-to-end demo that demonstrates our Interaction design.
* [ ] Identify milestones for firmware, including "shipping" milestones and "advanced" milestones to follow.

### Hardware

Our goal is to design an ESP32 board that allows us to rapidly test out our product requirements, get out prototype hardware to contributors, and test out real world workloads like speed, power consumption, and radio range. See `hardware-esp32/` for a work in progress schematic and BOM.

*Next steps:*

* [ ] [Identify power consumption for ESP32 BLE & Wifi, in addition to other architectures and radios.](https://github.com/tessel/reach-wg/issues/15)
* [ ] [Complete V1 schematic, layout, and design review](https://github.com/tessel/reach-wg/issues/16)
* [ ] Have V1 manufactured & assembled in-house, then determine issues.
* [ ] Layout V2 with revisions for general distribution to contributors.
* [ ] More board revisions as needed...
* [ ] Create a final "form factor" design with input from production house.
* [ ] Identify milestones for hardware, including "shipping" milestones and "advanced" milestones to follow.

## License

Software licensed under MIT or Apache 2.0, at your option.

Hardware designs licensed under CC-BY-SA.
