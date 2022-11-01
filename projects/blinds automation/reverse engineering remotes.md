# Reverse engineering remote control

A cool way to get into automation is making existing appliances smart. Motorised window shutters are an intriguing 
Each shutter has a remote which is programmed based on the motors number. There are 3 commands
* Up,
* Down, and
* Stop

The commands are idempotent in the sense that when the shutter is in the up position it will ignore the Up command. The same is true for the other commands

The goal is to reverse engineer how the commands are sent and create our own transmitter. Next we would make it connected so it is controllable over the network. Finally it would be cool to provide a method of automatically opening/closing the 
shutters on a schedule.

## The plan
This project has several big steps, most of which require new things. First we need to be able to capture the signal. Once the signal has been captured we need to analyse it and define the protocol.
This can be done using a small device like an arduino which uses a receiver to read the signal. After buffering the capture can be sent to a computer for inspection. The easier method is to use a receiver like the [rtl-sdr dongle](https://www.rtl-sdr.com/).

Once the signals are captured we need to create our transmitter. We can either directly use an arduino which listens for commands specific for the application. A different method is to define the interface as a configurable application which in turn sends actual payloads. 
We can either opt to use 1 arduino/transmitter combination per category of devices (1 for the blinds, another for some other automation device).
The latter option requires specific firmware for each category to be written. For example with my blinds it could receive commands in the form `<DeviceID>$<Command>`.

This makes the arduino firmware simple while a more generic approach would send a suitably encoded raw message with some additional parameters like pulsewidth etc. This means the payload is bigger and the code handling the command is more complex as well. Furthermore it becomes more difficult to identify which devices control which appliances.

By writing the control software as a fully configurable, connection-based application we can have the configurability, extensibility and avoid overly complex firmware. The connection-based part means we will define a connected system by its connection settings. The commands can be defined either explicitly or as a property of the connected system.
Finally we have the devices coupled to a connected system which can only execute the commands defined for the system.


## Links
[Connecting Remote Controlled Blinds to Alexa Smart Home – Stuart Hinson](https://stuarth.github.io/alexa-blinds/)