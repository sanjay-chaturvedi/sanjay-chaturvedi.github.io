---
title: "AC Voltage Measurement using Arduino Uno"
excerpt: "Measurement of AC voltage using Arduino Uno development board. A voltage transformer is required in AC voltage measurements and alongwith a resistor voltage divider."
collection: projects
---


This project is on the measurement of AC voltages in the range 180 V to 270 V, using an open-source microcontroller development board. Here we have used Adruino Uno as the development board.

Since, you can not directly use an Arduino Uno board for AC voltage measurement, therfore a circuit is built to generate a suitable input signal for microcontroller that corresponds to AC voltage. This circuit does the job as described further in this article. 

## The following steps are followed to measure the AC voltage

1. Reduce the voltage levels using a voltage transformer.
2. Convert the reduced AC voltage to DC voltage using a rectifier.
3. Smoothening the rectifier output. 
4. Reducing the DC voltage levels to the levels of Arduino input levels using a resistor voltage divider circuit.
5. Finally, we need to find a map between the AC voltage and final DC voltage value through lab tests.

The schematic diagram of the circuit that does the above mentioned job from step 1 to step 4 is shown below:

<br/><img src='/images/rectifier.png'>

## Mapping the input AC voltage with DC output of the above circuit

The microcontroller in Arduino Uno development board has a 10-bit ADC, so the maximun output from this ADC will be 1024 and this corresponds to a maximum input of 5 VDC. Since, the input signal for the development board is in range of 0 VDC to 5 VDC, the ADC output is mapped directly as follows:

* 0 VDC - ADC Value = 0
* 5 VDC - ADC Value = 1024

The maximum applied AC voltage of 270 V is mapped to a rectifier output of 5 VDC by adjusting the variable resistor (used as a voltage divider at the rectifier output). And the 5 VDC input to ADC is mapped to a value of 1024. Using this relation in reverse, we can now say that an ADC value of 1024 means an input of 5 VDC to the ADC and 5 VDC means an AC input voltage of 270 V. Hence, 1024 value maps to 270 VAC. This relation is then used to find the AC voltage value at a given value of ADC output.

* 1024 maps to 270 VAC
* 1 maps to (270/1024) VAC
* x maps to ((270/1024)*x) VAC

## Hardware components used and the implementation images

List of items for the circuit:
1. Diode 1N4007 - 2 No.
2. 230/12-0-12 V voltage transformer - 1 No.
3. Electrolytic Capacitor, 22 uF-35 V - 1 No.
4. Arduino Uno development board - 1 No.
5. Jumper cables/single-core cable
6. Breadboard - 1 No.

List of items for testing the circuit:
1. Auto Tranformer(Variac) - 1 No.
2. Oscilloscope
3. Multimeter

**Rectifier with a smoothening capacitor and a variable resistor as voltage divider**
<br/><img src='/images/voltage_setup1.png'>

**Rectifier without a smoothening capacitor, output as shown on oscilloscope**
<br/><img src='/images/voltage_setup2.png'>

## NOTE

Ideally, the above setup should be able to measure values from 0 VAC to 270 VAC, but practically this does not happen. As the AC voltage level goes down the error in the measurement increases considerably. Empricially, measurements upto 180 VAC on the lower side have less error hence we set it as the lower limit of AC voltage that can be measured accurately with this arrangement. 

The major reason for error in measurement at lower AC voltages are:

1. The non-ideal behaviour of the step-down transformer at lower voltages. That is the reduction in voltage levels at lower values is not in the same ratio as in case of higher voltages.
2. The lower resolution(10-bit) of in-built ADC in the microcontroller.