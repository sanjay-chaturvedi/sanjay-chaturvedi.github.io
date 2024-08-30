---
title: "AC Voltage Measurement using Arduino Uno"
excerpt: "Measurement of AC voltage using Arduino Uno development board. A voltage transformer is required in AC voltage measurements and alongwith a resistor voltage divider."
collection: projects
---

This project is on the measurement of AC voltages in the range 180 V to 270 V, using an open-source microcontroller development board. Here we have used Adruino Uno as the development board.

Since, we can not directly use an Arduino Uno board for AC voltage measurement, therfore we have two options:

1. To use a sensor to generate a signal corresponding to the applied AC voltages, which is suitable as an input to Arduino Uno board. 
2. To do the job of the sensor yourself.

In this work, we will go with the second step. 

## We need to follow the following steps to measure the AC voltage:

1. Reduce the voltage levels using a voltage transformer.
2. Convert the reduced AC voltage to DC voltage using a rectifier.
3. Smoothening the rectifier output. 
4. Reducing the DC voltage levels to the levels of Arduino input levels using a resistor voltage divider circuit.
5. Finally, we need to find a map between the AC voltage and final DC voltage value through lab tests.

The schematic diagram of the circuit that does the above mentioned job from step 1 to step 4 is shown below:

<br/><img src='/images/rectifier.png'>

## Mapping the input AC voltage with DC output of the above circuit

The microcontroller in Arduino Uno development board has a 10-bit ADC, so the maximun output from this ADC will be 1024 and this corresponds to a maximum input of 5 VDC. Since, the input signal for the development board is in range of 0 VDC to 5 VDC, the ADC output is mapped directly s follows:

* 0 VDC - ADC Value = 0
* 5 VDC - ADC Value = 1024

The maximum applied AC voltage of 270 V is mapped to a rectifier output of 5 VDC by adjusting the variable resistor (used as a voltage divider at the rectifier output). And the 5 VDC input to ADC is mapped to a value of 1024. Using this relation in reverse, we can now say that an ADC value of 1024 means an input of 5 VDC to the ADC and 5 VDC means an AC input voltage of 270 V. Hence, 1024 value maps to 270 VAC. This relation is then used to find the AC voltage value at a given value of ADC output.

* 1024 maps to 270 VAC
* 1 maps to (270/1024) VAC
* *x* maps to (270/1024)**x* VAC