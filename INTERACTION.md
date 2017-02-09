# Reach Interaction (WIP)

These notes are old but are being brought up to date.

## Reach Operation Modes

*TODO:* In what modes can Reach devices operate? What configurations are possible?

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

## An Example Reach API

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
