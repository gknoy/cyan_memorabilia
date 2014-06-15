Cyan Memorabilia on an Arduino
==========================

This repository is dedicated to collecting a series of programs that run on an Arduino Uno with an RGB LCD shield
attached. Each program is created by a different coworker during my internship and is used as a means to remember them by.


Setting Up Your Environment
---------------
I highly recommend working on a Linux machine. I haven't tested working with Mac OS X or Windows. There are many ways to set up your 
environment to work on Arduino projects, however these instructions will take you through setting up a Vagrant + Virtual Box + Ubuntu development
workspace. If you want to work on barebones Linux you can skip the Vagrant instructions. 

### Install Vagrant and Virtual Box
I'm going to assume you have prior work experience with Vagrant and Virtual Box.

### Connect the Arduino

Start off by plugging the Uno into your computer. Make sure your computer recognizes the device with the command:
```
    $ VBoxManage list usbhost
    UUID:               45dc9928-b695-449c-8800-5a0dd6be60ce
    VendorId:           0x2341 (2341)
    ProductId:          0x0043 (0043)
    Revision:           0.1 (0001)
    Port:               2
    USB version/speed:  0/1
    Manufacturer:       Arduino (www.arduino.cc)
    SerialNumber:       85231363136351210152
    Address:            p=0x0043;v=0x2341;s=0x00001097b59604cc;l=0x14200000
    Current State:      Captured
```

### Working with Vagrant
    You can now run `vagrant up` with the Vagrantfile configuration given. Once you're ssh'd in, go ahead and run
    `lsusb`. If you can't see the device, unplug it and plug it back in. Run `lsusb` again.

### Setting up your environment
    For starters we need the arduino IDE for some libraries and files.
    ```     sudo apt-get install arduino ```
    We'll install pip as our package manager
    ```     sudo apt-get install python-pip ```
    With pip installed we can grab our command line utility ino. Ino is essentially the arduino ide without the GUI.
    ```     pip install ino ```
    Go ahed and make  directory for our new project. For sake of simplicity I'll refer to the root project directory as myproj.
    cd into myproj and run `ino init`.

    Finally we'll need to grab the LCD libraries which can be found [here](https://github.com/adafruit/Adafruit-RGB-LCD-Shield-Library).
    Go ahead and clone the repo:
    <pre><code>     git clone git@github.com:adafruit/Adafruit-RGB-LCD-Shield-Library.git</code></pre>
    Copy the example pde file from examples/HelloWorld/HelloWorld.pde to myproj/src

    You'll now want to move the entire Adagruit-RGB-LCD-Shield-Library directory to /usr/share/arduino/libraries/

    Make sure your pwd is myproj. Go ahead and run <code>ino build</code>. Once this has completed run <code>ino upload</code>. If all goes
    well the LCD should light up. Congrats!

    **Note: There are some libraries in /usr/share/arduino/libraries that may not be able to compile correctly. Go ahead and precede each library dir with a . that gives you a compilation error (for example Robot_Control becomes .Robot_Control).
