{{\#ev:youtube|id=[http://youtu.be/opSofzCnbJo|480x320|right|Beispielanimation|frame](http://youtu.be/opSofzCnbJo%7C480x320%7Cright%7CBeispielanimation%7Cframe)}}
<onlyinclude> Ein Projekt, welches Lichter oder sonstige Geräte in
Abhängigkeit von einem Audiosignal ansteuern kann. Die ursprüngliche
Idee war es, eine Matrix aus RGB-LEDs so anzusteuern, dass eine
Lichtshow abläuft, welche durch die Frequenz und Geschwindigkeit eines
Liedes beeinflusst wird. </onlyinclude>

# Idee

Ich wollte eine Beleuchtung haben, welche je nach Takt bzw. Frequenz
einer Melodie ihre Farbe ändert. Es gibt zwar einige Projekte, welche
LEDs aufblinken lassen, wenn ein Beat innerhalb eines Frequenzbandes
vorliegt (z.B. [diese
Lichtorgel](http://www.dieelektronikerseite.de/Circuits/3%20Kanal%20LED-Lichtorgel.htm)).
Jedoch gibt es kein Projekt, welches komplexere Zusammenhänge zwischen
Licht und Musik erlaubt und vollkommen autark, ohne z.B. einen PC,
arbeitet.

# Konzept und Vorüberlegungen

Ein analoges Audiosignal wird durch einen Mikrocontroller über einen
Klinkenstecker eingelesen. Die Daten werden ausgewertet und folgende
Parameter berechnet: Amplitude, Beats und Intensität verschiedener
Frequenzen. Diese Werte werden benutzt, um Farbveränderungen bzw.
Animationen auf einer LED-Matrix zu steuern.
In einem ersten Test wurde eine Eingangs- und Filterstufe aufgebaut,
welche ein Mono-Audiosignal aufbereitet. Ein atmega328 hat dieses
Abgetastet und eine FFT des Signals durchgeführt. Damit wurde eine
einzelne RGB-LED angesteuert. Diese hat ihre Farbe in Abhängigkeit der
Frequenz geändert. Mit diesem System wurden die Grenzen des atmega328
ausgetestet. Da dieser Controller nur mit 16MHz läuft, waren diese
Grenzen zwar schnell erreicht, die Ergebnisse konnten sich allerdings
schon sehenlassen. Das Einlesen der Daten und die FFT wurden 10x pro
Sekunde durchgeführt, so dass die resultierenden Daten für eine flüssige
Animation sorgten. Für ein Stereo-Signal wären jedoch nur noch 5 Updates
der Daten pro Sekunde und Kanal möglich.
Für das fertige System sollte also ein anderer Controller zum Einsatz
kommen. Die Anforderungen waren: 2 ADC, DMA, auch für Hobby-Bastler
leicht zu beschaffen, programmieren und löten. Daher wurde ein
atxmega128-A3U gewählt. Dieser ist durch den Bootloader [von diesem
Projekt](http://matrixstorm.com/avr/tinyusbboard/) einfach zu
programmieren, auch ohne Programmiergerät. Vorprogrammierte Controller
sind bei ebay durch den Händler
[matrixprog](http://www.ebay.de/usr/matrixprog) erhältlich. Durch die
Kombination aus 2 unabhängigen ADC und DMA kann ein Stereo-Audiosignal
problemlos umgewandelt werden. Es sind genügend Pins und
Hardwareressourcen vorhanden, um weitere Geräte, wie z.B. Taster und LCD
anzuschließen. Auch die Audio-Eingangsstufe wurde leicht angepasst.
Eine Echtzeitauswertung in dem Sinne, dass das System innerhalb weniger
ms oder sogar µs auf ein Audiosignal reagiert, ist mit dem Aufbau nicht
möglich. Der Grundgedanke ist es, die Audiodaten 20mal pro Sekunde zu
erfassen und auszuwerten. Diese Daten werden gespeichert und durch ein
Animationssystem, welches 60 Bilder pro Sekunde berechnet, optisch
dargestellt. Dadurch, dass das menschliche Sehempfinden recht träge ist
und sich in hoher Geschwindigkeit immer etwas verändert, wirkt es am
Ende so, als ob die Animation schnell auf die Musik reagiert, obwohl
diese Reaktion nur alle 100ms erfolgt.

# Hardware

![audio_board_schematic.svg](audio_board_schematic.svg
"audio_board_schematic.svg") Das Audiosignal wird über einen
Stereo-Klinkenstecker in das System eingegeben. Die Audio-Eingangsstufe
beinhaltet eine
[AGC](http://de.wikipedia.org/wiki/Automatische_Verst%C3%A4rkungsregelung),
welche die maximale Amplitude des Signales so begrenzt, dass es einem
Übersteuern entgegen wirkt. Außerdem wird ein Bandpass-Filter
eingesetzt, welcher alle Signale zwischen ca. 16Hz und 16kHz durchlässt.
Der Aufbau der Eingangsstufe orientiert sich an [diesem
Projekt](http://sound.westhost.com/project62b.htm).
Als Controller wird ein atxmega128A3U eingesetzt. Die Hauptgründe dafür
sind, dass er über 2 unabhängige ADC verfügt, damit linker und rechter
Kanal gleichzeitig in ein digitales Signal umgewandelt werden können,
und dass DMA vorhanden ist, damit dieses Umwandeln komplett von der
Hardware erledigt werden kann. Durch die Pinkompatibilität ist es
möglich, alle Controller der atxmega A3U Reihe einzusetzen. Je nach
Anwendung ist jedoch mindestens der 128A3U anzuraten, da die kleineren
Controller über weniger RAM verfügen. Alle nicht benutzten Leitungen
sind herausgeführt und können frei verwendet werden.
Die Spannungsversorgung erfolgt entweder über USB oder ein 5V Netzteil.
Dieses wird über einen Spannungsregler auf 3,3V heruntergesetzt, um den
Controller damit zu versorgen. Es ist auch möglich, das Board direkt mit
3,3V zu versorgen.

## Technische Details und Anmerkungen

  - Der Controller arbeitet mit 3,3V, daher niemals mehr an den
    Signalleitungen anlegen
  - Den internen Spannungsregler niemals mit mehr als 5V betreiben
  - Jumper JP1 offen lassen, wenn mit Stereo-Signalen gearbeitet wird.
    Schließen, um aus einem Stereo-Signal ein Mono-Signal zu machen
  - Benutzte Pins:
      - Port A, Pin 7: Audio Input
      - Port B, Pin 0: Analoge Referenz Spannung
      - Port B, Pin 1: Audio Input
      - Port D, Pin 6 und 7: USB
  - Pin Header P17 "Stereo Pot" war vorgesehen, um ein Potentiometer
    anzuschließen, damit die Empfindlichkeit der Eingangsstufe
    eingestellt werden kann. Es hat sich jedoch gezeigt, dass dieses
    nicht notwendig ist. An P17 können Pin 1 und 3 bzw. Pin 2 und 4
    direkt mit einem 100 Ohm Widerstand verbunden werden. (**Wichtig für
    Nachbau\!**)
  - Taster SW1 ist nicht verbunden. Dieser kann, je nach verwendetem
    Bootloader oder anderen Ansprüchen, frei benutzt werden.

## Konkreter Testaufbau

![audioboard_testaufbau_konkret.png](audioboard_testaufbau_konkret.png
"audioboard_testaufbau_konkret.png") Ein Anwendungsbeispiel ist die
Ansteuerung einer Matrix aus RGB LEDs. Es werden LEDs mit einem WS2812
Controller verwendet, da diese schon einen Treiber eingebaut haben und
der Hardware Aufbau (zu Ungunsten des Softwareteils) vereinfacht wird.
Auf die LEDs wurden billige Tischtennisbälle (Bastelladen, EBay) geklebt
und dienen als Diffusionsfläche für das Licht.
Auf einem kleinen Stück Lochrasterplatine befindet sich ein ca. 1"
kleines OLED Display, welches mit I2C angesteuert wird, und ein
Drehgeber mit eingebautem Taster. Diese Platine wird derzeit zum
Debuggen benutzt und soll später ermöglichen zwischen unterschiedlichen
Betriebsmodi zu wählen.
Der Audioverstärker mit Lautsprecher dient lediglich als Debug-Ausgabe
für das Audiosignal, damit zu hören ist, was am Ende des AGC und
Filters herauskommt.
Das PC Netzteil versorgt die LEDs mit 5V und wird benötigt, da USB nicht
genug Strom liefern kann. Die Versorgung der Logik erfolgt wahlweise
über USB oder ebenfalls über das Netzteil.
In der finalen Version soll die Logik in einem Holzkasten verschwinden
und das PC Netzteil soll gegen ein kompakteres 5V Netzteil ausgetauscht
werden. Dieser Kasten kann dann an die Wand gehängt werden und erzeugt
dynamische Animationen mit Farbwechseln und -verläufen in Abhängigkeit
zum eingegebenen Audiosignal. Eine mögliche Erweiterung wäre ein
Mikrofon einzusetzen, um das Audiokabel einzusparen. Dann würden jedoch
alle Umgebungsgeräusche mit aufgenommen werden. Dies kann je nach
Situation ein Vorteil oder Nachteil sein.

# Software

Die Software ist natürlich je nach der Anwendung sehr unterschiedlich.
Daher wird ein Basis-Quelltext angeboten, welcher die Datenerfassung und
-auswertung für das Matrix-Projekt beinhaltet. Weitere Anpassungen
sollten problemlos möglich sein.
Download des Quelltextes (als Atmel Studio Projekt)
Im Folgenden werden die grundlegenden Gedanken und Funktionen
besprochen. Diese sollten eine eigenständige Weiterentwicklung
vereinfachen.

## Datenerfassung

  - adc.cpp, adc.h
  - Nutzt ADCA Ch0, ADCB Ch0, DMA Ch1 und DMA Ch2, TCC0

Der ADC wird im Freerun Modus konfiguriert und der Timer TCC0 auf eine
Frequenz von 32kHz gestellt. Wird eine Messung mit
**adc_startSampling()** gestartet, werden die DMA Kanäle aktiviert und
laden mit jedem overflow von TCC0 einen Messwert in den Speicher. Auf
diese Weise werden 128 Messwerte je Kanal erfasst. Ist diese
Datenerfassung abgeschlossen, wird *adc_state* durch **adc_check()**
auf *ADC_STATE_SAMPLING_DONE* gesetzt.

## Auswertung

  - fffft.S, fffft.h, CFFT.cpp, CFFT.h

Für die Berechnung der FFT wird die [FFT Lib von elmchan
verwendet](http://elm-chan.org/works/akilcd/report_e.html). Wenn die
Daten mit 32kHz eingelesen werden, ist es möglich, Frequenzen bis 16kHz
zu rekonstruieren. Mit Hilfe der FFT werden diese Frequenzen bestimmten
Bändern zugeordnet. Mit den Funktionen **getLeft()** bzw. **getRight()**
lassen sich die letzten Ergebnisse abrufen. Diese ist ein Zeiger auf
einen Datensatz vom Type *fft_result_t*.

    typedef struct {
        uint16_t spectrum[FFT_N / 2];
        uint16_t adc_min, adc_max;
    } fft_result_t;

spectrum ist in diesem Fall ein Array mit 64 Elementen (128 Abtastwerte
/ 2). Jeder dieser Werte umfasst die Intensität für einen bestimmten
Frequenzbereich. spectrum\[0\] gibt einen Wert für Frequenzen im Bereich
0 ... 250Hz; spectrum\[1\] für den Bereich 250Hz ... 500Hz. Dies ergibt
sich aus dem gesamten Frequenzbereich 16kHz und den 64 Elementen der
FFT. 16kHz / 64 = 250. Somit lassen sich Frequenzen bis auf 250Hz
bestimmen. Es ist möglich, die Auflösung der Gesamtfrequenz zu
verbessern, indem die Anzahl der Samples erhöht wird. Dadurch steigt
natürlich die CPU- und Speicherauslastung.
Die Elemente adc_min und adc_max sind die Werte für den minimalen bzw.
maximalen ADC Wert. Damit kann die Amplitude des Signals berechnet
werden.
Die Berechnung ist mit Hilfe einer State-Maschine in kleine Schritte
aufgeteilt. Mit der Funktion **doFFT()** wird diese gestartet. Danach
muss solange **doStep()** aufgerufen werden, bis diese Funktion den Wert
*FFT_STATE_IDLE* zurückgibt. Der Sinn besteht darin, die
rechenintensiven Sachen, die die CPU blockieren, möglichst auseinander
zu ziehen. Wird die CPU zu lange blockiert, können andere Events, wie
z.B. das Auswerten einer Eingabe oder die Berechnung der Ausgabe,
verzögert werden. Die Animation läuft dann teilweise flüssig und kommt
teilweise ins Stocken. Dies ist für den Betrachter sichtbar und sieht
nicht schön aus. Ähnlich kann auch die Eingabe mal mehr und mal weniger
empfindlich wirken.


  - animation.cpp, animation.h

Die durch die FFT erhaltenen Daten werden über die Funktion
**anim_inputData(fft_result_t \*left, fft_result_t \*right)** in
das Animationssystem eingelesen. Diese fasst die Daten der FFT in 7
Bänder zusammen und führt eine einfache Beat Erkennung durch. Die
Bänder sind wie folgt eingeteilt:

| Band | Frequenzbreich | FFT Buckets |
| ---- | -------------- | ----------- |
| 0    | 0 ... 250      | 0           |
| 1    | 250 ... 500    | 1           |
| 2    | 500 ... 1000   | 2 ... 3     |
| 3    | 1000 ... 2000  | 4 ... 7     |
| 4    | 2000 ... 4000  | 8 ... 15    |
| 5    | 4000 ... 8000  | 16 ... 31   |
| 6    | 8000 ... 16000 | 32 ... 63   |

Die Ergebnisse davon lassen sich in den globalen Variablen *uint16_t
bands_l\[ANIM_BAND_NUM\], bands_r\[ANIM_BAND_NUM\]* für den linken
und rechten Kanal finden.
Diese Funktion berechnet ebenfalls die Amplitude und stellt diese als
globale Variablen *uint16_t amplitude_l, amplitude_r* zur
verfügung.
Die Beaterkennung läuft ebenfalls über die Ergebnisse der FFT. Sie wird
für Tiefen (16Hz ... 750Hz), Mitten (750Hz ... 5kHz) und Höhen (5kHz ...
16kHz) durchgeführt. Für jedes dieser 3 Frequenzbänder wird ein
fließendes Mittel gebildet. Ist der momentane Wert um einen bestimmten
Prozent-Wert höher als dieses Mittel, wird es als Beat gewertet. Für die
Tiefen funktioniert dies recht gut, aber für die Mitten, gerade wenn
Gesang vorhanden ist, und meistens auch für die Höhen, funktioniert es
nicht so gut. Die BPM werden über die globalen Variablen *uint8_t
bpm_h, bpm_m, bpm_l, bpm_all* (h - Höhe, m - Mitte, l - Tiefe, all -
in irgendeinem Band) bereitgestellt. Zusätzlich kann über *uint8_t
beats* abgefragt werden ob gerade ein Beat erkannt wurde, indem auf die
Bits *BEAT_HIGH*, *BEAT_MID* bzw. *BEAT_LOW* zugegriffen wird.
Es gibt eine einfach Funktion zur Kalibration der Daten im Quelltext des
Matrix Projektes. Diese sind in der Struktur

    typedef struct  {
        uint8_t ident;
        uint16_t bands_calib_l[ANIM_BAND_NUM], bands_calib_r[ANIM_BAND_NUM];
        uint16_t amplitude_l, amplitude_r;
    } bands_calibration_t;

zusammengefasst. In der Funktion **anim_init()** werden diese Werte mit
Standardwerten belegt bzw. werden aus dem EEPROM geladen. Mit
**anim_startCalibration()** kann die Kalibration gestartet werden,
sofern das erweiterte Animationssystem benutzt wird. Diese Funktion muss
aufgerufen werden, wenn das Audiokabel verbunden ist und kein Signal
anliegt. Die Störungen, die nun auf der Leitung sind, werden gemessen,
gemittelt und gespeichert. Danach werden die Kalibrationswerte in
**anim_inputData()** benutzt um diese Störungen herauszurechnen. Die
Daten der FFT werden dabei nicht verändert. Lediglich die
zusammengefassten 7 Bänder und die Amplitude werden abgeglichen.

## Hauptschleife

  - MusikDing.cpp
  - Nutzt TCC1

Timer TCC1 wird als Systemtimer genutzt und löst jede ms einen Interrupt
aus. Die Anzahl der vergangenen ms können über die globale Variable
*volatile uint32_t systick* abgefragt werden. Zusätzlich werden im
Timer die Flags für Events gesetzt, wie z.B. ein neuen Frame berechnen
und das Einlesen der Daten zu starten.
In der Hauptschleife werden diese Flags abgefragt und entsprechend
darauf reagiert. Es sind einige stellen mit TODO markiert. Hier ist der
eigene Code einzutragen, sofern die Funktionen genutzt werden sollen.
Wichtig ist, dass die Funktionen das System nicht zu lange blockieren,
z.B. bei der Ausgabe auf Displays, damit die Animationen und das
Einlesen der Daten nicht hinausgezögert werden.
Das System zum Daten einlesen und auswerten wird alle 100ms aktiviert.
Sobald das Einlesen fertig ist, wird *adc_state ==
ADC_STATE_SAMPLING_DONE* wahr und die FFT gestartet. Nun wird solange
**fft.doStep()** aufgerufen, bis alle Schritte abgearbeitet sind. Danach
wird das *FLAG_FFTDONE* Flag gesetzt und das ADC-System geht in einen
Idle Zustand, wodurch es bereit ist neue Daten einzulesen. Durch das
Flag wird **anim_inputData(fft.getLeft(), fft.getRight())** aufgerufen
und die Daten der FFT werden in das Animationssystem übertragen.

## WS2812 Lib

  - CWS2812.cpp, CWS2812.h
  - Nutzt USARTC1 und DMA Ch0

Die Vorteile der WS2812 LED liegen darin, dass diese einen eingebauten
Treiber besitzen und die Daten über eine einzige Datenleitung übertragen
werden. Dies macht einen Hardwareaufbau sehr einfach. Der Nachteil liegt
darin, dass das Protokoll für die Daten ein sehr striktes timing
erfordern. Andere Libraries machen dies über eine Verzögerung, wodurch
Rechenleistung mit warten verschwendet wird.
Daher erfolgt hier ein Ansatz über den USART (im SPI Modus) und DMA.
Dies hat jedoch den Nachteil, dass pro zu sendendem Bit 1 Byte RAM
benötigt wird. Eine LED erwartet 3 Byte, also 24 Bit, und benötigt
somit 24 Byte RAM im Controller. Dafür werden die Daten mit Hilfe von
DMA gesendet, so dass keine Rechenleistung in Warteschleifen verbraucht
wird. Da der verwendete Controller 8kb RAM hat und nur 42 LEDs in der
Matrix sind, ist diese Lösung in dieser Situation gut brauchbar.
Die Initialisierung der Peripherie erfolgt im Konstruktor der Klasse. Es
wird USARTC1 benutzt und der Output liegt an Port C Pin 7. Port C Pin 5
und 6 sind die Clock- bzw. Empfangsleitung und werden nicht benötigt,
aber stehen nicht mehr für andere Anwendungen zur Verfügung. Die Anzahl
der LEDs muss in der CWS2812.h durch das Symbol *LED_NUM* definiert
werden. Mit **input(uint8_t \*led_data, uint16_t len)** werden die
RGB Daten in das WS2818 System übertragen. Pro LED werden 3 Byte, je
eines für Rot, Grün und Blau, erwartet. **transfer()** startet den DMA
Transfer und mit **isBusy()** kann geprüft werden, ob dieser
abgeschlossen ist (\!= 0).

## Animationen

Für das Matrix-Projekt soll es viele verschiedene Animationen geben, die
manuell oder automatisch ausgewählt werden können. Daher wurde ein
komplexes System mit einer Tabelle mit Funktionszeigern geplant. In der
Tabelle *anim_list_t anim_list\[ANIM_LIST_NUM\]* (animation.cpp)
werden die Animationen mit ihrer Funktion zum initialisieren, zur
Berechnung eines Bildes und einem Namen eingetragen. Über die Funktion
**anim_start(uint16_t num)** wird Animation Nummer *num* gestartet.
Nun muss nur noch periodisch **anim_frame()** aufgerufen werden und das
System kümmert sich um den Rest.
Zur Vereinfachung oder wenn nur 1 Animation vorhanden sein soll, kann
der komplette Inhalt der Funktion **anim_frame()** durch eigenen Code
ersetzt werden. Dadurch muss jedoch auch die Kalibration und/oder die
Standartwerte angepasst werden. Dies ist in der Basic Version des
Quelltextes der Fall.

## Weiterführende Ideen

Als Idee für eine Animation soll hier kurz eine existierende Vorgestellt
werden, wie sie im Video zu sehen ist. Die Matrix ist 7 LEDs breit und
das Animationssystem fasst das Spektrum in 7 Bänder zusammen. Dadurch
kann auf jeder Spalte eines dieser Bänder wiedergegeben werden. Jedes
Band hat eine vorgegebene Grundfarbe, welche sich in Abhängigkeit von
der Amplitude verändert. Die Anzahl der leichtenden LEDs pro Spalte
richtet sich nach dem Wert im zugeordneten Band. Dadurch ergibt sich
eine einfacher Frequenzanzeigen, welche über die Zeit leicht ihre Farbe
verändert. Zusätzlich blitzen die Tiefen, Mitten bzw. Höhen kurz auf,
wenn ein Beat in dem Bereich erkannt wurde.

# Download

[Download über GitHub](http://github.com/MarJong/AudioBoard)

# Bilder

Datei:audioboard_debug_ausgabe.png|Debug Ausgabe auf dem Display. Es
zeigt: Name der Animation, Bilder pro Sekunde (FPS) und Samplevorgänge
pro Sekunde (SPS), die BPM in den Höhen, Mitten, Tiefen und Alle
zusammen, die 7 Bänder für linken und rechten Kanal und ganz unten
rechts den Zoomfaktor für den Graphen.
Datei:audioboard_animation1.png|Mono-Spektrum Anzeige. Die Daten vom
linken und rechten Kanal werden zusammengefasst und angezeigt.
Datei:audioboard_animation2.png|Stereo-Spektrum Anzeige. Die Daten vom
linken und rechten Kanal werden getrennt links und rechts angezeigt und
können sich in der Mitte überlagern.
Datei:audioboard_animation3.png|Etwas abstrakter: Mit jedem Beat fliegt
1 Partikel, dessen Farbe und Geschwindigkeit von der Frequenz bzw. den
BPM abhängig ist, über die Matrix.
Datei:audioboard_animation4.png|Bunter Kreis, der sich bewegt. Die
Farbe ändert sich mit der Frequenz.