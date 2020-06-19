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

## Running Modulation Programs

At this point, I am unfamiliar with using CMake or makefiles in general. Therefore, I use the following to compile and run my code:

`aman@Pendragon:~/Documents/Live-Modulation/portaudio/examples$ gcc mirror.c libportaudio.a -lrt -lm -lasound -ljack -pthread -o bihhh.out && ./bihhh.out`


## Performance Optimization

Though the programs seem to work in their initial configuration, there are still problems with underrun, some compilation warnings and errors, and generally a need for cleaner, faster, and proper code. 

__ERRORS:__

1. `ALSA lib pcm.c:8526:(snd_pcm_recover) underrun occurred`: Occurs whenever other tasks are run on the computer at the same time as the program. Seems to relate to resource constraints? Is non-deterministic. 

2. Upon startup for __any__ example files, the following errors occur:
```
ALSA lib pcm_dsnoop.c:641:(snd_pcm_dsnoop_open) unable to open slave
ALSA lib pcm_dmix.c:1089:(snd_pcm_dmix_open) unable to open slave
ALSA lib pcm.c:2642:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.rear
ALSA lib pcm.c:2642:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.center_lfe
ALSA lib pcm.c:2642:(snd_pcm_open_noupdate) Unknown PCM cards.pcm.side
Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
ALSA lib pcm_oss.c:377:(_snd_pcm_oss_open) Unknown field port
ALSA lib pcm_oss.c:377:(_snd_pcm_oss_open) Unknown field port
ALSA lib pcm_usb_stream.c:486:(_snd_pcm_usb_stream_open) Invalid type for card
ALSA lib pcm_usb_stream.c:486:(_snd_pcm_usb_stream_open) Invalid type for card
ALSA lib pcm_dmix.c:1089:(snd_pcm_dmix_open) unable to open slave
``` 



