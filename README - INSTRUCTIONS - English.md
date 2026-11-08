**----------------------------------------------------------------------------------------------------------------------------------------**

				**SPREADSHEET USER MANUAL**

**----------------------------------------------------------------------------------------------------------------------------------------**



**Code Version: v0.1 (BETA)**



**------------------------------------------------------- NOTES --------------------------------------------------------------------**



Whenever **PINS** are mentioned, I am referring to the actual cells on the spreadsheet. All electrical connections are handled via code and established when the component-specific update functions are called.



Further below, I outline a basic example. The actual code for this setup and its connection guidelines are detailed in the **"README - CODE"** file. Please read it for comprehensive programming instructions.



The arrival of new components is planned for version **v0.2**: **POTENTIOMETER, BUTTON, BUZZER, LDR, and native logic gates NOT, AND, and OR**.



**------------------------------------------------------- REQUIREMENTS ---------------------------------------------------------------------**



A computer capable of running Microsoft Excel (all jokes aside, this project was not designed to run on mobile phones or tablets);



Microsoft Excel;



A basic understanding of VBA syntax and programming logic (this is optional);



Familiarity with editing and formatting Excel cells;



**----------------------------------------------- COMPONENT LAYOUT GUIDELINES ---------------------------------------------------------**



**ALL** components **WITHOUT EXCEPTION** must follow these rules when placed on the spreadsheet grid: 



	Each component has a specific number of pins defined in the source code, which must be explicitly declared when building your circuits and writing VBA macros;



	The visual drawing/shape of the components is completely customizable and technically optional, as long as the required pin cells are properly allocated;



**------------------------------------------------- COMPONENT PINOUTS -----------------------------------------------------------------**



**LED**: Features 2 pins, **POSITIVE** (Anode) and **NEGATIVE** (Cathode) | Reserve 1 cell to act as the emitting/glowing body;



**RESISTOR**: Features 2 pins | Allocate 1 cell to hold the resistance value in Ohms;



**7-SEGMENT DISPLAY WITH 4511 CHIP**: Uses a total of 4 input pins for the **4511 CHIP** and 10 output pins connected to the display layout | Use 7 cells to wire the **4511 CHIP** mapping directly into the 7-segment display layout to render the digits. It is recommended to frame the display cells with a black background (this aesthetic choice can be tweaked in the code);



**ARDUINO**: Equipped with 10 digital pins, 5 analog pins, 2 GNDs, and 1 5V pin (this pinout will be updated in future releases to match the exact hardware specifications of a physical board) | **TX** and **RX** serial communication is not yet implemented | The **ARDUINO** **REQUIRES** 1 cell to act as the Serial Monitor (you can reassign this in the source code | Default cell: D5);



**CHIP 4511**: Features 4 input pins and 10 output pins (this reflects my custom chip representation, structured this way to optimize backend code handling);



**7-SEGMENT DISPLAY**: Features 7 input pins | It **REQUIRES** a current-limiting resistor unless the current remains below 20 mA (a **150 Ohm** resistor for each segment pin is highly recommended).



**----------------------------------------------- HOW THE COMPONENTS OPERATE ---------------------------------------------------**



**LED**: The cell will light up when the **POSITIVE** pin receives a current value of 20 or less, and the **NEGATIVE** pin is tied to 0;



**RESISTOR**: The default input voltage is hardcoded to 5V (to be made dynamic in future updates), and the output is calculated in mA (perfectly scaled for driving LEDs). It computes A = 3 / Ohms, where A is the output current in mA, and Ohms is the value typed into the designated cell;



**CHIP 4511**: The input bus is represented by 4 pins processed **FROM BOTTOM TO TOP** in the source code. It reads a 4-bit binary number from these pins and decodes it into a decimal integer. The output bus consists of 10 pins that receive power based on the binary decoding. Pin 0 goes HIGH when the result is 0, and so forth.



**7-SEGMENT DISPLAY**: The input consists of 7 segment pins. In the code, whenever one of these pins receives power, its corresponding LED segment illuminates;



**ARDUINO**: All digital pins supply a 5V output when set to HIGH | Analog pin functionalities are not yet implemented.



**-------------------------------------------- ASSEMBLING YOUR FIRST CIRCUIT (MAKING AN LED LIGHT UP) ------------------------------------------**



Follow these step-by-step instructions:



	Pick specific cells on your grid to represent the 5V and GND (Ground) rails of the **ARDUINO**, the input and output terminals of your **RESISTOR** (don't forget the cell to type in the resistance value), and the **POSITIVE** and **NEGATIVE** pins of your **LED** (as well as the cell designated to change colors);



	Set the **RESISTOR** cell value to **150**;



	Map and execute all electrical connections using the function calls in your VBA code.
