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

* **[Read the design document.](https://github.com/tessel/reach-wg/blob/master/SPEC.md)**
* Join #reach-wg on [Tessel slack](//tessel.io/slack)
* Ongoing software / hardware work to come.
* Read the meeting minutes in `meetings/`

## Development Process

Reach is a work in progress. We have three tasks to address:

### Interaction

How do you interface with a network of sensors? How do you perform autodiscovery? And when talking to a sensor, what is the API like to control its I/O interfaces? We're investigating these questions by designing an API proposal that we can eaasily prototype and test in a few common scenarios.

**[Read more about our design for interacting with reach.](https://github.com/tessel/reach-wg/blob/master/INTERACTION.md)**

To help develop our interfaction usecase, please look at our `case-studies/` folder and contribute to it.

### Firmware

We are currently prototyping on the ESP32 board. We want to build a realtime firmware that can handle asynchronous radio communication, enter and wake from low power sleep modes, can handle a novel protocol design communicating with T2, and which exposes the full range of I/O.

See `firmware-esp32/` for WIP instructions on how to compile and run our firmware on an ESP32 dev board.

### Hardware

Our goal is to design an ESP32 board that allows us to rapidly test out our product requirements, get out prototype hardware to contributors, and test out real world workloads like speed, power consumption, and radio range. See `hardware-esp32/` for a work in progress schematic and BOM.
