# Flashing firmware

!!! Tip annotate "Note" 
    When flashing new firmware make sure you disconnect power connection and uart connection.


   |   |   Needed hardware
    ---- | ---- 
    You can change all variables using UART and CAN so flashing firmware a lot is not necessary<br /> You will usually flash it when:<br />  1. New version of Spectral BLDC firmware is available <br />2. You are doing custom code developement <br /> 3. You are using SimpleFOC firmware | You will need programming adapter from [here!](https://source-robotics.com/products/jtag-programming-adapter-1-27-pitch?variant=47293352903004) <p align="left"> <img src="../assets/ADAPTER.jpg" alt="drawing" width="600"/> <br /> </p>


## **Connecting to PCB**


=== "Using [Adapter](https://source-robotics.com/products/jtag-programming-adapter-1-27-pitch?variant=47293352903004) "

    Step 1 | Step 2
    ---- | ---- 
    Locate JTAG PINS | Press programming adapter like shown in the picture (apply small amount of pressure on the pins to get a good contact)
    <p align="left"> <img src="../assets/JTAG_PINS.PNG" alt="drawing" width="750"/> <br /> </p> | <p align="left"> <img src="../assets/FLASHING2.PNG" alt="drawing" width="500"/> <br /> </p> 


## **Flashing using visual studio code**
Download visual studio code: [Link](https://code.visualstudio.com/download)<br />

1. Open [Spectral BLDC firmware](https://github.com/PCrnjak/Spectral-Micro-BLDC-controller/tree/main/Spectral%20BLDC%20Firmware) folder in VS code. (You need to have platformio installed)
2. Press uplaod in VS code (Bottom left corner in VS code)
<p align="left"> <img src="../assets/VSUPLOAD.png" alt="drawing" width="800"/> <br /> </p>


## **Flashing using STM32 ST-LINK Utility**
Download STM32 ST-LINK utility [Link](https://www.st.com/en/development-tools/stsw-link004.html)

!!! Note annotate "HEX and binaries" 
    Using STM32 ST-LINK Utility you can flash only Binary or HEX files. These can be obtained from compiling source code of spectral BLDC firmware

**Open STM32 ST-LINK utility Drag and drop the [binary file](https://github.com/PCrnjak/Spectral-Micro-BLDC-controller/tree/main/Binaries) inside.**

<p align="left"> <img src="../assets/stlink2.PNG" alt="drawing" width="700"/> <br /> </p>

**Go to Target/settings and make sure they look like this.**

<p align="left"> <img src="../assets/stlink1.PNG" alt="drawing" width="700"/> <br /> </p>

**Go to Target/connect. In case you get a error try to install stlink drivers from [here!](https://www.st.com/en/development-tools/stsw-link009.html)**

<p align="left"> <img src="../assets/stlink_conn.png" alt="drawing" width="700"/> <br /> </p>

**Go to Target/program and verify. You should get pink output msg like below.**

<p align="left"> <img src="../assets/stlink_prog.png" alt="drawing" width="700"/> <br /> </p>







