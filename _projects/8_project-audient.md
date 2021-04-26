---
layout: post
title: "Phantom Power"
description: "Audient iD22 giving up the ghost?"
---


## The Audient iD22 audio interface


{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/id22.png)
{: refdef}


I bought my Audient iD22 sometime back in 2016.  It was B-stock from a music store and has been rock-solid in the ways that I've used it. Mostly as a DAC and monitor controller, plus the occasional line-level synthesizer recording.  

However, recent purchases have required the use of phantom power, which I have unforuntately discovered my interface cannot provide.

## Phantom power, giving up the ghost

After some testing, the issue seems to be down to the output voltage.  It's low.  A multimeter directly on the combo jacks measures 38VDC on a cold start, gradually creeping upwards to about 45VDC after 10-15 minutes, but without any current. (measured according to [here](https://service.shure.com/s/article/how-to-test-phantom-power-voltage-and-current?language=en_US)).

[I'm not alone](https://gearspace.com/board/music-computers/1050068-audient-id22-issues-11.html).  This gearspace thread starts in 2015, with a good deal more activity into 2020 and 2021.  It seems mine, and other problems, are starting to plague this unit.

While these claims drew some comments from Audient ([Post No. 292](https://gearspace.com/board/showpost.php?p=15291215&postcount=292)) :

> ...we have spent the last couple weeks collecting service data from all of our major markets across the world to get a deeper understanding of the situation (hence the delay in responding here). After much consideration, the data we have collected and further analysed is not reflective of some of the comments that have been indicated here. However, we very much appreciate each and every customer and do not take any of the issues you have experienced lightly.

I highly doubt this is as uncommon as they'd have us believe. After taking a look inside, I see a few failure modes from some design choices.  


## What lies beneath

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/insides.jpg)
{: refdef}

Specifically the use of some C-tier capacitors (Fujicon, Jamicon, and ...LH. Nova?). There is also a [known-problematic Capacitor](https://www.youtube.com/watch?v=pRiQl7Vy4R8), CF2, which is *right next to a heatsink* and only rated at 85C.

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/badcap.jpg)
{: refdef}

## Too hot to handle
Replacing this specific cap has solved some issues for people with pops/crackle in the audio, but the *reason* for this failure is likely due to a shortned lifespan from overheating. 

Why?  Khron has a very nice teardown and electronic exploration on his blogpost ([Audient iD22 Teardown](https://khronscave.blogspot.com/2021/02/66-audient-id22-teardown.html?m=1), and [the repair](https://khronscave.blogspot.com/2021/02/67-audient-id22-part-2-repair.html?m=1)).  His unit had an entirely dead analog section, with a detached heatsink.  Turns out the overall thermal management on his Audient seemed.... pretty inadequate!  Besides being undersized, the heatsink looked to be merely wedged/glued in place from the silastic, and the [LT3949](https://www.analog.com/media/en/technical-documentation/data-sheets/3439fs.pdf) beneath wasn't even soldered to the ground plane!  

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/chip.jpg)
{: refdef}

I haven't deconstructed my own as far, but a quick thermal measurement found the heatsink getting to 142.1F (61.2C)

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/temp.jpg)
{: refdef}


## Thermals 

The [LT3439 datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/3439fs.pdf) gives operational ranges up to 125C, but a footnote (pg.2) guarantees performance specifications only up to a junction temperature of 70C (158F).  

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/datasheet.png)
{: refdef}

Hitting 60C+ is bad enough, but considering the measurement was taken in a chilly apartment (68F) and outside of the enclosure...it cannot be good to be this close to the margins, especially in such ideal measurment conditions.  

Considering this board sits in an unventilated metal enclosure that regularly receives afternoon sun on its black face, I can only assume the junction temperature is well into the "statistical process" territory.  There's also the added 'always-on' design flaw for the iD22.  Without a power switch, the unit will draw power, dissapate heat, and slowly cook itself to death.

## Capacitor life

For the sake of argument, lets assume that the problem cap, CF2 --  [a 2000 hour part](https://store.comet.bg/en/Catalogue/Product/29481/) -- gets roughly as hot as the heatsink, say 140F (60C).  This seems reasonable given it will be in a metal box, and closest to the heatsink.  Using [this calculator](https://eepower.com/tools/electrolytic-capacitor-life-calculator/#), and the following inputs:

* L1- Load Life Rating: 2000hrs
* Vr - Max Volt. rating: 63V
* Tm - Max temp. rating: 85C
* Ta - Ambient temp: 60C

the calculated capacitor lifetime is 22,627 hrs.  This translates to the following lifetimes for various duty cycles (assumes daily use):

* 4hrs / day : 15.5 years
* 8hrs / day : 7.75 years
* 12hrs / day: 5.2 years
* 24 hrs / day : 2.6 years

These last two are particularly troubling.  Because the device is always on, it's not unreasonable to assume use cases where it's on 24/7 just from being directly plugged into an outlet, or 8-12 hours a day if used at a workstation.  

Ambient temperature has the biggest effect on this computation. Lets be generous and assume the capacitor only gets to 120F, or approximately 49C.  That's a 48,503 hour lifetime.  With a 100% duty cycle (my unit was pretty much always plugged into the wall), thats 5.5 years.  

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/pikachu.png)
{: refdef}

## Other caps and lifetimes

Other capacitors on the analog board include:

* 220uF, 25V at 105C (qty. 4)
* 100uF, 25V at 85C (qty. 16)
* 10uF, 16V at 105C (qty. 28)
* 47uF, 63V at 105C (qty. 3)

Four of the 100uF 85C caps are not that much further away from the heat sink, on the other side, making them susceptible as well.  Why not make all these caps 105C rated?  And why aren't they nichicon or rubycon?  I would have hoped such a prosumer device would have better quality parts.


## Conclusion

Given the thermal measurements and always-on design, it is no wonder people's units are failing after ~4-6 years.  Audient *has* extended their warranty from 1 to 3 years, but this move will do nothing to fix this problem.

There's about [80 electrolytic caps](https://docs.google.com/spreadsheets/d/1ARY4sbc7E2XFgQhkSMwCjVR8KNS4MbVoTxi-IBfXW9o/edit?usp=sharing) on the device, and I wonder whether it would be worthwhile to go through and re-cap the entire unit.  The 85C caps, at the very least.   I might get around to it if I feel the need to procrastinate on my work.


## Update: April 25, 2021 -- Low voltages?

Absent any schematics, I've tried probing around to see where certain voltages are coming from.  
{:refdef: style="text-align: center;"}
![voltages](http://www.sci.utah.edu/~jimmy/website/audient/voltages.png)
{: refdef}

I'd be curious if anyone with a working iD22 has similar readings.  I have a nagging suspicion that these are low, which could point to an ailing LT3439.  This is as far as I think I can get on my own.
