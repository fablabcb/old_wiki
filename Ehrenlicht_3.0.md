![Ehrenlicht_3.0.jpg](Ehrenlicht_3.0.jpg "Ehrenlicht_3.0.jpg")
<onlyinclude> Das Ehrenlicht 3.0 ist die dritte Generation eines
Projektes, welches eine Lampe zur Folge haben soll, die Musik visuell
darstellt. Diese Version ist die digitale Fortführung der bisher analog
gebauten Vorgänger und basiert auf dem im Fablab Cottbus entwickelten
[Audio Board](http://fablab-cottbus.de/index.php/Audio_Board).
</onlyinclude>

## Idee

Das Ziel war es, eine Lampe zu entwickeln, die Musik rudimentär über
Licht wiedergibt. Angelehnt an ein spectrum analyzer sollte dies über
die Helligkeits- und Farbansteuerung von LEDs passieren. Das Ziel ist
ein Beleuchtungssystem, welches den ganzen Raum in eine Lichtstimmung
taucht, die auf die Musik abgestimmt ist. Bei der Idee geht es nicht
darum, eine einfache Lichtorgel für Partyzwecke zu entwickeln, sondern
um ein kompliziertes System, das das Musikhören zu einem audiovisuellen
Erlebnis macht.

## Basis

Das Ehrenlicht 3.0 wurde mit Hilfe des im Fablab Cottbus entwickelten
[Audio Boards](http://fablab-cottbus.de/index.php/Audio_Board)
umgesetzt. Dies ist ein autarker Aufbau, der unabhängig von einem
anderen System über die Analyse des über ein Audiokabel eingegebenen
Audiosignals folgende Parameter zur Verfügung stellt: BPM, Pegel
(Stereo) und Frequenzband (Stereo). Diese Daten werden 20 mal pro
Sekunde erfasst und gespeichert. Das Animationssystem wurde in die
Programmroutine des Audio Boards geschrieben.

## Technischer Aufbau

Das System besteht aus zwei Teilen:

  - 1\. dem Audio Board (Basis: ATxmega128A3U), das einen Sound-Stream
    erfasst und durch eine fft digitalisiert sowie eine rudimentäre
    BPM-Analyse durchführt und
  - 2\. der eigentlichen Lampensteuerung (Basis: ATmega328P), die die
    Animation berechnet und die WS2812 LEDs ansteuert.

Verbunden sind die beiden Teilsysteme durch zwei nRF24L01 Funkmodule,
die über master SPI mit den jeweiligen AVRs kommunizieren (Grundlage für
die Ansteuerung der nRFs ist die von Ernst Buchmann erstellte
[Lib.](https://www.mikrocontroller.net/articles/NRF24L01_Tutorial)). Die
Lampe selbst besteht aus 60 übereinander angeordneten WS2812 RGB LEDs
(zerschnittener LED Streifen, jede LED einzeln ansteuerbar), die in 6er
Gruppen zusammengefügt sind. Jede dieser Gruppen beleuchtet eine von 10
10\*10\*1,5 cm großen Acrylglasplatten, die in eine 150\*10\*2,5 cm
große Tulpenholzleiste eingebettet sind. Die RGB LEDs werden durch
bit-banging angesteuert (es wird die light wight
[Lib.](https://github.com/cpldcpu/light_ws2812) von Tim benutzt) und die
Farben durch den [HSV
Farbraum](https://de.wikipedia.org/wiki/HSV-Farbraum) manipuliert, da
dieser der menschlichen Farbwahrnehmung ähnelt. Der Widerstand in der
rechts aufgeführten Schematik wird beim 3,3V Betrieb (wie beim
Ehrenlicht der Fall) nicht benötigt. [Den Code findet ihr
hier](https://github.com/maximusvo/Ehrenlicht).
![WS2812_schematic.png](WS2812_schematic.png "WS2812_schematic.png")

{{\#ev:youtube|id=[https://youtu.be/IKv1kGGX70Y|480x320](https://youtu.be/IKv1kGGX70Y%7C480x320)||Neuste
Version|frame}}
{{\#ev:youtube|id=[https://youtu.be/6lgkiiwZq3Y|480x320](https://youtu.be/6lgkiiwZq3Y%7C480x320)||Demonstration
des ersten Aufbaus|frame}}

## Hinweise zu NRF24L01 Funkmodulen

Wenn die Module auf anderen Plattformen verwendet werden sollen, muss
lediglich die spi.c/h angepasst werden. Um die Funktionalität der Module
zu gewährleisten, sollte auf ein Netzteil mit ausreichender Leistung
geachtet sowie ein 10µF Kondensator für die Stabilisation und Entstörung
zwischen +/- der nRFs gelötet werden.

## Pinkonfiguration

  - nRFs (spi.c):
      - ATmega328P: PORT_SPI PORTB, DDR_SPI DDRB, DD_MISO DDB4,
        DD_MOSI DDB3, DD_SS DDB2, DD_SCK DDB5
      - ATxmega128A3U: PORT_SPI SPIC -\> PORTC, DD_MISO PIN6, DD_MOSI
        PIN5, DD_SS PIN4, DD_SCK PIN7

<!-- end list -->

  - WS2812 (ws2812_config.h):
      - ATmega328P: Port C, Pin 1

## Aktuelle Projektarbeiten

Um eine höhere Auflösung der Animation zu ermöglichen (durch mehr
Prozessorleistung) und um auch digitale, optische Lichtleitersignale
verarbeiten zu können, soll das Audio Board mit einem Cortex Controller
bestückt werden. Außerdem ist eine App in Planung, mit der das System
konfiguriert werden kann.

## Fotodokumentation

![Ehrenlicht_Bau_1.JPG](Ehrenlicht_Bau_1.JPG "Ehrenlicht_Bau_1.JPG")
![Ehrenlicht_Bau_2.JPG](Ehrenlicht_Bau_2.JPG "Ehrenlicht_Bau_2.JPG")
![Ehrenlicht_Bau_3.JPG](Ehrenlicht_Bau_3.JPG "Ehrenlicht_Bau_3.JPG")
![Ehrenlicht_Bau_4.JPG](Ehrenlicht_Bau_4.JPG "Ehrenlicht_Bau_4.JPG")
![Ehrenlicht_Bau_5.JPG](Ehrenlicht_Bau_5.JPG "Ehrenlicht_Bau_5.JPG")