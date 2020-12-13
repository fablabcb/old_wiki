Wikipedia listet die folgenden [Funksysteme zur
Gebäudeautomatisierung](https://de.wikipedia.org/wiki/Funksysteme_zur_Gebäudeautomatisierung):

  - **DECT ULE** (Ultra Low Energy), energiesparende Erweiterung des
    Schnurlostelefon-Standards DECT für die Hausautomation
  - **EN 50090**, der weltweit erste offene Standard für die Haus- und
    Gebäudeautomatisierung (Draht/TP, Powerline, Funk)
  - **Enocean**, seit 2012 internationaler Standard, dessen
    Sicherheitsoptionen jedoch nicht alle EnOcean-Produkte nutzen
  - **HomeMatic** (auch BidCoS), Funksystem für die Hausautomation
  - **KNX-RF**, Funkversion des KNX-Standards für die Gebäudeautomation
  - **ZigBee**, Funkstandard zur Gebäudeautomation mit Beteiligung
    zahlreicher internationaler Firmen
  - **Z-Wave**, besonders in den USA stark verbreiteter Standard der
    Z-Wave-Alliance

Im folgenden weitere Details zu einigen dieser Systeme (Quelle
hauptsächlich Wikipedia):

# Z-Wave

Z-Wave nutzt eine Zweiwege-Kommunikation mit Rückbestätigung. Nur
erfolgreich bestätigte Datagramme gelten als erfolgreich versendet. Bei
Kommunikationsfehlern wird der Sendevorgang bis zu dreimal wiederholt.
Z-Wave implementiert als Netzwerktopologie eine Funkvermaschung, bei der
jedes netzbetriebene Gerät Datagramme anderer Geräte im eigenen Netz
weiterleiten kann. Das damit entstehende vermaschte Netz wird ebenfalls
vom Primärcontroller gesteuert und die Routen bei Veränderungen des
Netzes aktualisiert. Routen können sich über bis zu 4 Zwischen-Hops
erstrecken.

Alle netzbetriebenen Geräte sind ständig funkaktiv und können daher als
Router dienen. Batteriebetriebene Sensoren und Aktoren sind meist
inaktiv und wachen periodisch auf, um Kommandos entgegenzunehmen und
auszusenden.\[1\]

In Europa arbeitet Z-Wave auf einer Frequenz von 868,4 MHz bzw. 869 MHz.

# EnOcean

Die Idee der Enocean-Technologie beruht darauf, dass für das Senden von
kurzen Funksignalen nur geringe Mengen an Energie benötigt werden. Die
Sender nutzen daher die Piezoelektrizität von Schaltern (Energy
Harvesting), die Energie von Solarzellen oder Peltier-Elementen oder
auch die Bewegungsenergie mittels elektrodynamischer Energiewandler.
Diese Energie reicht aus, um Sender batterielos und somit wartungsarm zu
betreiben. In einigen Anwendungsfällen sind jedoch weder gute
Lichtverhältnisse noch mechanische Betätigungen zu erwarten, sodass
teilweise auch Batterien als Energiequelle eingesetzt werden. Das
Funkprotokoll ist darauf ausgerichtet, Informationen energiearm mit
hoher Zuverlässigkeit zu übertragen. Dafür werden in Europa die Frequenz
868,3 MHz, in Japan die Frequenz 928 MHz, und in Nordamerika die
Frequenzen 315 MHz (vorrangig) sowie 902 MHz verwendet.

Es existiert kein Mechanismus zur Vermeidung von Kollisionen; es wird
versucht, diese durch die Beschränkung auf möglichst kleine und dadurch
kurze Datenpakete gar nicht erst auftreten zu lassen. Zur Funkmodulation
kommt die Amplitudenumtastung zum Einsatz, die sich elektronisch einfach
und energiesparend umsetzen lässt.

Erweiterte Sicherheitskonzepte wie Verschlüsselung der Funkdaten und
Rolling Code verhindern es, die Datenpakete von Enocean-Sendern
unbemerkt abzugreifen. Zudem wird das Senden eines Datenpaketes von den
originären Enocean-Komponenten nur unter Verwendung festgelegter 32bit
großer IDs erlaubt, sodass die Manipulation eines Enocean-gestützten
Systems von außen nur bedingt möglich ist. Einen Schutz gegen Signale
einer eigenen Implementierung des relativ simplen Funkstandards gibt es
jedoch nicht.

Im Gegensatz zu anderen Gebäudeautomatisierungstechnologien ist eine
Bestätigung des Empfangs eines Datenpaketes in der Spezifikation
vorgesehen. Mittlerweile sind auch kommerzielle Geräte verfügbar, die
die Feststellung ermöglichen, ob ein Steuerbefehl erfolgreich ausgeführt
wurde.\[2\]

# ZigBee

ZigBee ist eine Spezifikation, welche ein Framework für drahtlose
Funknetzwerke beschreibt. ZigBee baut auf dem IEEE 802.15.4 Standard auf
und erweitert dessen Funktionalität insbesondere um die Möglichkeit des
Routings und des sicheren Schlüsselaustausches. Im IEEE 802.15.4
Standard sind die PHY-Schicht und die MAC-Schicht definiert. ZigBee
erweitert diesen Protokollstapel um die Schichten NWK und APL. Wobei zu
beachten ist, dass es sich bei ZigBee um ein Framework handelt und eine
Anwendung in die APL-Schicht eingebettet wird.

Die Einsatzmöglichkeiten von ZigBee sind vielfältig, z. B. in der
Gebäude-Automation, im medizinischen Bereich, für Steuerungsanlagen und
für alle Arten von Sensormessungen.

Die ZigBee-Spezifikation stellt dem Entwickler drei verschiedene
Gerätearten (ZigBee Devices) zur Verfügung. Mit diesen Geräten wird ein
ZigBee Wireless Personal Area Network (WPAN) aufgebaut. Man
unterscheidet drei Rollen, die ein ZigBee-Gerät erfüllen kann:

**Endgerät (ZigBee End Device, ZED)**

Geräte wie zum Beispiel Steuerungs- oder Sensormodule werden meist mit
Batterien betrieben. Diese können als ZigBee-Endgeräte implementiert
werden und benötigen nur einen Teil der Funktionen der
ZigBee-Spezifikation. Sie nehmen nicht am Routing im Netzwerk teil und
können in einen Schlafmodus gehen. Sie melden sich an einem Router
ihrer Wahl an und treten so dem ZigBee-Netzwerk bei. Sie können
ausschließlich mit dem Router kommunizieren, über den sie dem Netzwerk
beigetreten sind. Werden Daten an ein solches Endgerät geschickt und
dieses befindet sich im Schlafmodus, speichert der Router diese Pakete,
bis das Endgerät sie abruft.

**Router (ZigBee Router, ZR)**

ZigBee-Router nehmen am Routing der Pakete durch das Netzwerk teil. Sie
benötigen einen größeren Funktionsumfang und damit auch etwas mehr
Hardwareressourcen. ZigBee-Router treten einem Netzwerk bei, indem sie
sich an einem im Netzwerk befindlichen Router anmelden. Das Routing im
Netzwerk erfolgt entweder entlang eines sich so bildenden Baumes
(Stackprofil ZigBee) oder durch dynamisches Routing als Meshnetzwerk
(Stackprofil ZigBee PRO). Tritt ein Funkmodul über einen Router dem
Netzwerk bei, vergibt dieser diesem eine 16-Bit-Kurzadresse (engl. short
address). Bei Meshnetzwerken erfolgt dies zufällig. Auftretende
Adresskonflikte müssen erkannt und dann behoben werden.

**Koordinator (ZigBee coordinator, ZC)**

Ein ZigBee-Koordinator startet das Netzwerk mit festgelegten Parametern.
Nach dem Start übernimmt er dieselben Aufgaben wie ein
ZigBee-Router.\[3\]

# Bluetooth

# Referenzen

<references />

1.  <https://de.wikipedia.org/wiki/Z-Wave>
2.  <https://de.wikipedia.org/wiki/Enocean>
3.  <https://de.wikipedia.org/wiki/ZigBee>