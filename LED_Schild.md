<onlyinclude> Ein blinkendes Schild als Logo/Werbung für das Fablab.
Inklusive Musikspielereien wie auch im [Audio
Board](http://fablab-cottbus.de/index.php/Audio_Board). </onlyinclude>

# Idee

Eine portable Abwandlung des Audio Projektes, die wir mit auf
Ausstellungen nehmen können.

# Konzept

Mehrere LED werden in verschiedenen Mustern auf einem Holzbrett
angebracht. Es soll autonom laufen und verschiedene Blinkmuster haben.
Es könnten 4 LED Stränge mit je 20 LED benutzt werden. Aussehen z.B.

Datei:Wandding_Zeichnung.svg|Fablab Logo
Datei:Wandding_Zeichnung2.svg|Muster

Die einzelnen LED Streifen können dann mit jedem Beat in Tiefen, Mitten
bzw. Höhen blinken und die Farbe bzw. Helligkeit kann Anhand der
Intensität angepasst werden. Die Blinkmuster der LED passen sich somit
dynamisch an das Lied an. Alternativ können auch statische Animationen
und Farbwechsel vorgegeben werden.

Folgende Anforderungen werden gestellt:

  - Portable
  - LED auch im hellen sichtbar
  - Nachbaubar
  - Gut aussehen
  - Stabil verarbeitet


Offene Fragen:

  - Bedienung über Display + Taster oder Fernbedienung?
  - Controller Arduino (weit verbreitet, einfach zu nutzen) oder
    Nucleo-F446 (viel mehr Rechenleistung, DSP, DMA, S/PDIF Eingang
    usw.)?
  - Nur Mikrofon oder auch Line-In bzw. S/PDIF?


Bestehende Analogschaltung muss etwas überarbeitet werden. Anpassung an
neue Anforderungen (nur Mono statt Stereo, Mikrofonverstärker). Wird
direkt als Schild für das Entwicklungsboard entworfen. Sofern möglich
1-Seitige Platine zum einfacheren Nachbau.