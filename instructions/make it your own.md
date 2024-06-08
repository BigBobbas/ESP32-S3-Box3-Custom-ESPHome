# Making it your own.
The ESP32-S3-Box-3 is not just a voice assistant. In the following guide I will detail how you can make it your own and customise the device, giving you control over your other HomeAssistant devices and display sensor values and much more.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/d5268d37-94bf-4cad-87e4-c4360fa7c76b)

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
in order to do this you will need to access your Home Assistant config/esphome/images folder. (Samba share add-on makes this very easy)
You can use any image including transparencies and they should be named to match the device configuration to avoid changing any code. The files need to be 320 x 240 pixels and should be named as followed.
* error.png
* loading.png
* thinking.png
* replying.png
* listening.png
  <br><br>
Once you have your set of 5 images, you need to copy them into the config/esphome/images folder from your local computer, using Samba share. You can either delete or simply overwrite the existing images in the images folder.(making sure not to delete any images that are for other ESPHome projects if there are any)<br><br>
Now that the images are copied over you will need to install the device config from the ESPHome dashboard (add-on) You do not to change or save anything in the config as the code pointing to the images will already in place and the images just need to be compiled into a new firmware .bin file so that they are present on the device.<br><br>
As always, I recommend rebooting the device after the firmware has been installed, to do this press the reboot button on the bottom left side of the device.<br><br>
  
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
You can switch between on-device wakeword and Home Assistant wake word from the info page on the s3Box or from the ESPHome integration for the device as per the image below, this can be done on the fly and there is no need to reboot the device.<br>
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
2. What you visually see on the screen to represent the button.<br>
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
to add a new button, you can copy and paste the block for one button and change the id: so that it is unique, you can't use the same id: twice. Define which page you want the button to be active on, using page_id: , adjust the dimensions and location of the button and finally add the automation for what you want the button to do.<br><br> There are various other things that can be done using the touchscreen that are beyond the scope of this guide. More information can be found [here](<https://esphome.io/components/touchscreen/index.html>)<br><br>
#### The Display<br><br>
So now we have covered how the touch buttons ae created and how they work, let's take a look at how we make them visible on the display. There are several ways that you can visually represent the area to be touched to make it a button. You can simply display text, and image or in this case we will use material design icons, these are used in HomeAssistant so it is nice to have uniforimty accross platforms.<br><br>
The source I use for obtaining the icons is [here](<https://pictogrammers.com/library/mdi/>)<br>
In this example I will show how to add an icon that can be used in your config. The first part of the config we need to look at for this is the font: section<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/c159cf5e-e05c-4d6e-a633-c51258f01e45)<br>
Here we can define a liste of icons to be used throughout the config.<br>
all of the mdi-icons are defined in the same manner "\U000" and then after the thress 0's we add the code from the site i posted above. I will show how to add a switch icon. Firstly search for the icon you want in this case i will type "switch" <br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/a05ce114-dcb1-4ec2-8957-fb58ffd48265)<br>
I will use the light-switch for this example. If you click on the icon you want to use you will now see a box with the relavant code required in order to use that icon.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/2fea9c65-563f-40df-81f4-76ca550c0048)<br>
I have outlined the code we need in red in the image above. all you need to do is add this code after the three zeros asshown above. the result being "\U000F097E" add this to the list in the code like so.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/ad541c60-9471-4495-a00d-a8642f43cfe3)<br>
adding #name(light switch in this case) will make it easier for you to loacte the icon code to use later. the # prefix is required to make this a comment and not part of the yaml config.<br><br>
Now that you have your icon added you can now use it on the display. To do this we need to locate the display: part of the config<br><br>
and the part we are interested in is this<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/b3dfbd09-32ef-4c67-bacd-ba3ed498d05c)
<br>
The line that we want to change is this one.<br>
```yaml
          it.printf(120, 75, id(icon_font_80), yellow,"\U000F06E8");
```
<br>
lets break it down<br>

```yaml
it.printf
```

is the instruction to print the following to the screen<br>
the numbers are the x and y coordinates. So the icon will be positioned at 120 pixels accross and 75 pixels from the top. These coordinates define the top left corner of the icon and because the icon has it's own dimensions depending on the pixel size for the font, we don't need to define a size.<br><br>
```yaml
id(icon_font_80)
```
defines which font set to use which is identified by it's id: <br>
in the config under font: you will see<br>

```yaml
   - file: "fonts/materialdesignicons-webfont.ttf"
      id: icon_font_80
      size: 75
```

<br>   
which tells the config where the font file is located, what id: to use to reference this font and what size the font is. in this case 75px<br><br>
you can replace and add fonts, by adding font files to the config/esphome/fonts folder and then creating a codeblock under font: to define it's location, id:, size and any non-standard characters to use, under glyphs:<br><br>
next we have 'yellow' which is the colour that the icon will be displayed as. colours are defined under the color: section and are defined with an id: which allows you to reference the colour to use in that section of code and also the hex value so that the colour can be translated into a value that the code can use. You can add your own colours by copying an entry already in the color: component and assigning an id: and a hex value of the colour you want to use.<br>I have kept the colour id's the same as the colours name to make it easy when editing code, it avoids having to keep scrolling up to get the id.<br>The section in the config for colours is like below<br>

```yaml
color:
  - id: green
    hex: '75D15F'
  - id: red
    hex: 'FF3131'
  - id: blue
    hex: '47B7E9'
  - id: blue_drk
    hex: '085296'
```
<br><br>
please remember that any code using color, needs to be spelled in that way, please excuse my use of colour but I am a brit!!<br>
whenever copying sections of code it is very important to make sure you add everything in the exact same manner, including any punctuation and also make sure that everything lines up the same, as where things are placed prom the lefthand column (indentation) is vital. incorrect indentation will result in errors when compiling.<br><br>
more information with regards to display configuration can be found [here](<https://esphome.io/components/display/index.html>)<br><br>
In the next steps we will show how to change the devices icon and color depending on the state of the output you are controlling.<br><br>
Again we will use the light bulb icon as our example. The default is that the bulb is a static yellow icon. what we will do is change this to an icon that is dark blue and and doesnt have the light illumination dashes when the light is off and change to yellow with illumination dashes when the light is on.<br><br>
In order to do this we will need:-
* Add a text_sensor: to track the state of the light from HA, so that if the light is controlled elsewhere the display will refelect its current state. 
* the 2 icon codes to put into the display code (display lambda)
* the id:'s of the 2 colours
<br>
the display line that we will be working with is this one.

```yaml
          it.printf(120, 75, id(icon_font_80), yellow,"\U000F06E8");
```
and the text_sensor: we will create is below, Which will be added as a new component. This is required as we are only sending an instruction to HomeAssistant to turn the light on or off, therefore the S3box doesn't know from HomeAssistant what the state of the light is. The config required is below. substituting entity_id: switch.sitting_room_s1 with the entity id of the device you wish to control.<br>
This can be placed anywhere in the config, however as this is a new component, the text_sensor: line is not indented and will sit against the lefthand columm and will look like below.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/13934218-829d-4250-b606-e3b09fe58af7)


```yaml
text_sensor:
  - platform: homeassistant
    id: light1_state
    entity_id: switch.sitting_room_s1
    internal: true
```
<br>
Next we need to make some changes to the line that prints our output to the screen. To do this we need to use 2 print lines, 1 for each state. We will use an if statement to tell the display which line to print depending on state.<br>
this is how the completed block will look.
```
          if(id(light1_state).state == "on") {
                it.printf(120, 75, id(icon_font_80), yellow,"\U000F06E8" );
          } else {
                it.printf(120, 75, id(icon_font_80), blue_drk,"\U000F0335" );
          }
```
the first print line is the state when the light is on so use your icon and colour of choice in the lines above. light1_state is the id: we gave to the text sensor so you need these to match.  The line below else is the line used to print the off state of the light, again use your colour and icon of choice. It is very important in order to avoid compile errors that the whole block is in line and correctly indented with the rest of the config. the completed result should like below.<br>
this section displays the 3 icons in the middle row on the display.<br>

![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/ec41b7e1-f217-4e9f-9df7-5fa0bd1b8c26)

<br>
Now that you have changed the config, you can go ahead and save and install, and as always after the device has the updated firmware go ahead and reboot it and test. Hopefully everything should now be working with a device being toggled on and off when the touch button is tapped and the icon and colour should change to refelect the state.<br>
The steps above are exactly the same for all on/off devices that you want to control from HomeAssistant. You should now be able to configure the other buttons in this example config to control the devices that you want.<br><br>

#### Adding pages.<br><br>
If for example you have more than one light you wish to control, we can create a new page to display the buttons for all of those lights. For simplicity we will use the same button that we configured but will revert back to the original config for this example.<br><br>
The sections of the config we will be looking at are as follows:-<br><br>

The print line
```yaml
          it.printf(120, 75, id(icon_font_80), yellow,"\U000F06E8");
```
The touch button<br>
```yaml
  - platform: touchscreen
    page_id: idle_page
    id: control_2
    internal: true
    x_min: 110
    x_max: 210
    y_min: 90
    y_max: 170
    on_click:
      min_length: 10ms
      max_length: 500ms
      then:
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.sitting_room_s1
```
<br>
We will also add a new entry to the display: component to configure the page, which is where we will start.<br>
in the display block <br><br>

Creating a new page is quite simple and we just need to add the lines below.<br>

```yaml
      - id: lights_page
        lambda: |-  
          it.fill(id(black));
```
This will create a blank page, the id: for the page which we will use later is lights_page and the background colour of the page will be black, as defined by the it.fill line which basically says Fill the screen with the colour 'black', black being the id for the colour defined in the color: component above in the config.<br><br>
Now that you have a blank page you want to add some icons. the easiest way is to copy and paste these from another section of the display config to make sure that the icons are displayed in the correct position.<br> 
The process then will be the same as above for changing the light icon. You will need to add a text_sensor: for each entity to be controlled. Don't repeat the text_sensor: line and add each additional entity with it's on id: for the state. example below<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/b1d2e4cb-7d75-400c-a9de-42a97365487a)<br><br>
and remember that each entity will need 2 print lines in the display section with an if: / else:<br><br>
To add the touch controls for this page, you can copy and paste to duplicate the control buttons from the idle page making sure to change the id: of each button and also the page_id: as we will only want these buttons to be actionable on the newly created page. you will also need to add the service call automation so that HomeAssistant will know which entity to turn on and off.<br>below is an example of how it should look.<br><br>
```yaml
  - platform: touchscreen
    page_id: lights_page
    id: light_control_1
    internal: true
    x_min: 5
    x_max: 105
    y_min: 90
    y_max: 170
    on_click:
      min_length: 10ms
      max_length: 500ms
      then:
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.sitting_room_s1

  - platform: touchscreen
    page_id: lights_page
    id: light_control_2
    internal: true
    x_min: 110
    x_max: 210
    y_min: 90
    y_max: 170
    on_click:
      min_length: 10ms
      max_length: 500ms
      then:
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.sitting_room_s2

  - platform: touchscreen
    page_id: lights_page
    id: light_control_3
    internal: true
    x_min: 215
    x_max: 315
    y_min: 90
    y_max: 170
    on_click:
      min_length: 10ms
      max_length: 500ms
      then:
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.sitting_room_s3
```
Once you have made the changes above, you can now save and install, I may have mentioned previously ;) restart the device after the firmware has uploaded.<br><br>
#### Extra buttons and prescence 
We are left with just 3 more components that you can customise and they are the top lefthand side button, the front red circle button, and the radar sensor. with these you can use the instructions above to add service call or an on device automation to these. all three are buttons(binary sensors) and are customised in the same way. The 3 blocks that we need to edit are :-
<br>
```yaml
###### top left hand physical button #######
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO0
      mode: INPUT_PULLUP
      inverted: true
    name: Top Left Button
    entity_category: diagnostic
    on_press:
      - light.toggle: led
#######     red circle home button   #####################
  - platform: gt911
    name: "Home"
    index: 0
    on_press:
      - display.page.show: idle_page
###### radar sensor ########
  - platform: gpio
    pin:
      number: GPIO21
    name: "Presence detect"
    disabled_by_default: false
    device_class: "occupancy"
```
<br>
in both cases you can change the line below on_press: to call the action that you want to perform. As you can see from the config above. the top left button is set to toggle led - led is the id: of the screens backlight so pressing this will turn the screen on or off. you can change this to perform any action that we have mentioned in the sections above for customising the touch buttons.<br>
The front red circle is currently configured to show the idle page a 'Home' button in this config. <br><br>
Finally the radar button currently has no automation configured. by adding the following this will now toggle the defined light on and off based on prescence detected. ( this is not a practical automation but a sample to show how it works.<br>

```yaml
  - platform: gpio
    pin:
      number: GPIO21
    name: "Presence detect"
    disabled_by_default: false
    device_class: "occupancy"
    on_press: 
      then:
        - homeassistant.service:
            service: switch.toggle
            data:
              entity_id: switch.sitting_room_s1
```

You can change any of these buttons/sensor to do many things.<br>
There are lots of automation options in the ESPHome docs, and I will provide a list of links summary that you may find useful and are relevant to what has been covered in this guide.<br><br>

#### Displaying Sensor information<br><br>
Now that we have covered how to display things on the screen and adding functionality to send actions to other devices, lets take a look at displaying information from sensors. Starting with the sensors that are on the device. We will look at how to add the value from the temperature and humidity sensor that are built into the s3box device base.<br>
Because these sensors are already setup in the config no additional component setup is required and we can use the id: of the sensors to display their readings on the screen. The full sample config already has the temperature displayed, which is overlaid on top of the temperature icon.<br>
The sensor which is configured in this block<br><br>
```yaml
sensor:
  - platform: aht10 
    i2c_id: bus_b
    variant: AHT20
    temperature:
      name: "Temperature"
      id: s3temp
    humidity:
      name: "Humidity"
      id: s3hum
    update_interval: 60s
```
and the display config we need to look at is here. <br>
```yaml
          it.printf(20, 75, id(icon_font_80), blue,"\U000F050F");
          it.printf(40, 120, id(my_font3), white, "%.f", id(s3temp).state);
```
<br>
You will notice that this part of the print line is different to what we have encountered so far.<br>

```
"%.f", id(s3temp).state);
```
for the best description of what this means and what effect it has on the displayed line is best described [here](<https://esphome.io/components/display/index.html>)
<br>
in the line you can see (s3temp) this is where we put the id: of the sensor we wish to display. changing this to (s3hum) would display the current reading of the humidity sensor. The same principle is applied if we wish to display sensor values from other devices that are configured in HomeAssistant. We will however need to add a sensor to our ESPHome config that pulls in the values from HomeAssistant and provides an id: for us to use in the display config. To do this we need to add the following to the sensor: component.<br>
```yaml
  - platform: homeassistant
    id: liv_temp
    entity_id: sensor.living_room_temp
    internal: true
```
in the above config, we have given the sensor an id: which is what we will use in the display print line. Then add the entity_id: of the sensor from HomeAssistant, we covered this earlier in the guide. and finally setting internal: true , says don't expose this to HomeAssistant (we got it from there so no need to send it back) <br>
now to display this sensors value, we just need to put the id in so the print line looks like so. <br>
```yaml
          it.printf(40, 120, id(my_font3), white, "%.f", id(liv_temp).state);
```
There are many other options beyond the scope of this guide that can be found by reading the [ESPHome display docs](<https://esphome.io/components/display/index.html#display-component>) 

### A final note from me.
I hope that the information that I have given has been as easy as can be to follow and that it has given you the insight as to how the config works, and given you some pointers to allow you to tackle customising your device. The information in this guide can be applied to lots of other devices and is not entirely specific to the ESP32 S3 box.<br><br>
Resources that have been invaluable to me in my journey configuring ESPHome devices have been the ESPHome docs and the  ESPHome Discord server. I have found the best way of finding ESPHome docs has to been to google "esphome" followed by the name of component i need help with, then selecting the results that are linked to esphome.io, this search term has most often taken me straight to the pages i've needed.<br> 
If you have any feedback, issues or have spotted any inacuricies or ways you think would be better to describe how to do certain parts in this guide. Please make me aware by raising an issue from the link at the top of the github page. 

links:
docs
display
touch
gt911
automations
home assistant































