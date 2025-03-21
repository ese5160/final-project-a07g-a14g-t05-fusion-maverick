# a07g-exploring-the-CLI

* Team Number: T05
* Team Name: Fusion Maverick
* Team Members: Qingyang Xu, Ruizhe Wang, Xinyi Wang
* GitHub Repository URL: https://github.com/ese5160/final-project-a07g-a14g-t05-fusion-maverick.git
* Description of test hardware: (development boards, sensors, actuators, laptop + OS, etc)

<br>


## 1. Software Architecture
<b><i>1. Updated HRS & SRS are elaborated below.</i></b>
* <b><i>HRS:</i></b>
    * <u><i>Magic Wand PCBA:</i></u>
        * HR01 - project shall be based on SAMW25 core.

        * HR02 - external-connected slide switch shall be used for activation of the wand.

        * HR03 - external-connected Force-Sensitive Resistor(FSR) Interlink Model 402 shall be used for for command detection. <br>
        The sensor will detect if continuous force exerted in the sensing area, as a start flag and maintaining state for the wand gesture recognition.

        * HR04 - mounted 6-axis IMU MPU6500 shall be used for for wand gesture recognition. <br>
        The sensor will collect 6-axis data(3-axis gyroscope and 3-axis accelerometer) while the FSR sensing area is continuously pressed.<br>
        The collected data shall be then used to recognize the swing trajectory of the wand for gesture recognition.
        The tentative way we've designed for gestures are:<br>
        gesture 1: Wave tilde---LCD image 1;<br>
        gesture 2: Zigzag---LCD image 2;<br>
        gesture 3: Clockwise circle---Turn on the motor;<br>
        gesture 4: Swipe up---Speed up the motor and LCD shows related image 3;<br>
        gesture 5: Swipe down---Slow down the motor and LCD shows related image 4;<br>
        gesture 6: Anticlockwise circle---Turn off the motor;

        * HR05 - external-connected LED strip shall be used for command emission indication.<br>
        The LED strip will quickly flash simultaneously as the control command sent out via MQTT to the cloud, imitating the laser emission process.

        * HR06 - external-connceted vibration motor drived by DRV2605L haptic motor controller shall be used for actuator execution feedback.<br>
        The vibration motor will funtion as a feedback reponse to different actuators' actions. The tentative way we're going to execute it is:
        <br>
        LCD tasks---Vibration Motor soft fuzz 60%;<br>
        Motor speed up task---Vibration Motor short double click2-80%;<br>
        Motor slow down task---Vibration Motor medium click2-80%;<br>

        

    <br>

    * <u><i>Acuator PCBA:</i></u>
        * HR07 - project shall be based on SAMW25 core.

        * HR08 - mounted state LED shall be used to reflect the state of the actuator. <br>
        If there is no control demand, the state LED maintains off; vice versa, the state LED will be turned on when instruction send until the task execution.

        * HR09 - external-connected gearmotor drived by DRV8874 motor driver shall be used as one of the actuator.<br>
        The motor will be drived to execuate the wand command. Such as clockwise to turn on, swipe up to increase the rotation speed, swipe down to decrease the rotation, and anticlockwise to turn off.

        * HR010 - external-connected LCD shall be used as the other actuator.<br>
        The LCD would have two function modes, one is the visulization of motor control, which would reflect the motion state of the motor, such as, as the rotation speed increase, the LCD will display volume up animation.<br>
        In addition, the LCD would solely interact with the magic wand, such as the LCD will antimate a wave pattern when wand has a 'Tilde' tranjectory gesture, and animate a twinkle with respect to wand 'Zigzag' tranjectory gesture.


<br><br>

* <b><i>SRS:</i></b>
    * SR01 - slide switch on/off.<br>
        - configured as an external interrupt;
        - programmed state machine controlling the entire state(ON/OFF) of the system.
    
    <br>

    * SR02 - FSR based command detection.<br>
        - configured as an external interrupt;
        - a FSR will be used to monitor the use condition of the wand:
            - if no strain/stress detected(<b><i>logic 'high'</i></b>), the wand is a common stick used for fun;
            - if concontinuous strain/stress detected(<b><i>logic 'low'</i></b>), the wand is utilized as our proposed "magic wand".

    <br>

    * SR03 - IMU-based gesture recognition.<br>
        - configued as a SPI(SERCOM0) + one external interrupt;
        - the 6-axis IMU MPU6500 will be used for collecting data when the user touches the sensing area of the strain/stress sensor until no strain/stress detected at that area or stopping swinging of the wand;<br>
        the collected data will be used for the recognition of trajectory gestures of the wand, and then send out the correspoding control demand to the cloud.

    <br>

    * SR04 - LED strip based command emission.<br>
        - configued as a digital output;
        - a LED strip will be programmed to flash simultaneously when the control demand is sent out after correct gesture recogonition.<br>
        Neopixel library will be utilized for this implmentation.

    <br>


    * SR05 - actuartor execution.
        - the corresponding actuator(determined by the pre-defined gestures) will response to the magic wand instruction, execute the command and send feedback to the cloud to actiavte the vibration motor on the wand;<br>
            * state LED: keep off while no command, turned on when received the command and turned off when the tasks are successfully executed.
            * motor:
                * activation: clockwise circle drawn by the wand;
                * brake: anticlockwise circle drawn by the wand;
                * accelerate: wand swipes up;
                * decelerate: wand swipes down.
            * LCD:
                * mode 1: visulization of motor motion state:
                    * motor accelerates: volume up animation;
                    * motor decelerates: volume down animation.
                * mode 2: intaction with wand:<br>
                the LCD would solely interact with the wand. For instance, the LCD will animate a twinkle with respect to wand 'Zigzag' tranjectory gesture.
        

    


    * SR05 - vibration motor based actuator exection feedback.<br>
        - a vibration motor will be activated for about few seconds once the control demand has been successfully received and executed by the actuator.



<br>


<b><i>2. Block diagram is shown below.</i></b>
![Block_diagram1](A07G_images/Block_diagram1.jpg)
![Block_diagram2](A07G_images/Block_diagram2.jpg)

<b><i>3. Flowchart illusatrations are shown below.</i></b>
![Flow_Chart](A07G_images/Flow_Chart.jpg)

## 2. Understanding the Starter Code


<br>

## 3. Debug Logger Module 



<br>

## 4. Wiretap the convo!




<br>

## 5. Complete the CLI




<br>

## 6. Add CLI commands




<br>

## 7. Using Percepio