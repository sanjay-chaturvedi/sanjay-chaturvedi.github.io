---
title: "AC Voltage Measurement using Arduino Uno"
excerpt: "Measurement of AC voltage using Arduino Uno development board. A voltage transformer is required in AC voltage measurements and alongwith a resistor voltage divider."
collection: projects
---

This project is on the measurement of AC voltages in the range 150 V to 250 V, using an open-source microcontroller development board. Here we have used Adruino Uno as the development board.

Since, we can not directly use an Arduino Uno board for AC voltage measurement, therfore we have two options:

1. To use a sensor to generate a signal corresponding to the applied AC voltages, which is suitable as an input to Arduino Uno board. 
2. To do the job of the sensor yourself.

In this work, we will go with the second step. For that we need to follow the following steps:

1. Reduce the voltage levels using a voltage transformer.
2. Convert the reduced AC voltage to DC voltage using a rectifier.
3. Smoothening the rectifier output. 
4. Reducing the DC voltage levels to the levels of Arduino input levels using a resistor voltage divider circuit.
5. Finally, we need to find a map between the AC voltage and final DC voltage value through lab tests.

<br/><img src='/images/500x300.png'>
