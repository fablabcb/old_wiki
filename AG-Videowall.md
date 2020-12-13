Teilnehmer: Christian, Martin S. AG ist gerade inaktiv.

TODO:

  - Ideen sammeln zum Monitorverbund
  - Monitor aufschrauben
  - Konstruktion des Aufbaus
      - Rahmen, Gestell, Kühlung (passiv?, aktiv?), Elektronik

<noinclude>

## Plan

  - Verbund von 24 (B:6 ; H:4) Monitoren
      - annähernd 16:9 Format

## Verbindung der Monitore

  - <http://www.piwall.co.uk/> -\> PC-Desktop lässt sich nicht
    darstellen, nur Einspielung von Videos

## Kommentare

PiWall benötigt Monitore mit HDMI Eingang; Haben wir nicht.
Für Eigenbau wird benötigt:
\* pro Monitor eine "Grafikkarte": 1x FPGA mit configuration IC (oder
überdimensionierter ARM Prozessor mit DMA), 2x RAM für Bildspeicher

  - 1x Hauptcontroller (FPGA/ARM SoC?)
  - Wasserkühlung für die Hintergrundbeleuchtung


Kostenpunkt:

  - PiWall: 24x RPi mit HDMI/DVI Adapter: ca. 960€
  - Eigenbau: 24x Grafikcontroller: ca. 720€
  - Zu beidem: Entsprechendes Netzteil (Nein, eine Verteilerdose mit 24
    Steckern geht nicht), Kühlung, Hauptcontroller, Gestell
  - Summe: Unter 1500€ wird das nichts


Fazit: Beamer werden aus gutem Grund verwendet. Grosse, moderne Bühnen
nutzen LED anzeigen, da weniger Wärme entsteht.
Edit:
Falls du per 8-Bit Controller (Arduino) dran willst:
<http://people.ece.cornell.edu/land/courses/ece4760/FinalProjects/s2012/raf225_dah322/raf225_dah322/index.html>
Hat ganze 256x460 Pixel Auflösung mit 256 Farben. Du musst "nur noch"
den Datenbus dranbauen. Sieht aber richtig schlecht aus wenn man das auf
1024 raufskaliert
\- Marcel

Ich kann auch eher
[Projektion-Mapping](https://www.youtube.com/watch?v=FcIDQSn26fw)
empfehlen - Nanu