---
layout: post
title: "Une Table Sonore by Raphael Panis"
date: 2018-12-15
categories:
  - "Instruments"
  - "Projects"
  - "Sound Design"
  - "Installations"
description: "Une Table Sonore by Raphael Panis"
image: table-sonore/header.jpg
author: bela
---

In this post Raphael Panis introduces us to Une Table Sonore: a percussive table that uses vibration sensing, audio transducers, additive synthesis and Bela to create an intuitive and exciting musical instrument.

{% include single-image.html fileName="table-sonore/playing-hat.jpg" %}


This project was created as part of Raphael's work on the masters course [Réalisateur en Informatique Musicale](https://musinf.univ-st-etienne.fr/rim.html) (Producer in Computer Music) at the University of St Etienne. Raphael will now talk us through the inspiration for this project and and the techniques he used to create it.

# Une Table Sonore

Below is a video of Raphael explaining and playing the instrument (in French):

{% include vimeo.html vimeo="264852700" %}

For my final year project on the RIM Masters at St Etienne I was very interested in creating an augmented instrument and in using the opportunity to work with Bela.
I envisioned the project as combining elements of real-time percussion (the role of Bela) with a generative electronic part that the performer would play along with.
The electronic part was created using MAX/MSP which I used to analyse the playing of the instrumentalist and to follow their performance in relation to a score using [Antescofo](https://forumnet.ircam.fr/product/antescofo-en/) from IRCAM, the real-time score following external.

{% include single-image.html fileName="table-sonore/purple-1.jpg" %}



## The instrument:

The percussion instrument at the centre of this project is in the form of a table that the performer directly strikes and which uses Bela to enrich the timbre of the acoustic sound produced.
There is one surface cut into two parts, one for each hand. Underneath each part there is a sound box.
Piezo sensors allow the detection of striking on the surface. A transducer is fixed to each sound box and Bela is in the middle of the chain, capturing signals from the piezos, and sending sounds to the transducers.
Having four piezos per surface gives a very approximate idea of the position of the hands, enough to be used to modulate timbre.

{% include single-image.html fileName="table-sonore/Table-Caisse.JPG" caption="The actuators within the sound boxes." %}

{% include single-image.html fileName="table-sonore/Table-Electronique.JPG" caption="The piezo discs and Bela board under the top surface." %}


## Additive synthesis:

As there are two surfaces, there are in fact two instruments. The sound for each is generated using additive synthesis. Each instrument has 12 partials, and each partial is controlled independently. Each one of these partials is parameterisable in frequency and in amplitude, and has an Attack-Decay amplitude envelope assigned to it.
The parameters of these partials are stored in an array which defines a strike's timbre. In addition to the fixed parameters, there are some variable coefficients of these parameters, so that by varying the force and the position of the strike the timbre changes, allowing for a rich and varied performance.

{% include single-image.html fileName="table-sonore/playing-hand.jpg" %}

I also took advantage of the connection of Bela to the computer to send information on the strikes. By doing so I didn't need a microphone to record the performance of the instrumentalist for the score-following because the information already arrived formatted in Max/MSP.


## Working with Bela:

The construction of the instrument, which in the end was only one aspect of this project, was very fast thanks to the quality of the Bela environment. In only a few months, and during a busy period, it was possible to go from prototype to a performance-ready instrument.

{% include single-image.html fileName="table-sonore/header.jpg" %}

As someone used to working with Arduino and able to write small scripts in Python, the passage to Bela was quite easy. I can only thank the Bela team for having built such a clear and user-friendly environment that can be very powerful, without the need to be a seasoned programmer! This project is a work in progress and still developing. For example I have also added capacitive sensing and copper strips to increase the palette of strikes and thus of timbres.

I should also add that to design the filters, I made use of [FAUST](https://faust.grame.fr), by modifying the C++ code generated by the FAUST compiler. The integration of FAUST was also pretty smooth. I have also recently been working at [GRAME](http://www.grame.fr) in Lyon on improving the integration of FAUST and Bela: more information on that coming very soon!


## Performances and installations:

Over the course of 2018 I have had the opportunity to present the instrument a couple of times.

### Textures Festival, St Etienne

During this festival the table was presented as part of an immersive audio and video installation that consisted of the table, 3 video projections and a quadrophonic sound system.
The video was generated by a video synthesizer built around an FPGA: for more info see [http://seetton.blogspot.fr/](http://seetton.blogspot.fr/).
The table was installed in the centre of the room and visitors were invited to freely explore the table. When they played the table it made sound and the quadraphonic sound environment and video reacted.

{% include vimeo-2.html left="261379091" right="261378683" %}

{% include single-image.html fileName="table-sonore/playing-scarf.jpg" %}


### The IRCAM Forum

In March 2018 I had the opportunity to present the instrument at the [IRCAM forum](https://forumnet.ircam.fr/) in Paris. For more information see here: [http://forumnet.ircam.fr/ircam-forum-workshops-paris-preliminary-program-2018/](http://forumnet.ircam.fr/ircam-forum-workshops-paris-preliminary-program-2018/)

{% include single-image.html fileName="table-sonore/purple-2.jpg" %}

For more information on Raphael's work you can visit his blog [http://rpanis.blogspot.fr/](http://rpanis.blogspot.fr/). Thanks to Raphael for sharing this project with us and we look forward to hearing more in the future.


