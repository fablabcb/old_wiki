Die Idee ist einen Arcade-Automaten zu bauen mit einem Raspberry Pi.
[Hier](http://blog.oscarliang.net/turning-raspberry-pi-gaming-console-project-c/)
gibt es einige Beispiele in unterschiedlichen form factors.

# Materialien

## Emulation

Die Emulatoren sollen auf dem Raspberry (ca. 28€) laufen. Es gibt
fertige Images:

  - [Lakka](http://www.lakka.tv)
  - [RetroPie](http://blog.petrockblock.com/retropie/retropie-downloads/download-info/retropie-sd-card-image-for-rpi-version-1/)

## Controller

### Knöpfe/Joystick

  - großer Retro-Joystick und Knöpfe:
    [21,99€](http://www.ebay.de/itm/Arcade-Set-3-mit-1-Joystick-2-4-8-Wege-6-Taster-Mame-Automat-Jamma-Kit-/351252892153?pt=LH_DefaultDomain_77&hash=item51c84dc9f9)
    für einen Controller + 4€ Versandt

oder

  - alten Gamecontroller ausschlachten

### Input Interface für die Knöpfe

  - direkt über die GPIO pins des Raspberry (eventuell nicht genug Pins
    für zwei Spieler vorhanden):
      - <https://github.com/mmoller2k/pikeyd>
      - <https://github.com/notro/fbtft-spindle/wiki/GPIO-keyboard>
  - 1x für eingebaute Controller oder 2x für zwei kabelgebundene
    Controller:
      - Board aus Gamecontroller
      - Controllboard aus altem Keyboard verwenden (falls das klappt)
      - Teensy LC als USB-Keyboard, Maus oder Joystick controller
        [12,50€](http://www.exp-tech.de/mainboards/teensy/teensy-lc)
      - Arduino Leonardo als USB-Keyboard oder Maus controller
        [21,42€](http://www.exp-tech.de/mainboards/arduino/arduino-leonardo-with-headers)
        oder für ca 6€ direkt aus Hongkong bestellen
      - Arduino Microals USB-Keyboard oder Maus controller
        [19,04](http://www.exp-tech.de/mainboards/arduino/arduino-micro-without-headers)
        oder billiger direkt aus Hongkong

oder kabellos über Bluetooth:

  - 2x Bluetooth Keyboard controller
    [18,99€](http://www.exp-tech.de/bluefruit-ez-key-12-input-bluetooth-hid-keyboard-controller-v1-2)
    für zwei portable Controller (eventuell aus Einschub herausnehmbar)

## Bildschirm

  - 15 Zoll gebrauchter Monitor (braucht noch einen HDMI auf DVI oder
    VGA Adapter ca
    [6€](http://www.ebay.de/itm/HDMI-zu-auf-VGA-Konverter-mit-Audio-Adapter-Kabel-bis-1080p-Full-HD-HDTV-AC107-/311270078457?pt=LH_DefaultDomain_77&hash=item48792477f9))
  - kleiner TFT Bildchirm über AV kabel (kein Adapter benötigt) (z.B.
    3,5 Zoll für
    [16€](http://www.ebay.de/itm/400808411917?_trksid=p2060353.m1438.l2649&ssPageName=STRK%3AMEBIDX%3AIT))

## Gehäuse

Zwei Varianten wären möglich:

  - für 15 Zoll Monitor: Großes Gehäuse für 2 Spieler zum auf den Tisch
    stellen oder mit eigenen Füßen zum ans Sofa stellen oder irgendwo in
    die Ecke.
  - für 3-7 Zoll Monitor: kleines Gehäuse für auf den Tisch. Hätte
    wahrscheinlich nur Platz für einen eingebauten Controller. Ansonsten
    kabelgebundene Controller oder Bluetooth-Controller.
    Batteriebetriebene Variante (Bildschirm braucht ca. 6-12V) denkbar.

Gehäuse sollte aus Holz mit wenig Aufwand baubar sein.

# Vorgehen

Erledigt:

  - RetroPie läuft, einige Roms sind schon installiert
  - große Bildschirme vorhanden, Adapter fürs erste auch
  - kleiner Bildschirm zum testen ist bestellt
  - Ein USB-Gamecontroller ist vorhanden, funktioniert bisher aber nur
    im Menü von RetroPie

Todo:

  - für eine Controller-Variante entscheiden + Materialien bestellen
  - für eine Bildschirm-Variante entscheiden + Holz kaufen

# Evaluierung

## Lakka

  - Pro
      - Optisch der CrossBar der PS angelehnte uebersichtliche
        Oberflaeche
      - Grafik und Sound ueber HDMI funktionieren ohne Konfiguration
      - Roms brauchen nur in einen zentralen Ordner abgelegt werden und
        sind danach ordentlich in die GUI eingebunden
      - junges Projekt, aber Entwicklergemeinde scheint noch sehr aktiv
        zu sein
      - SNES Roms laufen auf einem RasPi B+ fluessig (DOOM mal
        ausgenommen)
      - XBOX360 Controller wird erkannt und korrekt gemappt
  - Cons
      - Standardinstallation ist ziemlich offen zum Netz (public samba
        share, ssh zugang ueber root:root)
  - Offen
      - Testen ob man die GPIOs unter der Distri gut ansteuern kann

# Diskussion

  -
    Ich hab das Projekt hier mal angelegt und freue mich über jeden der
    mitmachen möchte\! - [Nanu](Benutzer:Nanu "wikilink") 19:54, 3. Apr.
    2015 (CEST)