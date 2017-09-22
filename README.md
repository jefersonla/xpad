# Xpad

This is an ever so slightly modified version of the Linux xpad kernel module.

Some games do not go through the Joystick API and so do not respect deadzones set by jscal.

To "fix" this, I simply added a deadzone to the kernel module itself.

You can edit the deadzone by changing the `XPAD_DEADZONE` variable to whatever value you like. The maximum axis value is 32768. Something around 5000 to 8000 usually works well for me.

xpad.c was originally copied from https://github.com/torvalds/linux/blob/master/drivers/input/joystick/xpad.c

This fork add compatibility for Intel Galileo boards which don't come with xpad kernel module.

## Compiling / Installing

You’ll need linux kernel and libusb headers installed and kernel scripts compiled before compile and install xpad module. This should do the trick on Yocto Linux (Intel Galileo):

```bash
opkg update
opkg install libusb-1.0-0 libusb-1.0-dev linux-libc-headers-dev kernel-dev kernel-modules
cd /usr/src/kernel
make scripts
```

Once you have the dependencies, just compile, install, and load the module:

```bash
make
make install
depmod -a
modprobe xpad
```

### REMEBER!

Remember that using modprobe activate module only on this session, to make this module
available at boot you should execute the following command

```bash
echo "xpad" > /etc/modules-load.d/xpad.conf
```
