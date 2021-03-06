---
layout: post
title: "SuperCollider and Bela: live code your sensors"
date: 2017-10-29
categories:
  - "Tutorials"
  - "Software"
description: "Live-coding hardware"
image: bela-and-supercollider-live-coding-sensors/alo-allik.jpg
author: bela
---
This post is an update on the latest developments in using SuperCollider with Bela. It explains how to get SuperCollider running on Bela and how you can start live coding your projects.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/bela-sc-3.png" %}

Bela is a polyglot: we've always wanted it to be as flexible as possible and to be able to speak the favourite computer music language of the people who use it. Right now it is possible to code Bela projects in [C++](https://github.com/BelaPlatform/Bela/wiki/Example-projects-and-tutorials) and [Pure Data](https://github.com/BelaPlatform/Bela/wiki/Running-Puredata-patches-on-Bela), and more experimentally in [Faust](https://github.com/BelaPlatform/Bela/wiki/Compiling-Faust-code-for-Bela) and [Pyo](https://github.com/belangeo/pyo-bela). This post gives an update on the latest language that is supported on Bela, the ever-flexible [SuperCollider](https://supercollider.github.io/).

## What is SuperCollider?

[SuperCollider](https://supercollider.github.io/) is an open source software environment and dynamic coding language for audio synthesis and algorithmic composition. It was developed by James McCartney in 1996, and since 2002 when it was released with as a free and open software it has blossomed into one of the most popular computer music languages used by musicians, artists and researchers working with sound. The SuperCollider software offers a different paradigm for creating electronic music in comparison to code-based options such as C++ or data-flow options such as Pure Data and Max/MSP: instead of having to compile your code after every edit SuperCollider allows execution of lines of code on-the-fly, without interrupting the audio. This opens up a set of new possibilities that revolve around the practice of live-coding: rewriting programs on-the-fly in an improvised manner to create live sound or visuals.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/live-code-fest-knotts-allik.jpg" caption="Shelley Knotts and Alo Allik live coding visuals and sounds at the Live Code Festival 2013." %}

There are three main components to SuperCollider: `scsynth` is the audio core of the platform which features hundreds of unit generators (UGens, the SuperCollider term for a plugin) for analysis, synthesis and processing; `sclang` is the interpreted programming language (i.e. instructions can be executed directly without compilation) that acts as the algorithmic and sequencing heart of SuperCollider that controls scsynth via [Open Sound Control (OSC)](https://en.wikipedia.org/wiki/Open_Sound_Control); `scide` is the glue that binds the above two parts together, an editor for writing and executing `sclang`.

The whole system has a client/server architecture: the server `scsynth` runs the audio processing and can instantiate, connect and control new audio processing blocks in response to specific OSC messages it receives from a client.
The SuperCollider client of choice has been `sclang` (often referred to as "the language" of SuperCollider), but the client can be any program capable of formatting messages as OSC.
`Sclang`, itself, is an object-oriented programming language that allows the definition of synth voices, the running of patterns, the creation of GUI elements, and the execution of many base units of algorthimic composition.
The benefit of this particular architecture comes from its flexibility: in many cases the server and the client will run on the same machine, however they can easily live on separate machines on the same network, opening up great possibilities for distributed control of multiple synth engines and networked performances. As we'll see, this is really handy for working with Bela, as the audio synthesis and sensor processing can be run on the board with the control coming from a separate machine that executes lines of code on-the-fly.

## Writing code in SuperCollider

Typically users write their code in the SuperCollider IDE which allows you to send the code line-by-line or block-by-block to the interpreter.
This is the foundation of many live coding performance practices where artists will improvise with their code blocks, executing blocks one at a time and updating parameters and coding structures as they go.
`Sclang` is just one language that can be used with SuperCollider, there are many other high-level languages that build on the same logic and interact with the SuperCollider server, for instance [Tidal](https://tidalcycles.org/getting_started.html), [ScalaCollider](http://www.sciss.de/scalaCollider/), [Overtone](http://overtone.github.io/) or [ixi lang](http://www.ixi-audio.net/content/software.html).

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/live-coding-sc-ide.jpg" %}

## SuperCollider and Bela

Bela allows you to take control of the audio generated by SuperCollider in realtime by connecting analog and digital sensors to the board which can interact with the code. Additionally, the analog and digital outputs allow you to interface with analog synthesizers by outputting CV, or to control LEDs, motors or other bits of hardware for kinematic installations.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/bela-sensors.jpg" %}

Bringing Bela and SuperCollider together has been a large community effort, with many people contributing to its development. Thanks to the combined work of [Marije Balmaan](https://www.marijebaalman.eu/), [Giulio Moro](https://github.com/giuliomoro), [Dan Stowell](http://www.mcld.co.uk/research/), [Till Bovermann](http://tai-studio.org/), [Jonathan Reus](http://jonathanreus.com/) and many others, it is now possible to run SuperCollider on Bela and to access all the inputs and outputs of Bela from within the SuperCollider server, all this with the low-latency that characterizes the whole Bela environment.
The first major steps towards integrating SuperCollider with Bela happened around the instrument building workshop that we led at [STEIM in August 2016](http://blog.bela.io/2016/12/15/steim/). At this workshop we had five of the eight instruments running on SuperCollider. Since then we have held various [workshops](http://blog.bela.io/category/workshops/) that have focused on using SuperCollider with Bela and a couple of internal hackathons where the support of the language has been pushed forward.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/la-diantenne.jpg" caption="La Diantenne, a pitched percussion instrument by Dianne Verdonk. This instrument was ported to Bela running SuperCollider during the STEIM workshop." %}

Getting SuperCollider to work on Bela has been achieved by creating a number of customized `UGens` and an audio backend which ties them to the Bela API.
Bringing SuperCollider and Bela together offers a new paradigm for live coding, adding physical interation to the core SuperCollider environment.

## Getting started

If your Bela board is up-to-date then SuperCollider will already be installed, however you will want to make sure you are running the [latest release](https://github.com/giuliomoro/supercollider/releases) which is being updated regularly.
To get started with SuperCollider on Bela you can go through the examples provided on the board, which can be found in the example browser in the IDE.
These example can be run just like any other Bela project, by simply pressing the "run" button: if there is a `_main.scd` file in your project this will be passed to `sclang` for execution.
The below images summarise the two different ways that Bela and SuperCollider can interact. In the first case both `sclang` and `scsynth` are run on the board.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/Bela SuperCollider workshop2.jpg" %}

In the second case we can take remote control of `scsynth` running on the board by running `sclang` within SuperCollider on a separate machine and communicating with Bela through OSC messages.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/Bela SuperCollider workshop3.jpg" %}


Each of the example projects that we have created also contains a wiring diagram to help you connect sensors or any other hardware that is required: [github.com/giuliomoro/bela-sc-examples](https://github.com/giuliomoro/bela-sc-examples).

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/sc-wiring.jpg" %}

## Bela inputs and the language

This snippet of code shows how to read a digital input and activate a digital output in response:

```supercollider
	SynthDef('buttonControl', {arg inPin, outPin;
		var button = DigitalIn.ar(inPin);
		DigitalOut.ar(outPin, button);
	}).add;
```

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/blinking_led_bela_sc.gif" %}


Similarly the analog inputs and outputs can be read as follows, and are received with the same low latency performance as when running c++ code on Bela:

```supercollider
	SynthDef('ledFade', {
		var rate = AnalogIn.ar(0).exprange(0.3, 20);
		var amp = AnalogIn.ar(1);
		// returns a value from 0-1
		rate.poll(1); amp.poll(1);
		AnalogOut.ar(0, SinOsc.ar(rate).range(0.0, amp));
		// send to Analog Output 0
	}).add;
```

In SuperCollider high-level behaviours such as patterns, tasks, routines are typically implemented in the language.
For this reason controls such as MIDI, serial, network are typically handled by the langauge itself.
However in the case of Bela the analog and digital inputs are available to the server only, in order to guarantee low-latency and high bandwidth to control sound parameters.
Conveniently it is still possible to send these controls back to the language using the `SendReply` object.
In the snippet below, the values read from the analog inputs 0 and 1 are sent back to the language 10 times per second:

```supercollider
	var a0 = AnalogIn.ar(0);
	var a1 = AnalogIn.ar(1);
	SendReply.kr(Impulse.kr(10), '/ctrl', [a0, a1]);
```

When using SuperCollider on Bela you can also take advantage of the server/client architecture by running the language and the SuperCollider IDE on your computer while running `scsynth` on Bela. Like this so you can use a live coding approach for experimenting and trying things out. Then once you've finalized your project you may want to run `sclang` on Bela to be able to run your program without live-coding interaction, for instance to make a stand-alone instrument running on battery.

If you want to live code Bela from the SuperCollider IDE, you have to download the [Bela class files](https:/github.com/sensestage/bela-remote) on your computer and follow the instructions in the README file. This way of working allows you to execute code on your machine and directly communicate with scsynth running on the Bela board.
For this to work you need to make sure you are running SuperCollider 3.8 or above on your computer.

{% include youtube.html youtube="T7KMe1TPMCk" %}

## Projects made using SuperCollider and Bela

### [Fielding by Till Bovermann](http://tai-studio.org/portfolio/fielding.html)

{% include vimeo.html vimeo="237296449" %}

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/fielding-bovermann-2.jpg" %}

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/fielding-bovermann.jpg" %}


### [The Intimate Earthquake Archive](http://sisselmarietonn.com/The-Intimate-Earthquake-Archive) by [Marije Baalman](https://www.marijebaalman.eu/), [Jonathan Reus-Brodsky](http://jonathanreus.com/) and [Sissel Marie Tonn](http://sisselmarietonn.com/)

{% include vimeo.html vimeo="215224777" %}

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/the-intimate-earthquake.jpg" %}

## What's next?

Porting SuperCollider to Bela has involved the efforts of many people and the process of making it fully supported on Bela is still not 100% complete. We recently have announced the Beta version, but we are aiming to release a stable version in the near future. Any feedback we can get from users of SuperCollider who are working with Bela would be much appreciated so please get in touch or list issues on our [forum](https://forum.bela.io/). In the near future you can expect the following developments:

### Integrating support for the Bela Scope.

The Bela oscilloscope that can be used via the browser is not currently accessible via SuperCollider.
We are hoping to make this possible soon, as it is a very useful tool and offers more advanced features than SuperCollider's own `Scope` object.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/scope-advanced.gif" %}


### Live coding from within the Bela IDE.

Currently the Bela IDE can be used only to run code non-interactively and we need to resort to the SuperCollider IDE running on the host computer to do live-coding.
We are going to add the possibility of executing snippets of code from within the Bela IDE, making it even easier to get started.

{% include single-image.html fileName="bela-and-supercollider-live-coding-sensors/supercollider-execute.gif" %}


### More bug fixes

SuperCollider was designed with a desktop environment in mind, and porting it to the constrained environment of an embedded platform requires further work and optimizations.
We hope that some of the improvements we propose will eventualy make their way upstream so that they can be useful to all SuperCollider users, not only those that use it on Bela.
Ultimately we aim to be able to merge the Bela developmnet branch back into the main SuperCollider development branch, which would make maintenance easier for us.
You can track the open issues on [github.com/sensestage/supercollider/issues](https://github.com/sensestage/supercollider/issues) and get the latest release of SuperCollider for Bela from [github.com/giuliomoro/supercollider/releases](https://github.com/giuliomoro/supercollider/releases).

### Links

For more information about supercollider and some great resources for learning this language have a look at these links:

- [SuperCollider](https://supercollider.github.io/)
- [Algorave](https://algorave.com/about/)
- [Toplap](https://toplap.org/)
- [Till Bovermann's pointers for using Bela and SuperCollider](http://blog.bela.io/2017/09/29/till-bovermann-bela-supercollidor/)
