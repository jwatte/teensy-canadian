teensy-canadian
===============

configuration files for building a Teensy GCC compiler on an AMD64 machine for running on a Raspberry Pi.

There are several hacks here.

## inputs

First, check out master of crosstool-ng from GitHub.

Then apply a patch that always runs the "copy headers" step. (This may be folded in later)

Then, create three folders for building three copies of GCC, and one folder for the destination. Make sure you have 20 GB free!

* x64-rpi
* x64-teensy
* rpi-teensy
* /opt/cross/x64

Make sure these are writable.

Then copy the config files of the appropriate names to a file named ".config" in each of the build folders.

Add the folder /opt/cross/x64/bin to the beginning of your PATH.

Then, in the order listed, "cd" into each of the directories, and do a "ct-ng build" in order. Each must complete before you finish the next.

## outputs

Now, you have three compiler suites:

* x64-rpi can build Raspberry Pi linux executables from a amd64 computer
* x64-teensy can build Cortex-M4 barebones executables from a amd64 computer
* rpi-teensy can build Cortex-M4 barebones executables from a Raspberry Pi (if moved over there.)

The compiler and install libraries/headers/etc live in /opt/cross/x64. Easiest is to move this entire directly wholesale to your Raspberry Pi, but it is kind-of big.

A pre-compiled version of 4.8.3 is available in the directory "x64" -- you can dump this on your Raspberry Pi and execute it.
Make sure the x64/bin directory is in your PATH, call the compiler by full name (arm-jwatte-eabi-gcc, etc,) and use the .ld link scripts in https://github.com/PaulStoffregen/cores/tree/master/teensy3

