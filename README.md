# -Analog-Circuits-555-Waveform-Generator-and-Converter-Project
This project designs a square wave and sine wave generation circuit based on the NE555 (timer) and TL072 (general-purpose dual operational amplifier).

<div align="center">

# 🛠️ Tools & Ecosystem

Here is a list of the EDA software, open-source hardware platforms, and manufacturing services used in this project:

| Platform / Tool | Logo / Preview | Description |
| :--- | :---: | :--- |
| **[EasyEDA](https://easyeda.com/)** | <img src="https://easyeda.com/favicon.ico" width="28"> | Used for schematic capture and PCB layout design. |
| **[OSHWLab](https://oshwlab.com/oshwlab/project_ugkqsemj)** | <img src="https://oshwlab.com/favicon.ico" width="28"> | Dedicated open-source hardware platform (Allows community members to instantly open complete schematics and PCBs in EasyEDA Pro for reproduction and updates). |
| **[LCSC Electronics](https://lcsc.com/)** | <img src="https://lcsc.com/favicon.ico" width="28"> | Provides one-click BOM component online ordering. |
| **[JLCPCB](https://jlcpcb.com/)** | <img width="40" height="40" alt="logo - blue" src="https://github.com/user-attachments/assets/904368db-c0b7-4102-8ae2-d9642f2ab255" />| PCB manufacturing and fabrication (Standard 2-layer process, 80 mm × 60 mm dimensions). |

</div>


<h1>1. Project Features</h1>
High Integration: Combining digital and analog circuits, it is a typical mixed-signal system.
Practicality: Covers the complete electronic fabrication process, from circuit simulation to schematic design, PCB layout, soldering, and debugging.
Low Cost: The core ICs (NE555 and TL072) are widely available and inexpensive, while peripheral components are standard resistors and capacitors, resulting in low project costs and suitability for large-scale teaching.
 

<h1>2. Circuit Principle</h1>

According to the design requirements, a 2 kHz square wave must first be generated using a 555 timer circuit. The sine wave can then be produced by passing the generated square wave through a second-order band-pass filter. The circuit system block diagram is shown below:

<div align="center">
<img width="746" height="99" alt="822d66b7d00b46c78064cadd01edfe7a" src="https://github.com/user-attachments/assets/ac46ed35-42d0-41c1-87c5-4349eb54d5c3" />
</div>
 

<h2>2.1 Square Wave Generation Circuit</h2>

A square wave circuit with adjustable frequency and duty cycle is designed using a 555 timer. The 555 timer derives its name from the three 5 kΩ internal resistors used to establish reference voltages. Due to its low cost and simple peripheral circuitry, the 555 family of ICs is widely used in timers, pulse generators, and oscillator circuits. Thanks to these features, the 555 timer is extremely versatile and frequently found in various small electronics projects.

 
| Pin | Name | Function |
| :--- | :--- | :--- |
| 1 | GND | Ground |
| 2 | TRIG | Trigger: When the voltage drops below 1/3Vcc, the output goes HIGH and the internal discharge transistor turns OFF. |
| 3 | OUT | Output: Outputs high or low logic levels. |
| 4 | RST | Reset: Driven HIGH for normal operation; driven LOW to force Pin 3 (OUT) LOW. |
| 5 | CTRL | Control Voltage: Connected to ground via a 0.01 µF capacitor by default to eliminate interference; can be connected to an external voltage to adjust threshold levels. |
| 6 | THR | Threshold: When the voltage rises above 2/3Vcc, the output goes LOW and the internal discharge transistor turns ON. |
| 7 | DIS | Discharge: Discharges the capacitor through an internal open-collector (OC) transistor. |
| 8 | VCC | Supply Voltage |
 

A 555 timer can be used to construct a monostable circuit. To operate it as an astable multivibrator that triggers continuously in each cycle, Pins 2 and 6 must be connected together. If you want to make both the duty cycle and frequency adjustable, two variable resistors and two diodes can be connected to the circuit, as shown in the figure below:

<div align="center">
<img width="684" height="328" alt="67f648bfdab241bf9cab23cf96479c0b" src="https://github.com/user-attachments/assets/d4e6a98d-3bb6-487f-8bed-46726cef454b" />
</div>


When the power is turned on, capacitor C1 is charged through RP1 and D1. When the capacitor voltage reaches 2/3Vcc​, it begins to discharge through D2, RP2, and RP1 into the internal discharge transistor at Pin 7. When it discharges down to 1/3Vcc​, this charge-discharge cycle repeats continuously.

 

According to the formulas, both the frequency and duty cycle are jointly determined by the values of RP1 and RP2. Adjusting either RP1 or RP2 will change both frequency and duty cycle. The tuning method is to first adjust RP2 to set the target frequency, and then fine-tune RP1. Iterative adjustments between RP1 and RP2 are required to simultaneously achieve the desired frequency and duty cycle.

 

<h2>2.2 Sine Wave Generation Circuit**</h2>

According to the Fourier transform of a square wave, a square wave is composed of multiple sine waves with different amplitudes and frequencies. The function of a band-pass filter is to retain the desired waveform while filtering out redundant frequencies. Based on the design requirements, the corresponding circuit can be designed using the parameters of the second-order band-pass filter: center frequency, gain, and set bandwidth.

<div align="center">
<img width="1020" height="442" alt="837a05f2c17e45d7a5b53612944fd368" src="https://github.com/user-attachments/assets/2d2853eb-6c3b-414d-a767-eaa2c5e41b8c" />
</div>

RP1 is the resistor that determines the center frequency. Due to calculated parameter deviations and component tolerances, RP1 is replaced with a 100 Ω variable resistor. Since a single power supply is used, R3 and R4 are employed to pull up (bias) the voltage.

 

<h1>3 PCB Design</h1>
 

<h2>3.1 Schematic Design</h2>

When designing the schematic, refer to the following component list. You can find and place the specified components by searching for their component numbers in the JLCPCB EDA online component library. Note that M3 standoffs can be found in the mounting components of the common library.

 
<div align="center">
Component List (BOM)
</div>

| Item | Name | Value / Parameter | Package | Part No. |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Electrolytic Capacitor | 10uF | CAP-TH_BD5.0-P2.00-D0.8-FD | C43347 |
| 2 | Ceramic Capacitor | 104 | CAP-TH_L8.5-W5.0-P5.00-D1.2 | C914519 |
| 3 | Ceramic Capacitor | 103 | CAP-TH_L8.5-W5.0-P5.00-D1.2 | C94713 |
| 4 | Ceramic Capacitor | 473 | CAP-TH_L8.5-W5.0-P5.00-D1.2 | C94710 |
| 5 | Diode | 4148 | DO-35_BD2.0-L4.2-P8.20-D0.5-RD | C406389 |
| 6 | Pin Header | HDR-M-2.54_1x2 | HDR-M-2.54_1X2 | C124375 |
| 7 | LED | LED-TH-3mm_R | LED-TH_BD3.0_RED | C84774 |
| 8 | Terminal Block | CONN-TH_2P-P5.00 | CONN-TH_2P-P5.00 | Common Library |
| 9 | Through-Hole Resistor | 1K | RES-TH_BD2.5-L6.5-P10.50-D0.6 | C57435 |
| 10 | Through-Hole Resistor | 47K | RES-TH_BD2.5-L6.5-P10.50-D0.6 | C58605 |
| 11 | Through-Hole Resistor | 20K | RES-TH_BD2.4-L6.3-P10.30-D0.6 | C410662 |
| 12 | Through-Hole Resistor | 8.2kΩ | RES-TH_BD2.3-L6.5-P10.50-D0.5 | C714014 |
| 13 | Through-Hole Resistor | 100kΩ | RES-TH_BD2.3-L6.5-P10.50-D0.5 | C714036 |
| 14 | Through-Hole Resistor | 16K | RES-TH_BD2.4-L6.3-P10.30-D0.6 | C1371066 |
| 15 | Potentiometer | 10K | RES-ADJ-TH_3P-L10.0-W10.0-P2.50-L | C118954 |
| 16 | Integrated Circuit (IC) | TL072 | PDIP-8_L10.2-W5.9-P2.54-LS7.6-BL | C110329 |
| 17 | Integrated Circuit (IC) | NE555 | DIP-8_L9.8-W6.6-P2.54-LS7.6-BL | C398063 |
| 18 | Copper Standoff | M3 Screw | M3 Screw | Common Library |


The canvas drawing is set to A4 size by default, but you can change it to A5 size in the Canvas Properties on the right panel. After searching for components, connect and place them according to the reference schematic. Some components retrieved from the search may look slightly different from those in the reference diagram; as long as the connected nets for each pin are identical, it is fine. Alternatively, you can click on a component, right-click, and select "Modify Symbol" to align the visual style of the component with the reference diagram (schematics can have multiple visual styles, and pin ordering may vary).

<div align="center">
<img width="1064" height="603" alt="cc275493fae44cbabccac4b3c3c24fe8" src="https://github.com/user-attachments/assets/dd2b5019-de31-4f8d-b4f0-809ceb508f8e" />
</div>
 

<h2>3.2 PCB Design</h2>

After completing the schematic design, first make sure to check whether the circuit is properly connected and if there are any missing or unconnected nets. Once everything is verified to be error-free, click Design -> Update/Convert Schematic to PCB in the top menu bar of the schematic editor to proceed with PCB design.

 

<h3>(1) Board Outline Design</h3>

After generating the PCB, you need to define the board outline. The dimensions can be set based on the number of components and layout requirements. Since JLCPCB provides free PCB prototyping within a 10 cm × 10 cm size limit, this project adopts a rectangle of 80 mm in length, 60 mm in width, and a corner radius of 2 mm as the PCB size based on practical needs.

 

<h3>(2) Component Layout</h3>

When components are transferred from the schematic to the PCB, their initial layout can be quite messy. The second step of PCB design is to categorize and arrange these components. The placement strategy is to cluster components belonging to the same circuit module together. You can quickly lay out each circuit module using the Layout Transfer feature provided by JLCPCB EDA. Note that interface connectors should be placed along the board edges to facilitate wiring operations.

 

<h3>(3) PCB Routing</h3>

When designing a single-layer board, the top layer traces are red by default. Routing refers to connecting copper traces on the circuit board. Simply select the appropriate layer under Layers & Elements and connect pads belonging to the same net. Although it looks like a simple matching game, it requires patient adjustments, as component placement directly affects routing difficulty. Here are a few reference suggestions for routing this project:

Set power traces to 30 mil width and signal traces to 20 mil width.
Primary routing should be done on the bottom layer; use vias to switch to the top layer only when routing gets blocked.
GND does not require manual routing—simply apply copper pour on the bottom layer.
Prioritize straight lines during routing. When turns are necessary, use obtuse angles or arcs instead of sharp turns.
After completing the routing, add appropriate silkscreen labels to indicate the purpose of the PCB and the functions of the interfaces.
Remaining blank areas can be used to add explanatory text or images.

 <div align="center">
<img width="1498" height="572" alt="c041b61293c74290b98f730f129a60b4" src="https://github.com/user-attachments/assets/931254c5-9b8b-462d-9691-a85504d14987" />
</div>

 
<h1>4 Soldering and Commissioning**</h1>
 

<h2>4.1 Soldering Precautions</h2>
 

During soldering, refer to the Bill of Materials (BOM) to match the component locations on the PCB. You can download the interactive HTML soldering assistance tool to view component placements on your computer or mobile device.

 <div align="center">
<img width="1092" height="763" alt="f6837f58954b4c949b1ea14db7a1c9c7" src="https://github.com/user-attachments/assets/2869d1ef-2ec1-4f32-b99a-e70c1127657a" />
</div>
<div align="center">
Soldering Assistance Tool
</div>

<div align="center">
<img width="1917" height="908" alt="73f61ad8dc4c41f297ab559d4522c17e" src="https://github.com/user-attachments/assets/43df6cdb-3adb-4cd4-961f-0380ece7452f" />
</div>
<div align="center">
Soldering Assistance Tool Interface
</div>

The soldering order follows the principle of "from low to high, and from signal source to load." The soldering sequence and reference designators are shown in the table below; the actual designators are subject to your own PCB design.

 

<h2>4.2 Commissioning Methods</h2>

The instruments used during testing include a multimeter, an oscilloscope, and a laboratory power supply.

Step 1: Solder Joint Inspection
After soldering, carefully check whether the solder joints on the board are smooth and rounded, and ensure there are no cold solder joints or short circuits.

Step 2: Power Supply Inspection
Without inserting the ICs, use the multimeter's continuity mode to check for any short circuit between VCC and GND on the board. If no short circuit is detected, power on the circuit using the laboratory power supply set to 12V, and measure with the multimeter's DC voltage mode to verify if the supply voltage is indeed 12V.

Step 3: Functional Testing
During functional testing, first use the oscilloscope to test the square wave output. Adjust RP2 and RP1 to generate a stable 2 kHz square wave with a duty cycle of approximately 50%. Then, adjust the parameter of RP3 to convert the output triangle wave into a sine wave. Note that RP3 requires patient adjustment to obtain a stable sine wave. Finally, record the waveform frequency and amplitude.
