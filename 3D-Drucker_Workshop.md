<onlyinclude>In unserer Mitmachwerkstatt steht allen Interessierten ein
[3D-Drucker](3D-Drucker "wikilink") zur Verfügung, der Schichtweise
Plastik zu dreidimensionalen Modellen bis 20x20x20cm aufschichten kann.
Wer bei uns etwas ausdrucken möchte, kann sich in unserem 3D-Druck
Workshop mit dem Gerät und dessen Arbeitsweise vertraut machen.
Kursinhalte sind die Vorbereitung von 3D-Modellen, die Bedienung des
Druckers, das Kennenlernen der Möglichkeiten und Grenzen des Druckbaren
und Tricks und Kniffe, wie man das Beste aus dem 3D-Drucker herausholt.
Zur Anmeldung bitte eine Mail an:
<nanu@fablab-cottbus.de>.</onlyinclude>

For the Englisch course description click
[here](3D-Printer_Workshop "wikilink").

# nächste Termine

  - Bisher keine geplant aber schreibt uns einfach, dann setzen wir
    wieder einen Termin an:

Ansprechpartner und Anmeldung: [Nanu](Benutzer:Nanu "wikilink")
(<nanu@fablab-cottbus.de>)

# Kosten und Vorraussetzungen

  - 5€ Pro Person, die an unseren allgemeinnützigen Verein gehen
  - Es werden keine Vorkenntnisse erwartet
  - Optimal wäre es, wenn ihr einen Laptop mitbringt

# Inhalte

## Grundlagen

  - Funktionsprinzip des Druckers
  - Wie löse ich den 3D-Druck von der Auflagefläche

<!-- end list -->

  - Cura, die Software zum Vorbereiten der 3D-Drucke
  - Drucken von SD-Karte
  - Drucken mit direkter Verbindung zum Computer
  - OcotoPi (IP [141.43.4.84.68](http://141.43.84.215:5000))

## Modelle vorbereiten

  - 3D-Software - Umwandlung in .stl oder .obj
  - [Thingiverse](http://thingiverse.com) - 3D-Objekte runterladen und
    drucken

## Drucker kalibrieren

  - Druckbetthöhe einstellen
      - in Cura
      - mit OctoPrint
  - Druckkopf abstand kalibrieren (für Dual-Extrusion) in Cura

## Voreinstellungen in Cura

Einstellungen die beim ersten Start von
[Cura](http://software.ultimaker.com/) gemacht werden müssen:

  - Gerät: Ultimaker Original (ohne Plus)
  - Upgrade des Extruder-Antriebs
  - Beheizter Drucktisch (offiziell)
  - Eine Druckdüse

Später muss dann unter `Datei>Geräte-Einstellungen...` dann noch der
Abstand zwischen den Druckköpfen eingestellt werden. Dafür im Abschnitt
`Extruder 2` den `Abstand X` auf 1.0 und `Abstand Y` auf 22.0
einstellen.

## Druckparameter einstellen

In [Cura](http://software.ultimaker.com/) sind folgende Einstellungen
für die Qualität des Drucks maßgebend:

  - Schichtdicke - Verantwortlich für die Genauigkeit des Drucks. Werte
    von 0,02 bis 0,3 mm sind möglich. 0,06 mm ist die "high quality"
    Einstellung in Cura, 0.1 mm die "normal quality".
  - Stärke der Außenhülle - abhängig davon werden eine oder mehrere
    Bahnen gefahren
  - Stärke Unten/Oben - Dicke von Boden und Decke - bestimmt die Anzahl
    der Layer, die zum Abschließen nach oben und unten gedruckt werden
  - Fülldichte - abhängig davon wird die Dichte der Füllstruktur
    (rechteckige Waben) berechnet
  - Druckgeschwindigeit - Der Hersteller gibt 30 und 150 mm/s an. Jedoch
    haben wir über 50 mm/s oft Probleme, dass das Filament nicht mehr
    schnell genug aufgeheizt wird und deshalb nicht aus der Druckdüse
    kommt. Daher drucken wir das meiste unter 50 mm/s. Letztendlich kann
    man noch live am Drucker die Geschwindigkeit wieder hoch regeln,
    wenn man merkt, dass man doch schneller drucken kann.
  - Drucktemperatur - für PLA, mit dem wir meistens drucken liegt die
    bei 210°C

Wir haben euch [die besten
Einstellungen](https://www.dropbox.com/s/7jclirfxj3i2065/fablab-Cottbus-3D-Drucker-Einstellungen.ini?dl=1)
in eine Datei gelegt, die ihr in Cura reinladen könnt. Damit sollten die
meisten Drucke problemlos funktionieren.

## Weitere Einstellungen direkt im Code vornehmen

  - was ist
    [gcode](http://reprap.org/wiki/G-code#M104:_Set_Extruder_Temperature)?
  - Druckkopf wechseln
  - Temperatur anpassen
  - Temperatur Stück für Stück anpassen
  - gcode Befehle live während des Drucks im OctoPi-Terminal ausführen

## Grenzen des Druckbaren

  - nichts kann in die Luft gedruckt werden
  - Auflösung des Druckers

## Probleme beim Drucken

Bei Problemen mit dem Druck gibt es
[hier](http://support.3dverkstan.se/article/23-a-visual-ultimaker-troubleshooting-guide)
einen visuellen Troubleshooting Guide.

## Grenzen des Druckbaren erweitern

  - Überhang
  - bridging
  - Supportstrukturen

## Zweifarbdruck

  - Wipe & prime tower
  - Ooze shield

# Online-Anleitungen

  - [Anleitung
    auf 3dhubs.com](https://www.3dhubs.com/what-is-3d-printing)