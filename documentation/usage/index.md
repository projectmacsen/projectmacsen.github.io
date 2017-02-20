---
title: Using Macsen
layout: default
currentpage: usage
---

Defnyddio Macsen
===

<h2 class="linked" id='dechrau_macsen'><a href="#dechrau_macsen" title="Permalink to this headline">Dechrau Macsen</a></h2>

Ar ol <a href="/documentation/configuration/">Ffurfweddu Macsen</a>, gallwch ddechrau Macsen drwy deipio:
{% highlight bash %}
/home/pi/jasper/jasper.py
{% endhighlight %}

Gallwch hefyd ddechrau Jasper yn awtomatig bob tro mae'r cyfrfifiadur yn ailgychwyn. I wneud hynny, -e `crontab -e`,  yna ychwanegwch y llinell ganlynol, os nad yw yno yn barod

{% highlight bash %}
@reboot /home/pi/jasper/jasper.py;
{% endhighlight %}

Ailgychwynnwch y Raspberry Pi


<h2 class="linked" id='interacting'><a href="#interacting" title="Permalink to this headline">Rhyngweithio gyda Macsen</a></h2>

Y ffordd fwyaf cyffredin o siarad â Macsen yw drwy ddefnyddio'r dilyniant canlynol:

- _chi_: "Macsen"
- _Macsen_: *biip uchel*
- _chi_: *siarad eich gorchymyn*
- _Macsen_: *biip isel*
- _Macsen_: *yn siarad yr ymateb*

Ar ôl dweud Macsen, rhaid i chi aros am y sain uchel cyn siarad eich gorchymyn. Os nad ydych yn dweud y gorchymyn o fewn ychydig eiliadau, bydd Macsen rhoi'r gorau i wrando neu yn gofyn i chi ailadrodd eich gorchymyn.

<h2 class="linked" id='modules'><a href="#modules" title="Permalink to this headline">Modiwlau i roi cynnig arnyn nhw</a></h2>

Rydym wedi rhagosod y modiwlau canlynol o fewn meddalwedd Macsen er mwyn dangos beth all Macsen wneud:

- Amser: "FAINT O’R GLOCH YW HI?" "BETH YW'R AMSER?" "BETH YDI'R AMSER?"
- Newyddion: "BETH YW’R NEWYDDION?" "BETH YDI'R NEWYDDION?"
- dihareb : "RHO DDIHAREB I MI"
- Tywydd: "BETH YW'R TYWYDD HEDDIW" "BETH YDI'R TYWYDD HEDIW?"

Os bydd Macsen yn cael anhawster i glywed eich ciwiau, ceisiwch symud y microffon yn bellach oddi wrth y seinyddion, gostwng lefel y sain, a / neu siarad yn nes at y microffon.
