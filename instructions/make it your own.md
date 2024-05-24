## Making it your own.
The ESP32-S3-Box-3 is not just a voice assistant. In the following guide I will detail how you can make it your own and customise the device, giving you control over your other HomeAssistant devices and display sensor values and much more.
<br><br>
The following guide will cover these topics.
* Customise the voice assistant.
   * setting your own display images for the Voice Assistant process.
   * Changing the on-device (micro wake word) wake word.
   * Divert audio responses to other media players.
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
in order to change the wake word you will need to open the device card from the ESPHome dashboard by clicking 'EDIT'.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/8ef00b76-0d09-4692-9005-75fefb9349e7)<br>
Once you are in the editor near the top of the config you will see this section<br>![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/0fe31a1e-093f-4b11-a651-5457a2f54b92)<br>
it is as simple as changing the name circled in red <br>![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/5e8899d3-7c6e-4c4d-be83-fc39876d6210)<br>
make sure you type it exactly the same as it is shown in the comments above the line you edit.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/a1825d9a-706a-43e2-81d4-d9a82b2a7f4b)<br>
Now you can go ahead and click 'save' then 'install' followed by wirelessly. after compiling and uploading reboot the device from the integration as described above. Once the device has restarted go ahead and test out the wake word.<br><br>
You can switch between on-device wakeword and HomeAssistant wake word from the ESPHome integration for the device as per the image below, this can be done on the fly and there is no need to reboot the device.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/5d5265fe-7692-4419-a636-6248c371cc1e)
<br><br><br>
### Outputting audio responses to another media player device
as great as the S3 Box 3 is, the internal speaker is hardly earth shattering, so you may wish to output your audio to another device. Thats fine, due to the simplicity that ESPHome provides we can acomplish this with a few lines of code.<br><br>
Firstly find the entity_id: of the media player you want to stream the audio to. You should be able to find this from the device in question in HomeAssistant Devices & Services. Open the device page and click on the media player entity then click on the clog icon at the top of the enity box. You should now see a page similar to below, you need to make a note or copy the 
Entity ID <br>![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/ff31a6ea-86f9-4483-a06e-c7b19ae64e77)<br>
Now go to the ESPHome dashboard and click 'EDIT' on the device card. You now need to scroll down and find the voice_assistant: section.<br>
Paste in the following lines, making sure to keep the on_tts inline with the other on_xxx lines.
Don't forget to change the entity_id: to the one you copied earlier.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/27c16c06-304d-41a9-b9bb-945de94ed5cf)<br>
to make it easier here is the code that you can copy and paste.<br>
```yaml
  on_tts_end:
        then:
        - homeassistant.service:
            service: media_player.play_media
            data:
              entity_id: media_player.YOUR_MEDIA_PLAYER_ENTITY_ID
              media_content_id: !lambda 'return x;'
              media_content_type: music
              announce: "true"
```
if you only want the sound output on the external device and not on the s3box you can remove or comment out the following lines.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/d72e1bc8-6100-4d8e-ae1c-9cf630c785c4)<br><br>

Now you have edited the device config you can click save and install. NOTE:- if you have commented out or removed the speaker: lines in the screenshot above, this time before you install you will need to carry out a 'clean build files' as described in the installation guide [here](<https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md>) under step 8.<br>
Once the clean is done you can then proceed to click 'install' followed by 'wirelessly'. After the firmware has uploaded, reboot the device and your new config should be working, with audio outputting to your external speaker.<br><br>
if you have no audio after the above steps , make sure that the s3box is allowed to make services calls. To do this open the ESPhome integration in HA next to the device there will be a configure button, click this and then tick the box as shown below.<br>
https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/18e4999c-54ba-482f-897d-505828dfe71a
<br><br>
### Adding entities to the touch buttons, so that you can 'tap' to toggle on or off an external device.
in the example firmware it is possible to assign devices to the 6 buttons from the home screen (bottom 2 rows). this is a fairly straight forward process for on/off entities.<br><br>
I would be looking at introducing more complex controls in the next release of this config. Such as sliders for brightness and the ability to change light colours etc. This can be done now using scenes, which we will cover later in this guide. However I'm sure you will agree that having direct control from the screen would be much better!<br><br>

In the config the middle button on the middle row is for a simple on/off light entity. We can control this by making a service call to HomeAssistant.<br><br> 
Firstly you will need to find the Entity ID of the device you want to control. Follow the steps above that we used for finding the media player ID, it should be a similar method.<br><br>
In the config the touch buttons are defined under the binary_sensor: section, which is right towards the end of the config. The buttons have an id of control_1 to control_6, in this example we will be looking at control_2
<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/171547b8-d433-4bda-9367-ff2968710432)<br>
the lines you are interested in are these :-
```yaml
      then:
        - display.page.show: lights_page
```
everything above is the configuration of the button itself.<br>
Currently this button is configured to open a separate page, if for example you wanted to add multiple light entities.<br>
In order to change this we need to add the service call to HomeAssistant like so<br>
```yaml
        - homeassistant.service:
            service: light.toggle
            data:
              entity_id: light.workshop_light
```
If your light is controlled by a relay , or you want to control a smartplug / socket or other on/off device. The config would look something like this.
```yaml
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.workshop_light
```
the changed config should be similar to this <br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/b459b975-c7af-41ba-b998-c4fe191bb057)<br>

After changing the config, you can go ahead and click 'save' followed by 'install' and 'wirelessly' and yes... after install is complete, reboot the device from the integration! (hopefully you are getting the routine at this stage). Now go ahead and test that tapping the button toggles your light or switch on or off.<br><br>
this method can be applied to any of the buttons.<br><br>
I will now go into a little more detail, to hopefully give you the information to create your own touch buttons.<br><br>
Each button consists of 2 parts.<br>
1. The touch - where on the screen you click and how it reacts.
2. What you visually see on the screen to represent the button.
   #### The Touch
this defines that the following block is part of the touchscreen component<br>
  ```yaml
  - platform: touchscreen
```
The page_id: sets which page the button will be active on, for example if you have 2 or more pages and don't define the page_id: then tapping the screen will result in the action being applied to all pages. This can lead to unwanted results, with actions from multiple pages being actioned at once, or actions being applied that are not relevant to the page being displayed.
```yaml
    page_id: idle_page
```
The id: you will see in multiple places within any ESPHome yaml config, this is used to reference this section internally within the code, to allow other components and services access, for internal automations etc. 
```yaml
    id: control_2
```
This line defines that the entity is not to be exposed to HomeAssistant and only to be used internally by the config.
```yaml 
    internal: true 
```
The following lines define where and what area that you want the button to be active on the display. With the s3box3 the screeen dimensions are 320 x 240 pixels. The below lines instruct that the start of the touch area will be at the 110th pixel accross and will end at the 210th pixel accross, it will start at the 90th pixel down and end at the 170th pixel down, resulting in a rectangle that will be active as a button. It is important whne defining touch areas that the co-ordintates don't overlap as this will result in 2 buttons being pressed simultaneously.

```yaml
    x_min: 110
    x_max: 210
    y_min: 90
    y_max: 170
```
You will often see lines in ESPHome configs that start with on_ these are triggers, or hooks and in this instance say that 
on_click (when you tap the defined area) and your touch was for at least 10ms and no more than 500ms then carry out the action defined below. 
```yaml
    on_click:
      min_length: 10ms
      max_length: 500ms
```
This is the action part of the automation so reading the full config it essentially says if this area is pressed for this duration then do the following. in this case is is configured to make the service call to HomeAssistant to toggle an entity and the entity is ...
```yaml
       then:
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.workshop_light
``` 
to add a new button, you can copy and paste the block for one button and change the id: so that it is unique, you can't use the same id: twice. Define which page you want the button to be active on, using page_id: , adjust the dimensions and location of the button and finally add the automation for what you want the button to do.<br><br> There are various other things that can be done using the touchscreen that are beyond the scope of this guide. More information can be found [here](<https://esphome.io/components/touchscreen/index.html>)











