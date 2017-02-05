# Product Opportunity Assessment
Based on the [Silicon Valley Product Group](http://svpg.com/assessing-product-opportunities/) assessment technique

Last update: May 2016

## Exactly what problem will this solve? (value proposition)
Make it easy and intuitive to develop large data-collecting IoT networks by creating a low-power [BLE]1 node hardware which receives instructions from a base Tessel 2 in [compiled high-level to low-level language]2

1 I think BLE is not a requirement of the problem. It could be packets delivered over 980MHz or using a different protocol like 6LoWPAN and it could still solve many of the problems. -@johnnyman727

2 I was never comfortable with this aspect. I think a remote device (think Fermata or in fact how our SAMD21 operates) controlled by a master works fine for most circumstances. - unknown

## For whom do we solve that problem? (target market)
The intersection of
* [People who want to have many (more than 10) sensor nodes]1
* People who want to write in a high-level language
* People who may not have access to power outlets at sensor node locations

1 I would argue for a low number of sensors (>= 3). Sensors residing in difficult places (a fridge, a lawn) or even "one remote per room in a house" can still be advantageous over running wires. - unknown

## How big is the opportunity? (market size)
Essentially every large-scale/industrial deployment of IoT involves many low-power sensors for data acquisition

## What alternatives are out there? (competitive landscape)
* Arduino/RPi/Tessel 1 (but not well suited for very many nodes/questionably easy and intuitive)
* Espruino (though not designed for star networks)
* Custom solutions (not easy and intuitive)
* Lightblue bean
* Particle spin-off using BLE
* Pinoccio
* ESP8266
* [Lots more]1

1  I've seen IoT implementers paralyzed by analysis of the options for any particular scenario. The technology has been built out far in advance of the use cases. -@johnnyman727

## Why are we best suited to pursue this? (our differentiator)
We have experience working on compiled JS > lower level
[We have existing hardware and beginnings of a protocol for this]1

1 We actually use this protocol today, the SOC -> SAMD21 bridge. - unknown

## Why now? (market window)
T2 just shipped as an ideal base station for a network of this kind (except that it doesn’t have BLE built in…)
[Price of BLE chips?]1
[BLE has been established as a go-to protocol for many sensor nodes (as opposed to earlier-market Zigbee etc. attempts)]2

1 hasn't changed much recently -@johnnyman727
2 I'd like to see more evidence this is true, but also more reasoning if it matters; I don't know much about either. - unknown

## How will we get this product to market? (go-to-market strategy)
[redacted] is interested in producing this for us
[Breakdown of labor? Who will take on hardware/software/etc.]1,2

1 As I mentioned in our meeting, I think in addition to the Reach hardware, we'll also need to start building more modules because the three or so 10-pin sensors we have aren't enough. -@johnnyman727

2 If we have to pin a number to it, we want (X) number of Reach-compatible modules. I'd say five, six at minimum. - unknown

## How will we measure success/make money from this product? (metrics/revenue strategy)
We think we can make it for a retail cost of ??? (can someone who has Kicad PDF the hardware so I can take a look at chip prices?)
* New contributors working on the project.
* Royalty revenue coming in once we ship.
* Number of production deployments

## What factors are [critical to success?]1 (solution requirements)
* Build hardware capable of serving as a 10-pin low-power node that operates from battery power for months-years
* Build reliable method which runs on T2 to take high-level instructions and turn them into low-level commands for sending to Reach node
* Establish excellent system of communication T2 <> Reach node
* [Figure out a best solution to make T2 work well with this (BLE dongle & you’re done?)]2

1 Again, more sensors are critical -@johnnyman727

2 This part I think is huge! T2 alone isn't enough of a value prop—maybe bundling T2 + reaches is. - unknown

## Given the above, what’s the recommendation? (go or no-go)
