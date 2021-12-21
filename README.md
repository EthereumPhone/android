ethOS
===========

Getting started
---------------

To get started with Android/ethOS, you'll need to get familiar with [Source Control Tools](https://source.android.com/setup/develop).

To initialize your local repository using the LineageOS trees, use a command like this:
```
repo init -u git://github.com/EthereumPhone/android.git -b ethOS
```
Then to sync up:
```
repo sync
```
Please see the [LineageOS Wiki](https://wiki.lineageos.org/) for building instructions, by device.


Submitting patches
------------------
Patches are always welcome! Please submit your patches via LineageOS Gerrit!

Simply follow our guide on [how to submit patches](https://wiki.lineageos.org/submitting-patch-howto.html).

To view the status of your and others' patches, visit [LineageOS Gerrit Code Review](https://review.lineageos.org/).

# Build Info

This is just a small how-to on building and flashing ethOS.

## System requirements for a build

To build EthOs you need to fulfill the following system requirements:

+ 250 GB for the source code
+ Additional 150GB to build it (If you conduct multiple builds, you need additional space.)
+ At least 24 GB of available RAM is required, but Google recommends 64 GB.

Also, your system needs to run on Ubuntu 20.04 or 18.04.

At the end of the day, the faster the machine, the faster the build. Google uses 72 core machines internally, and their build times are 40 min. So it will probably take much longer on slower machines.

## Getting the source-code

To download the source you need to install `git-repo`. To install git-repo just open up the Terminal and type `sudo apt install repo`.

Once you have the tool installed, create a working-directory where you will store the source. You can do this with the command `mkdir WORKING_DIR`, then enter the created directory using `cd WORKING_DIR`.

You can initialize the repo-tool with the following command: `repo init -u git://github.com/EthereumPhone/android.git -b ethOS`. It basically points the repo-tool to the default.xml file in the above given git repo. The branch we choose is the ethOS branch, where the current commit for the system-service is located.

The above command will only initialize repo, it will not yet download anything. To download the source you just need to type this into `the` command-line: `repo sync`. Depending on your connection speed this can take a very long time.

## Compiling the code

First setup the environment by running `source build/envsetup.sh`. 

After that we need to tell AOSP what device we are building for by doing this: `breakfast XXX`. Replace XXX with the name of the Pixel. For example, to build and flash for a Pixel 2 you need to enter this command: `lunch aosp_walleye-userdebug`. The device names (for pixel) can be seen here:  https://developers.google.com/android/images#oriole

Note: When you run the breakfast command you need a device which is already flashed with lineageos, also turn on USB-Debugging and Rooted Debugging enabled. If you need any help setting this up, or you encouter some weird error, you can always message me on the discord. My at is `@mhaas.eth`

Now, to compile it just input the command `breakfast blueline`. This will probably take a long time.

## Flash the device

At the end of the compile it will output a path to a zip-file. This zip-file contains ethOS. 

Now, plug you phone into your PC and enter the command `adb reboot bootloader`, this will put the device into the bootloader. Once you are in the bootloader, enter into recovery mode. Then press `Apply Update` and then `From ADB`. 

On your PC you will now execute the following command: `adb sideload XXX` and replace XXX with the file path of the zip-file. Once you press enter it will start to flash ethOS on your phone. Note: It may stop at 47% and read "failure to read: success", this is still fine. Now press "Reboot" and you have ethOS installed!
