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

        * HR05 - external-connected LED strip shall be used for command emission indication.<br>
        The LED strip will quickly flash simultaneously as the control command sent out via MQTT to the cloud, imitating the laser emission process.

        * HR06 - external-connceted vibration motor drived by DRV2605L haptic motor controller shall be used for actuator execution feedback.<br>
        The vibration motor will funtion as a feedback reponse to different actuators' actions. For instance, the motor would be drived to vibrate in different frequencies accoring to the motor rotation speeds.
        

    <br>

    * <u><i>Acuator PCBA:</i></u>
        * HR07 - project shall be based on SAMW25 core.

        * HR08 - mounted state LED shall be used to reflect the state of the actuator. <br>
        If there is no control demand, the state LED maintains off; vice versa, the state LED will be turned on until the task execution.

        * HR09 - external-connected gearmotor drived by DRV8874 motor driver shall be used as one of the actuator.<br>
        The motor will be drived to execuate the wand command, such as swipe up to increase the rotation speed, swipe down to decrease the rotation, etc.

        * HR010 - external-connected LCD shall be used as the other actuator.<br>
        The LCD would have two function modes, one is the visulization of motor control, which would reflect the motion state of the motor, such as, as the rotation speed increase, the LCD will display volume up animation.<br>
        In addition, the LCD would solely interact with the magic wand, such as the LCD will animate a twinkle with respect to wand 'Zigzag' tranjectory gesture.


<br><br>

* <b><i>SRS:</i></b>
    * SR01 - slide switch on/off.<br>
        - programmed state machine controlling the entire state(ON/OFF) of the system.
    * SR02 - strain/stress based user detection.<br>
        - a strain/stress sensor will be used to detect the use condition of the wand:
            - if no strain/stress detected, the wand is a common stick used for fun;
            - if strain/stress detected, the wand is utilized as our proposed "magic wand".
    * SR03 - IMU-based gesture recognition.<br>
        - a 6-axis/9-axis IMU will be used for collecting data when the user touches the sensing area of the strain/stress sensor until no strain/stress detected at that area or stopping swinging of the wand;
        - the collected data will be used for the recognition of gesture of the wand, and then send out the correspoding control demand to the cloud.
    * SR04 - LED strip based command emission.<br>
        - a LED strip will be programmed to flash simultaneously when the control demand is sent out after correct gesture recogonition.
    * SR05 - vibration motor based actuator exection feedback.<br>
        - a vibration motor will be activated for about few seconds once the control demand has been successfully received and executed by the actuator.
    * SR06 - actuartor execution.
        - the corresponding actuator(determined by the pre-defined gestures) will response to the magic wand instruction, execute the command and send feedback to the cloud to actiavte the vibration motor on the wand;<br>
        a state LED will change its color corresponded to the actuator state, for instance,
            - green: actuator in standby;
            - red: actuator in execution.



<br>


<b><i>2. Block diagram is shown below.</i></b>



<b><i>3. Flowchart illusatrations are shown below.</i></b>


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