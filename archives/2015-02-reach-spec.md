# Product Spec: Reach

Last update: February 2015

# The Story: what is it and why are we building this?

## Pain Points

Users want a way to remotely monitor/control sensors/actuators in a way that is easy, cheap, and requires minimal interaction. Users also currently have no easy way to interact with these low power sensors/actuators using their smartphone.

For users to do this now, they would have to prototype and produce on their on. Prototyping a single low-power device requires the ability to design low-power hardware, understand the BLE protocol and security mechanisms, and program in a low-level, resource-constrained environment. Once users finish prototyping the system they'll need to begin managing supply chain, negotiating with manufacturers, and actually producing the product which is an entirely opaque and time intensive process that slows down the user's time to market. Overall it's a mix of complexity, cost, and time to market that creates an extremely high barrier to entry.

Current development board options include various BLE boards such as the BlueGiga BLE113A, Intel Edison, and SeeedStudio Smurf. These development boards offer hardware to get started with but still require low level programming, knowledge of the BLE protocol, and offer no path to production (cost reduction and partnerships with manufacturers).

Tessel is another available option however it is too expensive, unreliable, and uses too much power to be feasible in production. Note - the excessive power usage is due to the onboard WIFi chip and JavaScript programmability on board.

## New Technology

Reach promotes an IoT architecture of low power sensors communicating with a controlling base station. The technology which makes this feasible at very low power is **Remote Code Execution** (RCE). The idea behind RCE is that higher level languages can be executed on a base station that has the memory and power capacity to do so. When the base station needs data from a peripheral, it can send a small, low-power packet to the low-energy device. The device executes the command and returns the results.

In this way, a developer doesn't need to worry about the tedious programming of a low-energy device and still gets the benefit of excellent battery life.

The low-power device protocol which enables Reach to talk to high processor devices is **Bluetooth Low Energy** (BLE). There are many different low power protocols to choose from but we've chosen BLE for it's projected market size. In five years, the iBeacon/Bluetooth Low Energy device market is expected to reach 60 billion devices. In quarter two of 2014 alone apple sold 44 million iPhones, 16 million iPads And 4 million Macs, all of which have BLE capability and could potentially serve as base stations for Reach devices. Google is investing in this as well with Physical Web specification, giving urls to physical items allowing code to run on a base station that comes within reach.

The production path for Reach is dependent upon the idea of **"Puzzle Pieces"** (also discussed in the V2 spec). The term "Puzzle Pieces" refers to a method of designing a PCB such that two circuit boards can be fit together (like two puzzle pieces) and soldered such that it appears to be a single PCB. We can use this technology to assemble a single PCB with both a remote radio and module after a user has prototyped using a 10-pin header. This innovation is key to the "Path to Production" as users move from prototyping to placing their inventions in a production environment.

## Customer/Market

The market for Reach are the set of people that are looking for an easy way to interact with remote sensors. This group, coupled with the fact that the number of BLE devices is rapidly growing, creates the need for an easy to use device that allows rapid prototyping of low-power devices at low cost. This is our market.

Keep in mind, the system itself will be installed by our customer and require little to no maintenance on the part of the end-user. Also note that the long-term user might be someone different from the person who installs the product and may need to maintain it themselves.

## Solution

Reach is our answer to the above needs of our customer. It offers the battery life of a low-power device and the programming flexibility of a higher-powered Tessel; all at a low low price of just $29.99\. We accomplish this by running all high level code on a Tessel, computer, or other BLE-enabled device and sending small requests for data to the Tessel Reach. The Reach will interpret that request for data, interact with any module ports as requested, and return data.

Once the user has finished prototyping their idea, we will offer the ability to "bake" the Reach and module(s) onto a single PCB, using "Puzzle Piece" technology as described above.

Our solution solves the low-power development complexities, reduces both the users cost of prototyping and cost to market, as well as making the entire experience quick and easy.

## Drawbacks

This solution is not ideal for high throughput applications or time-critical (microsecond data transfer) applications. BLE is simply not designed for high traffic or real time processing. BLE transfers occur in 20 byte packets, and our estimated latency over USB, wake up events, and actual transfer is ~20ms.

BLE does not have a good design for security during short term key exchange, so significant engineering time will have to be invested into building in house security.

BLE is more complex than necessary for mesh network applications. Note - we're we're looking into different architectures for future products.

# Use Cases

Reach is unlike existing solutions, so it is difficult to interview for concrete use cases.

Some user research was conducted by pulling characteristics from Bean and MetaWear projects. The research can be found [here](https://docs.google.com/spreadsheets/d/1OGogEh3B2SAioygcVNVWLAKHMK9L1vG2WKvt4uLv3UI/edit#gid=1591202038). Overall, users typically attached **one sensor/actuator to a node, and not more than two**. Most project did not use buttons or LEDs, though a few called for **one button and up to two LEDs**. Comms used included: **SPI, I2C, UART, Digital I/O, Analog in, PWM**.****Projects required average of **three or up to eight wires** from the main chip. Most applications were not size constrained, but **small (wearable) size was typically preferred**. Mount holes (though not more than two) were required in some cases, and a flat back surface was preferred but never required.

The project research showed a variety of sensors and applications, but were largely hobbyist. Use cases below are partially derived from users' feedback and applications, but not all are specific projects or products currently under development. They are aimed more precisely at our target market of product developers.

## Cases

- Mimo/OmSignal type of devices: several sensors on a wearable transmitting accelerometer, respiration, sweat data
- Miners in a mine shaft communicating vital chemical data to each other/via a base station to aboveground
- On MTA train cars sensor nodes track performance/wear/maintenance needs
- Hospital patient tracking– nodes triangulate location of beacons on patient bracelets and transmit it back to central tracking
- Device on animal tracks location (herd management)
- Track basic attribute information about products in a warehouse, auto-inventory and auto-ID expired items
- Gather soil moisture data at each watering head in a huge field
- Home automation integration with August, Hue, etc. Attaching sensors/actuators/io around the house to allow monitoring and control
- Retail docent: phone app shows you more info about things as you pass by the beacons
- Craigslist locker: the correct BLE device approaches, the locker unlocks
- Application depends on many phones passing through (like Tile Community Find <https://www.thetileapp.com/community-find>)
- Tinyfarms - A device that measures/controls the environment that houses bugs.

## Case Analysis

Case              | Conn    | Power 1 (hours) 2 (daily) 3 (weeks) 4 (months) 5 (years) 6 (forever) | Size 1 (small wearable) 10 (car battery) | Quantity 1 (1-10) 2 (10-100) 3 (100-1000) 4 (1000-10000) 5 (10000+) | Data Transfer Frequency 1 (when read) 2 (minutes) 3 (hours) 4 (days) 5 (when write)
----------------- | ------- | -------------------------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------- | -----------------------------------------------------------------------------------
Biometrics        | ble     | 2                                                                    | 1                                        | 1                                                                   | 1
Miners            | mesh    | 4                                                                    | 4                                        | 2                                                                   | 2
Train car         | ble     | 6                                                                    | 8                                        | 2                                                                   | 5
Patient tracking  | ble     | 3                                                                    | 1                                        | 3                                                                   | 2
Herd tracking     | mesh    | 5                                                                    | 6                                        | 3                                                                   | 5
Warehouse         | ble     | 6                                                                    | 6                                        | 2                                                                   | 2
Irrigation data   | mesh    | 5                                                                    | 5                                        | 2                                                                   | 4
Home Automation   | ble     | 5                                                                    | 2                                        | 2                                                                   | 2
Retail docent     | ble     | 6                                                                    | 3                                        | 1                                                                   | 5
Craigslist locker | ble     | 6                                                                    | 3                                        | 2                                                                   | 5
Tile              | mesh    | 5                                                                    | 1                                        | 1                                                                   | 2
Tinyfarms         | ble     | 4                                                                    | 2                                        | 3                                                                   | 3
AVERAGE           | 70% ble | 4.75 (almost a year)                                                 | 3.5 (smaller than a kiwi)                | 2 (10 -100 units per application)                                   | 3.17 (either minutes or only when requested) INCONCLUSIVE

## Derived Functionality

Based off the analysis above, use cases require many small low-power nodes that need to last several months to years. // What do various use cases do when battery runs low?

An important factor with these use cases are enclosures. Seeing that casing is the final step in the 'path to production' it's important that we're involved. However since we don't want to offer this service, and/or do casing, it would be great to partner up with an enclosure producing facility. This not only provides users the ability to easily get their final form factor going, it's an additional revenue stream if we get rev share.

Note that higher power applications (such as a camera or audio devices) do not fall under the category of something that Reach will support. Typically these are USB devices that require higher power for a lot of data processing. These type of devices are better suited for use with V2 (or old Bluetooth, but we're not going there) and not BLE.

# Design Priorities

Reach allows for easy interaction with BLE powered devices. Whether that means the devices are communicating with a Reach Base dongle plugged into a V2 or directly with the users smartphone/tablet. The idea is that Reach is there to make the process easy, cheap, and require minimal intervention.

This product is only feasible if the user can deploy as many sensor nodes as they need (anywhere from 1 to 1000+) and expect them to "just work": no connectivity issues, no need to recharge or wire power, no issues with OTA programming.

As such, these are the design priorities, in order:

1. **User experience**: this should be as simple as plugging in a module to Tessel. No special programming should be required on the device. Connectivity should be easy and straightforward; powering the device should be documented well.
2. **Cheap****: **recall users are potentially going to be buying thousands of these**
3. **Low power**: lasts months to years per Reach node (based off use cases)
4. **Fractal Compatible**: should be compatible with our ideas of Fractal

Moving forward it's important to note that Fractal should not be left out of the picture. We need to remember that V2 and Reach are not end goals, but a means to an end.

# Software Interaction

The interaction should match Tessel module programming as closely as possible. All software interactions should be made via Tessel– there will be no USB (or otherwise wired) programming of Reach.

## Reach CLI

The Reach CLI is going to be available via npm. The user will simply have to `npm install tessel-reach -g` (up for discussion), and they'll be able to access these options.

Command          | option                          | description
---------------- | ------------------------------- | -----------------------------------------------------------------------------------------------------------------------------------------------
reach list       |                                 | scans for discoverable devices and returns device ids. Makes it clear which devices it is and is not already connected to (if any).
                 | -t                              | sets how long to scan for
                 | -i                              | brings up "Connect to

<dev-id> (y/n)" every time a device is found during discovery</dev-id>
                 | -v                              | verbose. list all devices and information about all the devices (signal strenght)
reach [dev-id] 1 |                                 | lists characteristics and information about the device (UUID, GATT characteristics, connectivity, signal strength, estimated battery life, etc)
                 | -rssi, -s                       | returns signal strength in dB's
                 | -b                              | estimation of battery life
                 | -test                           | connect to dev-id, blink the LED, disconnect
                 | -r

<new-dev-id>
</new-dev-id> | causes the GATT Generic Access Service to change it's Device Name (required characteristic)

1 Note the GATT protocol has a required Service called the 'Generic Access Service' that contains a 'Device Name'. This is the characteristic that will be presented for `<dev-id>`.

## Multi Master Pairing

It is possible for multiple BLE "master" devices to be present and able to act upon Reach nodes, such as a computer with built-in BLE, a single Tessel V2, or many Tessel V2s, on a network with a BLE dongle. It is also possible that a user may attempt to use Reach in conjunction with a Tessel V1 + BLE Module. We must spec out a method for deciding which BLE master device is acting upon a Reach node:

```
if (!master) {
  //error message. No way to connect to Reach nodes
} else if (ENV.FLAGS.DEVICE_TO_USE) {
  //use the device specified in the env var (warn user)
} else {
  if (v2.count > 0) {
    if (v2.count > 1) {
      //info message. Present options of tessels to use
    } else {
      //use the one tessel thats connected
    }
  } else {
    if (device.external_device_found) {
      //use third party ble device (ble dongle, ble module, etc)
    } else {
      //use built in ble functionality (macbook, phone, etc)
    }
  }
}
```

# Hardware Interaction

## Power

The main source of power is going to be supplied by a battery. The battery is going to be determined by the use case, but the provided connector will be a JST connector (or equivalent). This provides a standard connector that offers the potential for the longest battery life. This also aligns with the use cases that prefer longevity rather than size (aka coin cell batteries).

We are specifically avoiding µUSB connector for two reasons: We don't want to give the impression that Reach Nodes are programmable (UX), and we don't want the µUSB cable to be used for charging the board or recharging the LiPo battery (higher board cost due to onboard circuitry).

Production level will have the option to no-pop the jst connector in the case that through hole wiring is desired. This allows some flexibility to user.

Note - we should sell an USB device that allows the user to charge LiPo batteries. Similar to this that can be easily plugged into a computer or V2: <http://www.ebay.com/itm/E-Flite-EFLC1008-1S-USB-LiPo-Battery-Charger-350mA-Blade-Nano-QX-/381052019700>. Adafruit also sells this sort of thing.

Users will be provided with a battery with each Reach module they purchase unless otherwise specified. Different battery options will be provided at time of purchase. Large, small, none (with warning). Reference for batteries: <http://www.rogershobbycenter.com/lipoguide/>

## Connectivity

There will be a female 10-pin header that allows the user the plug in any first party module or any third party device. This is the exact same experience as plugging in a module in V1.

Hardware connectivity interactions use the sync button on the Reach node. [Pressing the button will cause the board to advertise for a short duration (~10 seconds). The advertising time is kept short in order to prolong battery life and decrease the possibility of advertisement packet sniffing.]1,2,3,4,5,6 This will allow the base station (when scanning) to easily connect to the Reach node.

1 The device should continue advertising automatically anytime it doesn't have a master attached to it. -@johnnyman727

2 We can change the interval to be slower (like 1Hz) -@johnnyman727

3 I think the real benefit of the device is for identification in the CLI. If you know which ID relates to the device you just hit the button of, you can write on the device (or whatever you need to do to keep track). -@johnnyman727

4 This seems like a security risk -@nplus11

5 i disagree. not having it seems like a UX nightmare. -@ekolker

6 @kevinmehall should weigh in on security -@ekolker

Disconnecting a device will also use the on board sync button. If the button is held for 3 seconds, the device disconnects from any paired device and blinks the led to indicate successful disconnect. Note this is the simplest user experience (in terms of hardware). There's no extra buttons, no software needed; just hold to disconnect.

Note that the Reach node itself should be able to keep track of previous pairings.

Software connectivity interaction use CLI-enabled wireless connect. Press the sync button on the Reach node, and then users will use CLI/script to see the list of possible devices and connect to the given device.

Secure wireless connect: ???

## Size

Smaller than V2\. Several of the use cases indicate Reach client themselves should be as small as possible; users have expressed interest in a small device. Many of the Reach clients are going to be attaching to sensors and put into devices. Note that the Reach node is an extension of the sensor. Taking these factors into account, Reach nodes should be as small as possible to make it less obtrusive.

# Software Implementation

## Reach API

var Reach = new Reach([dev-id]) | New reach object
------------------------------- | -------------------------------------------------------------------------------------------------------------------
Reach.connect([dev-id])         | Will extend current object with methods of attached module.
Reach.disconnect()              | Disconnects device.
Reach.id                        | stores dev-id
[Reach.battery()]1,2,3          | battery level
Reach.module                    | [module name space for api. returns null if not connected. [(i.e. Reach.module.moduleFunction)]11,12]4,5,6,7,8,9,10

1 Why is this not a function? It will have to be queried and thus, async. -@johnnyman727

2 I was thinking this would be done every time a packet was emitted, I am unfamiliar with BLE spec and what is sent on each packet. How much does it cost to send and update with every packet. -@harleykwyn

3 that is entirely dependent on how much resolution you want on your battery level. i believe we would set an attribute to be battery level and then the base could query it if it wanted. not entirely sure how the attribute-by-attribute advertising is done or how it maps to power consumption. -@ekolker

4 Not the cleanest interface :/ -@harleykwyn

5 I propose that Reach be made totally transparent (ie you don't need to modify 99% of your exiting code to communicate with the module over BLE). I think the easiest way is for Reach() to return a module port or equivalent that automatically handles the call/response forwarding. ... Need to think about it more. -@ekolker

6 In which case module.use(reach-id) would be good. Unsure of implementation. -@harleykwyn

7 It is doubtful the module port API is going to perform well over BLE latency and bandwidth. However, it's what we've got for now, since we can't run JS on the target device. -@kevinmehall

8 We could also build support for all first-party modules into the reach firmware, but that doesn't scale and kills extensibility. -@kevinmehall

9 Yeah, I don't like that idea of baking them in. I need a crash corse on the limitations of BLE and it's strengths. Any good resources for this? -@harleykwyn

10 <http://mbientlab.com/blog/bluetooth-low-energy-introduction/> is a really brief intro. We're probably not going to really use GATT properly, more abusing it as a dumb pipe for sending our commands over :( -@kevinmehall

11 isn't this going to be the main use case? Do we then expect people to do e.g. var accel = Reach(dev-id).accelerometer.use(...) not sure how this works actually. Shouldn't this still be var accel = require('accel-mma84').use(Reach(dev-id)) -@frijol

12 we could have a use function. That might be cleaner. There's questions of what happens when you disconnect or change used device. Cleaning up the prototype chain can be messy/not possible. Has this ever even been done before?? -@harleykwyn

Reach nodes receive low-level commands over low-power radio from the base station. The translation occurs on the Tessel.

Reach emits data while Base stations listen, the base station will emit an event like accel.on('data') that code on the baseboard can respond to.We need a simple api for the core script to interface with these events.

# Hardware Implementation

Reach nodes will consist of a single PCB with a Nordic chip to handle the radio and processing. Also on board are the various power options, a button, an led, and a 10-pin through hole with a female header for prototyping (puzzle piece for production).

In terms part selection we're trying to keep the cost to an absolute minimum. Remember that these devices are extra cost on top of the sensor itself. Cost was one of the biggest (if the not the biggest) factor when it came to people not using Tessel in production. We need to make this a super viable option.

Another factor to keep in mind with part selection is power. Remember that a battery is going to be the default option. This means we not only have to provide a decent battery, we have pick components that use as little power as possible.

The core BOM currently includes:

- nRF51822 - Cortex M0/BLE SOC
- NCP103 - 150mA 3.3V LDO
- button
- LEDs - two: red (err?) and blue (user)
- 0.1" JST-compatible connector

DNP addons:

- CAT24Cxx - I2C EEPROM in a common footprint, currently 2kB size in schematic

# [Security Implications]1

1 We need more information about what the flaws are with the BLE security mechanisms. -@johnnyman727

- What are the vulnerabilities?

  - Biggest concern - temporary key (TK) advertising. It's the advertising message the slave device sends out when trying to initially connect. It's an unencrypted message containing a temporary key that is used to set up encryption on the layer that exchanges the short term key (STK). Note the STK is then used to encrypt the layer that is used to exchange the long term key (LTK). The LTK is then used to encrypt data transferred between the slave and master for the duration of the connection. Thus, sniffing the TK -> STK -> LTK -> decrypting all transferred data. Our vulnerability is initially connecting a Reach node and a base station.

- [How do we resist this vulnerability?]1

  - Change our 128 unique UUID every so often? Kind of a problem if the STK was sniffed and then EVE listens to the entire encrypted back-and-forth. Apparently it works well enough (Apple does something like this)
  - Use the OOB pairing mode on V2 and Reach so the connection is harder to brute force.

1 @kevinmehall this could use some expansion. I included basics, but are we going to end up implemented our own LTK switching scheme? Thoughts appreciated. -@nplus11

# Development Plan

- MVP

  - The MVP needs to be able to transmit data from a remote sensor to the V2 base station.
  - We should be able to easily pair a Reach module and a V2 with the button syncing scheme described in the hardware interaction section.
  - A selected battery and connector that can power the Reach module and hosted module.

- How do we break this into smaller chunks?

  - Base dongle/chip selected (1 day)
  - Base dongle/chip driver/firmware working/written with Base (3 days)
  - Reach chip selected (1 day)
  - Reach chip manual pairing/disconnecting with Base (2 days)
  - Reach chip and accelerometer module communicating (2 day)
  - Reach chip sending data to Base (1 day)
  - Reach v0 hardware pick and source (3 days)
  - Reach v0 board in house (2 weeks)
  - Reach v0 firmware (1.5 weeks)
  - Reach API (1.5 weeks)
  - Base firmware update (Reach API compat) (3 days)
  - Reach and Base manual pairing/disconnecting via software (2 days)
  - Reach and Base pairing/disconnecting via hardware (1 day)
  - (optional) Reach v1 hardware (2 weeks)

- Total time estimate for MVP

  - 1+3+1+2+2+1+3+14+7+3+2+1 = 40 days
  - Add hardware revision = 40 + ~10 = ~50 days

# Test Cases

- How do we determine that the product fixes the need as described in section 1?

  - In house testing, projects, and customer validation

- What high level software tests do we need to ensure pass?

  - Reach API unit testing
  - Reach CLI unit testing
  - Accuracy and timing tests for BLE communication
  - Range tests
  - Device limit tests
  - Latency tests (precision level)

- What hardware tests do we run with each iteration and how do we determine success?

  - Power management. How it deals with powering the device with multiple power supplies.
  - Recharging. Can it recharge successfully and still power the device?
  - Battery life tests (best case - worst case life times).
  - Software tests to ensure comms between Module, radio chip, Base.

# Support Plan

- What does the first run experience look like for Reach?

  - `npm install tessel-reach -g`
  - access to reach CLI commands (list, etc)
  - simple easy to understand docs.

- What tutorials/documentation need to be ready at release?

  - FAQ
  - FRE process
  - Updated module decision tree (include reach as an option somewhere)
  - Landing page update

- Is there anything special people need to know about using third party modules with Reach?

  - Clear process/documentation about how third party modules work with Reach

- What do we need to support with Reach post launch?
