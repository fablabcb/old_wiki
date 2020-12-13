<onlyinclude>Alte Geräte wieder nutzbar machen, Zugriff auf Hardware-
und Software-Teile zu bekommen, die der Hersteller für den Endbenutzer
nicht vorgesehen hat, Funktionen hinzufügen, eigene Einstellungen
vornehmen, Geräte in einer Weise nutzen, die vom Hersteller nicht
vorgesehen hat - darum geht es beim Reverse Engineering.

Die Geräte werden uns in die Hand gelegt, die Baupläne jedoch nicht. Und
der Hersteller schreibt uns genau vor, wie wir das Gerät zu nutzen
haben. Durch Auseinandernehmen, Durchmessen und Ausprobieren lässt sich
jedoch herausfinden, wie ein Gerät aufgebaut ist und wie es
funktioniert. Mit diesem Wissen kann dann der Funktionsumfang des
Gerätes an die eigenen Wünsche angepasst und oft erheblich erteitert
werden.</onlyinclude>

# Grundlagen

## Serial Port nutzbar machen

### Was ist eine serielle Schnittstelle?

Die [serielle
Schnittstelle](https://de.wikipedia.org/wiki/Serielle_Schnittstelle) war
in Zeiten, bevor es USB gab die gängige Verbindung von Geräten zum
Computer. Den Stecker kennt man vielleicht noch von alten Druckern. Aber
auch viele Labor- oder Feldmessgeräte haben eine serielle Schnittstelle,
denn letztendlich benötigt man nur zwei Kabel. Auch unser
[3D-Drucker](3D-Druck "wikilink") kommuniziert letztendlich über die
serielle Schnittstelle, auch wenn er über einen USB-Konverter
angeschlossen wird.

### Wie kann ich die serielle Schnittstelle nutzen?

Um mit einem Gerät sprechen zu können, müssen verschiedene Parameter
eingestellt werden:

  - die Bitrate - was die Geschwindigeit des Datenaustauschs beeinflusst
    (\*)
  - data bits
  - parity
  - stop bits
  - flow control

(Anm.: häufig wird der Ausdruck "Baudrate" statt "Bitrate verwendet. Das
ist aber nicht korrekt. Baudrate bedeutet was ganz anderes. Ein
historisches Beispiel: Ein 9600-bit-Modem. Es arbeitet beispielsweise
mit 300 Baud, wobei jeder Datenblock kodiert 16 bit enthält (=Symbol).
Ergebnis: Baudrate 300, Bitrate 9600. Analog dazu die heutigen
Anwendungen, Mobilfunk, Digitalfunk, digitale Datenübertragung. Kurz
gesagt: Baudrate bezeichnet den Datentakt/Symboltakt und nicht die
Datenrate.)

Oft können diese Parameter auch am Gerät umgestellt werden. Wichtig ist,
dass Computer und Gerät beide auf die gleichen Parameter eingestellt
sind, sonst bekommt man nur Zeichensalat.

Mit Programmen wie [Coolterm](http://freeware.the-meiers.org/) (Windows,
Mac, Linux) kann man Geräte ansprechen oder deren Kommunikation
empfangen und aufzeichnen. Unter Linux kann man auch die Konsole oder
ein Shell-Script benutzen, um die serielle Kommunikation zu empfangen
und ggf. weiterzuverarbeiten, mit `minicom`, `screen` oder
`serialclient` ([hier eine
Anleitung](https://wiki.archlinux.org/index.php/working_with_the_serial_console)).
Mit `ttylog` oder einfach `cat` können die eintreffenden seriellen Daten
in einer Datei gespeichert werden. z.B. so:

`cat /dev/ttyS0 > file.txt`

Hier ist `/dev/ttyS0` das serielle Gerät.

### Versteckte serielle Schnittstellen

Was weniger offensichtlich ist, ist dass viele Moderne Geräte wie
DSL-Router, Tablets oder E-Reader auch serielle Schnittstellen besitzen.
Diese sind nicht für den Endnutzer gedacht und meistens irgendwo im
Gerät auf der Platine versteckt. Diese Schnittstellen werden genutzt,
um während der Entwicklung Debuginformationen vom Gerät zu erhalten oder
bei der Produktion oder bei einer eventuellen Reperatur Informationen
vom Gerät zu erhalten und Dinge einstellen oder aufspielen zu können. Da
viele dieser Geräte mit einem Linux-Betriebssystem laufen lässt sich
über diese Schnittstelle auf eine Shell zugreifen. Oft direkt mit
root-Rechten. Meistens muss man das Gerät öffnen, um an diese
Schnittstellen zu gelangen. Oft handelt es sich lediglich um vier
nebeneinander liegende Lötstellen, die manchmal mit `5V/3.3V`
(Stromversorgung), `RXD` (Receive), `TXD` (Transmit) und `GND` (Masse)
beschriftet sind, oft aber auch völlig ohne Kennzeichnung. Eine gute
Anleitung, wie man diese Kontakte findet, die richtigen Anschlüsse
identifiziert und die richtigen Kommunikationseinstellungen findet gibt
es
[hier](http://www.devttys0.com/2012/11/reverse-engineering-serial-ports/).

Einen Guten Vortrag zu dem Thema findet man in
[hier](http://www.livediesel.de/?p=581). Hier geht es darum,
ausrangierte Geräte wieder nutzbar zu machen (Thema
[Upcycling](Upcycling "wikilink")) und eventuell für ganz andere Dinge
zu verwenden, als für die sie gebaut wurden.

# Geräte

Die folgenden Geräte wurden in unserem fablab wieder nutzbar gemacht
oder in ihrem Funktionsumfang erweitert. Wie es gemacht wurde soll hier
dokumentiert werden.

## CalComp Drawing Board

Ich habe ein digitales Zeichenbrett von CalComp in einer Auflösung eines
Ingenieurbüros gefunden. So ein Gerät was sich super für
AutoCad-Zeichnungen eignet. Für das Gerät findet man schlecht noch
Treiber für aktuelle Betriebssysteme und grundsätzlich hat man erstmal
Probleme, das Ding an moderne Computer anzuschließen - das geht nur mit
einem USB-auf-Seriell Adapter. Mit Hilfe dreier Anleitungen
[1](http://www.relief.hu/index_5.html),
[2](http://courses.washington.edu/fe450/handbook/Digi_setup.htm),
[3](http://www.softree.com/Help/source/html/terr67of.htm) habe ich die
nötigen Einstellungen am Tablet und Computer vorgenommen, um die
Kommunikation über die serielle Schnittstelle herzustellen. Nun bekomme
ich in Coolterm die Koordinaten des Stifts angezeigt. Jetzt muss ich
noch Wege finden, um das in eine Mausbewegung umzuwandeln oder andere
Interessante Dinge damit zu veranstalten, wie z.B. Musik- oder
Lichteffekte steuern. Eventuell kann ich einen [Arduino
Micro](http://arduino.cc/en/Main/ArduinoBoardMicro) an das Gerät
anbauen. Dieser wird vom Computer als Maus (und Tastatur) erkannt. Somit
könnte ich über den Arduino das serielle Signal in eine USB-Maus
Bewegung umwandeln. Somit könnte das Board wieder an jeden Computer
angeschlossen werden, ohne irgendetwas installieren zu müssen.

## [HeliosMini Wetterstation/Datenlogger](HeliosMini_Wetterstation/Datenlogger "wikilink")

## Tolino Shine

Der E-Reader "Tolino Shine" ist leider verklebt. Deshalb muss man sich
schon trauen, das Gerät zu öffnen. Allerdings reicht es schon, wenn man
den Tolino an einer bestimmten Stelle etwas aufhebelt, dann kommt man
schon an die Kontakte heran. [Hier](http://www.livediesel.de/?p=561)
findet sich eine Anleitung. Über die Schnittstelle bekommt Zugriff auf
die Android-Shell und kann den [Tolino
rooten](http://www.livediesel.de/?p=581) und damit auch die
USB-Schnittstelle für weitere Shell-Zugriffe freischalten. Letztendlich
kann man damit auch andere Apps auf dem Tolino installieren, die der
Hersteller nicht vorgesehen hat.