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
