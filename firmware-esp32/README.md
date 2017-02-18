# Getting Started

## Installing esp-idf
To get started you'll need to first install the `esp-idf` toolchain.
Follow the link below for your operating system and make sure you are able to successfully complete the first two steps:

- [Windows install instructions](http://esp-idf.readthedocs.io/en/latest/windows-setup.html)
- [Linux install instructions](http://esp-idf.readthedocs.io/en/latest/linux-setup.html)
- [MacOS X install instructions](http://esp-idf.readthedocs.io/en/latest/macos-setup.html)

After installing the tool chain and downloading the `esp-idf` repository:
  - **On Windows:** Create the file `C:/msys32/etc/profile.d/` and add the line `export IDF_PATH="C:/path/to/esp-idf"`
  - **On Linux or MacOS:** Add the line `export IDF_PATH=~/esp/esp-idf` to your `~/.profile`, `~/.bashrc`, or equivalent terminal cofiguration dotfile.

This is just so you don't have to set the `IDF_PATH` every time you start a new terminal session.

## Building and flashing the Reach firmware

If you haven't already, clone this repository and enter the firmware directory:
```sh
git clone git@github.com:tessel/reach-wg.git
cd reach-wg/firmware-esp32/
```

Before you can flash the firmware you'll need to configure which port the device is connected to.
The following instructions will help you identify which port to use:

- **On Windows**:
  - After plugging either the Sparkfun Thing or DevKitC into your Windows computer, the drivers should automatically start installing.
  If not, you can get the FTDI drivers for the Thing [here](http://www.ftdichip.com/Drivers/VCP.htm), or the SI Labs drivers for the DevKitC [here](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers).
  - In either Windows Command Prompt or PowerShell and enter the command `chgport`.
  Among the output, you should see one or more `COM*` devices listed.
  The Thing will look like `\Device\VCPO` and the DevKitC will look like `\Device\Silabser0`.
  The `COM*` value is what you will use in `make menuconfig`.
- **On MacOS:**
  - If you are using the **Thing**, run `ls /dev/tty.*`.
  You should see something like `/dev/tty.Bluetooth-Incoming-Port	/dev/tty.usbserial-DN027NCK` in the output. Here `/dev/tty.usbserial-*` is the device you'll use in `make menuconfig`.
  - If you are using the the **DevKitC**, download and install the appropriate [SI Labs driver](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) and run `ls /dev/tty.*` with your devkit plugged in.
  You should see an output similar to `/dev/tty.Bluetooth-Incoming-Port	/dev/tty.SLAB_USBtoUART`.
  Here `/dev/tty.SLAB_USBtoUART` is the device you'll use in `make menuconfig`.

With your device's port identified, run `make menuconfig` to open an interactive configuration editor.

Use the arrow keys to enter the `Serial flasher config` submenu.

![esp-idf menuconfig editor: Serial flasher config is selected](http://imgur.com/EXfLyuO.png)

Select the `Default serial port` option to edit it.

![esp-idf menuconfig editor: Default serial port is selected](http://imgur.com/3daQTkf.png)

Paste the port name found in the above step.

![esp-idf menuconfig editor: Default serial port text entry](http://imgur.com/qMCEcTv.png)

Make sure it looks correct, then `Save` and `Exit`.

![esp-idf menuconfig editor: Default serial port has changed, Save option is selected](http://imgur.com/C0QNU5Y.png)

Now run `make flash` to build the project and upload to your board.

## Notes
 - As of the time of writing, the firmware consists of a blink example, configured to blink an LED on GPIO pin 5.
 This is the pin that the Sparkfun Thing has an on-board LED, so should work as-is.
 For the DevKitC you will need to attach a resistor and LED to pin IO5 to confirm the firmware is working.

 ![A DevKitC board with an LED connected](http://imgur.com/BdrupWt.png)
 - See the [espressif/esp-idf README](https://github.com/espressif/esp-idf#developing-with-the-esp-idf) for more available `make` commands.
