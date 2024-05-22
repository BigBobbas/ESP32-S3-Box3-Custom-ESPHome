# How to install
1. Download and unzip the neccessary files from here INSERT LINK
2. Delete the existing device from the HomeAsssistant ESPHome integration in HA >> Settings >> device & services >> ESPHome - click on the 3 dot menu next to the device name and select delete.
3. Open sb3.yaml from the zipped download and copy the entire contents too your clipboard.
4. Open your existing device config in your ESPHome installation either dashboard or editor of your choice.
5. Select the entire contents of the existing config and paste in the new config to overwrite everything in the file.
6. click 'save' and then install - select 'wirelessly' if your device is already up and runnning with the 'stock' firmware.  Once compiling has finished and the created firmware is uploaded to the device you can then re-add it to the ESPHome integration. HomeAssistant may detect this automatically, alternatively you can manually add the device in the integration. To do this you will need the ip address assigned to the device by your router. This will be shown in the ESPHome device logs after compiling or you can obtain this from your router.
if neither are working, open the device from
