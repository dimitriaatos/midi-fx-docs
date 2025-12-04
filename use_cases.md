# Use Cases

These will help during the design of the API. Feel free to add to it! Anything goes, there are no rules.

## Hardware Mapping/Integration

- Map buttons on a launchpad matrix to chords, with parameters like velocity, scale/key, octave, and strum/arp adjustable by knobs and buttons.
- Make different devices work together. 
	- use launchpad knobs to adjust the velocity curve of MIDI keyboard.
	- if a chord is played on the keyboard, the corresponding button on the launchpad matrix could light up

## Talking to DAW Scripts

FL Studio's MIDI scripting API can read/write the parameter values of the active plugin. 
The same physical knobs can be mapped to parameters of different plugins. 
The plugin in focus would have its parameters mapped to hardware.

## Accompaniment

You play notes, it plays notes back. Like these randomized delay effect from the MIDI HUB demo: https://www.youtube.com/watch?v=ASruOUG2HIs

## Procedural MIDI Generation

MIDI notes can be created based on rules. Like LFOs for CC values. Or something more creative like circle music: https://youtu.be/c1iqhWTPrU8

## Filter messages, based on other messages

It may be used to remember state. But this video shows a more fun use: https://www.youtube.com/watch?v=tQGt9yRUy2k

## Configuration of MIDI hardware

Sometimes we want to initialize MIDI hardware to certain parameters, like a particular preset, or the pitch bend range or other setting. 
Sometimes we may also want to configure it through the PC with a GUI instead of physically reaching out to the device.
