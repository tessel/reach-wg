# Reach

This is the design document for Reach, a remote I/O board for connecting to sensors.

The goal of Tessel Reach is to enable low-power internet-connected devices to be programmed in high-level languages - an extension of Tessel into the low-power realm, and a sensible/accessible way to connect many distributed sensor nodes to form a sensor ecosystem.

Tessel and Reach form star network whose origin is Tessel and points are Reach modules. The Tessel 2 is the entry point for the programmer:

* Tessel 2 has a higher-power CPU for processing data
* Tessel 2 supports our development environment and supports running high-level languages
* Internet connectivity is sourced by WiFi (as a station) or Ethernet; it can also act as a WiFi access point
* Only one Tessel 2 is required to control many BLE Reach nodes
* Tessel 2 requires a USB dongle to connect with Reach over BLE
* The Tessel 2 is likely wall-powered for long-term deployment

Reach modules are low-power sensor nodes placed around a room or environment:

* Reach modules are most likely powered by a coin cell battery for months to years
* They connect with Tessel over BLE or Wifi
* Each of these nodes can be controlled individually by the host, with the intent that fetching data is infrequent and requires few I/O operations.

### A Short History of Reach

Technical Machine conceived of a low-power sensor board for the Tessel ecosystem in 2015. There were a few prototypes developed:

* Gosper, a 6LoWPAN module using the SAMR21 chipset.
* BLE-only Reach, detailed [in this Github issue](https://github.com/tessel/project/issues/142). Early [hardware designs](https://github.com/tessel/reach-nrf51822-hardware) were manufactured with corresponding [software](https://github.com/tessel/reach-nrf51822).

The major variables in these prototypes were what radio protocol and base chipset to use, but the fundamental concept, a remote 10-pin I/O board, remained the same. The first proposal for Reach used a 2.4Ghz chipset with an identical architecture as the Tessel 2 microcontroller, the SAMR21. When the design requirement evolved to require BLE, we looked into Nordic BLE chipsets. With the release of new chipsets and interested partners, we're again revisiting the Reach concept.

## Motivation

What are usecases for Reach/BLE?

* ...
* ...

## Architecture

Among Reach's design requirements, we are constrained by our choice of available system architectures. The current proposal is to use the ESP32 by Expressif, an Xtensa-core processor that integrates WiFi and BLE circuitry, and has an excess of reconfigurable I/O. 

**TODO:** We are also considering low-power options. What options are available for BLE? We also need numbers of ESP8266 vs. ESP32 low-power wifi performance.

## Requirements

These detail the product features and user experience.

### Radio

There are few options, not mutually exclusive, for sensor networks.

**TODO:** What are the ranges for different networks? "Lorawan networks are coming up slowly (see e.g. the Things Network) - it might be interesting to mention that for communication with nodes between 1km - 5km, Lorawan might be interesting. Bluetooth is limited to a couple of meters only." As for bluetooth: "The distance is also going to increase significantly in the next couple years as [Bluetooth 5](https://www.bluetooth.com/news/pressreleases/2016/06/16/-bluetooth5-quadruples-rangedoubles-speedincreases-data-broadcasting-capacity-by-800)"

Bluetooth Low Energy is ideal for low-power sensor networks. The ability of a sensor to have direct interoperability with smart phones and BLE capable computers could enable Reach to be a development platform independent of Tessel or any other prototyping hardware. 

**TODO:** Does Bluetooth have [IPV6 Accessibility](http://www.nordicsemi.com/eng/News/News-releases/Product-Related-News/Nordic-Semiconductor-IPv6-over-Bluetooth-Smart-protocol-stack-for-nRF51-Series-SoCs-enables-small-low-cost-ultra-low-power-Internet-of-Things-applications)? Also as a motivation: "it's lower friction, IMO, to connect to a BLE device than a WiFI network and the work of The Physical Web builds upon that."

WiFi trades power for convenience: creating an HTTP API or addressing a device by IP enables many more technologies to interface with Reach.

ZigBee/6LoWPAN: We ruled these out based on accessibility criteria. **TODO:** Those criteria.

**Protocol:** We will be using a similar protocol to the Tessel 2 bridge protocol used to interface the OpenWRT system with the SAMD21 microcontroller. Because we are operating over a different link, modifications to this protocol may be added to suit WiFi or BLE as needed. The protocol may be specialized for our use case, but will be supported and tested by a cross-platform library.

### I/O Port

Reach has a 10-pin I/O header similar to Tessel's.

* Pin 1 is GND, pin 2 is 3.3V.
* Pins 3-10 can be mapped as GPIO.
* When I2C mode is enabled, pins 3 and 4 are mapped to SCL, SDA.
* When SPI mode is enabled, pins 5, 6, and 7 are mapped to SCK, MISO, and MOSI.
* When UART mode is enabled, pins 8 and 9 are mapped to TX and RX.

**TODO:** Because of how remappable ESP32's I/O is, we could conceivably have all modes operable at once, or even all pins available as signal emitters.

### Battery / Power

* USB power: Supports a 5V external battery charger. Fairly ubiquitous due to cellphone availability.
* Battery: Operate off lipo batteries, so 3.3V. Lipos are longer lasting & easier to use than AA/AAA battery packs.

### Programming

A Reach board will be able to be programmed OTA from a Tessel board. 

TODO: Do we have other programming requirements? Does this require a bootloader? Can an ESP32 self-program? How often do we program the Reach with new firmware?

### Memory Requirements

ESP32 chip has the following memory availability:

* Xkb RAM
* Xkb Flash

Additionally, we will add X amount of flash.

### API

User code will be able to instantiate a Reach port similar to a Tessel port, e.g.

```
var sensor = reaches[0];
var i2c = new sensor.I2C({ address: 0xA0 });
i2c.send(Buffer.from([0xff, 0x00]), () => {
  console.log('Sent two bytes.');
});
```

TODO: How to detect reaches?

### Programming

The Codebase is written in C.

Additional languages are not supported by the ESP32 toolchain.

TODO: Is it intended that we support users cross-compiling their own code kernels for Reach? Now or in the distant future?

### Recovery

The ESP32 exposes a UART port for programming. This can be wired directly to a Tessel for reflashing the device.

## Status

* [Hardware Schematics](github.com/jiahuang/reach-esp32)
