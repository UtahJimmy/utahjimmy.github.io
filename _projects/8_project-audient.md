---
layout: post
title: "Phantom Power"
description: "Audient iD22 giving up the ghost?"
---
{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/id22.png)
{: refdef}

I bought my Audient iD22 sometime back in 2016.  It was B-stock from a music store and has been rock-solid in the ways that I've used it. Mostly as a DAC and monitor controller, plus the occasional line-level synthesizer recording.  

However, recent purchases have required the use of phantom power, which I have unforuntately discovered my interface cannot provide.

After some testing, the issue seems to be down to the output voltage.  It's low.  A multimeter directly on the combo jacks measures 38VDC on a cold start, gradually creeping upwards to about 45VDC after 10-15 minutes, but without any current. (measured according to [here](https://service.shure.com/s/article/how-to-test-phantom-power-voltage-and-current?language=en_US)).

[I'm not alone](https://gearspace.com/board/music-computers/1050068-audient-id22-issues-11.html).  This gearspace thread starts in 2015, with a good deal more activity into 2020 and 2021.  It seems mine, and other problems, are starting to plague this unit.

While these claims drew some comments from Audient ([Post No. 292](https://gearspace.com/board/showpost.php?p=15291215&postcount=292)) :

> ...we have spent the last couple weeks collecting service data from all of our major markets across the world to get a deeper understanding of the situation (hence the delay in responding here). After much consideration, the data we have collected and further analysed is not reflective of some of the comments that have been indicated here. However, we very much appreciate each and every customer and do not take any of the issues you have experienced lightly.

I highly doubt this is as uncommon as they'd have us believe. After taking a look inside, I see a few failure modes from some design choices.  

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/insides.jpg)
{: refdef}

Specifically the use of some C-tier capacitors (Fujicon, Jamicon, and ...LH. Nova?). There is also a [known-problematic Capacitor](https://www.youtube.com/watch?v=pRiQl7Vy4R8), CF2, which is *right next to a heatsink* and only rated at 85C.

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/badcap.jpg)
{: refdef}

Replacing this specific cap has solved some issues for people with pops/crackle in the audio, but the *reason* for this failure is likely due to a shortned lifespan from overheating. 

Why?  Khron has a very nice teardown and electronic exploration on his blogpost ([Audient iD22 Teardown](https://khronscave.blogspot.com/2021/02/66-audient-id22-teardown.html?m=1), and [the repair](https://khronscave.blogspot.com/2021/02/67-audient-id22-part-2-repair.html?m=1)).  His unit had an entirely dead analog section, with a detached heatsink.  Turns out the overall thermal management on his Audient seemed.... pretty inadequate!  Besides being undersized, the heatsink looked to be merely wedged/glued in place from the silastic, and the [LT3949](https://www.analog.com/media/en/technical-documentation/data-sheets/3439fs.pdf) beneath wasn't even soldered to the ground plane!  

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/chip.jpg)
{: refdef}

I haven't deconstructed my own as far, but a quick thermal measurement found the heatsink getting to 142.1F (61.2C)

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/temp.jpg)
{: refdef}

The [LT3439 datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/3439fs.pdf) gives operational ranges up to 125C, but a footnote (pg.2) guarantees performance specifications only up to a junction temperature of 70C (158F).  

{:refdef: style="text-align: center;"}
![id22](http://www.sci.utah.edu/~jimmy/website/audient/datasheet.png)
{: refdef}


Hitting 60C+ is bad enough, but considering the measurement was taken in a chilly apartment (68F) and outside of the enclosure...it cannot be good to be this close to the margins, and in such ideal measurment conditions.  Given that this board sits in a sturdy metal enclosure, often receiving afternoon sun on its black face, and without any ventilation, I can only assume the junction temperature is well into the "statistical process" territory.  

Because the 2.2uF capacitor sitting right next to this heatsink is [a 2000 hour part](https://store.comet.bg/en/Catalogue/Product/29481/), it is no wonder people's units are failing more frequently after ~4-6 years.  Audient's warranty extension to 3 years will do nothing to fix this. This is still conveniently right before that cap would dry out.


I wonder whether it would be worthwhile to go through and re-cap the entire unit.  There's about [80 electrolytic caps](https://docs.google.com/spreadsheets/d/1ARY4sbc7E2XFgQhkSMwCjVR8KNS4MbVoTxi-IBfXW9o/edit?usp=sharing) on the device, and I might get around to it if I feel the need to procrastinate on my dissertation.


More to come as the story develops....

