---
title: Using Macsen
layout: default
currentpage: usage
---

Defnyddio Macsen
===

<h2 class="linked" id='ddechrau_macsen'><a href="#ddechrau_macsen" title="Permalink to this headline">Ddechrau Macsen</a></h2>

Ar ol <a href="/documentation/configuration/">Ffurfweddu Macsen</a>, gallwch ddechrau macsen drwy deipio:
{% highlight bash %}
/home/pi/jasper/jasper.py
{% endhighlight %}

Gallwch hefyd ddechrau Jasper yn awtomatig ar bob reboot. I wneud hynny, -e `crontab -e`,  yna ychwanegwch y llinell ganlynol, os nad ei fod yno yn barod

{% highlight bash %}
@reboot /home/pi/jasper/jasper.py;
{% endhighlight %}

Ail Dechrau y Raspberry Pi


<h2 class="linked" id='interacting'><a href="#interacting" title="Permalink to this headline">Rhyngweithio gyda Macsen</a></h2>

Y ffordd fwyaf cyffredin i siarad â Macsenyw gyda y dilyniant canlynol:

- _chi_: "Macsen"
- _Macsen_: *biip uchel*
- _chi_: *siarad eich gorchymyn*
- _Macsen_: *biip isel*
- _Macsen_: *yn siarad yr ymateb*

Ar ôl dweud Macsen, rhaid i chi aros am y Canu uchel i siarad eich gorchymyn. Os nad ydych yn siarad meistrolaeth o fewn ychydig eiliadau, bydd Macsen rhoi'r gorau i wrando neu ofyn i chi ailadrodd eich gorchymyn.

<h2 class="linked" id='modules'><a href="#modules" title="Permalink to this headline">Modiwlau i roi cynnig ar</a></h2>

Yn ddiofyn, rydym wedi cynnwys y modiwlau canlynol i ddangos galluoedd Macsen:

- Amser: "FAINT O’R GLOCH YW HI?"
- Newyddion: "BETH YW’R NEWYDDION?"
- dihareb : "RHO DIHAREB?"
- Tywydd: "BETH YW TYWYDD HEDDIW"


Efallai bydd Macsen yn cael anhawster canfod eich ciwiau pan fydd y gerddoriaeth yn uchel. Yn yr achosion hyn, mae'n helpu i ymbellhau'r meicroffon gan y siaradwyr, gostwng y gyfrol, a / neu siarad yn nes at y meicroffon.
