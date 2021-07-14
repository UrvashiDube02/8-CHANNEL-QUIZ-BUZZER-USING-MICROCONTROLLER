# 8-CHANNEL-QUIZ-BUZZER-USING-MICROCONTROLLER

**AIM**

Designing an 8 channel Quiz Buzzer Circuit using Microcontroller (8051) indicating the team which has pressed the button first. The 8-channel quiz buzzer circuit is a simple embedded system with a set of 8 input push button devices, a microcontroller as the main controller and the output being an LCD display screen. The operation is carried out by a microcontroller through a program written in assembly language and dumped inside the microcontroller. When one of the push buttons is pressed, the corresponding number is displayed on the LCD screen.

**BLOCK DIAGRAM**

![image](https://user-images.githubusercontent.com/87383888/125569427-5399bd48-e140-4e3e-bb5b-07717fb0453a.png)

The above block diagram consists of the following :

1. The push buttons indicating the contestants as the input . In the program total 8 push buttons are used, indicating 8 contestants. One of the push buttons needs to be pressed to get the program simulated.
2. Microcontroller AT89C51 is the body of the project which is basically the integrated circuit design onto which the push buttons are interfaced at different port pins .Once the button is pressed depending upon the ports and the button associated to it , the program is executed.
3. The LCD display screen is the electronically modulated optical device used as the output of the project onto which the pressed push buttons number reflects . The particular button after getting pressed along with its port program execution displays the required contestant number of the screen.
4. The reset button is also a kind of push button which clears the number displayed on the LCD display screen and restarts the process.

**FLOWCHART**

![image](https://user-images.githubusercontent.com/87383888/125569536-ba590bb1-d256-40e3-be80-60f7090fa211.png)

**CIRCUIT DIAGRAM**

![image](https://user-images.githubusercontent.com/87383888/125569565-2447a6f4-372c-4240-8ba1-93eb60b1aa6f.png)

**COMPONENTS REQUIRED**

1. AT89C51 (8051 Microcontroller)
2. LCD display
3. Push Buttons – 10
4. 10KΩ Resistors – 2
5. 1N4007 Diode
6. 10μF Capacitor
7. 33pF Capacitors – 2
8. 11.0592 MHz Crystal
9. 8051 Programmer
10. 5V Power Supply

**DESIGN**

Let us discuss the design process which consists of the following steps :
1. First step is designing the circuit.
2. The second step is drawing the schematic using any software.
3. Third step involves writing the code using high level language like C or assembly language and then compiling it on a software platform like Keil μVision.
4. Fourth step is programming the microcontroller with the code.
5. Finally, the fifth step is testing the circuit.

**QUIZ BUZZER CIRCUIT**

The circuit involves using three major components – 8051 Microcontroller, SPST Push Buttons and a LCD display screen . The microcontroller used in this case is AT89C51, an 8 bit microcontroller manufactured by Atmel (now Microchip).

1. RESET CIRCUIT DESIGN : The reset resistor is selected such that the voltage at the reset pin, across this 
resistor is at minimum of 1.2V and the width of the pulse applied to this pin is greater than 100 ms.
2. OSCILLATOR CIRCUIT DESIGN : The oscillator circuit is designed using a crystal oscillator of 11.0592 Mhz and two ceramic capacitors each 33pF. The crystal is connected between pins 18 and 19 of the microcontroller
3. MICROCONTROLLER INTERFACING DESIGN: The set of 8 push buttons are interfaced to port P2 of 
the microcontroller and a reset is interfaced to the port pin P3.0. The LCD display is interfaced to the 
microcontroller such that all the input pins are connected to port P1.
4. MICROCONTROLLER CODE : The code can be written using C language or assembly language.

Here I have written the program in C language using Keil μVision software. This is accomplished by the following steps:

1. Create a new project on Keil window and select the target (microcontroller).
2. Create a new file under the project and write the code.
3. Save the code with .c extension and add the file to the source group folder under the target folder.
4. Compile the code and create the hex file.

Once the code is compiled and a hex file is created, next step is to dump the code into the microcontroller. This can 
be done with an 8051 Microcontroller Programmer.

**CODE**

Let us now discuss the code of the program :

ORG 0000H

LCALL INTIALIZE_SYSTEM 

REPEAT: LCALL DISPLAY_NUMBER

SJMP REPEAT

INTIALIZE_SYSTEM:

MOV A, #38H ; initialise LCD 2 line , 5*7 matrix 

LCALL COMMAND ; call command subroutine 

MOV A, #0EH ; display on , cursor on


LCALL COMMAND ; call command subroutine 

MOV A, #01H ; clear LCD

LCALL COMMAND ;call command subroutine 

MOV A , #06H ; shift cursor right

LCALL COMMAND

MOV A , #083H ; cursor at line 1, pos 3

LCALL COMMAND ; call command subroutine 

MOV A, #'C' ; display letter C

LCALL DISPLAY ; call display subroutine 

MOV A,#'O' ;display letter O

LCALL DISPLAY ; call display subroutine 

MOV A,#'N' ; display letter N

LCALL DISPLAY

MOV A,#'T' ; display letter T 

LCALL DISPLAY

MOV A,#'E' ; display letter E 

LCALL DISPLAYMOV A,#'S'; display letter S 

LCALL DISPLAY

MOV A,#'T' display letter T 

LCALL DISPLAY

MOV A,#'A' ; display letter A 

LCALL DISPLAY

MOV A,#'N' ; display letter N 

LCALL DISPLAY

MOV A,#'T' ; display letter T 

LCALL DISPLAY

MOV A,# ' ' ; display ' ' 

LCALL DISPLAY 

RET

DISPLAY_NUMBER:

JNB P2.0,ONE ; branching port pin P2.0 with the button ONE 

JNB P2.1,TWO ; branching port pin P2.1 with the button TWO

JNB P2.2,THREE; branching port pin P2.2 with the button THREE 

JNB P2.3,FOUR ; branching port pin P2.3 with the button FOUR 

JNB P2.4,FIVE ; branching port pin P2.4 with the button FIVE 

JNB P2.5,SIX ; branching port pin P2.5 with the button SIX

JNB P2.6,SEVEN; branching port pin P2.6 with the button SEVEN 

JNB P2.7,EIGHT; branching port pin P2.7 with the button EIGHT 

SJMP DISPLAY_NUMBER

EIGHT: LJMP EIGHT1 

CLEAR:

MOV A,#08H ; display off ,cursor off 

LCALL COMMAND

LCALL DELAYMOV A,#0EH ; display on , cursor blinking 

LCALL COMMAND

LCALL DELAY

JB P3.0,CLEAR ; reset command

MOV A,#0C7H ; display on , cursor off 

LCALL COMMAND

MOV A,#' ' 

LCALL DISPLAY

WAIT_1: JNB P3.0,WAIT_1 

LCALL DELAY 

RET

ONE: MOV A,#0C7H ; display on cursor off

LCALL COMMAND 

MOV A,#'1' ; load #1 

LCALL DISPLAY 

LJMP CLEAR

TWO: MOV A,#0C7H

LCALL COMMAND 

MOV A,#'2' ; load #2 

LCALL DISPLAY 

LJMP CLEAR

THREE: MOV A,#0C7H

LCALL COMMAND 

MOV A,#'3' 

LCALL DISPLAY 

LJMP CLEARFOUR: MOV A,#0C7H

LCALL COMMAND 

MOV A,#'4' 

LCALL DISPLAY 

LJMP CLEAR

FIVE: MOV A,#0C7H

LCALL COMMAND 

MOV A,#'5' 

LCALL DISPLAY 

LJMP CLEAR

SIX: MOV A,#0C7H

LCALL COMMAND 

MOV A,#'6' 

LCALL DISPLAY 

LJMP CLEAR

SEVEN: MOV A,#0C7H 

LCALL COMMAND 

MOV A,#'7' 

LCALL DISPLAY 

LJMP CLEAR

EIGHT1: MOV A,#0C7H 

LCALL COMMAND 

MOV A,#'8'LCALL DISPLAY 

LJMP CLEAR

COMMAND: ACALL DELAY

MOV P1,A ; issue A to P1 

CLR P3.2 ; RS=0 for command

CLR P3.3 ; R/W=1 to write in LCD 

SETB P3.4 ; EN=1 for H-to-L pulse 

CLR P3.4 ; EN =0 latch in

RET

DISPLAY: ACALL DELAY

MOV P1,A ; issue A to P1 

SETB P3.2 ; RS=1 for data CLR

P3.3 ; R/W=0 to read

SETB P3.4 ; EN=1 for H-to-L pulse 

CLR P3.4 ; EN=0 latch in

RET

DELAY: MOV R7,#0FFH LOOP1: 

MOV R6,#0FFH

LOOP: DJNZ R6,LOOP ; continuous execution till R6=0 

DJNZ R7,LOOP1

RET 

END

**ALGORITHM**

STEP 1 : START

STEP 2: Initializing the LCD and display 'CONTESTANT' 

STEP 3:Cconnectiong the push buttons to Port pin 2

STEP 4: Connecting the reset button to Port pin 3.0

STEP 5 : Writing the individual code for the push buttons from ONE - EIGHT

STEP 6: Writing the delay code for DISPLAY and COMMAND and also for continuously executing the program the DELAY code

STEP 7: END

**WORKING**

a. Once the circuit is powered, the compiler will initialize the stack pointer and the variables having the non-zero initial values and perform other initialization process and then calls the main function. It then checks if any of the buttons is pressed.

b. In other words the microcontroller scans for any of its input pins at port P1 to be zero or at logic low level. In case a button is pressed, the display function is called by passing the corresponding number. The microcontroller then sends the relevant signals to the port connected to the 7 segment display.

c. The microcontroller will turn on the buzzer for a second and turns it off but the number will be continuously displayed on the 7 segment display until the RST button is pressed.

**OUTPUT**

![image](https://user-images.githubusercontent.com/87383888/125570139-d50098c4-0d01-4766-900e-5116f3727194.png)

FIG : The LCD screen displaying CONTESTANT before any button pressed.

![image](https://user-images.githubusercontent.com/87383888/125570181-e7ff6b98-2d3e-4a3e-bfbf-b213ecc12cb5.png)

FIG : After the button 6 is pressed , the LCD displays CONTESTANT 6.

![image](https://user-images.githubusercontent.com/87383888/125570208-ee6a6d45-dcdc-489f-a763-49a20e93b319.png)

FIG: after pressing the RESET button , the contestant number disappears.

**CONCLUSION**

The 8 channel quiz buzzer is designed with the appropriate requirements , the algorithm and the code is being 
written and the working is successfully verified.

**PROS AND CONS**

The project has the following pros and cons:

PROS:

1. The circuit is useful at quiz competitions at schools , colleges and other institutions to display the only contestant number who has pressed the buzzer first , since human intervention in this case would be difficult.
2. It is also used at public places like banks , restaurants as a digital token display system.
3. Used in game shows as well , performing the same function as in the quiz competition.
4. LCD are energy efficient , long term cost effective

CONS:

1. Only 8 quiz buzzers can be connected per port to the 8051 microcontroller .
2. maximum of 32 ASCII characters can be displayed in the LCD screen .
3. LCD not suitable for dimly lit applications , can require frequent adjustments .
4. A loss of contrast in high temperature environments.

