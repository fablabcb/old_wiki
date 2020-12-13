# Ziel

Ein ein­fa­cher Da­ten­log­ger, z.B. aus Steck­brett­kom­po­nen­ten, der
Mess­da­ten auf eine SD-Kar­te auf­zeich­net. Op­ti­miert für ge­rin­gen
Strom­ver­brauch und Bat­te­rie­be­trieb. Er soll leich­tes er­wei­tern,
um­bau­en und an­pas­sen er­mög­li­chen. Der Fokus liegt also auf dem
Ex­pe­ri­men­tie­ren und Nach­voll­zie­hen und we­ni­ger auf super
ro­bus­tem Dau­er­ein­satz.

# Lernziele

### Elektrotechnik:

  - Messfühler in Schaltung integrieren
  - Messsignal in nutzbares Signal umwandeln (eventuell Spannungsbreite
    anpassen?)
  - SD-Karte ansprechen zum Daten speichern und ablesen
  - Realtime Clock
  - Optokoppler als Überspannungsschutz

### Datenverarbeitung

  - Umrechnung Messsignal in Messwert
      - z.B. Spannung in Temperaturwert
      - eventuell Berechnung nichtlinearer Zusammenhänge
  - Berechnung von Grenzwerten für Alarm, z.B.:
      - Temperatur/Batteriespannung
      - Änderungsrate Messwert
      - Zeit unter Grenzwert

# technische Umsetzung

Wie Randolf
[hier](http://www.station-weisswasser.de/arbeitsgemeinschaften:digitaltechnik:datenlogger:start)
zusammengestellt hat:

  - Logger muss sich mit Ar­dui­no-Soft­ware pro­gram­mie­ren las­sen
      - Steck­platz für US­B2­se­ri­al Ad­ap­ter
  - low power Va­ri­an­te des AT­me­ga­328 o.ä.
      - lässt sich mit AT­ti­ny der Strom­ver­brauch sen­ken ohne
        all­zu­viel P
  - 3,3V 8MHz da ge­rin­ger Strom­ver­brauch wich­ti­ger als
    Re­chen­leis­tung, ver­ein­facht auch den SD-Kar­ten­an­schluss
  - ef­fi­zi­en­ter Step­Down Wand­ler für 3,3V
  - Real­ti­me Clock (RTC) ist not­wen­dig um die Mess­da­ten sinn­voll
    ver­wer­ten zu kön­nen
      - FIXME DS1307 geht nur mit 5V. Der DS 1337 und MCP 7940 geht ab
        1,8V und hat eben­falls An­schluss für Puf­fer­bat­te­rie. Oder
        man nimmt gro­ßen Kon­den­sa­tor als En­er­gie­puf­fer an VCC.
        Bei Maxim gibt es RTCs mit „in­te­gra­ted trick­le-char­ging
        cir­cui­try“ um den Kon­den­sa­tor auf­zu­la­den. Liste
        pas­sen­der ICs:
        <http://​www>.​maximintegrated.​com/​en/​app-notes/​index.​mvp/​id/​3517
        Pas­sen­der Kon­den­sa­tor: SPK 220.000µF-V ::
        Spei­cher­kon­den­sa­tor, Ras­ter 5mm, 220.000µF
      - <http://​www>.​exp-tech.​de/​Shields/​Real-Time-Clock-module-with-DS1307.
      - oder DS 1307Z :: Real Time Clock I²C 56B NV SRAM, SO-8 und
        Bat­te­rie­hal­ter für Knopf­zel­le damit die Uhr wei­ter­läuft
        und nicht je­des­mal neu ge­stellt wer­den muss.
  - FIXME Mit wel­chen Senoren soll ge­re­det wer­den? Wel­che
    Span­nun­gen für Si­gnal­pe­gel usw. sind dabei not­wen­dig?
      - In der Sta­ti­on wol­len wir Im­pul­se von einem S-Bus zäh­len.
        Da hängt in der Regel ein Op­to­kopp­ler zwi­schen den bei­den
        S-Bus dräh­ten und dem einen Ein­gang des Mi­cro­con­trol­lers.
        Brau­chen wir nur einen Op­to­kopp­ler, der mit 3,3V schon
        funtioniert.
      - MCP 9808-EMS :: Tem­pe­ra­tur­sen­sor, MSOP-8 3,3-5V taug­lich,
        -20 bis +100°C, pro­gram­mier­ba­rer Tem­pe­ra­tu­r­alarm.
      - BTU???
  - Ana­log-zu-Di­gi­tal Ein­gang ver­wen­den um die
    Bat­te­rie­span­nung zu über­wa­chen. Mes­sung ist sel­ten und
    kann lang­sam sein. Die Auf­lö­sung ist si­cher wich­ti­ger. Die
    Span­nungs­über­wa­chung kann mit auf­ge­zeich­net wer­den und
    hilft, das Ver­hal­ten der Bat­te­rie und der Schal­tung im
    län­ge­ren Ein­satz bes­ser zu ver­ste­hen. Es gibt recht
    ein­fa­che Stra­te­gi­en vom Lehr­stuhl VSBS, um die
    Auf­zeich­nungs­ra­te dy­na­misch an­zu­pas­son, so dass ein
    Le­bens­zeit­ziel er­reicht wird.

# weitere Informationen

[Datenlogger mit Arduino
Yún](http://arduino.cc/en/Tutorial/YunDatalogger) → Hier gibt's
vielleicht nützliche Informationen und Codebeispiele

# Kursplanung

  - Umsetzbarkeit testen
  - Terminfindung
  - Werbung machen
  - Materialien festlegen
  - Materialien bestellen
  - Arduino-Chips vorbereiten?
  - Schaltpläne vorbereiten
  - nötige Daten auf Webseite bereitstellen (Schaltpläne, Plugins,
    Sourcecode etc.)
  - PowerPoint/Wandtafel/Ausdrucke vorbereiten?

# Teilnehmer

### Interessiert

  - Nanu
  - Randolf

### Verbindliche Zusage zum XX.XX.2014

# mögliche Folgekurse

### Messgeräte mit serieller Schnittstelle

  - Ansprechen und Aufzeichnen von Geräten mit serieller Schnittstelle
  - Reihenschaltung von seriellen Geräten - mehrere Geräte an einer
    Leitung aufzeichnen

### Gehäuse für Datenlogger Drucken