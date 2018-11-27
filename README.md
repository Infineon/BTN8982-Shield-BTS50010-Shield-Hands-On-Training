# BTN8982-Shield-BTS50010-Shield-Hands-On-Training

## SAFETY FIRST & Disclaimer

**WARNING:** 
If you put anything on end of MOTOR **it will spin fast and will hurt/make you bleed/damage** your surroundings…
You take full responsibility if you choose to put anything on the end of the motor!!!
**Bulbs Heat** Up…if you leave it on even a short time it will **burn you**!

## Hands On Training Agenda

* [BTN8982 Shield Project](#BTN8982)
* [Hardware Overview](#HardwareOverview)
* [Arduino Bi-directional Motor Control Demonstration](#MotorControl)
* [DAVE4 CE Project](#DAVE4)
* [BTS50010 Shield Project](#BTS50010)
* [Hardware Overview](#HardwareOverview2)
* [Arduino Blinky Bulb Demonstration](#BlinkyBulb)
* [DAVE4 CE Project](#DAVE4CE)

### BTN8982 Shield Project
<a name="BTN8982"></a>

#### Hardware Overview
<a name="HardwareOverview"></a>

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

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Hardware%20Overview.png" width=500>

##### XMC1100 Boot Kit Pin Descriptions

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/XMC1100%20Boot%20Kit%20Pin%20Descriptions.jpg" width=700>

##### BTN8982 Shield Overview

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/BTN8982%20Shield%20Overview.png" width=500>

##### BTN8982 Shield Pin Descriptions

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/BTN8982%20Shield%20Pin%20Descriptions.png" width=600>

#### Arduino Bi-directional Motor Control Demonstration
<a name="MotorControl"></a>

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

![Arduino File Preferences](https://github.com/Infineon/Assets/blob/master/Pictures/Arduino%20File%20Preferences.png)

##### Arduino -> Tools -> Board: “xyz” -> Boards Manager

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Arduino%20Boards%20Manager.2.png" width=500>

##### Arduino Board Manager -> “XMC” Search (Note: need network connection)

![Arduino Board Manager XMC search](https://github.com/Infineon/Assets/blob/master/Pictures/Arduino%20Board%20Manager%20XMC%20search.png)

##### Add BTN8982 Zip library

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Add%20BTN8982%20Zip%20Library.2.png" width=450>

##### Open the example Sketch

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Example%20Sketch.png" width=600>

##### Verify Board and COM “XMC1100 Boot Kit”

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Verify%20Board%20and%20COM%20XMC1100%20Boot%20Kit.png" width=450>

##### Upload Sketch (Auto Compiles)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Upload%20Sketch.png" width=450>

* Motor should spin up then down then reverse up then down

##### Bi-directional Arduino Code

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Bi-directional%20Arduino%20Code.png" width=600>

#### DAVE4 CE Project
<a name="DAVE4"></a>

##### Launch DAVE 4 – Assign a workspace

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Assign%20a%20workspace.png" width=500>

##### Create a new DAVE CE Project

![New DAVE CE Project](https://github.com/Infineon/Assets/blob/master/Pictures/New%20DAVE%20CE%20Project.png)

##### Select XMC1100 Boot Kit

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Select%20XMC1100%20Boot%20Kit.png" width=450>

##### If all was successful go to DAVE IDE and Project…

![Ready to go IDE and Project](https://github.com/Infineon/Assets/blob/master/Pictures/Ready%20to%20go%20IDE%20and%20Project.png)

##### Closer look at the tool bar…

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Tool%20bar.2.png" width=500>

##### So what are we trying to do…

* Essentially we have four pins to control
* For each half bridge (BTN8982)
  * We can enable the bridge INH_x
  * We can toggle the IN_x pin
* We can also monitor the current in each half bridge 
  * IS_x Current Sense or Diagnostics 

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Pin%20defintions%20and%20functions.3.png" width=500>

##### BTN8982 Truth Table…

* So if INH_x = 0 then half bridge is off; if it = 1 then IN_x toggles which FET (LSS or HSS) is active 
* In_x = 0; LSS is active 
* IN_x = 1; HSS is active 

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Truth%20Table_complete.png" width=500>

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

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Setup%20DAVE%20App%20for%20INH_1.2.png" width=500>

##### Should see DIGITAL_IO App…double click it

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/DIGITAL_IO%20App.png" width=750>

##### Change name by right clicking app…

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Change%20Name.png" width=350>

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Change%20Name_2.png" width=350>

##### Should look like this… (Note we haven’t assigned pins yet…)

![Change Name_Done](https://github.com/Infineon/Assets/blob/master/Pictures/Change%20Name_Done.png)

##### Repeat these steps for INH_2

* Add DAVE App DIGITAL_IO
  * Set as Input/Output
  * Set as High for Initial Output Level
  * Rename INH_2

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Repeat%20steps%20for%20INH_2.2.png" width=550>

##### Setup PWM for IN_1 Output Hmmm…2 different PWM options

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Setup%20PWM%20for%20IN_1%20Output.2.png" width=750>

##### Configure the App and Rename to IN_1

![Configure App and Rename to IN_1](https://github.com/Infineon/Assets/blob/master/Pictures/Configure%20App%20and%20Rename%20to%20IN_1.png)

![Configure App and Rename to IN_1_2](https://github.com/Infineon/Assets/blob/master/Pictures/Configure%20App%20and%20Rename%20to%20IN_1_2.png)

##### Setup PWM for IN_2 - Using other PWM Function

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Setup%20PWM%20for%20IN_2.4.png" width=900>

##### Configure App and rename to IN_2

![Configure App and Rename to IN_2.3](https://github.com/Infineon/Assets/blob/master/Pictures/Configure%20App%20and%20Rename%20to%20IN_2.3.png)

![Configure App and Rename to IN_2_2.4](https://github.com/Infineon/Assets/blob/master/Pictures/Configure%20App%20and%20Rename%20to%20IN_2_2.4.png)

##### Rearrange apps (not required)

![Rearrange Apps](https://github.com/Infineon/Assets/blob/master/Pictures/Rearrange%20Apps.png)

##### Let’s add an ADC measurement for IS_1

![ADC measurment for IS_1.2](https://github.com/Infineon/Assets/blob/master/Pictures/ADC%20measurment%20for%20IS_1.2.png)

##### Setup ADC App, rearranged, renamed to IS_1

![Setup ADC App_rearranged](https://github.com/Infineon/Assets/blob/master/Pictures/Setup%20ADC%20App_rearranged.png)

##### Let’s write some code

* What do we need... not a lot since we will use uC-Probe to control the system
* Some global variables for PWM duty cycle and to store ADC readings 
```
    volatile int32_t PWM_DutyCycle_IN_1 = 0; 
    volatile int32_t PWM_DutyCycle_IN_2 = 0;
    volatile XMC_VADC_RESULT_SIZE_t ADC_IS_1 = 0;
```
* Some code to set the values...
```
    PWM_CCU4_SetDutyCycle(&IN_1, PWM_DutyCycle_IN_1);
    PWM_SetDutyCycle(&IN_2, PWM_DutyCycle_IN_2);
    ADC_IS_1 = ADC_MEASUREMENT_GetGlobalResult();
```
##### Where to put the 2 blocks of code…

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/2%20Blocks%20of%20code.2.png" width=700>

##### Pin Mapping

![Pin Mapping.2](https://github.com/Infineon/Assets/blob/master/Pictures/Pin%20Mapping.2.png)

##### Assign the HW Pins to the DAVE App Signals

* IN_1 = D3 = P0.0
* IN_2 = D11 = P1.1
* INH_1 = D12 = P1.0
* INH_2 = D13 = P0.7
* IS_1 = A0 = P2.6
* Right click on pin to select Signal

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Assign%20the%20HW%20Pins.png" width=600>

##### Generate DAVE code then build…

![Generate DAVE Code](https://github.com/Infineon/Assets/blob/master/Pictures/Generate%20DAVE%20Code.png)

##### Launch Debugger and run code

![Launch Debugger.2](https://github.com/Infineon/Assets/blob/master/Pictures/Launch%20Debugger.2.png)

##### Setup debug interface…(double click Segger)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Setup%20debug%20interface.2.png" width=700>

##### Opens Debug Perspective – click run

![Debug Perspective.2](https://github.com/Infineon/Assets/blob/master/Pictures/Debug%20Perspective.2.png)

##### Setup uC_Probe

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Setup%20uC_Probe.2.png" width=700>

##### Point to DAVE Workspace .elf file

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Point%20to%20DAVE%20Workspace%20(2).png" width=700>

##### Save your file (I use DAVE debug workspace)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Save%20file.png" width=700>

##### Add a slider for IN_1 Duty Cycle - Drag and drop

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Add%20a%20slider%20for%20IN_1%20Duty%20Cycle.png" width=700>

##### Configure the slider (0000 to 10000 are correct range for Duty Cycle)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Configure%20the%20slider.png" width=700>

##### Name (Drag text box and edit it)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Name%20%20(Drag%20text%20and%20edit%20it).png" width=700>

##### Assign the Duty Cycle Variable to it (Drag and Drop over slider)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Assign%20the%20Duty%20Cycle%20Variable.png" width=800>

##### Add cool meter for Duty Cycle IN_1

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Add%20cool%20meter%20for%20Duty%20Cycle%20IN_1.2.png" width=700>

##### Repeat for Duty Cycle IN_2 (Copy widgets from IN_1, drag new Variable)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Add%20cool%20meter%20for%20Duty%20Cycle%20IN_2.2.png" width=700>

##### Run uC Probe (be sure DAVE Debug code is running)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Run%20uC%20Probe.2.png" width=700>

##### Left slider = Forward 

##### Right slider = Reverse

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Left%20slider%20%3D%20Forward%20Right%20slider%20%3D%20Reverse.png" width=700>

##### Add graph for IS_1 Signal (resize to fit)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Add%20graph%20for%20IS_1%20signal.png" width=700>

##### Should look something like this... (Do not forget to save)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Pattern.png" width=700>

##### What´s up with the IS_1 singal???

* If you look at the truth table...

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Truth%20Table_IS_1%20signal.png" width=500>

* So only valid reading when HSS FET is high otherwise it’s an offset(Diagnostics)
* Currently code just continuously makes IS_1 ADC conversion and is displaying in uC-Probe…
* Note if you run in reverse (PWM IN_2) the HSS_1 never goes high and IS_1 signal is steady = offset

##### How can we make our code smarter???

* Let´s try to trigger the ADC when IN_1 is High during the PWM 
* Good thing we used the PWM_CCU4 App for IN_1 signal, as it seems to be a little more feature rich than the PWM App
* Basically we will wire our existing DAVE Apps to accomplish this and we should not have to change our C code at all
  * I.e. we will only make an ADC during the high time of the IN_1 PWM Signal… **{Correction, we read ADC at period match, if duty cycle     is 0 or low it will still take reading}**
  * We will only make changes to the Apps configuration
  * We will need to generate the new App code and rebuild
  
##### Modify the ADC (Stop the debugger, click DAVE CE perspective)

![Modify the ADC](https://github.com/Infineon/Assets/blob/master/Pictures/Modify%20the%20ADC.png)

##### Modify PWM_CCU4 IN_1

![Modify PWM_CCU4 IN_1.3](https://github.com/Infineon/Assets/blob/master/Pictures/Modify%20PWM_CCU4%20IN_1.3.png)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Modify%20PWM_CCU4%20IN_1_2.png" width=600>

##### Connect HW Signals (Right Click)

![Connect HW Signals.2](https://github.com/Infineon/Assets/blob/master/Pictures/Connect%20HW%20Signals.2.png)

##### Configure IN_1

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Configure%20IN_1.png" width=600>

##### Generate Code and Build; run Probe 

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Generate%20Code%20and%20Build.png" width=600>

### BTS50010 Shield Project
<a name="BTS50010"></a>

#### Hardware Overview 
<a name="HardwareOverview2"></a>

* XMC1100 Boot Kit
* BTS50010 Arduino Shield 
* 12V Power Supply 
* USB Cable 
* Automotive 12V Bulb 
* Power Sequence 
  * Connect Shield to Boot Kit
  * Connect Bulb to LOAD and GND
  * Power XMC Boot Kit through micro USB cable
  * Program XMC Boot Kit (through DAVE/Arduino)
  * Connect 12V GND to Shield GND 
  * Connect 12V Power to Shield VBAT 
  * Turn on supply (aka plug in supply)

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Hardware%20Overview%20BTS50010.png" width=500>

##### XMC1100 Boot Kit Pin Discriptions 

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/XMC1100%20Boot%20Kit%20Pin%20Descriptions.jpg" width=700>

##### BTS50010 Shield Overview

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/BTS%2050010%20Shield%20Overview.png" width=500>

##### BTS50010 Pin Descriptions 

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/BTS50010%20Pin%20Descriptions.png" width=600>

#### Arduino Blinky Bulb Demonstration
<a name="BlinkyBulb"></a>

##### Arduino Blinky Bulb Demo

* Open Blinky Bulb Demo Sketch 
  * [your path]\Avnet FAE Training 10-10-2018\Arduino Workspace\bts50010 Shield Sketches\BTS500010_Automotive_Bulb
* Connect Shield to Boot Kit
* Connect Shield to LOAD and GND
* Connect Bulb to LOAD and GND
* Power XMC Kit through micro-USB cable
* Program XMC Boot Kit (Arduino)
  * Make sure XMC1100 Boot Kit and COM set correctly 
* Upload sketch
* LED1 and LED2 should alternate
* Apply 12V Power (GND first) to Shield 
* Bulb should turn on and off 
* **WARNING: Bulb will get hot!!!**

##### Blinky Blub Code

<img src="https://github.com/Infineon/Assets/blob/master/Pictures/Blinky%20Bulb%20Code.png" weidth=300>

#### DAVE4 CE Project
<a name="DAVE4CE"></a>

##### BTS50010 Shield DAVE Project

* Exercise 1:
  * Create new DAVE CE Project 
  * Target XMC1100 Boot Kit w/BTS50010 Shield
  * Use DAVE Apps to turn on/off bulb with uC-Probe Switch
* Hint: Can create a switch variable, and then check if switch is high or low to call appropriate DAVE I/O app method; assign the switch   variable to a uc-Probe widget
* Advanced Exercise 2 & 3:
  * Make Bulb Blink like in Arduino Demo
* Hint 1: PROFET PWM max speed is 100Hz; for bulb, shoot for on/off time in seconds range 
* Hint 2: or use systimer 

##### Exercise 1 (Cheat Sheet)

* Create new DAVE CE Project 
* Drop DIGITAL_IO App
  * Configure as Output
  * Rename it to "IN_BTS50010"
  * Set initial level to 0
* Map Pin to correct I/O Pin
  * Hint: It is P0.3
* Create a volatile int called light_switch default = 0
  * volatile int32_t light_switch = 0;
* Create C-Code logic in the while{1U} loop
  * If (light_switch == 0) then {turn off bulb} else {turn on bulb}
* Call DIGITAL_IO Methods for turning on I/O
  * DIGITAL_IO_SetOutputHigh(&IN_BTS50010);
  * DIGITAL_IO_SetOutputLow(&IN_BTS50010);
* Generate  DAVE Code then compile your code then run debugger 
* Launch Probe; point to new .elf file 
  * Drop widget with values 1 or 0; (Toggle)
  * Drag light_switch variable to widget 
  * Should be good to go

##### Exercise 2 (Cheat Sheet)

* Create new DAVE CE Project 
* Drop PWM App
  * Configure as Output 
  * Rename it to "IN_BTS50010"
  * Set frequency to min 1Hz or something you can see
  * Set Duty Cycle to 50% (more or less to your preference)
  * Start on initialization
* Map Pin to correct I/O Pin
  * Hint: It is P0.3
* Should not need C-Code 
* Generate DAVE Code then compile your Code then run debugger 
* Bulb should be blinking; but fast

##### Exercise 3 (Cheat Sheet)

* Setup DIGIT_IO pin as in the other examples 
* Use SYSTIMER to create a 1 or 2 second timer
* See `usage´ from DAVE App Help for SYSTIMER for cheat codes 
 
