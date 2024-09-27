# ESP32-S3-Box3-Custom Firmware
# The S3 BOX 3  is not just a voice assistant... it can do so much more!! 
Video demo available [HERE](<https://youtu.be/5W52TOQU_oM>)
> ### Please have a read through this page and also the instruction pages to see what this config does and what is involved to set it up.
> Also check out the [Discord server](<https://discord.gg/U3SRYCG6Kp>) or [Discussions](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/discussions>) section in the repo, for latest updates, new features, and to ask questions or make suggestions 👍

## This firmware will enable your S3 Box 3 to use the touch screen and home button, and configure the box to act like a dashboard for Home Assistant. Giving you the power to control your entitities and display sensor information. 
## The box will also be configured as a media player, giving you volume control (also improves the overall volume of the internal speaker compared to the ESPHome stock config) and easily broadcast messages to the device or stream media. Oh, and don't forget! it is also a Voice Assistant!!
The following features are now included with the latest version of this configuration and all accessible using the touchscreen or the HA ESPHome integration.
- Alarmo integration
- Timers
- Output all audio to external HA media player with a tap of a switch
- Advanced device information
  - WIFI connection info, Device uptime, ip address, hostname
- Brigtness control
- Volume control of internal and external speakers
- Screensaver with on screen timeout settings
- Radar motion sensor
- 24hr/12hr time switch
- Touch Screen buttons - to control your home
- Media Player with controls too for an external player
- Red circle button on front of display
- Top lefthand side hardware button
- Temp and Humidity Sensor
- Push to talk voice assistant
- Voice assistant with switchable on Device wake word or Home Assistant wakeword engine eg. Openwakeword

There are also some settings that can be changed within the config and these can be found at the very top under the `substitutions:` section MOre details of these can be found in the 'how to customise' Guide[click here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/make%20it%20your%20own.md>)<BR>


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

 ## Requirements
 * ESP32 S3 Box 3
 * ESPHome installation, either Home Assistant add-on, Local Cli install or docker.
   Please note that the compile of the config is fairly resource hungry and may fail on older devices with low ram and low processing power. However running ESPHome from a local machine with more power, will make this much faster and less likelihood of encountering errors.
   Details of how to run ESPHome in different ways, can be found [here](<https://esphome.io/guides/installing_esphome.html>) for OS installs or Docker [here](<https://esphome.io/guides/getting_started_command_line.html>) 
 * A Working installation of HomeAssistant preferably on the same network/vlan as the device, to avoid connection issues.
 * Samba Share Home Assistant add-on (available in the add-on store)or some other means of accessing your Home Assistant files and folders. you will need to access the config/esphome folder from your local computer in order to copy the required sound files. 
 * For Voice Asssistant to function you will either need a Nabu Casa (HomeAssistant Cloud) [subscription](<https://www.nabucasa.com/>) or the Whisper & Piper add-ons. If you don't intend to use the on device Micro Wake Word, you will require a wake word engine such as openwakeword. The following add-ons are all available in the Home Assistant add-on store Whisper, Piper & openwakeword

Click [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>) if you have everything ready and are ready to start the installation.<br><br>

### I really hope you enjoy this project and I thank you for your support. If you have found this project useful and would like to buy me a coffee then the link is below ❤️<br>
<a href="https://www.buymeacoffee.com/BigBobba" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
