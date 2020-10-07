Here is an explanation on how this code runs and how to make it run on the Nordic device:

Documentation on how to successfully run examples on Thingy:52 devices


HARDWARE NEEDED: 2 x Thingy:52, 1 x nRF52840 Board, 1 x micro USB cable, 1 x  10-pin 2x5 Socket-Socket 1.27mm IDC (SWD) Cable, 1 x smartphone 

The HW setup is the following:
[PC] ----micro USB----[nRF52840]----SWD cable----[Thingy:52]

SOFTWARE NEEDED:
- The PC needs to have Segger Embedded Studio installed (I used the version Embedded Studio for ARM, Windows, 64-bit)
- In Segger Embedded Studio, steps 8 and 9 from this link https://github.com/NordicPlayground/thingy52-mesh-provisioning-demo need to be followed. However, Step 9 is not so well explained, so I will explain it in more detail later
- The phone needs to have the following apps installed:
** Nordic Thingy - https://play.google.com/store/apps/details?id=no.nordicsemi.android.nrfthingy&hl=en_US 
** nRF Mesh 

Remarks:
- No HW modifications need to be made to the  nRF52840 board or to the Thingy:52 in the beginning (e.g. no jumpers).
- The nRF52840 will be supplied from the cable (alternatively, it may also use the battery)
- The Thingy:52 boards are always supplied just from the battery. Connecting the SWD cable, the battery will charge

Initial Steps, to run the default SW on Thingy:
- For this step, the Thingy:52’s can run just on battery – no cable needed
- The Thingy:52 devices come with a default firmware installed. This may be used in order to interact with the board for the first time and check its functionalities. For this, the Nordic Thingy Application needs to be downloaded on the smartphone.
- Afterwards, turn on the Thingy:52’s – there is a small switch on the bottom left side. Now, the Thingy:52 will start to advertise 
- Next, activate Bluetooth and location from your phone and enter the Nordic Thingy Application. Now, your phone will be looking for available devices, to connect to
- From now on, you should be able to connect to each new Thingy, give them names and discover all its sensors data in real time.
-----------------------insert photo here------------------------------------------
- All this information is kept after turning off the Thingy’s. To erase the firmware, please have a look at the next steps

Next Steps, to run the Mesh Software, on Thingy:52:
- After discovering the Thingy:52 features,  the Mesh firmware can be loaded into the boards, so that they can participate in a Mesh network. This will give the user the possibility of assigning the boards different individual or group addresses, so that controlling multiple Thingy’s from the phone can be achieved easily

-To achieve this, the Thingy:52 devices need to be erased of this initial firmware and loaded with a new one. For this, the mentioned tutorial in the link shall be followed: https://github.com/NordicPlayground/thingy52-mesh-provisioning-demo 
- As I mentioned in the the HW setup part, the way to load the code on Thingy’s is via the SWD cable.

Additions to the already mentioned steps are the following:

Step 5. Clone this repo into \examples\ --> it refers to nrf5_SDK_for_Mesh_v320\examples
Step 9: The following needs to be done from Segger Options:






Last thoughts:
- After successfully completing the steps and loading the code on the Thingys, their provisioning needs to be made, from the phone. That is, assigning them with addresses. This is done using the nRF Mesh App, available here: https://play.google.com/store/apps/details?id=no.nordicsemi.android.nrfmeshprovisioner&hl=de
- And here is an video example on how the addresses can be assigned from the phone, to achieve a Light Switch – Light Bulb(s) scenario: https://www.youtube.com/watch?v=XthbU9NP0Yg
- Finally, the boars are loaded with a Client – Server model. Depending on the addresses assignment from the nRF Mesh App, some boards can act as a switch (publisher) and the other(s) as light bulb (subscriber, client).
- Bonus: by having a look in the C code, we may notice that the relay feature is enabled. So now, if we wish to have an end-to-end communication over multiple Thingy’s as hops, this software enables messages forwarding through them. 
