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
```
- Another application is using your device:
    
    > alsaaudio.ALSAAudioError: Device or resource busy [plughw:1]

### Checking if your system audio works
1. To test playback, run `aplay /usr/share/sounds/alsa/Front_Center.wav`
2. To rest recording, run `arecord -D yourdevice test.wav` - exit with CTRL+C and `aplay test.wav`


This site has some good information regarding alsa: [http://www.volkerschatz.com/noise/alsa.html](http://www.volkerschatz.com/noise/alsa.html)


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
