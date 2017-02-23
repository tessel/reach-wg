# Case study-- connecting Particle Photons to a T2 for wearables

Steps taken:

* Wrote firmware for the Photon that did the following:
  * Removed the photons from the Particle cloud
  * Connected them to the T2 WiFi AP
  * had calls to set/get pin values
    * We can do even more with the reach in this respect

* Modified the Tessel to run as an AP and Station at the same time [info](https://medium.com/from-the-nodebotanists-lab/ongoing-lab-experiment-using-the-tessel-2-as-a-wifi-access-point-and-station-simultaneously-4d9705b73c0d#.ams5j737g)

* Wrote firmware for the Tessel 2 that
  * Registered each Photon that connected to it and kept its IP
  * Made various rest calls to the photons to get/send info

I think we can take a lot of this experience and use it for designing the reach
boards.
