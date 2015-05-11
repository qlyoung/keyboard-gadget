keyboard-gadget
===============

keyboard-gadget is a shell script that sets up a simple HID keyboard
gadget via ConfigFS.

Usage
-----
The script defines all the configurable data at the beginning; edit to
suit your purposes. When you're satisfied, ensure all other gadget modules
have been unloaded from the kernel and then:
```shell
# ./gadget-setup.sh
```
This will configure the gadget and bind it to the system UDC driver, which
must be set by you. It is one of the variables defined in the beginning of
the script and must be the name of one of the special files in ```/sys/class/udc/```.

After it is configured you can write HID reports to ```/dev/hidg<xx>```, a device file
created when the ConfigFS gadget is bound to the UDC driver (last line of the script).
The host will read them at its leisure as per the USB spec.

Dependencies
------------
* ConfigFS support must be enabled in the kernel. This must be done at kernel
  build time. It's usually enabled by default, though.

* HID support (f_hid) was added in kernel 3.19, so you need >= 3.19 to use ConfigFS
  to build HID gadgets (and subsequently use this script).
