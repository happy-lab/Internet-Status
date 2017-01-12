# Internet Monitor
The Internet Status monitor started as a few changes to the
[internetup](http://whiskeytangohotel.com/internetup) program.
It got completely rewritten but uses its original command line output.

## License
Internet Monitor is released under a MIT [license](./LICENSE).

## Requirements
* Allow flexible number of sites to poll.
* Provide the internet status to be available in more than one location.
* Run on a headless system.
* No log file to manage.

## Components

### internet-statusd
Program to poll site to determine the condition of the internet connection.
Publishes current condition to a ***MQTT*** server.  Also broadcasts detailed
status information using a single UDP packet to the local host.

### internet-status_pi
Program that subscribes to the topiic on the ***MQTT*** server.
Presents the internet condition on a single RGB LED.  This program is provided as the basis for other presentation mechanisms.

### internet-status
Program to listen for the UDP packet and print it.

## Implementation
All program are written in Python 3 and require that the
[Python MQTT package](https://pypi.python.org/pypi/paho-mqtt/1.1)
be installed.  The programs were developed and tested on **Arch Linux**
systems running on ARM processors, a Fedora 22 system and OS X 10.11.

## Installation
* Install and configure the MQTT server.
* Install the programs
	* On an **Arch Linux** system use *makepkg* and *pacman -S*
	* Copy the programs to the desired directory, e.g., `/usr/local/bin`
on the monitoring system and any Raspberry Pis for condition presentation.
* Modify the configuation file and place in `/etc/internet-status/monitor.conf`
* Enable the service(s) appropriate for the system.

## Usage
With the monitor service started the internet condition is published
to the ***MQTT*** server.  To check the detailed status of the service,
SSH into the system and run the status command.  The monitoring status
is presented at regular intervals.  The monitor program could be changed
to broadcast on the subnet and the status program run on any system if
desired.

Running the internet-status_pi will present the status on a LED(s) using
the GPIO pins.  The presentation can be easily changed to to support
multiple LEDs, toy traffic lights, flags on servo motors, ...

## Things To Do
* Record status at intervals to a database.
* Add collecting internet speed at regular intervals.
* Switch to direct ARP calls to reduce the elapsed time consumed by
the ***ping*** command.
* Develop a generic ***Presenter*** class to abstract presenting
the internet condition.
* Use the prior to support using a *blink(1)*.
* Provide the ability to blink the LED when running on a Raspberry Pi.
* Better documentation.
