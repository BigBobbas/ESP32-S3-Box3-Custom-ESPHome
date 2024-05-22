# How to install
1. Download and unzip the files from here [here](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/s3b.zip) clicking the icon shown in the screenshot below , circled in red.
   ![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/5fff9caf-415b-48c1-865d-61fc38c3a6e3)

   
3. Copy the images and fonts folders to your config/esphome folder using Samba share add-on. If the folders already exist then copy the contents of both folder from the zip and paste them into the existing corresponding config/esphome/images and config/esphome/fonts folders.
   
4. Delete the existing device from the HomeAsssistant ESPHome integration in HA >> Settings >> Devices & Services >> ESPHome - click on the 3 dot menu next to the device name and select delete.
   
5. Open sb3.yaml from the zipped download and copy the entire contents to your clipboard.
   
6. Open your existing device config in your ESPHome installation either dashboard or editor of your choice.
   
7. Select the entire contents of the existing config and paste in the new config to overwrite everything in the file.
   
8. click 'save' and then install - select 'wirelessly' if your device is already up and runnning with the 'stock' firmware.  Once compiling has finished and the created firmware is uploaded to the device you can then re-add it to the ESPHome integration. HomeAssistant may detect this automatically, alternatively you can manually add the device in the integration. To do this you will need the ip address assigned to the device by your router. This will be shown in the ESPHome device logs after compiling or you can obtain this from your router.
Once the device is added to the integration, open the device from the integration and press the 'reboot' button, under the Configuration section.
After rebooting, test functionality of the touch screen and Voice Assistant, if Voice isn't working then go to the next steps. if everything is working then thats the installation complete and you can move on to the 'make it your own' guide [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/make%20it%20your%20own.md>)

9. Voice is not working after initial install - The next steps are required if voice and touch are not both functioning.

   1. You will need to comment out parts of the config as shown in the screenshots below. To comment a block of yaml, click and drag down to highlight the block to comment out then press ctrl & / (control and forward slash) . eachline should then be prefixed with a # and the block should change colour (green if using ESPHome add-on dashboard)
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/0552c1a6-7ca1-4064-bb66-bc8b5b76ea8c)<br>
The line below is in a lambda and requires a different way to comment out. this is simply by placing 2 forward slashes at the start of the text.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/6fae229c-a35b-452b-a291-2b7e7ec573ff)<br>
now highlight everything including the i2c: line all the way to the end of the config and also comment this out , there will be many lines!<br> 
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/e0152499-6d50-4842-a343-f0a71fd448a7)<br><br>

Once everything has been commented out, click save and exit the editor. Now from the device card in the dashboard click on the 3 dot menu , followed by 'clean build files' <br><br>
  2. Once the dialogue says done! click install and select wirelessly.<br><br>
  3. After the firmware has uploaded the device will restart. Touch will not function and we just need at this point to check that Voice Assistant is working, assuming all is good at this point. it's now time to do the final steps.<br><br>
  4. Open the device config once more in the editor from the dashboard. you now need to un-comment all of the lines that you commented out in the steps above. simply repeat the above steps 1 & 2 (pressing ctrl & / will also remove commented blocks when highlighted) make sure to follow all of the steps including 'clean build files'<br><br>
  5. Once the firmware has uploaded and the device rebooted test the touch and voice both work, if touch isn't working at this point, go to the device in the ESPHome integration and press the reboot button. Once the device reboots that should now be everything complete and voice and touch should be working. 
you can now move on to making the device your own , by controlling your own entities and importing values from your sensors you can follow this guide 'make it your own' guide [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/make%20it%20your%20own.md>)














