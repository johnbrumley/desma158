---
layout: slides
title: Day 18
---
# Today

The end of the quarter is approaching fast! Please let us know how your projects are coming along and if you are stuck on anything.

Also please evaluate the class if you can. You can go to [this link](https://be.my.ucla.edu/directlink.aspx?featureID=161&src=r0](https://be.my.ucla.edu/directlink.aspx?featureID=161&src=r0) to access your evaluations.


![](https://lh7-us.googleusercontent.com/Yk9wV1Y3taImmIvkmREzgfYbmkwO5YbW_wfDnK_bm5tRDe3_vbxow6DGnnXwsWH0SWP8DHodfba3m3u9XE33j6sY_uH2QwcWjW-tcnb1u9hQh3uMMK3blg0aKqDSSpoM0T1exvUriTqlfln5RhsNM2nbjHIuarING433aVCqmRYomeu-l-oZMEdn79WNgQ)


# Arduino & Unity (with Uduino)

This guide will walk you through setting up Unity and an Arduino. With some examples included.

I am using an Arduino Leonardo in the examples, check if your board is compatible [here](https://marcteyssier.com/uduino/docs/compatibility)

> If you don't want to use Uduino and are more comfortable writing your own arduino code, check out [this project](https://github.com/dyadica/Unity_SerialPort) which has an example project for getting non-blocking serial port communication. If you just want the script, here's the [UnitySerialPort.cs](https://raw.githubusercontent.com/dyadica/Unity_SerialPort/master/Unity_SerialPort/Assets/Scripts/UnitySerialPort.cs) file.


# Arduino Info

Arduino is a company that develops programmable boards (microcontrollers) and an associated software platform for developing code and uploading it to the board. An Arduino is great for developing projects and experimenting with a system before designing a more permanent piece of hardware (or you can also keep using the Arduino board). 

There are many varieties of Arduino boards. Additionally, the board designs are open source, so there are also many third-party boards that may even appear to be official boards. Generally, most people start with the Arduino UNO, but if you have a very specific use case you might consider one of the other [boards](https://www.arduino.cc/en/hardware).

![](https://lh7-us.googleusercontent.com/2a5RxZPMsI321XbZ-cPtj_n_Ikxs006uaisdswlUfYS1ayHtWItU_8X7_pVHwCTGkIGwfyE_9y1nnWKa2GTQe7XQlOL_FwwPvP10LEE8Ffujlu61EUkQILdYdQo-1-qIiP_yO7LEjwMhvJUdxogOjOc)

Arduino is not the only option for development boards. The ESP32 is a popular microcontroller at the base of many [alternative boards](https://all3dp.com/2/best-arduino-alternatives/) that focus on WiFi and Bluetooth connectivity. 

The UNO has 14 digital input/output pins (of which 6 can be used as PWM outputs) and 6 analog inputs. Digital pins can be used to set things On/Off or receive values from switches, while analog inputs can receive a range of values and PWM outputs can also output a range of values.

![](https://lh7-us.googleusercontent.com/lsNNr_don__q3mOEOZhEB9fn7YNi55zZSPED0a5YDPixecz1IS2QuOteE6KO1cWR2E-kLLuhVvwKTrw-26oncUVmLnJMtPowHXTUpqk7-EbT6qS0l-wBQ9R5eUmAVbTCUOOSRyw4Sx-7ZLVz3xR7mR4)

## Arduino IDE

The Arduino IDE ([https://www.arduino.cc/en/software](https://www.arduino.cc/en/software) ) allows you to detect Arduino (and other) hardware connected to the USB port of your computer. You can write code using the Arduino programming language ([https://www.arduino.cc/reference/en/](https://www.arduino.cc/reference/en/) ) which is built on C/C++ (similar to how Processing is a superset of Java). There is an online code editor ([https://create.arduino.cc/editor](https://create.arduino.cc/editor) ) but for setting up Uduino, you’ll need to use the desktop version.
### Setting up the desktop IDE 

1. You can download the editor at this [page](https://www.arduino.cc/en/software), but the Uduino Arduino library is not currently updated to work with the newest version (2.0.0). I would recommend downloading the most recent legacy version of the IDE (1.8.x), but it is also possible to manually update Uduino to work. (see below)
2. When downloading, try and keep the default settings so that you don’t need to modify settings later. If you need to change any folder paths, then remember the location for later.
# Uduino

Uduino is a Unity and Arduino library that simplifies serial communication between physical hardware connected to the arduino and a Unity scene. The official website and documentation is found here: [https://marcteyssier.com/uduino/](https://marcteyssier.com/uduino/) 

Uduino is not free, so if you want to purchase it as an asset you can use the official [Unity Asset Store page](https://assetstore.unity.com/packages/tools/input-management/uduino-arduino-communication-simple-fast-and-stable-78402). For this class, I wanted to allow everyone to try out Uduino, so I am providing a copy [here](https://drive.google.com/file/d/1r5sBn88_dq5kS1OCRkq5qYAn3GHGhx58/view?usp=sharing). If you plan to use the asset in future projects, please purchase a copy from the Asset Store. 
## Uduino Setup

1. [Download](https://drive.google.com/file/d/1r5sBn88_dq5kS1OCRkq5qYAn3GHGhx58/view?usp=sharing) and unzip the Uduino library
2. Drag the entire folder into the Assets folder of your project
3. To check that it has been installed, try opening the BlinkLed example found at 

“Uduino/Examples/Basic/BlinkLed/BlinkLed.scene” 

If the scene opens and you don’t see any errors then you can start configuring Uduino.

4. In the Hierarchy panel in the Unity Editor, highlight the Uduino GameObject and follow the instructions in the Uduino Manager panel in the inspector. You can move from top to bottom clicking any buttons to fix compatibility issues. You should see something similar to the image below when all the steps are done.
  

![](https://lh7-us.googleusercontent.com/-Rtx7bnY6WNaRF4NXwS8D7kwAIs42YIX3oRsM9Yp8MvwsiUkCqndRmpRnvWgExEernl7JBpkK6H1vlBUp7nKmL1aaX9_244yKYYBkbhOtxkSMLeDuGb78wsGi2rNN8939fQ-oDvppOn8mW5fJiPeWvo)

5. At this point you’ll need to set up your Arduino by uploading the Uduino library to the board. Move to your Arduino IDE and open File > Examples > Uduino > Uduino. If the example isn’t showing up, check the “For Arduino IDE 2.0.0 users” section below.
6. Connect your Arduino board to your computer.
7. In the IDE select your board and port in Tools > Board and Tools > Port. In version 2.0.0, you can select both using the Select Board menu :

![](https://lh7-us.googleusercontent.com/mwvZdFDeTzNlfrNXZQM0Gf0KPDaN6cnb6LonmxxSRMoOdEbV5Pr6A5QdlXcygOHUWf-yYlyRLZ6LX0_dfGZlEQ1Ebi6ABbMyOP5Lx-pz3nr6eF0jci_Y04uKkxCj4SXN8Vkz9CJvaSaewoeWaN2ilLA)![](https://lh7-us.googleusercontent.com/wejh_KiVQuFuzHBeCTJWk-cdED-2-koBa_fJgOg8LXBWyPBwmbB18RFQ8alDd_Ol1R2uYpwExWgd0knwYIrxkm5QAjCQrkJv4xjP9rpu0a547pBcnfum7FBLHvDDTQQw4sBZLYeZyafF3zb0XzTqpFQ)

8. Click the Arrow button to upload the code to your Arduino board. The lights on the board should flash and you’ll see a “Done Uploading” message.
9. Back in Unity, return to the Uduino Manager in the Inspector and click the Discover Ports button. You should see “uduinoBoard” appear. 
10. Press the Play button to start the scene. If your arduino has a built-in LED connected to port 13. Then that LED will blink once per second. You can select the BlinkLed GameObject to change the pin output and the speed.

![](https://lh7-us.googleusercontent.com/4TFuhi2-4pGGf4RjM7qGy2XuK5O4TKkXckyXTTSagSAodScYgCrXPcYMfg3BW7hZ1FzVnnw7aUhi7WNw0k_FgcJoEpz7xD0_FZF8ooL5t0vTeGpC-yDgb1ACJXBzmAdiSGQuZi_6mfqJOz8j0cccKWw)

## For Arduino IDE 2.0.0 users:

To have the Uduino library show up in the most recent version of the Arduino IDE (2.0.0). You need to add a “library.properties” file to the folder that Uduino automatically added during the initial setup. I’ve added the file to the drive [here](https://drive.google.com/file/d/1ohry8W6tvxMkDT4fCOGWElvfWvJp0adl/view?usp=sharing). 

1. Navigate to the Uduino Arduino library folder, usually found in “Documents/Arduino/libraries/ Uduino” and place the “library.properties” file in that folder. 
2. Restart the Arduino IDE and now Uduino should show up in the examples
# More examples

## Blink with circuit

To set up the above example with an external LED (Light Emitting Diode). You can duplicate this circuit which uses an LED and a 220 ohm resistor. Note that your LED has one leg which is longer than the other. The shorter leg of the LED should connect to the Ground (GND) pin of the Arduino and the longer leg connects (via the resistor) to Pin 13.

![](https://lh7-us.googleusercontent.com/z5_NKq5SkmIJyt36OtTrCVNJr8o_Nop4-2lJzJPZe_FKCcu15sV0tUTgWAITlYYTShSvnAkiA_SEYwMQpe27aAitGrx58tjC1kcQ7JZFBcMXUpfr9zbCRtvXssgGRKl78XEZ2YwkuKqDR2hAm1EA5EQ)From: [https://www.arduino.cc/en/Tutorial/BuiltInExamples/Blink](https://www.arduino.cc/en/Tutorial/BuiltInExamples/Blink) 

You can change the output Pin or add multiple LEDs to different digital pins. In the BlinkLed example, you can duplicate the BlinkLed GameObject and set it to a different Pin to control multiple LEDs. Each LED should have its own resistor and pin connection, but all can connect to the same ground pin.

## Switch/Button

A switch or a button can be any device that can interrupt the flow of electricity depending on its state. There are many many types of switches and buttons and you can build your own custom switch using just about anything that can conduct electricity.

Parts:
- Switch / Button / etc
- 10k resistor (optional)

![](https://lh7-us.googleusercontent.com/wBxbFCVRrw5E9jnIekuQinJHsBczZF22E7FZWVr5oE3Nr_taHbHXFGTN_STx8KOCsCwddNWVS7PM-bbP3zY2ClFbSwsyflerc10O3NiajaC8kPhIfpG5C-RReLHMOvpJlqDaaiCUJIbO7G5RP3mN9S0)

This diagram shows a button placed between pin 2 and the 5V output of the arduino. When the button is not being pressed pin 2 is connected to ground through a resistor (known as a pull-down resistor). When the button is pressed, 5V passes through the button to pin 2.

In Uduino, we can set pin 2 to be an input pin and read input to see whether the value is LOW (ground) or HIGH (5V). 

We can simplify the circuit even more by taking advantage of an internal pull-up resistor. This is done in the code of the DigitalReadButton example scene. When declaring a pin type in the script, you can specify if you want it to use PinMode.Input or PinMode.Input_pullup:

![](https://lh7-us.googleusercontent.com/U88L9rI2-vaqhJEoceEC6dYH-FrVCxSAIcbXkpGYU8RvlDz71J5ElbpRX1DeAd9iOzTyjWGkn3iuhAlD4fXnTxLFooBLipmi1fiZngPjx3p3CKHkiSSjcYtnJLrCNlrrusyetrUwKcVxAz5U8clW4xU)

You don’t need to use the resistor in your circuit anymore and can place the switch directly between Pin2 and ground. When the switch is open (not allowing electricity to pass) the value at pin 2 will be HIGH due to the pullup resistor, and when the switch is closed pin 2 will read as LOW.

## Solenoid

A solenoid uses an electromagnet to move an actuator. Passing an electric current through a solenoid will cause the actuator to move in one direction, usually there is a spring to return the actuator to its original position. Solenoid valves can be used to control the flow of fluids like air in a pneumatic system or water in a hydraulic system.

There are a few more parts required for this circuit:
- Solenoid
- 220ohm resistor
- Diode
- Power Transistor
  

![](https://lh7-us.googleusercontent.com/OSAr9MgZPJOwU2NvaMPrVUHRc1Blv3-73RFj4eyRPKwVspnp5etIX2AkUbq2HzD2Mo_JQZnnM7SH-pgYDNNNw-EijMf-wGWIp92d5Pi_WhMncAML34L-YkFJPORcQzXXezMW1H-PKtYlqK_2U_NMkb0)


Be careful about the solenoid that you’re using. If it is larger, the current draw may be larger than 250mA, which is more than an Arduino can handle and you’ll need to bring in an external power supply. For much higher power, consider using a Relay instead of a transistor.

This circuit plugs into Pin 9 of the Arduino, but the function is nearly identical to the blink example we just covered. The arduino sends an On/Off signal from one of the digital pins to the circuit. You can modify the BlinkLed example to match the correct Pin on the diagram or change the wiring to use the pin in Unity.

However, this time it controls a transistor, which acts like a switch to turn power on and off for the solenoid. The diode is added to protect against current moving through the circuit in the wrong direction (also common with DC motors).

Because the solenoid is mechanically moving back and forth, the speed at which you can activate it is limited to how quickly it can return to its original state.

More info about this circuit can be found here:
[https://core-electronics.com.au/guides/solenoid-control-with-arduino/](https://core-electronics.com.au/guides/solenoid-control-with-arduino/) 

## DC Motor / Vibrating Motor

DC motors convert DC or direct current to rotary motion. A vibration motor is also a DC motor, but adds a weight to unbalance the motor and cause vibration. If you want to change the direction that the motor rotates, reverse the connections going into the motor. If you want to control multiple DC motors with an arduino, you’ll likely need to get a separate power supply that can handle the combined currents of the motors. There are also special motor control shields for arduinos that make building the circuit much easier. 

Parts: 
- DC motor
- 220ohm resistor
- Diode
- Transistor
  

![](https://lh7-us.googleusercontent.com/P22rY7hWecZxQl8eHaHpW9FcNi8SOH_kGwtj7P8U712QMS7jpEDO2YnNmx8m1wgRhmb3bVykPFSjHOi2N7gADTxx1SZuQ_K1Diq9TbLEzsNMnkOg00jx6_-YHrdT7bx6--9Ke568k_6PaMR_J4rDKo0)

You might notice that this circuit is nearly identical to the solenoid circuit. And it very nearly is. The only difference is that there’s a different transistor being used, which has a different pin configuration. Before, the pin went through the resistor to the leftmost pin of the transistor, while here it goes to the middle pin. In both cases it should be going to the Base of the transistor. 

Transistors have three pins known as the Base, Collector, and Emitter. Electricity will flow from the collector to the emitter, but only if some power is sent to the base. Here the arduino can turn on and off the electricity to the motor even though the output of the pin would not be enough to power the motor.

Note: If using a MOSFET, you might notice that the datasheet labels the pins as S,D, and G for Source, Drain, Gate rather than Collector, Emitter, and Base. In this case the Source goes to ground, the Drain goes to the positive voltage, and the Base is where the arduino signal should connect to.

Another difference is that we can send PWM values from our pin (as long as the pin has a “~” next to it on the board) to control the speed of the motor. 

The Uduino example FadeInOut allows you to send PWM values to a specified pin. 

More info here: [https://learn.adafruit.com/adafruit-arduino-lesson-13-dc-motors](https://learn.adafruit.com/adafruit-arduino-lesson-13-dc-motors) 

## Servo Motor

If you are interested in learning more about components and creative ways to assemble machines from components check out Tim Hunkin’s work:

[The Secret Life of the Vacuum Cleaner - Remastered](https://youtu.be/CJlrbMHLBd4)

[The Secret Life of components. A series of eight guides for designers and makers by Tim Hunkin](https://youtu.be/6JAgXz6xO0s)

  