# RtMidi

[![Build Status](https://travis-ci.org/thestk/rtmidi.svg?branch=master)](https://travis-ci.org/thestk/rtmidi)

A set of C++ classes that provide a common API for realtime MIDI input/output across Linux (ALSA & JACK), Macintosh OS X (CoreMIDI & JACK) and Windows (Multimedia).

By Gary P. Scavone, 2003-2019.

This distribution of RtMidi contains the following:

- `doc`:      RtMidi documentation (also online at http://www.music.mcgill.ca/~gary/rtmidi/)
- `tests`:    example RtMidi programs

On Unix systems, type `./configure` in the top level directory, then `make` in the `tests/` directory to compile the test programs.  In Windows, open the Visual C++ workspace file located in the `tests/` directory.

If you checked out the code from git, please run `./autogen.sh` before `./configure`.

## Overview

RtMidi is a set of C++ classes (`RtMidiIn`, `RtMidiOut`, and API specific classes) that provide a common API (Application Programming Interface) for realtime MIDI input/output across Linux (ALSA, JACK), Macintosh OS X (CoreMIDI, JACK), and Windows (Multimedia Library) operating systems.  RtMidi significantly simplifies the process of interacting with computer MIDI hardware and software.  It was designed with the following goals:

  - object oriented C++ design
  - simple, common API across all supported platforms
  - only one header and one source file for easy inclusion in programming projects
  - MIDI device enumeration

MIDI input and output functionality are separated into two classes, `RtMidiIn` and `RtMidiOut`.  Each class instance supports only a single MIDI connection.  RtMidi does not provide timing functionality (i.e., output messages are sent immediately).  Input messages are timestamped with delta times in seconds (via a `double` floating point type).  MIDI data is passed to the user as raw bytes using an `std::vector<unsigned char>`.

## Windows

In some cases, for example to use RtMidi with GS Synth, it may be necessary for your program to call `CoInitializeEx` and `CoUninitialize` on entry to and exit from the thread that uses RtMidi.

## OSX / macOS

- In *multithreaded* setups port enumeration might not properly update which is due to the macOS system processing loops not being called. To resolve make sure to call `RtMidi_multithreadRunLoop()` (declared only when `__APPLE__` is defined which should be automatically) in relevant threads (other threads (the first thread) in which RtMidi objects have been instantiated). Also see example `tests/backgroundscanner.cpp`.

## Further reading

For complete documentation on RtMidi, see the `doc` directory of the distribution or surf to http://www.music.mcgill.ca/~gary/rtmidi/.

## Legal and ethical

The RtMidi license is similar to the MIT License, with the added *feature* that modifications be sent to the developer.  Please see [LICENSE](LICENSE).
