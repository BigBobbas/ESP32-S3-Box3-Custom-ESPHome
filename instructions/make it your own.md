## Making it your own.
The ESP32-S3-Box-3 is not just a voice assistant. In the following guide I will detail how you can make it your own and customise the device, giving you control over your other HomeAssistant devices and display sensor values and much more.
<br><br>
The following guide will cover these topics.
* Customise the voice assistant.
   * setting your own display images for the Voice Assistant process.
   * Changing the on-device (micro wake word) wake word.
   * Divert audio responses to other media players.
   * Add a wake word detected response sound either local to the device or to another media player.
<br><br>
* Add entities to the touch buttons
* Add sensors to display the values on the screen
* Change the displayed icons
* Change the icon colours
* Add pages
* Change background colour and or image
* Change the function of the home button and the top left button<br><br><br>

## Customising Voice Assistant.
### Changing displayed images
in order to do this you will need to access your HomeAssistant config/esphome/images folder. (Samba share add-on makes this very easy)
You can use any image including transparencies and they should be named to match the device configuration to avoid changing any code. The files need to be 320 x 240 pixels and should be named as followed.
* error.png
* loading.png
* thinking.png
* replying.png
* listening.png
  <br><br>
  
I will cover adding other images for page backgrounds later in this guide.
Once you have your set of 5 images you need to copy them into the config/esphome/images folder from your local computer, using Samba share. You can either delete or simply overwrite the existing images in the images folder.(making sure not to delete any images that are for other ESPHome projects if there are any)<br><br>
Now that the images are copied over you will need to install the device config from the ESPHome dashboard (add-on) You do not to change or save anything in the config as the code pointing to the images will already in place and the images just need to be compiled into a new firmware .bin file so that they are present on the device.<br><br>
As always, I recommend rebooting the device after the firmware has been installed, to do this, press the reboot button in the ESPHome integration entry for the device.<br><br>
  
After rebooting , test the Voice Assistant and you should now see your new images displayed.<br><br>
### Changing wake word
* on device - Micro Wake Word
There are currently 3 available wake words that can be used with micro wake word and these are.
  * Alexa
  * OK Nabu
  * Hey Jarvis
in order to change the wake word you will need to open the device card from the ESPHome dashboard by clicking 'EDIT'. Once you are in the editor near the top of the config you will see this section<br>![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/0fe31a1e-093f-4b11-a651-5457a2f54b92)<br>
it is as simple as changing the name circled in red <br>![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/5e8899d3-7c6e-4c4d-be83-fc39876d6210)<br>
make sure you type it exactly the same as it is shown in the comments above the line you edit.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/a1825d9a-706a-43e2-81d4-d9a82b2a7f4b)<br>
Now you can go ahead and click 'save' then 'install' followed by wirelessly. after compiling and uploading reboot the device from the integration as described above. Once the device has restarted go ahead and test out the wake word.<br><br>
You can switch between on-device wakeword and HomeAssistant wake word from the ESPHome integration for the device as per the image below, this can be done on the fly and there is no need to reboot the device.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/5d5265fe-7692-4419-a636-6248c371cc1e)





