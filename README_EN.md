# PocketAdminWorkshop

Table of Content


## Introduction

In this repo, you will find assembly instructions for the [PocketAdmin](https://github.com/krakrukra/PocketAdmin) project, courtesy of @krakrukra. **I did not create the hardware, nor the software! All credits go to the original creators of the PocketAdmin project!** The goal for this repo is, to provide a streamlined building process for a kit with all the parts pre-selected, so you can do it on your own, or more specificaly: So you can use this guide in a workshop I am planing to hold.
If you have already some experiences with assembling pcbs with smd parts, you propably won't need this guide.

**This workshop is inteded to create an educational device, please be carefull with what you do with your PocketAdmin.**

## Assembly

### Preparation

First, start by placing all the parts before you.
You should have:

1x STM32F072C8T6 
![](/doc/Images/Picture_STM.png)

1x W25N01GVZEIG flash memory
![](/doc/Images/Picture_Flash.png)

1x IP4220CZ6 transient protection diode
![](/doc/Images/Picture_Diode.png)

1x MCP1700-3302E/TT linear regulator
![](/doc/Images/Picture_linear_regulator.png)

3x 10µF capacitors
![](/doc/Images/Picture_capacitors_10uF.png)

2x 18pF capacitors
![](/doc/Images/Picture_capacitors_18pF.png)

7x 100nF capacitors
![](/doc/Images/Pciture_capacitors_100nF.png)

2x 33 ohm resistors 
![](/doc/Images/Picture_resistor_33.png)

2x 4.7k ohm resistors 
![](/doc/Images/Picture_resistor_4k7.png)

1x GREEN LED 
![](/doc/Images/Picture_led.png)

1x NX5032GA 8MHz quartz crystal
![](/doc/Images/Picture_quartz.png) 

1x TL3342 tactile switch 
![](/doc/Images/Picture_switch.png)

1x USB type A plug
![](/doc/Images/Picture_usb.png)

In summary you should have 12 different packages, 1 PCB and 1 Case.


### Assembly

Download and open the included [IBOM HTML file](/doc/BOM/ibom.html). Select the back-side of the PCB.  
Then apply soldering paste with the stencil. 
If have no expereince on how to that, wait for a trainer to help you.

Now, start placing the different parts onto the pcb.
Be careful to place the STM correctly.
![](/doc/Images/Picture_back.png)

When you are done, place the PCB in a reflow oven and wait until the first side is done.

When the PCB is baked, wait for it to cool down, then continue with the other side.
**WARNING: Do NOT place the USB-Header for the second reflow process. You will need to solder it by yourself!**

![](/doc/Images/Picture_front-png)

When the second side is also soldered, put on the USB-plug and solder the 4 pins by hand.
![](/doc/Images/Picture_done.png)

Check the PCB for short circuts or errors. If you find some and need help with correcting the errors, ask a trainer to help you.

You are now done with the assembly. Continue with the programming part.


## Programming

Start by cloning the PocketAdmin repository:
https://github.com/krakrukra/PocketAdmin

Then install the **dfu-utils** package for you operating system.

Then, insert a pair of tweezers into the boot0 and the 3.3v holes on the lower end of the pcb. They are located adjecent to the square hole.
(x) (x) () () []

![](/doc/Images/Picture_dfu.png)

Then insert the PocketAdmin into your USB Port. You can then remove the tweezers.
Make sure the STM is detected by running  
**dfu-util -l**

Open a terminal and navigate to the /firmware directory of the PocketAdmin repo.
Then flash the .dfu file with   
**dfu-util -a 0 -D firmware_13006.dfu**  
(The filename might change with newer versions.)

The terminal output should show you a progress bar. When finished, remove and reinsert the flash drive.
Your operating system should now be able to detect an unformated partition on an unkown device.
Create a partition table and format the drive in FAT32. (For example with gparted.)

## What now?

After flashing and creating a partition, you should be able to use your PocketAdmin.  
For a complete list of the capabilities, check the PocketAdmin [Wiki](https://github.com/krakrukra/PocketAdmin/wiki).

As a quick-start guide, try the following:
- Remove the PocketAdmin
- Hold down the button and insert it. Wait for about 1 second bevore you let the button go.
- Now your operating system should detect the PocketAdmin as a flash drive.
- Copy the "payload.txt" file from the /files directory onto the PocketAdmin.
- - Open any text editor. Then remove and reinsert the PocketAdmin. It should write something like "ABCDEFG..." etc...