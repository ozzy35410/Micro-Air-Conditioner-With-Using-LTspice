# Micro-Air-Conditioner-With-Using-LTspice
Theoretical and practical design process of integrated analog micro-air conditioner.

Mustafa Alp Ekici, and Oğuzhan Oğuz

Middle East Technical University

(ekici.mustafa & oguzhan.oguz) @metu.edu.tr

# Project Report
__*Abstract* - This article aims to explain the theoretical and practical design process of integrated analog micro-air conditioner design. This article will include the design process of the project, circuit designs, theoretical results, and a comparison of experimental and practical results..__

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

12 and 6 V power supplies

# III. SENSING UNIT
In this project, LM35 element was used as the temperature sensor. LM35 has 10-mV/°C scale factor and has -55°C to 150°C temperature range [1]. The micro-air air conditioner built in the project operates between 24°C and 40°C.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/df4fab10-3e4e-4942-929d-5dc0d9b83766)
> Fig. 1. Sensing unit diagram

The sensing unit can be seen in figure 1. Since the output value obtained from LM35 will be between 240-400 mV, some discrepancies may occur. Therefore, to reduce these discrepancies, the output voltage value obtained from the LM35 was amplified using a non-inverting amplifier with 4 V/V gain. The voltage gain of the non-inverting amplifier is given by (1).
*Vsen = Vin * (100k+33k)/33k* (1)
![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/0cf06976-d31f-4297-969b-0944fcbeabd6)
> Fig. 2. Sensing unit output

As a result of this circuit, we set the sensing output value between 0.96V-1.6V. This result can be seen in figure 2. Experimentally, values consistent with these results have been obtained. Instead of 0.96 V, 0.94 V could be obtained as the minimum value. Therefore, instead of being cooled to 25 degrees, the circuit could be cooled to 24.3 degrees. The reason for the 0.2 V difference will be explained in the operating unit.
# IV. CONTROL UNIT
In this unit, the user can adjust the temperature of the environment between 24 and 40 degrees. The voltage values corresponding to these values must be in the same range as the sensing unit values. A 10k ohm potentiometer was used to change the desired temperature value. When the potentiometer is at the minimum value (0 ohms), a result of 0.96 volts should be obtained, and when it is at the maximum value (theoretically 10k ohms, experimentally 9.87k ohms), a result of 1.6 volts should be obtained. To meet the necessary conditions, the circuit in figure 3 was created.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/b286bc60-1d6f-415f-a9ba-697d96fd29dd)
> Fig. 3. Set subunit diagram

Voltage division method was used in this circuit. By using the resistor values in the circuit in Figure 3, a linear output value between 0.958V-1.64V was obtained. The output obtained as a result of the voltage division in figure 3 will be used as input in another op-amp circuit. A voltage buffer amplifier was used to prevent the new op-amp from seeing the effects of the resistor values used in figure 3.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/a87099bb-448f-4322-ac75-3608445df098)
> Fig. 4. Set subunit output

In LTspice, the .step param command can be used to sweep the resistor value. With this command, the potentiometer value can be simulated from 1 Ω to 9870 Ω. Set subunit output can be seen in the graph in figure 4. Experimentally, values consistent with these results have been obtained. No different results were observed.
While the set subunit represents the desired temperature, the sensing unit represents the ambient temperature. The outputs of both are in the same voltage range. Therefore, the difference between them can be calculated directly using the difference amplifier. One of the desired features in the project is that the air conditioner remains steady when there is less than 1°C difference between Vset and Vsen. To ensure this condition, 1N4007 diodes are used in the circuit. 1N4007 diodes have an opening voltage of 0.7 V [2]. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/1a6ad9f0-acb2-4af9-af66-95f7bd87dd18)
> Fig. 5. Difference subunit diagram

Difference amplifier (figure 5) was used to calculate the difference between Vset and Vsen. When the difference between these two values is less than 40 mV (1°C), the circuit should remain steady. In order to achieve this situation, the result of the difference amplifier must be less than the diode opening voltage. That is, the 40 mV value should be amplified to 700 mV from the difference amplifier. The gain of the difference amplifier is given by (2). 
_Vout = Vset *  R4/(R2+R4) – Vsen*  R3/R1_ (2)
Vset and Vsen coefficients should be equal to each other and gain should be 17.5 V/V. Resistors suitable for these conditions have been selected. Since there is no resistor directly corresponding to some of these resistors, the required resistance values were obtained by connecting them in series. Since the output value obtained in the difference amplifier will be used as the input value in different op-amps, a voltage buffer has been used for the same reason as in the set subunit. If the result obtained as a result of the difference amplifier is negative, it means the desired temperature is less than the ambient temperature. This negative current must be connected to the cooler subunit with a reverse diode. In this way, the cooler subunit will operate when the environment needs to be cooled. If the result is positive, it means the desired temperature is higher than the ambient temperature. It should be connected to the heater subunit with positive current. In this way, the heater subunit will operate when the environment needs to be heated. Thanks to the diode opening voltage, the circuit will remain steady when there is a difference of less than 1°C. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/dfce0699-4ff1-4e18-a7bc-91911a9e8d65)
> Fig. 6. Output of the difference amplifier when Vset = 1.64V [41 °C] and Vsen = 0.96V [24 °C]

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/497f714c-1783-4004-a0be-117895a246bf)
> Fig. 7. Output of the difference amplifier when Vset = 1.64V [41 °C] and Vsen = 1.6V [40 °C]

In Figure 6, it can be seen when it starts to rise from ambient temperature to the highest temperature. Heater operation will start due to 11.22V output voltage of the difference amplifier. Figure 7 shows the maximum value that the ambient temperature can reach. Since the output of the difference amplifier will drop to 700 mV, the circuit will remain in a steady state due to the opening voltage of the diode. 
Experimentally, slightly different results were obtained from the theoretical results. Due to the difference between the opening voltages of the blue and red LEDs, the cooling process starts when there is a difference of 0.6 °C. On the other hand, the heating process starts when there is a difference of 0.8 °C. The steady state that should occur when there is a difference of less than 1 °C can be approximately achieved.

# V. OPERATION UNIT: HEATING AND COOLING
At this point, a significant difference was noted between the theoretical design and experimental results. Although realistic op-amps were used in the LTspice program, these op-amps did not produce exactly the result observed in reality. The stone resistors used in the heater subunit have a resistance of approximately 10 Ω. When a 12 V power supply is used, stone resistors consume approximately 5W of energy. Although not that much, the 12 V DC fan used in the cooler sub-unit also consumes more than 1 watt of energy. Approximately 0.23 ampere current flows through the DC fan. Therefore, it consumes approximately 2.76 watts of energy. A LM741 has 500 mW maximum power dissipation [3]. Therefore, the required current for the heater and cooler subunits cannot be provided by using only LM741. In order to provide higher current levels, the use of power mosfet is needed. IRFZ46N power mosfet was used in the operation unit. The IRFZ46N power mosfet, unlike the LM741, has a maximum power dissipation of 107 W [4]. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/7e77aa2f-75ef-4dcf-9aac-07443232ccee)
> Fig. 8. Cooler subunit

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/030cdc78-ad7a-473b-9491-138a60b58f15)
> Fig. 9. Heater subunit

The constructed circuits can be seen in figure 8 and figure 9. A gain value was chosen (180 V/V) that would be absolutely sufficient for even the smallest voltage value difference (>40 mV). Since a positive voltage value will be connected to the power mosfet as input, another inverting amplifier was used to make the current value going to the heater positive. The output voltage value obtained from the amplifiers were connected to the gate end of the power mosfet. The source end of the power mosfet was grounded, and the drain end was connected to the heater and cooler. A 12 V supply was connected to the other end of the heater and cooler subunits. In this way, when a positive voltage is input to the gate of the power mosfet, it will function as a switch [5] and the drain end connected to the heater or cooler will be grounded. In this way, 12 V will drop to the heater and cooler subunits. To indicate which operation is being performed, a red LED was added parallel to the heater subunit and a blue LED was added parallel to the cooler subunit. To prevent too much voltage drop on the LEDs, 1k Ω resistors were added in series to the LEDs. During the experiment, it was observed that the heater subunit consumed approximately 8.5 W and the cooler subunit consumed approximately 2.75 W. If calculated theoretically, IRFZ46N has 1.3 V forward voltage, therefore approximately 10.7 V drops on the heater subunit. The power consumption is given by (3)  
_P = (V*V)/R_(3)
Therefore, power consumed by heater approximately equal to 11.5 W. Considering that in a real circuit, the heater subunit will drop less than 10.7 V, a consistent result can be considered to be obtained. Similarly, if the cooler unit is calculated theoretically, a result of approximately 2.29 W is obtained for a dc fan with 50 Ω internal resistance.
Additionally, heater and cooler operations worked sequentially, not simultaneously, as desired. A range where neither was working was successfully achieved. Reached from ambient temperature (24 °C) to maximum set temperature (40 °C) in less than 3 minutes. The air conditioner worked autonomously for the set value. Moreover, temperature is sustained in the set value with ±0.8°C. 

# VI. DISPLAY UNIT
In this part of the circuit, ambient and set temperature values were displayed using RGB LEDs. For temperature values of  24°C and lower, the blue LED should be at its brightest, and this brightness should continue to decrease up to 32°C . For temperature values of 32°C and higher, the blue LED should not light. A similar situation applies to the red LED. The red LED should not light up for temperatures lower than 32°C, and should turn on at full brightness for temperatures higher than 40°C. In the range of 32-40 °C, its brightness should increase. Green red should burn at full brightness at 32°C, and its brightness should decrease towards temperatures of 24 and 40°C. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/d81e41cc-a631-43b1-9047-bda04854a9aa)
> Fig. 10. RGB LEDs

Common anode RGB LED was used in the display unit which can seen in figure 10.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/af910489-eba1-49e5-9056-2a98a77ff035)
> Fig. 11. Blue and red RGB diagram

Blue and red RGB diagram can be seen in figure 11.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/4175bfd4-1c69-486e-851d-e991ce085c19)
> Fig. 12. Vsen2 node voltage graph

The operating value range of RGB LEDs is 0.96-1.6V (24°C-40°C). Therefore, the blue RGB LED range is 0.96-1.28V and the red RGB LED range is 1.28-1.6V. In order to design an LED that works this way, let's set the range between 0.96 V and 1.6 V to the range between -4V and 4V. Firstly, Vsen2 graph can be seen in figure 12.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/b52198d9-710a-47eb-b522-a38b114f5efc)
> Fig. 13. Vx node voltage graph

The result in figure 13 is obtained with the op-amp circuit containing an 8V supply. In this way, a negative current is obtained for values less than 1.28 V. This current will go to blue RGB. Since anode RGB is used, no additional processing is required. Additionally, this negative current increases towards 0.96 volts. In this way, the brightest blue light is obtained at 24°C. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/be0d35b0-2262-43c9-8f37-f931ddfb7d7b)
> Fig. 14. Current values of the red and blue RGBs

For values greater than 1.28 V, a positive current is obtained. This current is amplified with an inverting amplifier with 1 V/V gain and sent to the red RGB LED. It passes through the reverse connected LED, causing the RGB LED to emit light. In this way, the result in figure 14 is obtained.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/77972b45-40f2-4b04-a9c6-12cb76d10c6f)
> Fig. 15. Vbot and Vtop diagrams

Green RGB LED should get the maximum value at 32 °C. It must be zero for values less than 24 °C and greater than 40 °C. In this range, it should decrease linearly. To obtain such a result, the circuits in figure 15 can be used. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/e3279ac4-665b-4f40-8932-4d86cd786189)
> Fig. 16. Vbot graph

By using the saturation values of the op-amp, the graph in figure 16 can be obtained with the -4 to 4 V Vx input. 
 
![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/3f5f3590-277e-44a8-b588-f9bf0b2f052d)
> Fig. 17. Vtop graph

With similar logic, the graph in figure 17 can be obtained by using the inverting input pin of the input op-amp. The only difference in these two op-amps is the input pin of the input. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/7929b549-ec99-49ba-873f-fe30854cc9bc)
> Fig. 18. Inverting and difference amplifiers for getting proper current value

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/b6e919f7-bbac-4a6d-85d2-8388895c08e1)
> Fig. 19. Vout1 graph

The graph in figure 19 can be obtained by adding the two graphs in figure 16 and figure 17 with the help of difference and inverting amplifiers which in figure 18. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/cafc94c1-a19c-4737-b872-09a345e98808)
> Fig. 20. Vout2 graph

The graph in Figure 20 can be obtained by inverting the graph in Figure 19 and subtracting -6 volts.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/08b1e51c-3bbe-4bcf-a6fb-5152ba851be3)
> Fig. 21. Current values of green RGB

The graph in Figure 19 shows the voltage value at the node at the end of the green RGB LED. Since the green RGB LED lead is a reverse-connected diode, the current graph in figure 21 is obtained. As can be seen from the graph, green light reaches its brightest value around 1.28 V and decreases linearly towards 0.96 V and 1.6 V.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/e022d577-9465-43f0-8cc3-7b00a921a403)
> Fig. 22. Final current values for all colors

As a result, the result is obtained as in figure 22. If the current passing through the RGB LEDs is high, the resistor value connected to the LEDs in series can be increased. 
Experimentally, the biggest difference is caused by the opening voltages of the LEDs. Red RGB LED has an opening voltage of approximately 2V, while blue and green RGB LEDs have an opening voltage of approximately 3.2V. (These values were obtained experimentally.) In the display circuit created by combining the circuits in Figure 11, Figure 15 and Figure 18, small differences occurring anywhere in the circuit can cause major changes. 

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/c188abdb-2335-4995-908e-61b95bf51047)
> Fig. 23. Final current values for changed V1 value

For example, if the V1 value in figure 11 was 6V instead of 8V, a result like figure 23 would be obtained.

![image](https://github.com/ozzy35410/Micro-Air-Conditioner-With-Using-LTspice/assets/46710637/cbb4c068-7235-4e60-b8e5-cd7f7917203d)
> Fig. 24. Final current values for changed V1 value

If the V1 value in figure 11 was 10V instead of 8V, a result like figure 24 would be obtained. 
Due to differences that could not be fully determined experimentally, the maximum green brightness could not be achieved at exactly 32 °C. But a consistent result was obtained. The green value dropped to zero earlier than 24 °C. Therefore, the cyan color, which is a mixture of green and blue colors, could not be observed. But all other colors were observed with decreasing and increasing brightness (blue, green, yellow, red). Using a mechanical switch, the circuit was enabled to display the ambient or set temperature. 

# VII. CONCLUSION
In this project, an integrated analog micro-air conditioner was successfully designed, implemented, and analyzed. The design was divided into units, and the units were divided into subunits. First, the theoretical design and analysis of each unit was made. Later, experimental procedures were tried to be carried out in accordance with these results. An air conditioner consists of control unit, operation unit, set unit and display unit. Thanks to the control unit, the desired temperature adjustment was achieved, the difference between the desired temperature and the ambient temperature was found and the action to be taken was determined. According to the result from the control unit, the necessary cooling or heating process was performed in the operation unit. In addition, it was learned that an ordinary op-amp cannot provide high power, and for this, an element such as a power mosfet must be used. The necessary conditions for the air conditioner to remain stable were also met, thus the air conditioner managed to keep the ambient temperature at a set value. While the operation process was indicated with blue and red LEDs, the ambient temperature and set temperature were indicated with the help of RGB LEDs and mechanical switches. As a result, the integrated micro air-conditioner demonstrated successful autonomous temperature control, reaching the set values within a narrow margin of error. 
# REFERENCES
[1] Texas Instruments, “LM35 Precision Centigrade Temperature Sensors”, SNIS159H datasheet, August 1999 [Revised December 2017].
[2] Texas Instruments, “Types 1N4001 Thru Silicon Rectifiers”, DL-S 7211698 datasheet, November 1972.
[3] Texas Instruments, “LM741 Operational Amplifier”, SNOSC25D datasheet, May 1998 [Revised October 2015].
[4] International Rectifier, “ IRFZ46N HEXFET Power MOSFET”, PD-91277 datasheet, 
[5] Brown, J. (2004). Power MOSFET basics: Understanding gate charge and using it to assess switching performance. Vishay Siliconix, AN608, 153, 1-6.
