# hackpack
LED dot matrix display on a backpack!

A quick little project to get started on working with Arduino

A simple project to display cool 8bit art and animation on your backpack! This is a quick and easy project you could finish off in minutes and show off to your friends. What it does is, when you move your backpack, a dot matrix display turns on and shows any character you have programmed in it. In this case its a fun pixelated character.

Ingredients:

1. MAX7219 Dot Matrix Display Module

2. Arduino <Any version>

3. 9v Battery & Connector / Any other portable power source.

4. ADX335 Accelerometer Module

5. Jumper wires

How does it work?

The objective of the project is to light up a character on a dot matrix display. The display should light up when you move the bag. There are two parts to this project.

Part 1: The Wake Part

This part uses the accelerometer to sense when the bag moves. The accelerometer sends this data to the Arduino via the ‘Analog In’ pins.

Part2: The Display Part

The display shown on the LED matrix is driven by the MAX7219 IC. It talks to the Arduino using the SPI protocol. But we don’t need to know much about this because there’s a library “ledcontrol” that does the job for us.

STEP 1 : Wiring up the Dot Matrix Display, Arduino and Accelerometer

The circuit is as straight forward as it gets. The accelerometer returns analog values for acceleration in each axis. But here we only need the values for one axis. So connect either the X,Y or Z axis output from the accelerometer to any of the analog input pins (I have used A0 in the code provided). Power up the accelerometer. Be careful at this point because some modules use 3.3V and some use 5V. Give power accordingly or else you might end up with a burnt module. Connect its ground (GND) to the ground on the Arduino.

The dot matrix display has 3 input pins DIN (Data in), CS (Chip Select) and CLK (Clock). These are SPI (Serial Peripheral Interface) pins. Like I said before, the library does the job for us :) They are all digital, connect them to any of the GPIO pins. I connected DIN to pin 13, CS to pin 12, CLK to pin 11 in the code provided.

The dot matrix display takes in power via the 5V pins from the Arduino. Connect ground (GND) to the ground on the Arduino. And that’s all there is with the circuit.

STEP 2 : The Code

We should include the LedControl.h library to our code. This is what makes talking to the LED dot matrix display extremely easy. It is available here: https://github.com/wayoda/LedControl/releases

As this is not an included library in the Arduino IDE, we should manually add it. If you don’t know how to, follow this guide: https://www.arduino.cc/en/Guide/Libraries

The code available in the repo

Here are some of the basic functions in the header:

Creating a new LedControl object: (‘lc’ in this case)
  LedControl lc=LedControl(13,11,12,1);  // DIN, CLK, CS, No of grids used

Turning on the dot matrix display:
  lc.shutdown(0,false);
  Note: Initially the grid is in a low power state.

To Clear the display:
  lc.clearDisplay(0);

To set individual LEDs high:
  lc.setLed(0,row,col,true);

Setting entire columns/rows in one go:
  lc.setColumn(0,i,array[x]);
  lc.setRow(0,i,array[x]);

To know more read: http://wayoda.github.io/LedControl/pages/software

Upload the code provided to the Arduino.

Play around with the delay and A0’s division factor. Do this till you are happy with how sensitive your backpack is to motion.

You might have to play around with these values as you change power sources too.

Step 4 : Show off

Show off your cool new addon to your friends. And get them interested in becoming Makers too! :)

NOTE: You could add more characters to the display by playing around with the ‘disp’ function and the arguments it receives. Play around with the ‘sinvader’ functions to change the orientation of the characters. ‘lc.setColumn’ could be changed to ‘lc.setRow’ for this.



Originally posted by me on : http://diyhacking.com/dot-matrix-display-hackpack/