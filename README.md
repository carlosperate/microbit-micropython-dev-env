# BBC micro:bit MicroPython Development Environment
This repository contains a Vagrant script to facilitate the development of MicroPython for the BBC micro:bit.

This takes care of creating a virtual machine, installing all the development tools required, and get everything ready to compile.


## Prerequisites
You will need to have the following first:

* [VirtualBox](https://www.virtualbox.org/)
* [Vagrant](https://www.vagrantup.com/)
* An [mbed account](https://www.mbed.com/) (will need to login during installation!)


## Installing
Clone, or [download](https://github.com/carlosperate/microbit-micropython-dev-env.git) this repository, maybe with a shorter folder name:

```bash
git clone https://github.com/carlosperate/microbit-micropython-dev-env.git microbit-dev
cd microbit-dev
```

Getting the virtual machine up and running with Vagrant is extremely easy:

```bash
vagrant up
```

This will download the Ubuntu 14.04 32 bit virtual box image, so it might take a while depending on your internet connection.

Please note! During one of the last stages of the installation, the command line interface will request you to login to your mbed account.
A link should be printed on the console with a clear message, login to that page from your browser. The command line should automatically detect it and continue with the installation.


## Usage
Once you have the Vagrant box up and running (ensure it is up with `vagrant up`), you can SSH into it:

```bash
vagrant ssh
```

The MicroPython code is already there, but it hasn't been compiled yet:

```bash
cd shared_folder/micropython
yt build
```


## Load MicroPython to the microbit
The built hex file is saved into the following path from the project directory, which you can drop into the microbit USB drive for flashing:

```bash
vagrant_shared/micropython/build/bbc-microbit-classic-gcc-nosd/source/microbit-micropython.hex
```

To simplify the process [uflash](https://github.com/ntoll/uflash/) has been included with a wrapper script to load MicroPython with or without an additional Python program:

```bash
python load_upy.py
``` 

or

```bash
python load_upy.py <path to your python file>
```


## Access the MicroPython REPL
Once MicroPython is flashed, you will have access to the REPL on the USB CDC serial port, with baudrate 115200 (eg picocom /dev/ttyACM0 -b 115200).

If you have the python package PySerial installed (`pip install pyserial`), you can also use [microrepl](https://github.com/ntoll/microrepl), which is already included:

```bash
python vagrant_shared/microrepl/microrepl.py
```


## Trademarks
This projects is not endorsed, sponsored or associated with the BBC.
"BBC” and “micro:bit” are trade marks of the BBC. http://microbit.co.uk/

