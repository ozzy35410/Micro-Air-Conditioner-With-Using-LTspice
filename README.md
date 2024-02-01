# Micro-Air-Conditioner-With-Using-LTspice
Theoretical design process of integrated analog micro-air conditioner.
# Project Report
__*Abstract* - This article aims to explain the theoretical design process of integrated analog micro-air conditioner. This article will include the design process of the project, circuit designs, theoretical results.__
*Index Terms* – Air conditioner, Analog design, Autonomous system
# I. INTRODUCTION
An air conditioner is a device designed to control and regulate the temperature, humidity and ventilation of a space. In this project, a micro-air conditioner was designed using analog electronic components. The air conditioning system has four main units: control unit, operation unit, sensing unit and display unit. The sensing unit consists of an analog temperature sensor. The sensor measures the temperature and gives a certain voltage value in response to a certain temperature value. The control unit has two subunits. In the set subunit, user can adjust the desired temperature. The difference between the ambient temperature and the desired temperature is determined by difference subunit. In the operation unit, heating or cooling is carried out according to the information received from the difference subunit, and which process is being carried out is indicated using LEDs. The display unit contains an RGB LED to display the ambient temperature and desired temperature. This RGB LED continuously transitions the visible color spectrum from blue to red while displaying temperature readings between 24°C and 40°C.
# II. ELECTRONIC COMPONENTS
The electronic components used in the project are listed below:

LM35 (temperature sensor)
LM741 (operational amplifier)
10 Ω, 5W stone resistor
12 V, 0.12 A DC Fan
IRFZ46N (power mosfet)
Red, Blue and RGB (anode) LEDs
1N4007 diode
Resistors and jumpers
Mechanical switch
12 and 6 V power supplies,
# III. SENSING UNIT
In this project, LM35 element was used as the temperature sensor. LM35 has 10-mV/°C scale factor and has -55°C to 150°C temperature range [1]. The micro-air air conditioner built in the project operates between 24°C and 40°C.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/df4fab10-3e4e-4942-929d-5dc0d9b83766)
> Fig. 1. Sensing unit diagram

The sensing unit can be seen in figure 1. Since the output value obtained from LM35 will be between 240-400 mV, some discrepancies may occur. Therefore, to reduce these discrepancies, the output voltage value obtained from the LM35 was amplified using a non-inverting amplifier with 4 V/V gain. The voltage gain of the non-inverting amplifier is given by (1).
Vsen = Vin * (100k+33k)/33k (1)
![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/0cf06976-d31f-4297-969b-0944fcbeabd6)
> Fig. 2. Sensing unit output

As a result of this circuit, we set the sensing output value between 0.96V-1.6V. This result can be seen in figure 2. Experimentally, values consistent with these results have been obtained. Instead of 0.96 V, 0.94 V could be obtained as the minimum value. Therefore, instead of being cooled to 25 degrees, the circuit could be cooled to 24.3 degrees. The reason for the 0.2 V difference will be explained in the operating unit.
# IV. CONTROL UNIT
# V. OPERATION UNIT: HEATING AND COOLING
# VI. DISPLAY UNIT
# VII. CONCLUSION
# REFERENCES
