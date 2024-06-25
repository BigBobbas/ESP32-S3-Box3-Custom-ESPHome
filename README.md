# ESP32-S3-Box3-Custom-ESPHome
 Custom ESPHome config for ESP32-S3-Box-3 with sensors and touchscreen<br><br>
 
 To go straight to the web installer [click here](<https://support.bbdl.co.uk>)<br>
 
 To go straight to the config to use with the sensor dock [click here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/s3b.yaml>)<br>
 To go straight to a config for use without the sensor dock [click here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/s3b_no_sensors.yaml>)<br>
 
To go straight to Installation Guide [click here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>)<br>
To go straight to the 'how to customise' Guide[click here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/make%20it%20your%20own.md>)<BR>

![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/f70ec539-1d08-4ba2-84ad-684866000986)

 
 # Introduction.<br>
 >Firstly I am not a coder/developer/programmer. I Just know the small amount I do know from having a go, and spending many frustrated hours until things do what I want them to do. I apologise if the config makes you pro's cringe... as I am sure there will be many different ways that I could have made this config that would be the 'correct way' however it does what I want, so I will take that as a win.<br><br> 
This example config allows use of the touch screen and other sensors on the ESP32-S3-Box-3 using ESPhome for use with Home Assistant. The provided config is intended to be used as template for you to customise for your own purposes. I will provide as much detailed instruction as possible for you to achieve this.<br><br>
If you have any ideas, feedback or feel you could help make things 'even better' then it would be great to hear your thoughts.
#### Please Remember to backup any previous configs and associated files that you may have previously used for the device. <br><br>Using this config or installing the .bin via the web installer is at your own risk. They work for me... but I am not a professional.
 
## Installation and setup notes
follow the installation instructions [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>) 
to unleash more of the devices potential.<br>
The s3box is quite a capable device and NOT just a voice assistant.

## This configuration will enable the following features.
* *** new feature - Media Player ***
Thanks to [gnumpi](<https://github.com/gnumpi/esphome_audio>) 'ESPHome audio' has made it possible to have the s3box act as a media player. You can stream music and tts direct from Home Assistant.
* Touch Screen - to control your home
* Media Player
* Screen saver
* Red circle button on front of display
* Top lefthand side hardware button
* Temp and Humidity Sensor
* Prescence sensor
* Push to talk voice assistant
* Voice assistant with switchable on Device wake word or Home Assistant wakeword engine eg. Openwakeword

 ## Requirements
 * ESP32 S3 Box 3
 * ** no longer required 18650 Battery - not essential, but it helps to give the device constant power which will prevent Voice Assistant losing its functionality.
 * ESPHome installation, either Home Assistant add-on, Local Cli install or docker.
   Please note that the compile of the config is fairly resource hungry and may fail on older devices with low ram and low processing power. However running ESPHome from a local machine with more power, will make this much faster and less likelihood of encountering errors.
   Details of how to run ESPHome in different ways, can be found [here](<https://esphome.io/guides/installing_esphome.html>) for OS installs or Docker [here](<https://esphome.io/guides/getting_started_command_line.html>) 
 * A Working installation of HomeAssistant preferably on the same network/vlan as the device, to avoid connection issues.
 * Samba Share Home Assistant add-on (available in the add-on store)or some other means of accessing your Home Assistant files and folders. you will need to access the config/esphome folder from your local computer in order to copy the required image files and fonts. 
 * For Voice Asssistant to function you will either need a Nabu Casa (HomeAssistant Cloud) [subscription](<https://www.nabucasa.com/>) and Openwakeword or an installation of the following add-ons (available in the Home Assistant add-on store) 
Whisper, Piper & openwakeword



Click [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>) if you have everything ready and are ready to start the installation.
