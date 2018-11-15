# BTN8982-Shield-BTS50010-Shield-Hands-On-Training
## SAFETY FIRST & Disclaimer
**WARNING:** 
If you put anything on end of MOTOR **it will spin fast and will hurt/make you bleed/damage** your surroundings…
You take full responsibility if you choose to put anything on the end of the motor!!!
**Bulbs Heat** Up…if you leave it on even a short time it will **burn you**!
## Hands On Training Agenda
* BTN8982 Shield Project
* Hardware Overview
* Arduino Bi-directional Motor Control Demonstration
* DAVE4 CE Project
* BTS50010 Shield Project
* Hardware Overview
* Arduino Blinky Bulb Demonstration
* DAVE4 CE Project
### BTN8982 Shield Project
#### Hardware Overview 
* XMC1100 Boot Kit
* BTN8982 Arduino Shield
* 12V Power Supply
* USB Cable 
* Brushed DC Motor
* Power Sequence 
  * Connect Shield to Boot Kit
  * Connect Motor to OUT1 and OUT2 (for bi-directional control)
  * Power XMC kit through micro-USB cable
  * Program XMC Boot kit (through DAVE/Arduino)
  * Connect 12v GND to Shield GND
  * Connect 12v Power to Shield VBAT
  * Turn on supply (aka plug in supply)
![Picture 1]()
##### XMC1100 Boot Kit Pin Descriptions
![Picture 2]()
##### BTN8982 Shield Overview
![Picture 3]()
##### BTN8982 Shield Pin Descriptions
![Picture 4]()
#### Arduino Bi-directional Motor Control Demonstration
##### Arduino UI Setup
* Install Arduino per Arduino Website instructions
* Install XMC for Arduino per XMC Github instructions 
* Install BTN8982 Shield .zip package per BTN8982 Github instructions
* Setup Arduino UI
  * Make sure XMC1100 Boot Kit is the target board
  * Look at Windows `Device Manager´ to find COM Port
  * Make sure you are targeting the correct COM Port
  * Compile and upload Sketch 
##### Arduino -> File -> Preferences
![Picture 5]()
##### Arduino -> Tools -> Board: “xyz” -> Boards Manager
![Picture 6]()
##### Arduino Board Manager -> “XMC” Search (Note: need network connection)
