# Live-Modulation

Portaudio live modulation algorithms written in C for Linux (Ubuntu 20.04).

## Goal

The goal here is to make a very simple gain LFO that, based on what it reads from a local text file every second, will apply a gain LFO to a local audio file that it plays/modulates in real time.

## Installation

Process based on [PortAudio Tutorials](http://portaudio.com/docs/v19-doxydocs/tutorial_start.html):

1. Installed ALSA (Audio API): `sudo apt-get install libasound-dev`.
2. Downloaded most recent, stable release (October 30, 2016) from [here](http://www.portaudio.com/download.html). 
	- Extracted to `/portaudio`, ran `./configure && make`. 

## Basic Structure

The library is employed and customized through a `callback` function. The function has several input arguments including I/O buffers, user settings, and buffer lengths (because who doesn't live C's lack of array lengths). Seems like you can just perform operations on the input and/or output to synthesize/modulate different streams.

The question then arises, how does one employ various audio streams? Hopefully we will find this out over the course of our exploration. 

## Running Example Files

At this point, I am unfamiliar with using CMake or makefiles in general. Therefore, I use the following to compile and run my code:

`aman@Pendragon:~/Documents/Live-Modulation/portaudio/examples$ gcc mirror.c libportaudio.a -lrt -lm -lasound -ljack -pthread -o bihhh.out && ./bihhh.out`

