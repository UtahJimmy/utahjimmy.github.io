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

This was written in [D3.js](https://d3js.org/) and is a modified [Focus+Context block](https://observablehq.com/@d3/focus-context) with some [programmatic control](https://d19jftygre6gh0.cloudfront.net/micahstubbs/3cda05ca68cba260cb81) of the brush widths to match user-selected zoom levels, on the left.  This was skinned to look like Grafana people really liked it!  The red triangles indicate the presence of user-provided annotations to help contxtualized the data (more on that later).  The interface was intentionally stripped-down and kept simple because: (1) We didn't want there to be a high barrier-to-entry, and (2) we weren't sure what people might want to do with the system or their data, so we weren't about to go bounding into designing something blind.  This design served its purpose as a simple data review interface, and was good to get something in people's hands so that we could get some feedback (and observations) on how they used it.

Data Processing, Spike Detection & User Alerts
========

These deployments ran for a while (up to a year), and collected a *lot* of data.  This was challenging for fluidly displaying data on the cheapie Amazon fire tablets we used, as well as maintaining some visual fidelity of our minute-by-minute measurements from each sensor datastream.

#### The overplotting is real

{:refdef: style="text-align: center;"}
![header](/assets/images/projects/maav/overplot.gif)
{: refdef}
(from: ["Too Big Data: Coping with Overplotting"](https://www.infragistics.com/community/blogs/b/tim_brock/posts/too-big-data-coping-with-overplotting))


The chart portion of our interface had about 400 pixels of horizonal real-estate.  Utilized fully, it's possible to display 400 datapoints.   Because our system logged data every minute, this only allows you to show at most 6.66 hours before you run into [overplotting issues](https://www.infragistics.com/community/blogs/b/tim_brock/posts/too-big-data-coping-with-overplotting).  Not a problem for our 3 or 6 hour view modes, but anything more needed some help.  

Enter the 'Largest Triangle, Three Buckets' algorithm (demo [here](https://www.base.is/flot/)) fom [Sveinn Steinarsson's](https://github.com/sveinn-steinarsson) master's thesis: ["Downsampling Time Series for Visual Representation](https://skemman.is/bitstream/1946/15343/3/SS_MSthesis.pdf).  Inspired by cartographic methods for preserving coastline features on maps, this wonderful algorithm allowed us to downsample our data into a visually similar reproduction of arbitrary time ranges.  You need to convert 50,000 datapoints into a visually-equivalent 1000 point plot?  This does it.  A great piece of work and exactly what we needed to maintain fluid interactivity and visual fidelity of people's jagged and dynamic air quality measurements.  Simply using a windowed aggergation approach would have smoothed out those dynamics, which was a big no-no for us.





#### Detecting and alerting spikes

(TBD)
We used [Twillio](https://www.twilio.com/) and a variant of the [Smoothed Z-Score algorithm](https://stackoverflow.com/questions/22583391/peak-signal-detection-in-realtime-timeseries-data/22640362#22640362) to detect the presence of spikes as they occured so we could apply some "just-in-time interventions" to alert users of an air quality 'event' in their homes, and have them text us what they thought the cause to be.  This served multiple purposes in our study, but mostly to collect a self-annotated dataset, and keep participants engaged with their own deployment.




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

#### People want to do more than "compare two sensor streams"

Data logging systems could benefit from some more sophisticated practices


#### text messages are a good way to collect data from people


#### People's personal knowledge and usage patterns change over time

It would be nice to have flexible systems that could track people's experiential growth and offer new or different functionalities depending one people's skills, goals, knowledge, etc.


Reflections
=======


Looking back on this project....

