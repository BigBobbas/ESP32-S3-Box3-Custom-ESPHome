# Installation
What you will need.
* Esp32-S3-Box-3 with sensor dock
* 18650 battery
* USB C cable
* Home Assistant 
* ESPHome Add-on Dashboard
  
What will happen?
* an initial firmware will be loaded to the device
* you configure your wifi
* you connect to your network and add the device to Home Assistant
* you import the full working config into the ESPHome dashboard and finally upload this to the device.
  
How do I do it?
1. if you have set your device up previously in Home Assistant and ESPHome dashboard then it is best to remove these as they can cause the installation not to go as described. Make sure to delete any related devices from the ESPHome integration in Home Assistant>> Devices & Services >> ESPHome. Also delete any entries in the ESPHome dashboard, by clicking on the 3 dot menu on the device card followed by delete.
2. plug your S3box into your computer then right click this link <a href="https://support.bbdl.co.uk" target="_blank">S3 Box installation page.</a>and open in a new window or tab, to allow you to flip between the instructions and the installation page.
3. Click the blue CONNECT button.
4. Now select your COM Port and connect. You should see a box similar to the screenshot below.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/a76dfaba-fe8b-4b92-9597-a51a4ee905be) <br>
5. Click to install and confirm<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/b6476825-46c7-4190-80ea-8ece0d6b5505) <br>
6. The device screen will turn blank during the initial firmware flash, once the install is complete click next.<br>
7. Your S3Box should now be prompting to SETUP WIFI. click next on your computer,<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/4805b9ac-e056-4c22-9028-7769d59162e7)<br>
then configure your wifi.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/26df24c1-3a1e-468d-9f91-c909384bb7b8)<br>

8. After Wifi is connected, you now need to add the device to Home Assistant.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/90870960-1475-438a-8433-3e390a21e7ac)<br>

You should have a link on your computer screen. If this doesn't appear, you can add the device manually. To add manually, in Home Assistant go to Settings >> Devices & Services >> ESPHome (right arrow) >> at the bottom of the list of devices click 'add device'. You will be prompted for a host: you can use either the IP address or hostname displayed on the S3Box screen.<br>

9. Once the device is added to the integration as per step 8. you need to adopt the device into the ESPHome dashboard. This will pull down a full config for you to customise and add your own entities etc. Once this is imported to the dashboard it then needs to do one final install to the S3Box and then setup is complete.




















