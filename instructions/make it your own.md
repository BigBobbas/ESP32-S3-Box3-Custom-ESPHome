# Making it your own.
The ESP32-S3-Box-3 is not just a voice assistant. In the following guide I will detail how you can make it your own and customise the device, giving you control over your other Home Assistant devices and display sensor values and much more.<br>
![device_img](https://github.com/user-attachments/assets/e8dc5fd4-21f5-40e1-bab1-5cecd87f487d)

#### The following guide will cover these topics.<br>
* Change Variables - Substitutions
* Customise the voice assistant.
   * setting your own display images for the Voice Assistant process.
   * Changing the on-device (micro wake word) wake word.
* Add entities to the touch buttons
* Add sensors to display the values on the screen
* Change the displayed icons
* Change the icon colours
* Add pages
* Change background colour and or image
* Change the function of the home button and the top left button<br><br><br>

## Getting started 
Firstly I will explain the difference between the ESPHome add-on and the ESPHome integration. The add-on is totaly separate to Home Assistant although it is accessible and installed via Home Assistant it isn't actually part of it and can be installed completly independantly on another machine (my preferred method) And is not required for an ESPHome flashed device to function in Home Assistant.. The sole purpose of the addon is to enable you to create firmware files to be flashed to devices from the configuration file, using yaml. The yaml file is a list of instructions and parameters and the real `code` lies beneath in the ESPHome codebase. The configuration simply tells ESPHome which components are required and any parameters that can be configured. Once the config is compiled then all of the relevant code, libraries and other dependencacies are pulled all together and bundled into one file, the .bin file and this is what gets flashed to the device. Without you needing to do all of the hard work of coding. Imagine having to do all of that too! writing a config is hard enough as it is!
The add-on also alllows you to keep your config files in one place making them easily accessible. Home assistant does connect to the add-on dashboard to provide the online status of the device. This is not always reliable and require mDNS to be correctly configured on your network in order for it to talk to the dashboard. There is an option in the add-on configuration to enable 'ping for status' where it will use the IP addresses of devices to report back to the add-on.<br>

The ESPHome integration is part of Home Assistant and like any other device it is how Home Assistant knows what to do with the device and what entities are available and what controls they have. In order for the device to function with Home Assistant the device needs to be added to the ESPHome integration, without this you will be unable to control devices or see values from sensors.
 
in order to make any changes to the configuration file you will need to open the ESPHome add-on dashboard, there should be a button in the sidebar of your Home Assistant page. Once you have the dashboard open, locate the device card for the S3box and click 'edit' as shown below.
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/8ef00b76-0d09-4692-9005-75fefb9349e7)<br>
After making your changes click on `save` in the top right corner, followed by `install` you will see a list of options, select `wirelessly`
To enable the S3Box to send commands to Home Assistant to control your devices you need to allow the device to perform Home Assistant Actions (previously called services). To do this open the ESPhome integration in Home Assistant (this is found in settings>>devices and services>>ESPHome. Next to the device listing there will be a `configure` button, click this and then tick the box as shown below.<br>
![image](https://github.com/user-attachments/assets/06e8b262-9ef1-40ac-8008-12227f9e1b00)<br>
![image](https://github.com/user-attachments/assets/bbe3f106-489f-4175-95fe-0c70cc3afd1a)
<br><br>
## Substitions (variables).
At the top of the config there are a number of variables that can be changed to configure your device to suit your setup and locale.
![subs](https://github.com/user-attachments/assets/7345f7c7-1a81-405c-80d3-5615e74062a2)
1. The friendly name is how your device will be displayed in Home Assistant, it is safe to change this to anything you wish. The name is how Home Assistant connects to your device on your network, changing this can result in connection errors if the device has already been added to the ESPHome integration.
2. your_media_player is the entity id of an external Home Assistant media player for outputting the audio to an external device. only put the entity id after media_player. so media_player.sonos you would replace my_media_player with sonos. like so -> `external_media_player: sonos`
3. you can change the url here to eather your Home Assistant instance name followed by the port or the ip address of the server eg. http://192.168.1.10:8123
4. if you find that your tts responses are too slow sounding or too fast and sound like chipmunks then check the sample rate of the tts service you are using and change the number to match.
5. This is the current list of available wake words for 'on device' wake word by default all of these are enabled. you can use one or all or any number of these. To remove a wake word from being active search the config using `ctrl + F` and search for `models:` you can then comment out the ones that you don't wish to use by prefixing the line with a # like the sample below where the first one has been commented out.<br>
![image](https://github.com/user-attachments/assets/21681426-3301-4f10-83e0-1e8827d1d365)
6. This is a not yet released version of the okay_nabu wake word that you can use (results so far are very positive and this works very well with fewer false triggers and a higher response rate) to use this model, simply copy and paste the url and replace the words `okay_nabu`

Below the above substitutions there is a list of weekdays and months. You can change these to match your locale by changing the values on the right to the days and months in your preferred language.

## Customising Voice Assistant.
### Changing displayed images
in order to do this you will need to access your Home Assistant config/esphome/images folder. (Samba share add-on makes this very easy)
You can use any image including transparencies. The files need to be 320 x 240 pixels and should be named as followed.

* error.png
* loading.png
* thinking.png
* replying.png
* listening.png
  <br><br>
Once you have your set of 5 images, you need to copy them into the config/esphome/images folder from your local computer, using Samba share (if the folder doesn't exist, you will need to create it). You can either delete or simply overwrite the existing images in the images folder.(making sure not to delete any images that are for other ESPHome projects if there are any)<br><br>
Now that the images are copied over you will need to install the device config from the ESPHome dashboard (add-on) You will need to change the path in the config to your new images. <br>
Locate the image: secion in the config, and you will need to change the path to the file.<br>
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/88512211-f0f9-4149-b16d-c3fad900089c)<br>
change everything including the quotes to images/filename.png so it looks like below
![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/eaf38960-ff31-47e8-b34c-76f283de12e7)<br>
Once you have made the changes you can go ahead and click save followed by install and 'wirelessly'
  

![image](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/assets/150487209/ec4c4831-a966-4081-b13e-b80a2141ad54)


### Adding entities to the touch buttons, so that you can 'tap' to toggle on or off an external device.
in the example firmware it is possible to assign devices to the 6 buttons from the home screen (bottom 2 rows). this is a fairly straight forward process for on/off entities.<br><br>
I would be looking at introducing more complex controls in the next release of this config. Such as sliders for brightness and the ability to change light colours etc. This can be done now using scenes. However I'm sure you will agree that having direct control from the screen would be much better!<br><br>

In the config the middle button on the middle row is for a simple on/off light entity. We can control this by making a service call to Home Assistant.<br><br> 
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
In order to change this we need to add the service call to Home Assistant like so<br>
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

After changing the config, you can go ahead and click 'save' followed by 'install' and 'wirelessly' . Now go ahead and test that tapping the button toggles your light or switch on or off.<br><br>
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
all of the mdi-icons are defined in the same manner "\U000" and then after the three 0's we add the code from the site i posted above. I will show how to add a switch icon. Firstly search for the icon you want in this case i will type "switch" <br>
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
Now that you have changed the config, you can go ahead and save and install, and test. Hopefully everything should now be working with a device being toggled on and off when the touch button is tapped and the icon and colour should change to refelect the state.<br>
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
This will create a blank page, the id: for the page which we will use later is lights_page and the background colour of the page will be black, as defined by the it.fill line which basically says Fill the screen with the colour 'black', black being the id for the colour defined in the color: component above in the config. You can display an image on the screen, which includes transparancies. using <br><br>
`it.image((it.get_width() / 2), (it.get_height() / 2), id(your_image_id), ImageAlign::CENTER);`<br><br>To keep dimensions correct use an image that is 320 x 240. You will also need to add the image to the image: component, shown below, the image file needs to be stored in the 'esphome' folder on the computer that you are compiling the firmware from, if this is  the Home Assistant add-on then you will need to use Samba share or similar to access config/esphome/images This will then be compiled and built into the final .bin file that is flashed to the device.<br><br>
```yaml
image:
  - file: images/your-image-file.png
    id: my_img
    resize: 320x240
    type: RGB24
    use_transparency: true
```
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
Once you have made the changes above, you can now save, install and test.<br><br>
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

































