---
layout:post
title: Image dithering
---

A friend and I were talking about the old-school dithering effects of gameboys and apple II's, and I fell down a rabbit hole of spec sheets and image processing. 
Here are some links to read up on some of the details behind how those nostalgic image artefacts came to be, and how to re-create it.

[The GameBoy Camera](http://web.csulb.edu/~wmartinz/rssc/content/MS_77.html)

[The camera sensor spec sheet](https://people.ece.cornell.edu/land/courses/ece4760/FinalProjects/f2012/qs44_twc55/qs44_twc55/datasheets/MITSUB_image_sensor.pdf) (see pages 9 and 14 for the kernel and weights)

And some background on [edge-detection and laplacians](https://html.alldatasheet.com/html-pdf/146598/MITSUBISHI/M64282FP/6064/10/M64282FP.html) for good measure

**The modern re-creation**

Github Gist for converting PNGs (will not work on jpegs!): [link](https://gist.github.com/s3krit/39725ba2f4ca9e6a09d01ea6863516c7)

copy the script at the github link, make sure you have execution permission `($chmod u+x gbcam.sh)`, then run it via: `./gbcam.sh <picname.png>`


[This article](https://surma.dev/things/ditherpunk/) does a deep dive into some modern implementations and has a bunch of great info in general