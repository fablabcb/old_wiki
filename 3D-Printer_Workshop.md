<onlyinclude> In our workshop we have a [3D
Printer](3D-Drucker "wikilink") that builds up three dimensional models
by thin plastic layers. Everyone can use our printer for his own
projects, but you need to take a course first to get to know how to use
the printer. Topics of the course will be the preperation of 3D Models,
the operation of the printer, the possibilities and limits of the
printable and tricks how to enhance the print quality.</onlyinclude>

# next dates

  - Saturday 13.12.2014 17-20h in Englisch

Contact: [Nanu](Benutzer:Nanu "wikilink") (<nanu@fablab-cottbus.de>)

# costs and requirements

  - 5€ per person that will benefit our charitable organization
  - You don't need any pre knowledge
  - bringing your laptop would be optimal

# Topics

## basics

  - Funktionsprinzip des Druckers
  - Auflagefläche vorbeireiten (Tape)
  - Wie löse ich den 3D-Druck von der Auflagefläche

<!-- end list -->

  - Cura, die Software zum Vorbereiten der 3D-Drucke
  - Drucken von SD-Karte
  - Drucken mit direkter Verbindung zum Computer
  - OcotoPi (IP [141.43.4.84.20](http://141.43.84.20) oder
    [octopi.local](http://octopi.local))

## Modelle vorbereiten

  - 3D-Software - Umwandlung in .stl oder .obj
  - [Thingiverse](http://thingiverse.com) - 3D-Objekte runterladen und
    drucken

## Drucker kalibrieren

  - Druckbetthöhe einstellen
  - Druckkopf abstand kalibrieren (für Dual-Extrusion)

## Die wichtigsten Einstellungen in Cura

In Cura sind folgende Einstellungen für die Qualität des Drucks
maßgebend:

  - Layer heigth - Schichtdicke - Verantwortlich für die Genauigkeit des
    Drucks. Werte von 0,02 bis 0,3 mm sind möglich. 0,06 mm ist die
    "high quality" Einstellung in Cura, 0.1 mm die "normal quality".
  - Shell thickness - Dicke der Wände - abhängig davon werden eine oder
    mehrere Bahnen gefahren
  - Bottom/Top thickness - Dicke von Boden und Decke - bestimmt die
    Anzahl der Layer, die zum Abschließen nach oben und unten gedruckt
    werden
  - Fill density - Fülldichte - abhängig davon wird die Dichte der
    Füllstruktur (rechteckige Waben) berechnet
  - print speed - Druckgeschwindigeit - sollte zwischen 30 und 300 mm/s
    liegen.

## Weitere Einstellungen direkt im Code vornehmen

  - was ist gcode?
  - Druckkopf wechseln
  - Temperatur anpassen
  - Temperatur Stück für Stück anpassen
  - gcode Befehle live während des Drucks im OctoPi-Terminal ausführen

## Grenzen des Druckbaren

  - nichts kann in die Luft gedruckt werden
  - Auflösung des Druckers

## Probleme beim Drucken

  - Druck haftet nicht auf der Grundplatte
      - Lösung: (Anfangs-)Temperatur erhöhen

<!-- end list -->

  - Druck zieht Fäden
      - Lösung:Retraction (Rückzug des Filaments beim Absetzen des
        Druckkopfs) erhöhen oder Drucktemperatur etwas verringern

<!-- end list -->

  - (bei Kleinteilen:) Druck erhärtet nicht schnell genug, Werkstück
    bleibt weich und kippt irgendwann um
      - Lösung: Temperatur verringern, eventuell Temperatur erst nach
        der ersten Schicht verringern (erfordert manuelles Eingreifen in
        den `.gcode`)

<!-- end list -->

  - Füllungen sind nicht komplett gefüllt, sondern sehen aus wie ein
    Gitter
      - Lösung: Eingestellten Filamentdurchmesser verringern oder
        "Fluss" erhöhen (erzeugt mehr Material-Vorschub)

## Grenzen des Druckbaren erweitern

  - Überhang
  - bridging
  - Supportstrukturen

## Zweifarbdruck

  - Wipe & prime tower
  - Ooze shield