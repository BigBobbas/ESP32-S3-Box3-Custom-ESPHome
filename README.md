# ESP32-S3-Box3-Custom-ESPHome
 Custom ESPHome config for ESP32-S3-Box-3 with sensors and touchscreen<br><br>

![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/f70ec539-1d08-4ba2-84ad-684866000986)

 
 # Introduction.<br>
This example config allows use of the touch screeen and other sensors on the ESP32-S3-Box-3 using ESPhome for use with Home Assistant. The provided config is intended to be used as template for you to customise for your own purposes. I will provide as much detailed instruction as possible for you to achieve this.<br><br>
 
## Instalation and setup notes
follow the installation instructions [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>) 
to unleash more of the devices potential.<br>
The s3box is quite a capapable device and NOT just a voice assistant.

## This configuration will enable the following features.
* ### new feature - Media Player
* Touch Screen 
* Red circle button on front of display
* Top lefthand side hardware button
* Temp and Humidity Sensor
* Prescence sensor
* Voice assistant with switchable on Device wake word or HomeAssistant wakeword engine eg. Openwakeword

 ## Requirements
 * ESP32 S3 Box 3 (This config is only applicable to the version with the sensor dock)
 * 18650 Battery - not essential , but it helps to give the device constant power which will prevent Voice Assistant losing it's functionality.
 * ESPHome installation , either HomeAssistant add-on, Local Cli install or docker.
   Please note that the compile of the config is fairly resource hungry and may fail on older devices with low ram and low processing power. However running ESPHome from a local machine with more power, will make this much faster and less likeliehood of encountering errors.
   Details of how to run ESPHome in different ways, can be found [here](<https://esphome.io/guides/installing_esphome.html>) for OS installs or Docker [here](<https://esphome.io/guides/getting_started_command_line.html>) 
 * A Working installation of HomeAssistant preferably on the same network/vlan as the device, to avoid connection issues.
 * Samba Share HomeAssistant add-on (available in the add-on store)or some other means of accessing your HomeAssistant files and folders. you will need to access the config/esphome folder from your local computer in order to copy the required image files and fonts. 
 * For Voice Asssistant to function you will either need a Nabu Casa (HomeAssistant Cloud) [subscription](<https://www.nabucasa.com/>) and Openwakeword or an installation of the following add-ons (available in the HomeAssistant add-on store) 
Whisper, Piper & openwakeword



Click [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>) if you have everything ready and are ready to start the installation.

