# System description

This design is asynchronous, meaning it uses diodes for the low-side switching function. It also uses P-channel MOSFETs for the switching functions. Use of P-channel MOSFETs means there is no need for a charge pump. the asychronouse design means that the software is relatively simple and there is no transition between Continuous Current Mode (CCM) and Discontinuous Current Mode (DCM) as there would be for a synchronous design. 

The spreadsheet provides analysis of the losses from the 5 main switching components - that is, the input capacitor, the reverse current prevention switch Q1, the high side switch Q2, the low side switch D3, and the inductor L1. 

Because of the asynchronous design, the low side diode D1 consumes a significant part of the total loss energy (about 3.7% of the carried power, and almost 45% of the total loss at 20 Amps). 

# Capacitor

The critical value for the input capacitor (C1) is its Equivalent Series Resistance (ESR). With a 20 Amp inductor current, the RMS current in the input capacitor is almost 10 Amps. ESR values are not normally published, especially for cheaper capacitors even if they are marketed as "low ESR". In the past I bought a range of capacitors and tested the ESR, and did an assessment of the best way to achieve a low ESR and a low temperature rise. 

Based on that assessment, this design needs at least 6, and preferably 8, 100 uF electrolytic capacitors in parallel to form C1. This will give a combined ESR of 26 milli Ohms for a power loss of 2.6 Watts and a temperature rise of 26 C (for 8 capacitors). 

# Reverse current prevention switch Q1

This will be a single MOSFET IRF4905 which has an ON resistance of 20 milli Ohms at 25C, rising to 36 milli Ohms at 175 C. For this analysis I use the 175C value. This MOSFET only has to carry the maximum power point current of the solar panel, with no AC component and no switching activity. The loss is 2.3 Watts and assuming a good heat sink and a thermal resistance of 20 C per Watt gives a temperature rise of 46C which is acceptable. 

# high side switch Q2

This MOSFET performs the most critical function in the DC-DC conversion process. The IRF4905 is not an ideal one for this function. Much better MOSFETs exist but they are all N-channel (that I have been able to find, anyway). 

To get the loss and temperature rise into an acceptable zone, it is necessary to use 2 of these in parallel. Each gets its own gate drive IC (and IR2110) so as to keep the switching loss down. 

The loss in this component (or 2 components) has 3 contributors, which are a function of current level, panel voltage and switching transition time. The process to analyse these losses is quite complex and I will not try to explain it here. The equations are in the spreadsheet. These losses are:
DC current loss: 2.9 Watts
Switching loss:  1.3 Watts
Gate drive loss: 0.15 Watts
Total            4.4 Watts
Distributed across 2 MOSFETs with good heat sinks this leads to a temperature rise of 43C which is acceptable. That is at a switching frequency of 70 kHz. More on that later. 

# Low side switch D3

As mentioned above, the loss in this diode is the biggest problem. I am using 4 high power TO220 Schottky diodes in parallel to achieve a loss of 9 Watts and a temperature rise of 45C, also assuming good heat sinking. 

# Inductor L1

This is another critical component. The analysis of losses in inductors is another very complext process. The main components are DC loss and core loss. The core loss is the result of hysteresis in the magnetisation cycle of the core material. The equations in the spreadsheet follow those given in the data sheets from one of the toroid core manufacturers. 

This inductor will use a T130-26 toroid core (which means a toroid with an outside diameter of 1.3 inches and made from "type 26" powdered iron particles. There are 31 turns of 6 strands of 1mm diameter wire. This is the maximum amount of wire that will fit through the inside hole of the toroid.

Winding this toroid requires some care. First the wire is prepared, as 6 strands of 1mm wire each 1.55 m long. The strands need to be as straight as possible without any kinks. The winding has to be made one turn at a time for each strand in sequence. 

Turn 1 strand 1. Turn 1 strand 2. Turn 1 strand 3. ... Turn 1 strand 6. 
Turn 2 strand 1. Turn 2 strand 2. 
and so on until you reach Turn 31 strand 6.  

Each turn needs to be made close to the previous turn and also pressed in close to the inner surface of the toroid, otherwise the total number of turns may not fit. 

The calculations show that at 20 Amps the losses in the inductor will be:
DC loss:   2.2 Watts
Core loss: 0.8 Watts
Total:     3   Watts
Temperature rise: 35 C. 

# Summary of losses

Totalling these values, we have:

Capacitor    C1 2.6 Watts 26C

Reverse flow Q1 2.3 Watts 46C

High switch  Q2 4.4 Watts 44C           

Low diodes   D3 9   Watts 45C

Inductor     L1 3   Watts 35C

Total           21  Watts