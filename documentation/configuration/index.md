---
title: Configuration
layout: default
currentpage: configuration
---

## Setting up Audio on your Pi

The Audio on your Pi you need to set up after running the prepare.sh script in macsen/prepare-scripts

You may need to adjust the volume and/or input gain for the microphone, you can do this with `alsamixer`.
Once the adjustments have been made, you can save the settings using `alsactl store`.


## Debugging your setup

If there is an error in your log file complaining about _alsaaudio_ you may need to tinker your audio setup.
These errors might be these:

- Invalid `input_device` in config:

    > alsaaudio.ALSAAudioError: No such file or directory [plughw:1]

    Check the name of your sound card input device. Selecting the device `default` for input and / or output often works.

    You can use these commands to figure out your device names:
    ```
arecord -L
aplay -L
```

     If you for some reason cannot use a name from the list, use the override config option. Otherwise, please stick to the listed names.

    To list your sound cards, use 
    ``` 
aplay -l
arecord -l
````
- Another application is using your device:
    
    > alsaaudio.ALSAAudioError: Device or resource busy [plughw:1]

    If you are running a desktop OS, it might be PulseAudio in user-session mode. You have to run PA in system-wide mode in order to run AlexaPi. Scroll down for more info.

### Checking if your system audio works
1. To test playback, run `aplay /usr/share/sounds/alsa/Front_Center.wav`
2. To rest recording, run `arecord -D yourdevice test.wav` - exit with CTRL+C and `aplay test.wav`


This site has some good information regarding alsa: [http://www.volkerschatz.com/noise/alsa.html](http://www.volkerschatz.com/noise/alsa.html)


## Raspberry Pi-specific
### HDMI Audio

If you are using HDMI out and are losing the first part of audio playback try running `vcgencmd force_audio hdmi 1`. 

## Raspberry Pi

Works fine by default!

**HDMI Audio Users:**
_Note: If you are having trouble with the sound cutting off the first few seconds, try running the following command:_

` vcgencmd force_audio hdmi 1`

_If it works you can add it to cron, with these steps_

1. crontab -e 

2. @reboot  vcgencmd force_audio hdmi 1 

3. save, exit and reboot.

### Arch Linux

The internal audio is not enabled by default in Arch Linux see the [Raspberry Pi/Audio section in Arch wiki](https://wiki.archlinux.org/index.php/Raspberry_Pi#Audio) on how to do that manually.

### External DAC Support

Some external DACs might have issues with the default Device Platform configuration. This may or may not include an unresponsive audio system with no sign of normal ALSA audio errors.  The HiFiBerry DAC+ for example needs GPIO pins of its' own to receive audio from your pi. The default platform config uses PIN 18 as an optional button, which is one of the same pins used by the DAC to communicate.

Make these pin numbers don't overlap with your DAC's pinout:
```
  raspberrypi:
    button: 7
    plb_light: 24
    rec_light: 25
```

Alternatively, if you don't need a button, nor LEDs, you can just use the _dummy_ device platform and it won't touch your GPIO at all.


## PulseAudio

You might get errors regarding PulseAudio. This is very probably due to the fact that you're running a GUI installation of your OS with PA in session mode and you want to run Macsen as a daemon under another user. Unfortunately things don't work like this, because this way PA is there only for the user _pi_.

You have these options:

### Disabling PA

**Note:** You might not be able to run other apps that use audio output without some ALSA tweaking.

All under root (or `sudo` before every command):

```
mkdir -p /var/lib/Macsen/.config/pulse
cp /etc/pulse/client.conf /var/lib/Macsen/.config/pulse/
# edit /var/lib/AlexaPi/.config/pulse/client.conf and set "autospawn = no"
```

### Running PA in system-wide mode (recommended)

This is the preferred (and possibly the only sensible) way to run PA with AlexaPi. 

-- In addition i would call it experimental for now.

Note that there are some warnings about unexpected behavior and the like, but you can safely ignore it. Read more about [system-wide PA](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/SystemWide/) on their wiki.  

**Setup and Configure Pulseaudio:** 

- Install PulseAudio and optionally uninstall the deprecated modules as recommended on [freedesktop.org](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PerfectSetup/). Have a look at that page to understand how these things will work - there may also be things there to try if this setup doesn't work for you.

    ```
sudo apt install pulseaudio pavucontrol
sudo apt remove pavumeter paman padevchooser
```

- Run these commands:
    ```
mkdir -p /var/lib/Macsen/.config/pulse
sudo cp /etc/pulse/client.conf /var/lib/Macsen/.config/pulse/
```
    Edit `/var/lib/Macsen/.config/pulse/client.conf` and set `autospawn=no`.

    Also if you see issues with permissions in the log file for /var/lib/Macsen (if you have an older install), you may need to run these commands: 
    ```
# create and set a home directory for the user alexapi
chown -R alexapi:alexapi /var/lib/AlexaPi/
usermod --home /var/lib/AlexaPi alexapi
```

- Next, we add the _pi_ (or your user) and _alexapi_ users to the `pulse-access` group, and just for good measure add the _pulse_ user to the `audio` group:

    ```
sudo adduser pulse audio
sudo adduser <username or pi> pulse-access
sudo adduser alexapi pulse-access
```

    If you are running the root override (like on a CHIP or Orange Pi), you also need to add the user root into the pulse-access group: `sudo adduser root pulse-access`.

- Next we need to create the systemd service so PulseAudio will start on boot in system wide mode: 
Create the file in you text editor, i used nano:

    ```
sudo nano /etc/systemd/system/pulseaudio.service
```

    in the new blank file that opens, place the following text: 

    ```
[Unit]
Description=PulseAudio Daemon

[Install]
WantedBy=multi-user.target

[Service]
Type=simple
PrivateTmp=true
ExecStart=/usr/bin/pulseaudio --system --realtime --disallow-exit --no-cpu-limit
```

    exit and save the file in the editor (for nano `[Ctrl] + x`, then `y`, then `[Enter]`)

- Now we need to enable the systemd service so it starts automatically: 
    ```
sudo systemctl enable pulseaudio.service
```

- Last we need to configure `config.yaml` for AlexaPi to use PulseAudio:
(If you didn't install AlexaPi in `/opt`, the file `config.yaml` is in your _AlexaPi/src_ directory.)
    ```
sudo nano /etc/opt/AlexaPi/config.yaml 
```

    in this file, in the _sound_ section, set
    ```
input_device: "pulse"
output: "pulse"
output_device: ""
```

- Reboot your system and check to see that everything is working.  If the audio playback is choppy, you can try installing VLC manually with `sudo apt-get install vlc`.

### User session mode (AlexaPi as the only audio app)
TODO

### PulseAudio via dmix

Alternatively, you can force PA to use dmix, so other apps can use ALSA directly.
See https://wiki.archlinux.org/index.php/PulseAudio#ALSA.2Fdmix_without_grabbing_hardware_device
_Warning:_ This has not been tested. Feedback is welcome.

### Using other user's (pi for example) PA instance

This is crazy and not supported (nor will ever be). You'd have to setup up some permissions, the actual socket (unix or TCP) to communicate and you'd have to make sure the user pi is always (and first) logged in before starting AlexaPi.


Rhedeg Macsen am y tro cyntaf
===
Mae angen creu proffil ar gyfer Macsen cyn ei redeg am y tro cyntaf, er mwyn iddo wybod eich enw a.y.b.  Rhedwch y sgript ganlynol ac atebwch y cwestiynau 

```
$ python client/populate.py
```

Ar ôl ateb pob cwestiwn, mae modd cychwyn Macsen drwy redeg

```
$ python jasper.py  
``` 
