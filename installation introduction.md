# Introduction.
## Instalation and setup (draft)
Due to some quirks currently with i2c on the S3box3 an installation procedure is required to enable all features. In this guide I will go through the steps required in order to enable all features.
This guide assumes that you already have a working 'stock' firmware installed on the s3box that you would like to customise, to unleash more of the devices  potential. The s3box is quite a capapable device and NOT just a voice assistant. (a revised version of this guide will be available to install and configure on a new device out of the box - I am currently awaiting arrival of a new device in order to document this)

## This configuration will enable the following features.

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
   Details of how to run ESPHome in different ways, can be found here INSERT LINK
 * A Working installation of HomeAssistant preferably on the same network/vlan as the device, to avoid connection issues.
 * Samba Share HomeAssistant add-on or some other means of accessing your HomeAssistant files and folders. you will need to access the config/esphome ESPHome folder from your local computer in order to copy the required image files and fonts. 
 * For Voice Asssistant to function you will either need a Nabu Casa (HomeAssistant Cloud) subscription. INSERT LINK or an installation of the following add-ons (available in the HomeAssistant add-on store) 
Whisper, Piper & openwakeword



To get started INSERT LINK

