**------------------------------------------------------------------------------------------------------------**

				**CODE INSTRUCTIONS**

**------------------------------------------------------------------------------------------------------------**



**Code Version: v0.1 (BETA)**



**--------------------------------------- NOTES --------------------------------------------------------**



In terms of structure, the file is split into 2 modules. Module 1 contains the functions regarding the components and the **ARDUINO**, while Module 2 presents the user-specific **ARDUINO** code, acting as an IDE.



Here, I detail how the code works and how connections interact. To learn about the "physical" side of the layout, check the **"README - INSTRUCTIONS"** file.



**-------------------------------------- FUTURE VERSIONS -----------------------------------------------------**



The **LED** and **RESISTOR** functions will undergo changes regarding adaptability in version **v0.2**.



The arrival of new components **POTENTIOMETER, BUTTON, BUZZER, LDR, and native logic gates NOT, AND, and OR** is planned for version **v0.2**.



The **Sub loop()** function will be implemented in version **v0.3**.



**-------------------------------------- SYSTEM ARCHITECTURE ----------------------------------------------------------**



When starting your code inside the ARDUINO (Module 2), the **Sub setup()** entry function is recommended and already provided as a baseline | the **Sub loop()** function has not been implemented yet.



To run the code, click the **GREEN PLAY BUTTON** on the **VBA** interface.



To call any function, use **Call functionName(Parentheses if required)**.



The components used **REQUIRE** their specific function to be called so they can be updated | for instance, to make the LED light up.



In **VBA**, cells are handled using **Range(Cell)**, and for connections, components use **Range(Cell).Value** to read the value of that specific cell.



The execution order of the code depends entirely on the programmer; if the items are not placed in the correct sequence, the code will not work as expected.



Ex: To make the **ARDUINO** turn on an **LED**, first make the **ARDUINO** turn on the corresponding digital pin, and **ONLY AFTER THAT**, add the function that updates the **LED**.



**----------------------------------------- COMPONENT-SPECIFIC FUNCTIONS ----------------------------------------------**



 **- ARDUINO** :

	

	To turn on digital pins, use **pinoDigital(Pin cell, Pin state)**. This function is similar to the **pinMode()** function from **ARDUINO**. The cell must be passed as a **String**, and for the value, **0** represents **LOW** and **1** represents **HIGH**.



	**Example: Call pinoDigital("A1", 1)** | In this case, cell **A1** receives the value 5, which equals 5v.



 **- CHIP 4511** :

	

	To use **CHIP 4511**, use **chip4511(cell1, cell2, cell3, cell4)**. This function takes the values of the 4 cells and builds a 4-bit binary number (**bytes = Array(cell4, cell3, cell2, cell1)**). Then, it decodes it to decimal using a lookup array (**cola = Array(8, 4, 2, 1)**). The function loops through this list, and for values equal to 5 (**If** **Range(bytes(i)).Value = 5 Then**), it takes the corresponding index **i** and adds it to a **num** variable (**num = num + cola(i)**). The complete decoding block is as follows:



	**For i = 0 To 3**

       	    **If Range(bytes(i)).Value = 5 Then**

           		**num = num + cola(i)**

       	    **End If**

        **Next i**



	After that, it targets the 10 outputs declared in the code inside the **saidas** variable. (This part remains directly in the module body because putting it inside the function would require too many arguments, but this will be fixed in future versions). It then places the value **1** in the cell corresponding to the decoded number and sets the remaining cells to **0**.

	

	**For i = 0 To 9**

       	    **Range(saidas(i)).Value = 0**

   	**Next i**



	**Range(saidas(num)).Value = 1**



	**Example** : **Call chip("O16", "O14", "O12", "O10")** | In the mentioned cells, the received binary is **1010** which equals **5** in decimal, so the 5th cell of **saidas** will be set to **1**, and the rest to **0**.



 **- RESISTOR** :



	To use the **RESISTOR**, use **Resistor(Ohms, input, output)**. These arguments were not included in the example code snippet but are fully present in the module. Pass the cell coordinates where the **RESISTOR** is located. This function expects a default input of **5v** (to be updated to accept other voltage levels in future updates) and calculates **A = 3 / Ohms**, where **A** is the current in **mA**, returning it to the output cell.



	**ohms = Range("F8").Value**

   	**input = Range("G20").Value**



	**A = 3 / ohms**

        **A = A \* 1000**



	**If input = 0 Then**

       	    **A = 0**

   	**End If**



	**Range("E8").Value = input**

   	**Range("G8").Value = A**



	**Example** : **Call Resistor** | In this example, if the **Ohms** cell has a value of **150**, the value displayed in the output cell will be **20**.



 **- LED** :



	To use the **LED**, use **Led(positive, negative, brightness)**. Pass the corresponding cells as arguments. The **LED** performs a simple check: it verifies if **Positive** is **<= 20** (**If positive <= 20 Then**) and if **NEGATIVE** **is = 0**, then adjusts the color of the **brightness** cell accordingly (**Range("F14").Interior.Color = RGB(cor, 0, 0)**). If the **LED** is turned off or blown out, it switches back to the default color **RGB(128, 128, 128)**.



	**Range("E14").Value = Range("G8").Value   'This part is aesthetic**

   	**Range("G14").Value = Range("B12").Value  'This one is too**

 

   	**positive = Range("E14").Value**

   	**negative = Range("G14").Value**

 

   	**If positive <= 20 And negative = 0 And positive >= 10 Then**

   	    **cor = positive \* 12.5**

   	    **Range("F14").Interior.Color = RGB(cor, 0, 0)**

   	**Else**

   	    **Range("F14").Interior.Color = RGB(128, 128, 128)**

   	**End If**



	**Example** : **Call led** | In this case, if the **POSITIVE** cell reads 20 and the **NEGATIVE** cell reads 0, it lights up (**Range("F14").Interior.Color = RGB(cor, 0, 0)**).
