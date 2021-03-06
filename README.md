light_ws2811 V1.0
============



![Alt text](https://cdn-shop.adafruit.com/1200x900/1506-00.jpg"ws2811 for avrstudio v6  & Proteus simulation")


Light weight library to control WS2811 based LEDS and LED Strings on 8-Bit AVR and ARM microcontrollers. The new version 1 of this library supports a simplified interface and arbitrary CPU clock. 



 
Description
===========

This is a small Ansi-C library to control WS2811/WS2812 based RGB Leds and strings. Only the 800kHz
high-speed mode is supported. This library uses a bit-banging approach with cycle optimized assembler
innerloops. Some advantages of this approach compared to other solutions are:

- Compatible to all AVR MCUs since it does not rely on special periphery.
- The code timing is automatically adjusted to the CPU clock at compile time.
- A CPU clock speed of 8 MHz and up is recommended, but even 4 MHz may work under some circumstances.
- Much smaller program code: Size optimized assembler without unrolled loops (<50 bytes in most cases)
- Supports standard AVR, reduced core AVR (Attiny 4/5/9/10/20/40) and XMEGA (untested) without special case handling.
- Experimental Cortex-M0 ARM support.

The timing values used in the library were adjusted to work on all devices. Look [here](http://cpldcpu.wordpress.com/2014/01/14/light_ws2812-library-v2-0-part-i-understanding-the-ws2812/) and [here](http://cpldcpu.wordpress.com/2014/01/19/light_ws2812-library-v2-0/) for details.

Usage C - Interface
===================

- Add "light_ws2812.c", "light_ws2812.h" and "ws2812_config.h" to your project. 
- Update "ws2812_config.h" according to your I/O pin.
- Make sure F\_CPU is correctly defined in your makefile or the project. (For AtmelStudio: Project->Properties->Toolchain->AVR/GNU C Compiler->Symbols. Add symbol F_CPU=xxxxx)
- Call "ws2812\_setleds" with a pointer to the LED array and the number LEDs.
- Alternatively you can use "ws2812\_setleds\_pin" to control up to 8 LED strips on the same Port.

Examples are provided in the [Examples](https://github.com/cpldcpu/light_ws2812/tree/master/light_ws2812_AVR/Examples) folder. You can build them with the supplied makefile.


Troubleshooting 
================
Please note that incorrect timing is rarely the source of problems. If you want to save some time, go through the items below before altering the library.

#### None or only a part of the string is lighting up ####

 * Did you pass the correct array size in the function call?
 * Is the pin configuration correct?
 * Is anything else connected to the output pin you are using? Some development boards have LEDs connected to various pins.
 * Did you choose the correct CPU frequency setting? Did you initialize the clock correctly?

#### The LEDs are flickering and are not showing the intended color ####

 * This is often a problem with insufficient current sourcing capability.
 * Are you using a bypass capacitor for each LEDs as indicated in the datasheet? Not using a bypass capacitor will lead to erroneous behaviour. 
 * You may have to add an additional electrolytic capacitor at the input of your LED strip if you use long power supply lines.
 * Is your power supply able to supply the required current-level? If set to white at maximum brightness, each LED will draw 60mA. A single USB-Port is barely able to supply 10 LEDs.
 * The LEDs only display white: This can happen if the actual clock frequency of your MCU is lower than that given in F_CPU to the code.

Release History
================

-

Tested Combinations AVR
================

| Device             | 4 MHz  | 8 MHz  | 9.6 MHz | 12 MHz | 16 MHz | 20 Mhz |
| -------------       |:-------:| :-----: | :------: | :----:| :---:| :---:|
| ATtiny 85 (Standard Core )| X      |  X     |         |       |  X   |    |
| ATtiny 13 (Standard Core)|        |        |    X    |       |     |    |
| ATmega 8 (Standard Core)|        |        |         |   X    |  X  |    |
| ATtiny 10 (Reduced Core)| X      |  X     |         |       |     |    |
| ATmega 168 (Standard Core)|        |        |         |       |  X  |  X  |
| ATmega 32u4 (Standard Core)|        |        |         |   X    |  X   |  X  |


Please find updates on https://github.com/ws2811-Adafruit/ws2811-good

bug reports etc: elasa.group@gmail.com

