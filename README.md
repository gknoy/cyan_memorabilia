Cyan Memorabilia on an Arduino
==========================

This repository is dedicated to collecting a series of programs that run on an Arduino Uno with an RGB LCD shield
attached. Each program is created by a different coworker during my internship and is used as a means to remember them by.


Setting Up Your Environment
---------------
I highly recommend working on a Linux machine. I haven't tested working with Mac OS X or Windows. There are many ways to set up your 
environment to work on Arduino projects, however these instructions will take you through setting up a Vagrant + Virtual Box + Ubuntu development
workspace. If you want to run barebones Linux, skip the Vagrant instructions.

Lets start by forking and cloning this repo (if you're using Vagrant do this on the host):

    git clone git@github.com:<your_username>/cyan_memorabilia.git

and don't forget to add the upstream remote:

    git remote add upstream git@github.com:zysh/cyan_memorabilia.git

## Vagrant Instructions
I'm going to assume you have prior work experience with Vagrant and Virtual Box and that they are both installed correctly along with
Guest Additions. Note that in the Vagrantfile we do two things: Create a shared folder in the default vagrant users home directory and
set up our VM so it can see the arduino connected on the host machine. If you're using a base box with a user other than vagrant make
sure to change the shared folder location.

### Connect the Arduino

Plug the Uno into your computer. Make sure your computer recognizes the device. If you're running with Virtual Box and Vagrant then do something like this:

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

If you're running Linux a simple `lsusb` will do.
Once you know your host machine can detect the Arduino unplug it.
You can now run `vagrant up` with the Vagrantfile configuration given. Once you're ssh'd in go ahead and run
`lsusb`. If you can't see the device unplug it and plug it back in. Run `lsusb` again.

### Setting up the Arduino Environment
For starters we need the arduino IDE for some standard libraries.

    sudo apt-get install arduino

We'll install pip as our package manager

    sudo apt-get install python-pip

With pip installed we can grab our command line utility ino. Ino is essentially the arduino ide without the GUI. Feel free
to use a virtualenv wrapper.

    sudo pip install ino

Finally we'll need to grab the LCD libraries which can be found [here](https://github.com/adafruit/Adafruit-RGB-LCD-Shield-Library).
Go ahead and clone the repo:

    git clone git@github.com:adafruit/Adafruit-RGB-LCD-Shield-Library.git

Move the entire Adafruit-RGB-LCD-Shield-Library directory to /usr/share/arduino/libraries/

Make sure your pwd is cyan\_memorabilia. Go ahead and run `ino build`. Once this has completed run `ino upload`. If all goes well the LCD should light up (you may have to
unplug/plug it back in). Congrats!

**Note: There are some libraries in /usr/share/arduino/libraries that may not be able to compile correctly. Go ahead and precede each library dir with a . that gives you a compilation error (for example Robot\_Control becomes .Robot\_Control).

## References for Programming
    - Note that the example in Adafruit-RGB-LCD-Shield-Library/examples/HelloWorld is a good reference!
    - [Some Basic Information on the Shield](https://learn.adafruit.com/rgb-lcd-shield/using-the-rgb-lcd-shield)
    - [The LCD DataSheet](https://www.adafruit.com/datasheets/HD44780.pdf)
    - [Arduino Programming Guide](http://playground.arduino.cc/uploads/Main/arduino_notebook_v1-1.pdf)
