# CAN interface


CAN bus should be your primary choice when developing robotic aplication. <br />
Spectral micro uses 5V CAN bus that adheres to the CAN 2.0 standard. Each Spectral micro has 2 CAN bus connectors allowing you to easily daisy chain multiple devices. 


<p align="left"> <img src="../assets/CANID.PNG" alt="drawing" width="700"/> <br /> </p>


Bits **10 - 7** of CAN ID represent Node ID. <br />
Node IDs can range from 0 - 15 Meaning you can have maximum 16 different devices on one CAN bus.<br />

Bits **6 - 1** of the CAN ID represent Command ID.<br />
Command IDs can range from 0 - 63.

Bit **0** represents error bit. If spectral micro BLDC controller has any active error this bit will be set to 1.

Node with smallest Node ID is strongest in CAN bus arbitration.

If you want to learn more about CAN bus we recommend you read this [article!]()

## **List of commands**

!!! Tip annotate "**Messages prefixed with Send are messages that the host can send to the Spectral BLDC controller.**" 
!!! Note annotate "**Messages prefixed with Respond  are messages that the Spectral BLDC controller can send to the host.**" 
!!! Danger annotate "** Messages prefixed with Send_Respond are messages that host can request from BLDC controller and it will respond with the desired data packet with the same Command ID as recived command. Host is sending these msgs with RTR bit and Spectral is responding with RTR 0 and some data packet. **" 


 Command ID | Name | Type | Data 
---- | ---- | ---- | ---- 
9 | `Respond_Heartbeat` | Respond | None 
3 | `Respond_data_pack_1` | Respond | Position [Encoder ticks] <br /> Velocity [Encoder ticks/s] <br /> Current [mA]
5 | `Respond_data_pack_2` | Respond | Data 
7 | `Respond_data_pack_3`| Respond | Data 
60 | `Respond_Gripper_data_pack` | Respond | Position  <br /> Current <br /> Gripper activation status <br /> Gripper action status <br /> Object detection status  <br /> Temperature error <br /> Timeour error <br /> Estop error <br /> Calibration status


 Command ID | Name | Type | Data 
---- | ---- | ---- | ----
2 | `Send_data_pack_1` | Send | Position [Encoder ticks] <br /> Velocity [Encoder ticks/s] <br /> Current [mA]
6 | `Send_data_pack_2` | Send | Data
8 | `Send_data_pack_3` | Send | Data
4 | `Send_data_pack_PD` | Send  |Position [Encoder ticks] <br /> Velocity [Encoder ticks/s] <br /> Current [mA]
61 | `Send_gripper_data_pack` | Send | Position  <br /> Velocity  <br /> Current [mA]  <br /> Gripper activation  <br /> Gripper action <br /> Estop status <br /> Release direction
62 | `Send_gripper_calibrate` | Send | None
16 | `Send_PD_Gains` | Send | KP <br /> KD
17 | `Send_Current_Gains` | Send | Kpiq <br /> Kiiq 
18  | `Send_Velocity_Gains` | Send |Kpv <br /> Kiv 
19 | `Send_Position_Gains` | Send | Kpp
20 | `Send_Limits` | Send | Velocity limit <br /> Current limit
22 | `Send_Kt` | Send | Kt 
11 | `Send_CAN_ID` | Send | CAN ID
0 | `Send_ESTOP` | Send | None
12 | `Send_Idle` | Send | None
13 | `Send_Save_config` | Send | None
14 | `Send_Reset` | Send | None
1 | `Send_Clear_Error` | Send | None
15 | `Send_Watchdog` | Send | Time <br /> Action
30 | `Send_Heartbeat_Setup` | Send | Time
29 | `Send_Cyclic_command` | Send | Data

 Command ID | Name | Type | Respond data 
---- | ---- | ----  | ---- 
23 |`Send_Respond_Temperature` | Send/Respond | Temperature
24 |`Send_Respond_Voltage` | Send/Respond | Vbus voltage
25 |`Send_Respond_Device_Info` | Send/Respond | Serial number <br /> Hardware version <br /> Batch date <br /> software version
26 |`Send_Respond_State_of_Errors` | Send/Respond | Error <br /> Temperature error <br /> Encoder error <br /> Vbus error <br /> Driver error <br /> Velocity error <br /> Current error <br /> ESTOP error <br /> Calibration status <br /> Activated status <br /> Watchdog error 
27 |`Send_Respond_Iq_data` | Send/Respond | Iq current
28 |`Send_Respond_Encoder_data` | Send/Respond | Position [Encoder ticks] <br /> Velocity [Encoder ticks/s]
10 |`Send_Respond_Ping` | Send/Respond | None

## **Watchdog**

**By default watchdog is turned off.**<br />
Each valid CAN message received by the spectral BLDC resets its watchdog timer.<br />
Watchdog measures time between the commands that spectral BLDC receives.<br />
If it is bigger than time you set it will report Watchdog error and go to error mode.
To clear the error you will need to call:

    "Send_Clear_Error"



## **Heartbeat**
**By default heartbeat will send data at 1Hz or every 1 second.**<br />
Hearbeat is function that will Send "Respond_Heartbeat" msg every time interval you set in "Send_Heartbeat_Setup". <br />
This is usefull when your host device needs to see if spectral BLDC is connected/alive. <br />
In case your spectral BLDC sends any other data (as a response to command) it will reset its heartbeat timer.

!!! Tip annotate "**Heartbeat timer reset**" 
    For example if spectral BLDC is sending data every 10ms and heartbeat is setup to send every 1s; hearbeat will never send its data. 

## **Cyclic**
**TODO**


## **Detailed explanation of commands**


### **Respond_Heartbeat**

### **Respond_data_pack_1**

### **Respond_data_pack_2**

### **Respond_data_pack_3**

### **Respond_Gripper_data_pack**

### **Send_data_pack_1**

### **Send_data_pack_2**

### **Send_data_pack_3**

### **Send_data_pack_PD**

### **Send_gripper_data_pack**

### **Send_gripper_calibrate**

### **Send_PD_Gains**

### **Send_Current_Gains**

### **Send_Velocity_Gains**

### **Send_Position_Gains**

### **Send_Limits**

### **Send_Kt**

### **Send_CAN_ID**

### **Send_ESTOP**

### **Send_Idle**

### **Send_Save_config**

### **Send_Reset**

### **Send_Clear_Error**

### **Send_Watchdog**

### **Send_Heartbeat_Setup**

### **Send_Cyclic_command**

### **Send_Respond_Temperature**

### **Send_Respond_Voltage**

### **Send_Respond_Device_Info**

### **Send_Respond_State_of_Errors**

### **Send_Respond_Iq_data**

### **Send_Respond_Encoder_data	**

### **Send_Respond_Ping**


