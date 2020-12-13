.\" Automatically generated by Pandoc 1.16.0.2
.\"
.TH "" "" "" "" ""
.hy
.SH Ziel
.PP
Ein ein­fa­cher Da­ten­log­ger, z.B.
aus Steck­brett­kom­po­nen­ten, der Mess­da­ten auf eine SD\-Kar­te
auf­zeich­net.
Op­ti­miert für ge­rin­gen Strom­ver­brauch und Bat­te­rie­be­trieb.
Er soll leich­tes er­wei­tern, um­bau­en und an­pas­sen er­mög­li­chen.
Der Fokus liegt also auf dem Ex­pe­ri­men­tie­ren und Nach­voll­zie­hen
und we­ni­ger auf super ro­bus­tem Dau­er­ein­satz.
.SH Lernziele
.SS Elektrotechnik:
.IP \[bu] 2
Messfühler in Schaltung integrieren
.IP \[bu] 2
Messsignal in nutzbares Signal umwandeln (eventuell Spannungsbreite
anpassen?)
.IP \[bu] 2
SD\-Karte ansprechen zum Daten speichern und ablesen
.IP \[bu] 2
Realtime Clock
.IP \[bu] 2
Optokoppler als Überspannungsschutz
.SS Datenverarbeitung
.IP \[bu] 2
Umrechnung Messsignal in Messwert
.RS 2
.IP \[bu] 2
z.B.
Spannung in Temperaturwert
.IP \[bu] 2
eventuell Berechnung nichtlinearer Zusammenhänge
.RE
.IP \[bu] 2
Berechnung von Grenzwerten für Alarm, z.B.:
.RS 2
.IP \[bu] 2
Temperatur/Batteriespannung
.IP \[bu] 2
Änderungsrate Messwert
.IP \[bu] 2
Zeit unter Grenzwert
.RE
.SH technische Umsetzung
.PP
Wie Randolf
hier (http://www.station-weisswasser.de/arbeitsgemeinschaften:digitaltechnik:datenlogger:start)
zusammengestellt hat:
.IP \[bu] 2
Logger muss sich mit Ar­dui­no\-Soft­ware pro­gram­mie­ren las­sen
.RS 2
.IP \[bu] 2
Steck­platz für US­B2­se­ri­al Ad­ap­ter
.RE
.IP \[bu] 2
low power Va­ri­an­te des AT­me­ga­328 o.ä.
.RS 2
.IP \[bu] 2
lässt sich mit AT­ti­ny der Strom­ver­brauch sen­ken ohne all­zu­viel P
.RE
.IP \[bu] 2
3,3V 8MHz da ge­rin­ger Strom­ver­brauch wich­ti­ger als
Re­chen­leis­tung, ver­ein­facht auch den SD\-Kar­ten­an­schluss
.IP \[bu] 2
ef­fi­zi­en­ter Step­Down Wand­ler für 3,3V
.IP \[bu] 2
Real­ti­me Clock (RTC) ist not­wen­dig um die Mess­da­ten sinn­voll
ver­wer­ten zu kön­nen
.RS 2
.IP \[bu] 2
FIXME DS1307 geht nur mit 5V.
Der DS 1337 und MCP 7940 geht ab 1,8V und hat eben­falls An­schluss für
Puf­fer­bat­te­rie.
Oder man nimmt gro­ßen Kon­den­sa­tor als En­er­gie­puf­fer an VCC.
Bei Maxim gibt es RTCs mit „in­te­gra­ted trick­le\-char­ging
cir­cui­try“ um den Kon­den­sa­tor auf­zu­la­den.
Liste pas­sen­der ICs:
<http://​www>.​maximintegrated.​com/​en/​app\-notes/​index.​mvp/​id/​3517
Pas­sen­der Kon­den­sa­tor: SPK 220.000µF\-V ::
Spei­cher­kon­den­sa­tor, Ras­ter 5mm, 220.000µF
.IP \[bu] 2
<http://​www>.​exp\-tech.​de/​Shields/​Real\-Time\-Clock\-module\-with\-DS1307.
.IP \[bu] 2
oder DS 1307Z :: Real Time Clock I²C 56B NV SRAM, SO\-8 und
Bat­te­rie­hal­ter für Knopf­zel­le damit die Uhr wei­ter­läuft und
nicht je­des­mal neu ge­stellt wer­den muss.
.RE
.IP \[bu] 2
FIXME Mit wel­chen Senoren soll ge­re­det wer­den?
Wel­che Span­nun­gen für Si­gnal­pe­gel usw.
sind dabei not­wen­dig?
.RS 2
.IP \[bu] 2
In der Sta­ti­on wol­len wir Im­pul­se von einem S\-Bus zäh­len.
Da hängt in der Regel ein Op­to­kopp­ler zwi­schen den bei­den S\-Bus
dräh­ten und dem einen Ein­gang des Mi­cro­con­trol­lers.
Brau­chen wir nur einen Op­to­kopp­ler, der mit 3,3V schon funtioniert.
.IP \[bu] 2
MCP 9808\-EMS :: Tem­pe­ra­tur­sen­sor, MSOP\-8 3,3\-5V taug­lich, \-20
bis +100°C, pro­gram­mier­ba­rer Tem­pe­ra­tu­r­alarm.
.IP \[bu] 2
BTU???
.RE
.IP \[bu] 2
Ana­log\-zu\-Di­gi­tal Ein­gang ver­wen­den um die Bat­te­rie­span­nung
zu über­wa­chen.
Mes­sung ist sel­ten und kann lang­sam sein.
Die Auf­lö­sung ist si­cher wich­ti­ger.
Die Span­nungs­über­wa­chung kann mit auf­ge­zeich­net wer­den und
hilft, das Ver­hal­ten der Bat­te­rie und der Schal­tung im län­ge­ren
Ein­satz bes­ser zu ver­ste­hen.
Es gibt recht ein­fa­che Stra­te­gi­en vom Lehr­stuhl VSBS, um die
Auf­zeich­nungs­ra­te dy­na­misch an­zu­pas­son, so dass ein
Le­bens­zeit­ziel er­reicht wird.
.SH weitere Informationen
.PP
Datenlogger mit Arduino
Yún (http://arduino.cc/en/Tutorial/YunDatalogger) → Hier gibt\[aq]s
vielleicht nützliche Informationen und Codebeispiele
.SH Kursplanung
.IP \[bu] 2
Umsetzbarkeit testen
.IP \[bu] 2
Terminfindung
.IP \[bu] 2
Werbung machen
.IP \[bu] 2
Materialien festlegen
.IP \[bu] 2
Materialien bestellen
.IP \[bu] 2
Arduino\-Chips vorbereiten?
.IP \[bu] 2
Schaltpläne vorbereiten
.IP \[bu] 2
nötige Daten auf Webseite bereitstellen (Schaltpläne, Plugins,
Sourcecode etc.)
.IP \[bu] 2
PowerPoint/Wandtafel/Ausdrucke vorbereiten?
.SH Teilnehmer
.SS Interessiert
.IP \[bu] 2
Nanu
.IP \[bu] 2
Randolf
.SS Verbindliche Zusage zum XX.XX.2014
.SH mögliche Folgekurse
.SS Messgeräte mit serieller Schnittstelle
.IP \[bu] 2
Ansprechen und Aufzeichnen von Geräten mit serieller Schnittstelle
.IP \[bu] 2
Reihenschaltung von seriellen Geräten \- mehrere Geräte an einer Leitung
aufzeichnen
.SS Gehäuse für Datenlogger Drucken