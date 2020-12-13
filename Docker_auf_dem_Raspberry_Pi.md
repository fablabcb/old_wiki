.\" Automatically generated by Pandoc 1.16.0.2
.\"
.TH "" "" "" "" ""
.hy
.PP
Da der Raspberry Pi einem ARM\-Prozessor besitzt, müssen Docker
Container speziell für diese Architektur ausgelegt werden.
Ausserdem hat es auch eine Weile gebraucht, bis jemand Docker an sich
auf dem Raspberry zum laufen gebracht hat.
.PP
Mittlerweile gibt es vorgefertige SD\-Karten Images für den Raspberry,
auf denen Docker installiert ist:
.IP \[bu] 2
hypriotOS (http://blog.hypriot.com/downloads/)
.IP \[bu] 2
resinOS (https://resinos.io/)
.PP
Einige spezielle images lassen sich hier finden:
.IP \[bu] 2
hypriot (https://hub.docker.com/u/hypriot/)
.IP \[bu] 2
resin (https://hub.docker.com/u/resin/)
.PP
Oder suche einfach auf Docker Hub (https://hub.docker.com) nach dem
gewünschten Container zusammen mit dem Keyword \[lq]raspberry\[rq].
.PP
Hier einige Anleitungen:
.IP \[bu] 2
Heise.de: Ein Container voller
Himbeeren (https://www.heise.de/developer/artikel/Ein-Container-voller-Himbeeren-Docker-auf-dem-Raspberry-Pi-2572533.html)
.IP \[bu] 2
hypriot.com: getting started with docker on your arm
device (http://blog.hypriot.com/getting-started-with-docker-on-your-arm-device/)
.IP \[bu] 2
Raspberry im Docker Swarm mit
hypriotOS (http://blog.hypriot.com/post/how-to-setup-rpi-docker-swarm/)
.SS Make use of GPIO
.PP
In order to make use of additional hardware and add\-on boards you will
need to access the GPIO pins.
These require an additional flag at runtime of \-\-privileged to allow
the container to write to the special area of memory managing GPIO.
.PP
This is a sample Dockerfile for using the defacto RPi.GPIO library.
.PP
\f[C]\ FROM\ resin/rpi\-raspbian:latest\ \ \f[]
.PD 0
.P
.PD
\f[C]\ ENTRYPOINT\ []\f[]
.PD 0
.P
.PD
\f[C]\ \f[]
.PD 0
.P
.PD
\f[C]\ RUN\ apt\-get\ \-q\ update\ &&\ \\\ \ \f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ apt\-get\ \-qy\ install\ \\\f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ \ \ \ \ python\ python\-pip\ \\\f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ \ \ \ \ python\-dev\ python\-pip\ gcc\ make\ \ \f[]
.PD 0
.P
.PD
\f[C]\ \f[]
.PD 0
.P
.PD
\f[C]\ RUN\ pip\ install\ rpi.gpio\ \ \f[]
.PP
Build this image as a basis for adding your GPIO scripts at a later
date.
.PP
\f[C]\ $\ docker\ build\ \-t\ gpio\-base\ .\f[]
.PP
The following Python code can be used to will blink an LED connected to
GPIO pin 18.
.PP
\f[C]\ import\ RPi.GPIO\ as\ GPIO\ \ \f[]
.PD 0
.P
.PD
\f[C]\ import\ time\ \ \f[]
.PD 0
.P
.PD
\f[C]\ GPIO.setmode(GPIO.BCM)\ \ \f[]
.PD 0
.P
.PD
\f[C]\ led_pin\ =\ 17\ \ \f[]
.PD 0
.P
.PD
\f[C]\ GPIO.setup(led_pin,\ GPIO.OUT)\f[]
.PD 0
.P
.PD
\f[C]\ \f[]
.PD 0
.P
.PD
\f[C]\ while(True):\ \ \f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ GPIO.output(led_pin,\ GPIO.HIGH)\f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ time.sleep(1)\f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ GPIO.output(led_pin,\ GPIO.LOW)\f[]
.PD 0
.P
.PD
\f[C]\ \ \ \ \ time.sleep(1)\f[]
.PP
Just use ADD to transfer the script into a new image depriving from
gpio\-base:
.PP
\f[C]\ FROM\ gpio\-base:latest\ \ \f[]
.PD 0
.P
.PD
\f[C]\ ADD\ ./app.py\ ./app.py\f[]
.PD 0
.P
.PD
\f[C]\ \f[]
.PD 0
.P
.PD
\f[C]\ CMD\ [\f[]\[lq]\f[C]python\f[]\[rq]\f[C],\ \f[]\[lq]\f[C]app.py\f[]\[rq]\f[C]]\ \ \f[]
.PP
You will need to run this container in \-\-privileged mode in order to
be able to access the GPIO pins.
.PP
\f[C]\ $\ docker\ build\ \-t\ blink\ .\f[]
.PD 0
.P
.PD
\f[C]\ $\ docker\ run\ \-ti\ \-\-privileged\ blink\f[]
.SS Nützliche Docker\-Container für den Raspberry Pi
.PP
<https://hub.docker.com/r/nieleyde/rpi-nodered-gpio/> \[en]\ Node\-Red
mit ansprechbaren GPIO\-Pins
.SS Nütliche Services im Zusammenhang mit Docker Containern auf dem
Raspberry Pi
.IP \[bu] 2
Mit resin.io (https://resin.io/how-it-works/) kann eine ganze Flotte an
Raspberrys gemanaged werden und updates \[lq]over the air\[rq]
eingespielt werden.