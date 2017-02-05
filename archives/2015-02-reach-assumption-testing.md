# Reach assumption testing

*Ed. note 2/2017 this may be a useful way to approach future design challenges*

Testing plan
*done if italic*

* Research
  * *What does the GPIO need? 1 module port = 8 GPIO. Is more needed?
    * [Go through Bean and Pinnoc.io projects]1 and tally GPIO needs
      * # things attached
      * things covered by our modules
      * I2C, SPI, UART devices used
  * What is the need for buttons?
    * Go through Bean and Pinnoc.io projects and tally button usage*
  * What is the need for LEDs?
    * Think of use cases and list
    * Go through Bean and Pinnoc.io projects and tally LED usage
  * What is the physical interaction?
    * *Go through Bean and Pinnoc.io projects and answer the following questions
      * Does size matter? (If so, what are the limitations?)
      * Does orientation matter, e.g. antenna direction, where the button is?
      * What is the ideal mounting situation?*
  * What is the distance across which Reach nodes might be spread?
    * Go through imagined use cases and tally answers for ideal area interactions
  * What is the power need?
    * Go through Bean and Pinnoc.io projects and tally GPIO uses, show to
    * What are the power needs of our modules?
      * Examine power draw of our modules for common commands
      * What frequency of what sort of command do people send to each of our modules?
        * Gather this info from tessel.io/projects
  * What is the preferred battery interaction?
    * What is the expected battery life?
      * Gather this based on context of Bean/Pinnoc.io projects
    * [What sizes of battery will people need in order to fulfill their expectations re usage & life?]2
      * Calculate this from expected battery life
    * How do users expect to connect power?
      * [Are JST headers fine? Are we selling boards with JST connectors pre-populated, and different battery packs? Will there be a USB option?]3
    * In what situations will people want to recharge vs change out battery?
      * Go through use cases and determine likelihood of preference to recharge vs. replace battery
      * Figure out recharging situations available for battery sizes chosen above
        * Do we need to sell a recharger? (If weird battery sizes)
        * Do we add a LiPO recharger to the board? (Min $1 addition to BOM)
  * [How are Reach nodes programmed?]4,5
    * Is a Reach node paired with just one base station, or does it need to be more flexible?
    * What is the security protocol that makes the most sense?
    * Is there a wired programming option?
* In person
  * [What do we want to fake with a Bean?]6

1 Might also want to consider "arduino + ble" projects. my inclination is that you'll also find mostly "hobbyist" stuff with those markets. i don't know how you would look for industrial ble applications. also maybe these guys http://projects.mbientlab.com/ -@jiahuang

2 I imagine this is a huge range and power consumption varies wrt project -@tcr

3 not sure how to determine answers here -@frijol

4 not sure how to get answers for this section -@frijol

5 This ties into "physical interaction" also. Split this into security vs. "Pairing" sections -@tcr

6 We can fake a lot with bean using it and a Johnny-Five adapter quickly. Otherwise I wouldn't spend too much time trying to get it to work -@tcr

---


Assumptions/questions to address (used to formulate the above)

## IO

* Is a module port/puzzle piece good enough or is there some desire for more IO broken out? Assume 1 module port is the same as 8 GPIO. Currently assuming that one is enough, but we will likely have more IO to allocate...somewhere.
* Assuming 1 button is sufficient. Do we need more?
* Currently have 2 LEDs (blue because BLE and lower power/lux and red for error or something). Could be convinced that one is enough (blue), but I seriously doubt anyone is gonna say "take away my LEDs"

## Power

* Assuming max 5V in
* Assuming 150mA @ 3.3V is sufficient. The SOC will use ~20mA during peak transmit bursts, closer to 5mA most of the time, leaving >100mA for modules. If you are gravely concerned about this and have a use case to back it up, let me know, otherwise I really think this is plenty.
* Assuming charging of the battery is not handled onboard
* All things considered, if you want you thing to run for years, you want primary (non-rechargeable) cells, not a LiPo. There’s a reason alkaline AA batteries expire ten years after you buy them, but your laptop will die if left alone for a week. Please explore AA/AAAs and non-rechargeable Li cells as an option.
* Assuming ~3.5-5V source attaches to board via JST-compatible connector or similar. Note that "JST" is a brand, not part number, so they come in many different sizes.

## Charging, programming, etc.

* If we go for rechargeable, I’m assuming battery charging is handled either by dedicated chargers or a "programming base station" of some kind. This base station would presumably be sold in a ratio of 1:5 (or lower) to the Reach nodes themselves.
* If the base doubled as a LiPo charger, it would not be optimized for charging speed or throughput, but rather battery capacity (% charged).
* Most of the time, the user will not need to actually program Reach until well into the "production" phase of the project. However, the rig should be able to do this. Things of interest include security credential handoff over wire rather than the air,
* SWD (JTAG equivalent) broken out to...something on the board, compatible interface on the programming base station
* How should we pair?

## Physical

* At least two mount holes
* Small: ~1.5 square inches estimated
* antenna opposite module port; programming, battery, and button on 3rd side (top?)
* [Toying with the idea of all SMT assembly if possible. This means SMT headers and battery interface.]1,2,3
  * if we go with all SMT with the goal of embedding, we should also go with castellated edges
* What is the distance across which Reach nodes might be spread?

1 does this matter from a user perspective? -@frijol

2 + means the bottom of the board is completely smooth / can be mounted flat on something - the headers will have less mechanical strength and might tear off the board if abused -@kevinmehall

3 note: not 100% backwards compatible (aesthetically) with existing modules, which all poke down -@ekolker
