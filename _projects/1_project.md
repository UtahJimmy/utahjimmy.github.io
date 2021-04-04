---
layout: post
title: Working with asthmatics
description: Want effective data collection? Text them.
---

This is a quick summary of a previous research into how asthmatics would interact with a [wireless air quality system](https://vdl.sci.utah.edu/publications/2018_imwut_maav/){:target="_blank"}.

Air Quality?  Like Outside?
============

Mention "air quality" to people and they may tacitly assume you are talking about the outdoors.  But a lot of what we do *indoors* impact the air quality of our homes, as well.  There's the usual stuff you might expect:  cooking, cleaning, etc.  But also some things you would *not* expect:  making the bed, vacuuming, doing laundry.

As something that's mostly (hopefully!) invisible, air quality can be easy to ignore.  While invisible, it *is* higly dymanic and interconnected with the rest of you living space in ways you might not expect.  Does the cooking in your kitchen affect your bedroom?  How would you even know?

Detecting air quality -- which boils down to measuring the concentrations of [small, airborne particulates](https://www.epa.gov/pm-pollution/particulate-matter-pm-basics) (those [2.5 microns and below](https://blissair.com/what-is-pm-2-5.htm), in our case) --- is something your average, everyday person hasn't been able to do from a lack of affordable or commercially available systems. This has [started to change](http://www.aqmd.gov/aq-spec) of late, but was the motivation behind our project in 2017.

The System
============

{:refdef: style="text-align: center;"}
![header](/assets/images/projects/maav/IMG_9950.png)
{: refdef}

We hacked some [off-the-shelf Dylos air quality sensors](http://www.dylosproducts.com/ornodcproair.html) to add local datalogging and wireless transmission capabilities.  The software architecture behind this was *very* non-trivial and [received it's own write-up](https://span.ece.utah.edu/pub/EpiFi.pdf) for a sensors conference.



{:refdef: style="text-align: center;"}
![header](/assets/images/projects/maav/IMG_20170221_123704.jpg)
{: refdef}

We bought and modified about 20 of these senors and arranged to deploy them in the homes of six asthmatic families.  Each family would get three sensors to  place wherever they liked.  We let these run for about a month to collect some baseline data, then followed up with a tablet interface so people could interactively view and annotate their data, along with a Google Home for making voice annotations.


The Interface
======

{:refdef: style="text-align: center;"}
![header](/assets/images/projects/maav/interface.png)
{: refdef}


Data Analysis
========


Interviewing
=========


The Results
=======

* Having multiple monitors lets you make comparisons
* The ability to annotate your data improves the over-all user-experience and sense of engagement
* The interactive interface w/ data annotations let people explore their data
* People used this system for a long time!  Texting was very popular!

Recommendations
========

## People want to do more than "compare two sensor streams"

Data logging systems could benefit from some more sophisticated practices


## text messages are a good way to collect data from people


## People's personal knowledge and usage patterns change over time

It would be nice to have flexible systems that could track people's experiential growth and offer new or different functionalities depending one people's skills, goals, knowledge, etc.


Reflections
=======


Looking back on this project....

