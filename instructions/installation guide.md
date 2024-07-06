# Installation
What you will need.
* Esp32-S3-Box-3 with sensor dock
* USB C data cable
* Home Assistant 
* ESPHome Add-on Dashboard
  
What will happen?
* an initial firmware will be loaded to the device
* you configure your wifi
* you connect to your network and add the device to Home Assistant
* you import the full working config into the ESPHome dashboard and finally upload this to the device.
  
How do I do it?
#### If you have set your device up previously in Home Assistant and ESPHome dashboard then it is best to remove these as they can cause the installation not to go as described. Make sure to delete any related devices from the ESPHome integration in Home Assistant>> Devices & Services >> ESPHome. Also delete any entries in the ESPHome dashboard, by clicking on the 3 dot menu on the device card followed by delete.

1. plug your S3box into your computer then right click this link <a href="https://support.bbdl.co.uk" target="_blank">S3 Box installation page.</a>and open in a new window or tab, to allow you to flip between the instructions and the installation page.
2. Click the blue CONNECT button.
3. Now select your COM Port and connect. You should see a box similar to the screenshot below.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/a76dfaba-fe8b-4b92-9597-a51a4ee905be) <br>
4. Click to install and confirm<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/b6476825-46c7-4190-80ea-8ece0d6b5505) <br>
5. The device screen will turn blank during the initial firmware flash, once the install is complete click next.<br>
6. Your S3Box should now be prompting to SETUP WIFI. click next on your computer,<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/4805b9ac-e056-4c22-9028-7769d59162e7)<br>
then configure your wifi.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/26df24c1-3a1e-468d-9f91-c909384bb7b8)<br>

7. After Wifi is connected, you now need to add the device to Home Assistant.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/90870960-1475-438a-8433-3e390a21e7ac)<br>

You should have a link on your computer screen. If this doesn't appear, you can add the device manually. To add manually, in Home Assistant go to Settings >> Devices & Services >> ESPHome (right arrow) >> at the bottom of the list of devices click 'add device'. You will be prompted for a host: you can use either the IP address or hostname displayed on the S3Box screen.<br>

8. Once the device is added to the integration as per step 8. you need to adopt the device into the ESPHome dashboard. This will pull down a full config for you to customise and add your own entities etc. Once this is imported to the dashboard it then needs to do one final install to the S3Box and then setup is complete. Open your ESPHome dashboard and you should have a new card appeared that looks like the image below.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/c7ae7cb1-f59d-4964-a971-edcd785051d9)<br>

Click Adopt, followed by install. To avoid any complications at this point do not change the name of the device, you can always change the name once you know everything is working.<br>If you do not have a new card in the dashboard then try restarting your ESPHome add-on. If that fails, you can manually create a new card and copy in the config from [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/s3b.yaml>) you can select any board it doesn't matter as you are going to overwrite everything in a few clicks. DO NOT click INSTALL when the API Key is shown, CLICK SKIP. Then in the new card copy and paste the full config from the link above. Click Save then Install.
## NOTE:<br>
> The final installation will take some time and ideally requires 8gb of ram to compile comfortably. It is a little hit and miss with lower resources if this will compile without issues, it all depends on the hardware that you are running ESPHome on it's always worth a try ;). You will need the resources to compile and install the full config at least once. Subsequent compiles shouldn't require a full compile unless changes are made to components: in the config, adding entities and display changes shouldn't require a full compile so in theory, compile will be much faster, and requires less resource. (famous last words ;) ) <br>
EDIT:
> adding the line below to the `esphome:` component at the top of the config can help to compile on machines with lower available resources.. however this may increase the compile time further. But worth trying for sure.
```yaml
esphome:
  compile_process_limit: 1
```

Hopefully you now have the S3box configured with the template firmware. For a guide on how to personalise the device to suit you. [Click Here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/make%20it%20your%20own.md>)





















