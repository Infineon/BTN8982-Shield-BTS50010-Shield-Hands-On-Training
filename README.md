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
![Picture 7]()
##### Add BTN8982 Zip library
![Picture 8]()
##### Open the example Sketch
![Picture 9]()
##### Verify Board and COM “XMC1100 Boot Kit”
![Picture 10]()
##### Upload Sketch (Auto Compiles)
![Picture 11]()
##### Bi-directional Arduino Code
![Picture 12]()
#### DAVE4 CE Project
##### Launch DAVE 4 – Assign a workspace
![Picture 13]()
##### Create a new DAVE CE Project
![Picture 14]()
![Picture 15]()
##### Select XMC1100 Boot Kit
![Picture 16]()
##### If all was successful should have ready to go IDE and Project….
![Picture 17]()
##### Closer look at the tool bar…
![Picture 18]()
##### So what are we trying to do…
* Essentially we have four pins to control
* For each half bridge (BTN8982)
  * We can enable the bridge INH_x
  * We can toggle the IN_x pin
* We can also monitor the current in each half bridge 
  * IS_x Current Sense or Diagnostics 
![Picture 19]()
##### BTN8982 Truth Table…
* So if INH_x = 0 then half bridge is off; if it = 1 then IN_x toggles which FET (LSS or HSS) is active 
* In_x = 0; LSS is active 
* IN_x = 1; HSS is active 
![Picture 20]()
##### We have options…
* Option 1: PWM all four signals 
  * Most flexible but it is basically setting up the same DAVE App 4 times
* **Option 2: INH_x as a standard I/O; PWM the IN_x inputs**
  * Seems likle we´d have to setup a couple different apps 
  * Limited in the possible waveforms to generate, but will cover basics 
* Option 3: All four inputs as Standard I/O
  * Limited to on/off control verses controlling PWM to change speed 
  * Again only one DAVE App to setup 
* Lastly we can set up the A/D for the IS_x 
  * XMC1100 has simple A/D; we just setup one channel for ease of the training 
##### Setup DAVE App for INH_1
![Picture 21]()
##### Should see DIGITAL_IO App…double click it
![Picture 22]()
##### Change name by right clicking app…
![Picture 23]()
![Picture 24]()
##### Should look like this… (Note we haven’t assigned pins yet…)
![Picture 25]()
##### Repeat these steps for INH_2
* Add DAVE App DIGITAL_IO
  * Set as Input/Output
  * Set as High for Initial Output Level
  * Rename INH_2
![Picture 26]()
##### Setup PWM for IN_1 Output Hmmm…2 different PWM options
![Picture 27]()
##### Configure the App and Rename to IN_1
![Picture 28]()
![Picture 29]()
##### Setup PWM for IN_2 - Using other PWM Function
![Picture 30]()
![Picture 31]()
##### Configure App and rename to IN_2
![Picture 32]()
![Picture 33]()
##### Rearrange apps (not required)
![Picture 34]()
##### Let’s add and ADC measurement for IS_1
![Picture 35]()
##### Setup ADC App, rearranged, renamed to IS_1
![Picture 36]()
##### Let’s write some code
* What do we need... not a lot since we will use uC-Probe to control the system
* Some global variables for PWM duty cycle and to store ADC readings 
    volatile int32_t PWM_DutyCycle_IN_1 = 0; 
    volatile int32_t PWM_DutyCycle_IN_2 = 0;
    volatile XMC_VADC_RESULT_SIZE_t ADC_IS_1 = 0;
* Some code to set the values...
    PWM_CCU4_SetDutyCycle(&IN_1, PWM_DutyCycle_IN_1);
    PWM_SetDutyCycle(&IN_2, PWM_DutyCycle_IN_2);
    ADC_IS_1 = ADC_MEASUREMENT_GetGlobalResult();
