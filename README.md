# PCB repository template

This is a template repository for a PCB project. Using git allows you to keep track of different versions of the same PCB and effectively share files with other collaborators. The README page is very important: it's where you write down instructions, explanations, etc. on how you can use, test, improve your circuit. In this first paragraph, you can put a simple description of your project. In this example, we are developing a curtain controller that can be used to manage schedule opening and closing your curtains.

Adding a picture here or in the next sections can be useful too.

![Eagle design](/assets/Eagle_design.png)
<img src ="/assets/assembled_pcb.jpg" width="400">

## Features
This is where you list the things your PCB does. It is especially useful if your design has multiple boards. Ex:
* ESP32 WROOM32 module
* 1x button
* 1x programmable LED
* 1x VEML6030 ambient light sensor
* 1x CP2104 USB-UART bridge
* 1x DRV8825 stepper motor driver with controllable STEP, DIR, /SLEEP and /ENA

If your board has jumpers to select different modes. Here would be a good place to explain the options:
* SJ1: enable or disable ambient light sensor
* SJ2: select stepper driver current limit (1A or 2A)

## Connections and Pinout
Writing down which signal connects to which MCU pin can be useful when developing firmware, so you don't have to re-open your schematic file

|Signal|Arduino IDE Pin|Notes|
|:---:|:----:|:---:|
|Stepper_step|16||
|Stepper_direction|17||
|Stepper_enable|4|active low|
|Stepper_sleep|5|active low|
|Limit_switch_1|14|has external pullup (R23)|
|Limit_switch_2|12|no external pullup (R22), enable internal pullup|
|I2C_SCL|22||
|I2C_SDA|23||
|Ambient_light_sensor_int|21||
|LED|13||
|Button|15|enable internal pullup|
|Battery_voltage|I35, A1_7|ADC1 channel 7|

## Programming instructions (Optional)
While it might sound redundant for some, this section can be useful if you have your own unique programming instructions, a custom bootloader, or just for very beginners to get familiar with the process.  

## Errata, fixes and debugging notes
Your PCB will probably have bugs or mistakes. Keeping track of them is valuable.

#### Version 1.0
Fixes
* Switching regulator outputs 1.2V instead of 3.3V. Changed R12 to 2.2k and R16 to 10k to get 3.3V.
* Forgot to connect USB power line to 5V rail
* Remove R22: the external pullup messes with communication with flash when programming.
* Add 10k pull up resistor on the nENA line so that when the MCU is asleep the stepper is not enabled.
* MCU pin PA12 cannot be used for PWM. Cut trace and connected to PA13 instead.

Improvements for next version
* Use and external RTC chip with less drift than the internal MCU RTC
* Add a piezo-buzzer for notifications
* Add capacitive touch slider

#### Version 1.1

## References and Tutorials
As you design your board, you'll probably refer to a lot of online/other resources, such as tutorials, application notes, datasheets, etc. You can choose to keep all of them on the design journal or/and link some in  in this section. I typically link hardware information I used that might impact firmware development: this is because frequently, the people reading this page are the ones that have to program the board, whether they have designed it or not.

* [ESP32 deep sleep](https://lastminuteengineers.com/esp32-deep-sleep-wakeup-sources/)
* [Capacitive touch on ESP32](https://randomnerdtutorials.com/esp32-touch-pins-arduino-ide/)
* [Capacitive touch design guidelines](https://www.st.com/resource/en/application_note/dm00087990-design-with-surface-sensors-for-touch-sensing-applications-on-mcus-stmicroelectronics.pdfhttps://www.st.com/resource/en/application_note/dm00087990-design-with-surface-sensors-for-touch-sensing-applications-on-mcus-stmicroelectronics.pdf)

## About this template
* Customize it to make it work for you!

* Releases: when you get a new version of your board made, create a release tag with:
    * gerber files
    * Schematic and board in pdf
    * assembly file/instructions
    * Bill of Materials
    * release notes.

* the ```.gitignore``` file: when you design a board, your EDA software will probably generate a bunch of files that you don't want/need to sync up or share. If you include these files in the ```.gitignore``` they won't be synced. The sample ```.gitignore``` in this repository covers both Altium and Eagle designs. You can customize it to fit your development environment

* the assets folder: this is where you can save images or other assets you want to reference in your ```README``` documents.

* if you want to try visual diff tools on platforms like Cadlab, Inventhub or Allspice etc. you can always mirror your repository instead of migrating it completely

* this example repository only stores EE files. You could keep related firmware in this repository too or keep them separate. It's up to you.
