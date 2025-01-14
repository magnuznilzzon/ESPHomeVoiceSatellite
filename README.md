YAML code for ESPHome on a ESP32. For making a unit with microphone and speaker to use with Home Assistant: Voice Assistant.

- It has support for addressable LED-strip.
- 5 buttons for interactions.
- It has audio sounds for key-click and 'Listening' start/end.

[Djelle] have addressed the issue with voice assistant programs like this sometime locks up. It happens when the recorded sound has no recognisable speach in it. And thus it doesn't feel the need to reply. Which would normally be followed by an on_stt_vad_end event. Instead it send out an error: 'stt-no-text-recognized'.

> [!NOTE]
> Notice that Volume is not supported by Voice Assistant as of now. But probably will be in the future.

## Buttons
[Djelle] used a cheap (and faulty) bluetooth speaker for this project. Which happened to have 5 buttons. Though you can of course choose to use less than 5 or none.
- ⏻ Power: Wake Word On/Of
- ✆ Call: Push To Listen
- ⏯ Play/Pause: Change config selection. E.g. Volume, LED Brightness. (Future maybe: Mic-volume, Noise suppression, Gain).
- ➕ Next: Config selection increase
- ➖ Prev: Config selection decrease

## LED-strip
[Djelle] added an addressable LED-strip around it for state feedback. And made some custom light effects that can support my LED-brightness setting.

- White: "Not Ready" Not connected to HA.
- Orange: "Muted" Wake word disabled.
- Green: "Idle" Wake word enabled.
- Blue: "Listening" Listening for command.
- Pink: "Thinking" Waiting for interpretation of speach.
- Yellow: "Replying" Talking.
- Red: "Error" Is not used. As I am unaware of any errors that would need it.

State is also exposed in Home Assistant. So automations can be activated by it.

Non-addressable and single LED could be used too. I have added the option 'led_addressable' in the code. But I don't have a setup to test it. And I expect that some of the code would have to be deleted to not throw errors during compilation. Like 'addressable_lambda'.

[Djelle] LED-Strip is a 35 LED (144 / m) RGBW. I do not use the White channel. The LED effects will scale with the number of LEDs. Though [Djelle] will recommend at least 10 LEDs.

## Future

[Djelle] hope that it will be possible to send Text-To-Speach to the speaker in the future. Which could have many uses. Like annoucing which config-option is selected.

[Djelle] experimented with continous listening (no wake word). Which I didn't find especially useful. So [Djelle] removed that code, as [Djelle] didn't feel like debugging it right now. Might add it again later.

> [!TIP]
> - When connecting the physical modules together: Make sure the I2S connections are as short as possible.
> - The amplifier module can use 2 Amp of power. Though [Djelle] assume that is only if gain it set to max. (Gain here, is not refering the mic gain in the code.)
> - If you use a LED-strip with many diodes, don't feed it power though the ESP32. But connect the strip and the ESP32 through a common power plug like an USB-C or a barrel plug.

## Photos of the unit I made
![01](/docs/01.jpg)
There was just the perfect room for the electronics in a corner. I extended the screw 'pins' by 5 mm. So that there was room for a 6 mm latex tube (originally for aquariums) around all the edge. To diffuse the led-strip.

![02](/docs/02.jpg)
Idle green. Which is more like teal.

![03](/docs/03.jpg)
Brin-colored scan animation while thinking.

![04](/docs/04.jpg)
Example of LED colors while setting volume: Blue indicate it's volumen. White fills up the rest of the space according to percentage set.
