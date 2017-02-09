# Reach Interaction (WIP)

These notes are old but are being brought up to date.

## Reach Operation Modes

*TODO:* In what modes can Reach devices operate? What configurations are possible?

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
