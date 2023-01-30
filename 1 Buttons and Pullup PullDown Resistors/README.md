# Buttons and Pullup/Pulldown Resistors
## Buttons and Floating Inputs
For reasons, the buttons on your launchpad have been left as a simple button connected to ground with no pull up resistor. This will lead you to have issues trying to use them. This is a summary of why you are probably having issues, and the ways around getting the buttons to work (note, they are not broken).
## What is on your board?
Looking at the Launchpad Datasheet (https://www.ti.com/lit/ug/slau680/slau680.pdf?ts=1674790902969&ref_url=https%253A%252F%252Fwww.google.com%252F), you can scroll down to the schematic and find that the buttons are in fact just hooked into ground and then into the microcontroller. This seems like an odd thing to do, and will cause you to have floating inputs (where the pin is never actually being told what voltage to be at, hence when you are touching the pin or button, it will sometimes flip between a one or zero).
https://i.gyazo.com/678b2b3c1788134372efa4530e1a1f13.png

## Internal pull-up resistor
Inside of each one of the pins, there is a circuit which can be enabled to allow a resistor to be put in parallel with the pin and ground or Vcc.
https://i.gyazo.com/dccdf72d0c59fb83d662d86280db6f5e.png
This is actually really helpful and will come in handy later in the course as well. But for now, we can configure the hardware to allow us to connect a resistor from the switch pin to Vcc. This will allow the button to register a 0 when connected to ground, and then "pull up" the pin to a 1 (Vcc) when the switch is an open circuit.

##How to enable this internal resistor
You could either work through the diagram, or, if you search on the Family User Guide (https://www.ti.com/lit/ug/slau445i/slau445i.pdf?ts=1674790523141&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FMSP430FR2355) for "PXREN" [The "X" is the general place holder], you can see a table which will tell you how to configure the pin as an "Input with Pull Up Resistor"
https://i.gyazo.com/643ecba26d0e5bcf7fdaf977d318d385.png
