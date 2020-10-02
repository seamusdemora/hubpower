# hubpower
Control the power settings for a USB hub

## AFAIK:

`hubpower.c` was [first posted in 2010 by Alan Stern in this mailing list](https://marc.info/?l=linux-usb&m=127162615232234&w=2). He also posted what seems to be a decent README:

***NOTE:*** You can [subscribe to the *linux-usb mailing list*](http://vger.kernel.org/vger-lists.html#linux-usb) here. 

>Okay.  Attached is the source code for a program named hubpower.  You 
can use it to tell your hubs to turn their port power on and off.
>
>To compile the program, all you have to do is:

	gcc -o hubpower hubpower.c

>You'll probably need to run it with sudo.  Tell the program the hub's 
bus number and device number, and give it a list of ports and power 
settings.  For example,

	sudo ./hubpower 1:3 power 4 on 2 off

>This will tell hub 3 on bus 1 to turn port 4's power on and port 2's 
power off.  Because of the way the Linux USB stack works, the program 
will also unbind the hub from the kernel driver when you do this, so 
the system will think that all devices attached to the hub have been 
unplugged.

>You can tell the system to bind the hub back to the kernel driver.
The devices plugged into the hub won't work again until you do this:

	sudo ./hubpower 1:3 bind

>However when you do this, the kernel driver will turn power for all the
ports back on.  There is no way to tell the Linux hub driver to leave a
port powered off.

>Finally, you can see the current status of every port by doing:

	sudo ./hubpower 1:3 status

>Alan Stern

## Meanwhile...

What follows is a more-or-less random, and very incomplete, collection of information relevant to ***power control of USB devices***: 

#### 1. A StackOverflow Q&A in Jan, 2011 which remains active in Sep, 2020: [Controlling a USB power supply (on/off) with Linux](https://stackoverflow.com/questions/4702216/controlling-a-usb-power-supply-on-off-with-linux) 

#### 2. [One of the answers](https://stackoverflow.com/a/18098075/5395338) posted to the [question above](https://stackoverflow.com/questions/4702216/controlling-a-usb-power-supply-on-off-with-linux) offered a [*patch* to `hubpower`](https://github.com/grandrew/hubpower), but the comments had mixed reviews.

#### 3. Alan Stern again with [Power Management for USB](https://www.kernel.org/doc/Documentation/usb/power-management.txt) documentation for the Linux kernel. This was last updated in Feb, 2014. 

#### 4. [Another answer](https://stackoverflow.com/a/40495413/5395338), posted in Nov, 2016, proposed [`uhubctl`](https://github.com/mvp/uhubctl) as a solution.

#### 5. [PowerTop](https://01.org/powertop/) - Intel's open-source tool for Linux power management isn't strictly about USB power, but it's currently maintained (as of June 2020). It may be useful, and the [source code & other information is available on GitHub](https://github.com/fenrus75/powertop). 

#### 6. Alan Stern *weighs in* again on this question in a May 2017 thread on the [*linux-usb mailing list*](http://vger.kernel.org/vger-lists.html#linux-usb). This is an interesting thread! A couple of statements that seem to encapsulate the primary issues are: 

* `Linux's USB stack was designed with the idea that the driver is in full control of the device.`  

* `sorry, USB sucks :)`... Which I think is to say that USB standards are not comprehensive, and their implementation is not uniform.

