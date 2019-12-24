# ecg_pcb_design
Fall 2019 ENGR-UH 3611 Electronics Course Project
ECG PCB Documentation
Ken Iiyoshi
Fall 2019 
ENGR-UH 3611 Electronics
Overview + All Schematics Instantiation
Opamp, IA, resistors, capacitors, and battery retainers were created within the ecg_PcbLib Library folder. Audio jack and 2 header pins, and 3 header pins were imported from existing libraries on Digi-Key, EasyEDA, or PCB3D.


Opamp Schematic & PCB
According to the datasheet snippet shown below, TLV521DCKT is based on SOT23 Package (Small-outline transistor) with 5-Leads. The resulting PCB footprint is shown in both 2D and 3D.



Instrumentation Amplifier Schematic & PCB
The data sheet for  instrumentation amplifier, or AD620ARZ-REEL7, outlines the type of connections and footprints one can use. Note from the highlighted area that the IA is a SOIC (Small Outline Integrated Package).The following screenshot shows the resulting schematic for IA. Based on the datasheet, just as with op amp, the design data below was used for wizard’s dimensions specifications.The following screenshot shows the footprint for the IA.



Resistor Schematic & PCB


Capacitor Schematic & PCB


Battery Retainer Schematic & PCB



Audio Jack Schematic & PCB


2 Header Pins Schematic & PCB
Header pins are used to probe output to oscilloscope as well as to any other external device”.
By having header pins between the IA and filter, the IA signals can be tested without the filter. We’ll put a jumper on the header pins to connect the IA output to filter input.
See the screenshot below for the header pin layout.  



ECG Schematic Diagram

GND ports are connected to each other by default when the pcb is fabricated.  
Filter resistor/capacitor values: They are supposed to achieve gain=10 and 1~100Hz bandwidth. With IA gain = 1 + 50,000/54 = 927, the ecg’s total gain would be approx 10k.
R’’ selected as 162k= 62k+100k. Hence, R’ = 16.2k = 15k+1.2k
C’ = 1/(2*pi*16.2k)  = 10 uF. Gain = 10 so 1000C’’=C’. Thus, C’’= 10nF.
These resistors/capacitors are on Faraz’s sheet.
Multiple capacitors(10u,100n,1nF - to cover different frequency bands). Empty spaces can be used for routing. Power line should as thick as possible.
Bias voltage is most likely 0.2~0.3 V so the output voltage would range probs ± 2.7.
Note that in lab we used ±15V VDD/VSS. Our output was less than this so output signals weren’t clipped. But, the battery only provides ±3V. So here’s my suggestion for updating Rg:
INA121 Gain = 1 + 50k/Rg
Rg for lab:27 Ohms x 2. Thus, gain = 1 + 50k/54 = 940
Now, with filter gain = 10, the total gain for the ECG become 1k. I.e few mV ECG body signal amplifies to few Volts output
You can use net names to help make the schematic look nice, just don't try to validate your design until you have multiple net labels for each net
Place → net 
Once your schematic is ready make sure to annotate your schematic
Tools -->annotate 


PCB design: 
PCB Layout: It’s sensible to mirror the schematic design for the pcb layout, as seen in the screenshots below. Red is the top layer, blue is the bottom layer.



Recommended default route width is 10mil (0.254mm). For ground, 50mil (1.27mm) The main focus is to minimize noise on the ECG signal route (i.e. make the connections wide and short). 
I used 50% neck-down option in the design rules so that I can fit the 0.2543mm line into the opamp pins. The minimum line width is 0.001mil (0.000254mm) btw according to our manufacturer (https://www.sunstone.com/pcb-manufacturing-capabilities/detailed-capabilities).
Recommended pouring net: VDD for top layer, VSS for bottom layer.
Need Vias for VSS
Add Keepout layer to make boundary for pcb company.
One tool for checking missing connections is Tools->Design Rule Check… When you run it, it shows you message for any design warnings. (ignore Minimum Solder Mask Silver, as this detects opamp pins.)

Steps for PCB design
Create route
Redefine board shape
Explicitly make a board outline somehow
Generate output
File -> smart PDF ->
Deselect bill of materials
Prof said we don't need it at least for now
Edit the PCB board outline thing so that there are two specific layers, top and bottom and that they both include the board outline
