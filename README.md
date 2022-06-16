- [EchoMIDI](#echomidi)
  - [Application](#application)
  - [Library](#library)
  - [Building](#building)
  - [Support](#support)

# EchoMIDI

EchoMIDI is a program + library that copies the output of a midi device into multiple output devices. This can be used in combinartion with other software, like [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html), in order to use a single midi input in multiple audio / midi applications at the same time. In addition, each output target can be muted manually or auto muted (also called FocusMute) depending on which application currently has the keyboard focus.


## Application

In development.
Currently a very simple command line implementation of the EchoMIDI library, allowing one to echo a single input device, per exe instance.

## Library

### Overview

Generally, each program using the EchoMIDI library should call EchoMIDIInit() before any Echoer::start() method is called, ideally before any other EchoMIDI function, and should call EchoMIDICleanup() when the EchoMIDI library features are no longer needed.

Each input MIDI device that needs to duplicate (or echo) its output, is associated with an Echoer instance. On construction, it needs a MIDI device id, which you can manually determine, or find by using the getMidiInIDByName() method. After construction, the output targets are added with the add() method and removed with the remove() method. Finally, an Echoer instance only echoes its associated MIDI devices output, if it has been started using the start() method.

Additional documentation can be generated by building the ALL target or the EchoMIDI_DOCS target, see [Building](#building).

### Exceptions

If at any point an error occurs in the library code, an MIDIEchoExcept will be thrown. Additional sub exception types exists for more specific error types. The exceptions might be nested.

## Building

EchoMIDI Uses CMake as its build system. It exposes the following options and targets.

> EchoMIDI                      (LIBRARY TARGET)
> EchoMIDIApp                   (EXECUTABLE TARGET)
> EchoMIDI_CONAN_AUTO_INSTALL   (OPTION ON/OFF)
> EchoMIDI_GEN_DOCS             (OPTION ON/OFF)

`EchoMIDI_CONAN_AUTO_INSTALL`
Automaticly downloads any dependencies and makes them avaliable to the build system.
Currently no dependencies exists, but there will come some in the future.

This requires Conan to be installed.

`EchoMIDI_GEN_DOCS`
Creates the `EchoMIDI_DOCS` target, which generates an HTML documentation, using Doxygen. It is also generated when building the `ALL_BUILD` target.
The documentation is placed in the binary directory under the docs folder.

This requires Doxygen to be installed.

## Support

This is a Windows only library + application. It has been build and tested on Windows 10 using VS 2022.
