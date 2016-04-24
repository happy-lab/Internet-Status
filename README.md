# Internet Monitor
The Internet Monitor started as a few changes to the
[internetup](http://whiskeytangohotel.com/internetup) program.
It got completely rewritten but the original command line output is used.

## License
Internet Monitor is released under a MIT [license](./LICENSE).

## Requirements
* A flexible number of sites to poll.
* The internet status to be available in more than one location.
* Run on a headless system.
* No log file to manage.

## Components

### internet-monitor
Program to poll site to determine the condition of the internet connection.
Publishes current condition to a ***MQTT*** server.  Also broadcast detailed
status information using a sigle UDP packet to the local host.

### status-pi
Program that subscribes to the topc on the ***MQTT*** server.
Presents the internet condition on a single RGB LED.

### status
Program to listen for the UDP packet and print it.

## Implementation
All program are written in Python 3 and require that the
[Python MQTT package](https://pypi.python.org/pypi/paho-mqtt/1.1)
be installed.  The programs were developed and tested on **Arch Linux**
systems running on ARM processors, a Fedora 22 system and OS X 10.11.

## Installation
* Install and configur the MQTT server.
* Copy the programs to the desired directory, e.g., `/usr/local/bin`
on the monitor system and any Raspberry Pis for condition presentation.
* Modify the configuation file and place in `/etc/internet-monitor.d/monitor.conf`
* Modify as necessary the *service* files and place in the local systemd
services directory, `/etc/systemd/system`.
* Enable the service(s) appropriate for the system.

## Usage
With the monitor service started the internet condition is published
to the ***MQTT*** server.  To check the detailed status of the service,
SSH into the system and run the status command.  The monitoring status
is presented at regular intervals.  The monitor program could be changed
to broadcast on the subnet and the status program run on any system if
desired.

Running the status_pi will present the status on a LED(s) using
the GPIO pins.  The presentation can be easily changed to to suppot
multiple LEDs, toy traffic lights, flags on servo motors, ...

## Things To Do
* Record status at intervals to a database.
* Add collecting internet speed at regular intervals.
* Switch to direct ARP calls to reduce the elapsed time consumed by
the ***ping*** command.
* Develop a generic ***Presenter*** class to abstract presenting
the internet condition.
* Use the prior to support using a *blink(1)*.
* Complete ***pacman*** build.
* Provide the abaility to blink the LED when running on a Raspberry Pi.
* Better documentation.
