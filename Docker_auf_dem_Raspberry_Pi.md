Da der Raspberry Pi einem ARM-Prozessor besitzt, müssen Docker Container
speziell für diese Architektur ausgelegt werden. Ausserdem hat es auch
eine Weile gebraucht, bis jemand Docker an sich auf dem Raspberry zum
laufen gebracht hat.

Mittlerweile gibt es vorgefertige SD-Karten Images für den Raspberry,
auf denen Docker installiert ist:

  - [hypriotOS](http://blog.hypriot.com/downloads/)
  - [resinOS](https://resinos.io/)

Einige spezielle images lassen sich hier finden:

  - [hypriot](https://hub.docker.com/u/hypriot/)
  - [resin](https://hub.docker.com/u/resin/)

Oder suche einfach auf [Docker Hub](https://hub.docker.com) nach dem
gewünschten Container zusammen mit dem Keyword "raspberry".

Hier einige Anleitungen:

  - [Heise.de: Ein Container voller
    Himbeeren](https://www.heise.de/developer/artikel/Ein-Container-voller-Himbeeren-Docker-auf-dem-Raspberry-Pi-2572533.html)
  - [hypriot.com: getting started with docker on your arm
    device](http://blog.hypriot.com/getting-started-with-docker-on-your-arm-device/)
  - [Raspberry im Docker Swarm mit
    hypriotOS](http://blog.hypriot.com/post/how-to-setup-rpi-docker-swarm/)

## Make use of GPIO

In order to make use of additional hardware and add-on boards you will
need to access the GPIO pins. These require an additional flag at
runtime of --privileged to allow the container to write to the special
area of memory managing GPIO.

This is a sample Dockerfile for using the defacto RPi.GPIO library.

` FROM resin/rpi-raspbian:latest  `
` ENTRYPOINT []`
` `
` RUN apt-get -q update && \  `
`     apt-get -qy install \`
`         python python-pip \`
`         python-dev python-pip gcc make  `
` `
` RUN pip install rpi.gpio  `

Build this image as a basis for adding your GPIO scripts at a later
date.

` $ docker build -t gpio-base .`

The following Python code can be used to will blink an LED connected to
GPIO pin 18.

` import RPi.GPIO as GPIO  `
` import time  `
` GPIO.setmode(GPIO.BCM)  `
` led_pin = 17  `
` GPIO.setup(led_pin, GPIO.OUT)`
` `
` while(True):  `
`     GPIO.output(led_pin, GPIO.HIGH)`
`     time.sleep(1)`
`     GPIO.output(led_pin, GPIO.LOW)`
`     time.sleep(1)`

Just use ADD to transfer the script into a new image depriving from
gpio-base:

` FROM gpio-base:latest  `
` ADD ./app.py ./app.py`
` `
` CMD ["python", "app.py"]  `

You will need to run this container in --privileged mode in order to be
able to access the GPIO pins.

` $ docker build -t blink .`
` $ docker run -ti --privileged blink`

## Nützliche Docker-Container für den Raspberry Pi

<https://hub.docker.com/r/nieleyde/rpi-nodered-gpio/> – Node-Red mit
ansprechbaren GPIO-Pins

## Nütliche Services im Zusammenhang mit Docker Containern auf dem Raspberry Pi

  - Mit [resin.io](https://resin.io/how-it-works/) kann eine ganze
    Flotte an Raspberrys gemanaged werden und updates "over the air"
    eingespielt werden.