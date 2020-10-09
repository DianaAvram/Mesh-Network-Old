# Mesh-Network

# Notification_via_Mesh_Network

This project contains explanations and the necessesary code, in order to run a notification alarm system on the phone, propagated via a mesh system. 
The end devices are the phone and an alarm trigger. The communication is done using 2 Nordic Thingy:52 boards and one nRF52840 DK, using Bluetooth 5.

For more information about Bluetooth five, please check: [Bluetooth-5-short](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/Bluetooth-5) (on-short), respectively [Bluetooth-5-specs](https://www.bluetooth.com/specifications/bluetooth-core-specification/) (long version specifications) 

Steps on how this project was structured:   
1. Run a mesh network - on the Nordic Thingy:52 boards -  following: [Thingy Mesh Demo](https://github.com/NordicPlayground/thingy52-mesh-provisioning-demo) 
2. Run a mesh network - on the Nordic nRF52840 DK- following: [Light switch Demo](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.meshsdk.v2.2.0%2Fmd_examples_light_switch_README.html) 
3. Run the fire alarm notification - on the Nordic nRF52840 DK - starting from the Blinky example: [BLE Blinky Application](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.sdk5.v15.0.0%2Fble_sdk_app_blinky.html) 
4. Load the notification application - on a Android phone - with base code from: [Blinky Android Application](https://github.com/NordicSemiconductor/Android-nRF-Blinky) 
------------------------------------------------------------------------------------------------------------------------
Next steps:\
5. Combine the mesh infrastructure with the Blinky Application - try: [Integrating Mesh into nRF5 SDK examples](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.meshsdk.v4.2.0%2Fmd_doc_user_guide_integrating_mesh_nrf5_sdk.html) - not sucessful yet \
6. Run the application sucessfully on the phone - to be continued 


 >Step 5 detailed

This  tutorial needs to be followed: [Integrating Mesh into nRF5 SDK examples](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.meshsdk.v4.2.0%2Fmd_doc_user_guide_integrating_mesh_nrf5_sdk.html)\
More specifically, there are 3 main steps, which are detailed below. \
The project is in the following folder: \nRF5_SDK_1530\examples\ble_peripheral\ble_app_blinky\pca10056\s140\ses 
### Step 1 Including the source files from nRF5 SDK for Mesh in the nRF5 SDK example's project file.
 The source files can be added directly, in the project explorer. This video on youtube explains how this can be done in SES:
 [SEGGER Embedded Studio - Importing files and drivers](https://www.youtube.com/watch?v=t-kh1EbesvI&list=PLx_tBuQ_KSqGHmzdEL2GWEOeix-S5rgTV&index=7&t=0s). [1]
### Step 2 Adding the folders to the project include path of the nRF5 SDK example
 This can be done from SES options in the following way: 
 1. Right-click on your project -> "Options"
 2. In the upper left corner in the drop-down box, change from "Debug"/"Release" to "Common"
 3. Under "Code"-> "Preprocessor"
 4. Choose "User Include Directories" and add the path here
### Step 3 Add the preprocessor symbols to the project file of the nRF5 SDK example
In the menu described in the previous step, go to "Code"-> "Preprocessor" -> "Preprocessor Definitions" and add those three symbols

 ### UPDATE 17.09.2020 ###  
#### New approach #1:  ####
- Instead of trying to combine the mesh and SDK, try to understand the already made example	SDK UART coexistence example
- From <https://infocenter.nordicsemi.com/topic/com.nordic.infocenter.meshsdk.v3.2.0/md_examples_sdk_coexist_ble_app_uart_coexist_README.html?cp=5_2_3_5_1> \
  - does not work as expected \
  - More  specifically, it does advertise (can see on the phone), but the LED does not function accordingly. And putty does not work\
  - LED problem solved: it's pca10040 instead of pca10056!!!  :-) \
#### New approach #2: ####
- UART/Serial Port Emulation over BLE   - single version (no combination)\
- From <https://infocenter.nordicsemi.com/topic/com.nordic.infocenter.sdk5.v15.3.0/ble_sdk_app_nus_eval.html> \
  - LED and putty work OK \
  - however, the TX characteristic cannot be successfully written from the phone - TBD why \
  - issue is opened under: https://devzone.nordicsemi.com/f/nordic-q-a/66051/uart-serial-port-emulation-over-ble-problem \
  - problem with putty partially solved: connect from SES, then open putty, set baud rate 115200, then flash the code. \
  -  work in progress
 ### UPDATE 08.10.2020 ###  
 - It looks like the combined version needs provisioning with the help of an additional development board (not via the phone)
 - Therefore, we plan to use 1 x nRF52833 and 2 x nRF52840
 - Problem: the  nRF52833 code is in a newer version of Mesh SDK. And combining it with the SDK v15.3 is problematic 
 - Next step: try SDK Mesh 4.2.0 with newer version of SDK - confirm that SDK Mesh 4.2.0 requires some files (e.g. ble.h) and some modifications in current files. These modif. have been added in nRF5 SDK v16.0.0. 
 - Next step: : try SDK Mesh 4.2.0 & nRF5 SDK v16.0.0. 


Remarks:\
[1] If you experience problems with CMSIS Configuration at this step, please follow these explanations on youtube: [SEGGER Embedded Studio - CMSIS Configuration Wizard](https://www.youtube.com/watch?v=b0MxWaAjMco&list=PLx_tBuQ_KSqGHmzdEL2GWEOeix-S5rgTV&index=4).



