---
layout: post
title: LED Light Project
---

A description of an LED strip controlled by a Python web server running on a Raspberry Pi.

I had a conversation with a coworker about the great electronics tutorials at [adafruit.com](adafruit.com). These tutorials walk you through how to build a circuit on a breadboard and use a Raspberry Pi and a Python library to send digital output to the circuit. I had already picked up a Raspberry Pi Zero and found an LED light strip on Adafruit. The strip has 30 pixels, individually addressable, so each one can be programmed to emit its own RGB value. I got excited to build out the circuit and a small Python server running on the Pi to control the light strip.

Here's some shots of the final product:

<center>
<img src="/assets/led_lights/circuit_schematic.jpg" alt="circuit schematic" width="150"/>
<img src="/assets/led_lights/breadboard.jpg" alt="breadboard" width="150"/>
<img src="/assets/led_lights/wild.jpg" alt="" width="150"/>
<img src="/assets/led_lights/indigo.jpg" alt="" width="150"/>
<img src="/assets/led_lights/roygbiv.jpg" alt="" width="150"/>
<img src="/assets/led_lights/bluegreen.jpg" alt="" width="150"/>
</center>


I followed [these instructions](https://learn.adafruit.com/neopixels-on-raspberry-pi/raspberry-pi-wiring) to wire up the breadboard, using the Level Shifting Chip method. I spent maybe $30 for all the materials.

There's a [Python neopixel library](https://circuitpython.readthedocs.io/projects/neopixel/en/latest/) that does the hard work. It lets you initialize a light strip and then index into the LEDs to set a color.

```
strip = Adafruit_NeoPixel(LED_COUNT, LED_PIN, LED_FREQ_HZ, LED_DMA, LED_INVERT, LED_BRIGHTNESS, LED_CHANNEL, LED_STRIP)
strip.begin()
strip.setPixelColor(pixelIndex, rgbValue)
```

Each pixel can be updated many times a second. I wrote a program that defines a color loop, which continuously walks up and down the pixels in the strip and changes the color of that pixel. Additionally, this program runs a Python Bottle web server that has a few routes to control the strip. I created a map of pattern name to list of RGB values. For example, the pattern, Halloween, has a list of two colors, black and orange. There is a route that accepts a pattern name as input, and then sets the available pixel colors. The color loop selects pixel colors at random from the available pixel colors and updates the pixel color while it walks up and down. The effect of this is that the light strip flickers with the colors specified by the pattern. There is also an index page that lists all the defined patterns and lets you select one, which updates the light strip. 
