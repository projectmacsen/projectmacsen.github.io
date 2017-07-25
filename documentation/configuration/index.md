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

    Gwiriwch enw eich dyfais mewnbynnu cerdyn sain. Mae dewis y ddyfais ragosodedig ar gyfer mewnbwn a / neu allbwnyn gweithio yn aml. 

    Gallwch ddefnyddio'r gorchmynion hyn i weithio allan enwau eich dyfais: 
```
arecord -L
aplay -L
```

     Os na fedrwch chi am ryw reswm ddefnyddio enw o'r rhestr, defnyddiwch yr opsiwn 'override config'. Fel arall, cadwch at yr enwau sy'n cael eu rhestru. option. 

    I restru eich cardiau sain, defnyddiwch  
``` 
aplay -l
arecord -l
```
- Mae rhaglen arall yn defnyddio eich dyfais:
    
    > alsaaudio.ALSAAudioError: Dyfais neu adnodd yn brysur [plughw:1]

### Gwirio i weld os yw'r sain yn gweithio ar eich system 
1. I brofi chwarae yn ôl, rhedwch `aplay /usr/share/sounds/alsa/Front_Center.wav`
2. I orffwys y recordiad, rhedwch `arecord -D yourdevice test.wav` - allan gyda CTRL+C a `aplay test.wav`


Mae gan y safle hwn wybodaeth dda am alsa: [http://www.volkerschatz.com/noise/alsa.html](http://www.volkerschatz.com/noise/alsa.html)


Rhedeg Macsen am y tro cyntaf
===
Mae angen creu proffil ar gyfer Macsen cyn ei redeg am y tro cyntaf, er mwyn iddo wybod eich enw ac ati.  Rhedwch y sgript ganlynol ac atebwch y cwestiynau 

```
$ python client/populate.py
```

Ar ôl ateb pob cwestiwn, mae modd cychwyn Macsen drwy redeg

```
$ python jasper.py  
``` 
