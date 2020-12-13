Auf dieser Seite sammeln wir interne Informationen zur Wartung und zu
den Erweiterungen unseres 3D-Druckers. Wer sich informieren möchte, wie
man bei uns im fablab 3D-Drucken kann ist [hier](3D-Druck "wikilink")
besser beraten.

# Firmware

Wir benutzen die [Marlin Firmware](https://github.com/Ultimaker/Marlin).
Da wir einen Dual Extruder angebaut haben und ein beheiztes Druckbett,
muss man die Firmware vor dem Aufspielen anpassen.

Die Firmware ist hier zu kriegen:

<https://github.com/Ultimaker/Marlin>

Wie man die Firmware auf den Ultimaker läd ist
[hier](http://wiki.ultimaker.com/Uploading_customized_Arduino_firmware)
beschrieben.

## Anpassungen

In der Datei `Marlin/Configuration.h` müssen an den entsprechenden
Stellen folgende Änderungen vorgenommen werden:

### Extruder

`#define EXTRUDERS 2`

da wir mit dem Umbau jetzt wieder nur einen Extruder haben muss dies
wieder auf 1 gestellt werden.

### Heizbett

`#define TEMP_SENSOR_BED 1`

### E3D Extruder

Der E3D Extruder hat eine wesentlich höhere Heizleistung, wodurch die
Temperatur beim Aufheizen immer mehr als 10K übergeschwungen ist und
auch später nicht immer stabil gehalten werden konnte. Die Lösung war es
in der Firmware die maximale Heizleistung einzustellen. Diese
Einstellunge habe ich in [diesem
Thread](https://ultimaker.com/en/community/view/4634-pid-autotune?page=3)
gefunden:

`#define PIDTEMP`

`#define BANG_MAX 64 // limits current to nozzle while in bang-bang mode; 255=full current`

`#define PID_MAX 64 // limits current to nozzle while PID is active (see PID_FUNCTIONAL_RANGE below); 255=full current`

`#ifdef PIDTEMP`

`//#define PID_DEBUG // Sends debug data to the serial port.`

`//#define PID_OPENLOOP 1 // Puts PID in open loop. M104/M140 sets the output power from 0 to PID_MAX`

`#define PID_FUNCTIONAL_RANGE 200 // If the temperature difference between the target temperature and the actual temperature`

`// is more then PID_FUNCTIONAL_RANGE then the PID will be shut off and the heater will be set to min/max.`

`#define PID_INTEGRAL_DRIVE_MAX 64 //limit for the integral term`

`#define K1 0.95 //smoothing factor within the PID`

`#define PID_dT ((16.0 * 8.0)/(F_CPU / 64.0 / 256.0)) //sampling period of the temperature routine`

`// If you are using a preconfigured hotend then you can use one of the value sets by uncommenting it`

`// Ultimaker`

`#define DEFAULT_Kp 6.75`

`#define DEFAULT_Ki 0.42`
` `
`#define DEFAULT_Kd 27.80`

Nachdem man diese Änderungen in der Firmware gemacht hat, ist ein PID
autotune möglich (siehe Abschnitt unten).

# PID tuning

PID tuning verbessert die Heizkurve für die Extruderspitze. Mit unserem
neuen E3D Extruder gab es immer einen Fehler beim autotune, weil die
Spitze so schnell heizte, dass sie über 10K über die Zieltemperatur
hinaus schoss. Das konnte nur mit ein paar Einstellungen in der Firmware
behoben werden (siehe Abschnitt oben).

[Hier](http://reprap.org/wiki/PID_Tuning) ist das PID tuning
beschrieben.

`M301`

stellt die aktuellen PID Werte dar.

`M303 S210 C10`

startet PID autotune mit der Zieltemperatur 210°C. Mit dem optionalen
Parameter C kann man einstellen, wie oft die Messung wiederholt werden
soll. Am Ende des Autotunings werden einem Kp, Ki und Kd angezeigt.
Diese Werte kann man mit

`M301 P14 I1.5 D33`

einstellen. Mit

`M500`

speichert man die Werte in den EPROM des Arduino. Ansonsten kann man die
Werte auch in `Configuration.h` der Firmware speichern:

`#define  DEFAULT_Kp 14.10`
`#define  DEFAULT_Ki 1.50`
`#define  DEFAULT_Kd 33.03`

# Anbauten

## OctoPi

Wir haben einen [Raspberry
Pi](http://de.wikipedia.org/wiki/Raspberry_Pi) an den 3D-Drucker
angeschlossen auf dem [OctoPrint](http://octoprint.org) läuft. OctoPrint
liefert ein Web-Interface zum Steuern des Druckers. Durch die angebaute
Kamera kann man den Druck auch überwachen und eine Zeitrafferaufnahme
aufzeichnen. Es gibt ein SD-Karten Image, genannt
[OctoPi](http://octoprint.org/download/), dass alle Funktionalitäten von
OctoPrint auf den Raspberry Pi bringt ohne jeglichen
Installationsaufwand.

## Schaltung Stromzufuhr

Um Strom zu sparen haben wir fernsteuerbare Schalter eingebaut. Mit
diesen kann man erstens eine Lampe einschalten, um auch bei Nacht über
die Kamera etwas sehen zu können. Zweitens kann die Stromzufuhr des
Druckers geschaltet werden. Damit lässt sich nach dem Druck der Drucker
ausschalten, mit der Möglichkeit ihn wieder an zu schalten (der
OctoPrint Server läuft nämlich weiter). Drittens kann man auch den
Drucker inklusive OctoPrint Server ausschalten. Nach diesem
Schaltvorgang muss der Drucker manuell vor Ort wieder angeschaltet
werden.

Realisiert ist das mit drei 433Mhz Fernsteuerbaren Steckdoseneinsätzen,
wie wir sie auch in unserem Kurs zur [Haussteuerung mit dem Raspberry
Pi](Haussteuerung_mit_dem_Raspberry_Pi "wikilink") verwenden. Diese
werden über den GPOI Port des Raspberry und einem 433Mhz Funkmodul
angesprochen. Dazu muss auf dem Raspberry folgendes installiert werden:

[WiringPi](http://wiringpi.com):

`sudo apt-get install git-core`
`git clone `<git://git.drogon.net/wiringPi>
`cd wiringPi`
`./build`

[rcswitch-pi](https://github.com/r10r/rcswitch-pi):

`git clone `<https://github.com/r10r/rcswitch-pi.git>
`cd rcswitch-pi`
`make`

Ist alles richtig installiert, müsste man mit dem Befehl ` ./send
 `<Systemcode>`   `<Gerätecode>`   `<Schaltbefehl> die Steckdosen
schalten können. Z.B. die Steckdose "A" an und wieder ausschalten:

`./send 11111 1 1`
`./send 11111 1 0`

Um die Steuerung in die Oberfläche von OctoPrint zu bringen wurde in die
Datei `~/.octoprint/config.yaml` folgendes im Abschnitt `system`
eingefügt \[1\]:

`noch ausfüllen`

## E3D Extruder

Wir haben den Extruder auf einen E3D V6 umgerüstet. Unserer kam von Ebay
und war eine leicht modifizierte Variante von [diesem
hier](http://e3d-online.com/E3D-v6/Full-Kit?product_id=382). Als
Aufhängung haben wir [dieses
Thing](http://www.thingiverse.com/thing:397518) gedruckt. Die
Lüfterschächte mussten wir alledings modifizieren bzw. durch ein
Schacht aus gebogenem Blech ersetzen, da die gedruckten Schächte an der
Spitze weggeschmolzen sind und ausserdem zu sehr auf den Druckkopf
gerichtet waren. Ausserdem war das Problem, dass die seitlichen Lüfter
an die Läufer an den Stangen rechts und links stoßen. Unsere
Blechvariante hat eine geringere Bauhöhe und kann deshalb unter den
Läufer gleiten. Um wieder den maximal bedruckbaren Bereich zu
erreichen, musste an den Läufern einiges abgefeilt werden und ausserdem
die Endstops verschoben werden (neue Löcher bohren bzw. langlöcher
erweitern), da der neue Extruder nicht mehr so mittig sitzt wie der
originale und deshalb anderswo anstößt.

# Probleme und Lösungen

## Extruder verstopft

**Symptom**: Der Drucker druckt eine Weile gut, dann aber werden die
Bahnen dünner und irgendwann kommt gar nichts mehr. Eventuell tritt das
Problem periodisch auf, die Verstopfung scheint sich wieder zu lösen,
sodass erstmal wieder normal gedruckt wird, ein paar Bahnen weiter tritt
das Problem aber wieder auf.

**Was ist das Problem?** Technisch liegt das Problem darin, dass mehr in
den Extruderkopf hinein gedrückt wird, als aufgeschmolzen an der Spitze
hinaus läuft. Die Aufschmelzrate ist nicht hoch genug, dass das Filament
in der richtigen Zeit flüssig genug ist, um vorne heraus zu fließen. Da
der Input schneller ist als der Output wird das Filament im Extuderkopf
auseinander gedrückt und verklemmt sich. Daraufhin frisst sich der
Vorschub in das Filament.

Das Problem kann auch auftreten, wenn das Filament zwar genügend
aufgeschmolzen wird, die Fließrate aber so hoch gesetzt ist, dass mehr
auf die Druckplatte gedrückt wird als dort Platz ist. Das sieht man
daran, dass die einzelnen Bahnen so stark aneinander stoßen, dass sie
sich an den Kontaktstellen nach oben wölben. In diesem Falle wird auch
der Output blockiert.

**Lösung:** Die Lösung des Problems ist es, den Output zu erhöhen und
den Input zu verringern – und beides so einzustellen, dass genau so viel
heraus fließt, wie hinein geschoben wird.

  - Zuerst sollte man Verunreinigungen, die durch die Verstopfung
    entstanden durch die Cold-Pull Technik entfernen (siehe unten).
  - Um den Output zu erhöhen (das Material wird nicht schnell genug
    flüssig) kann man die Temperatur erhöhen. Diese liegt dann
    eventuell über dem Schmelzpunkt des Materials und würde bei
    langsamem Durchschub Probleme verursachen. Um auf eine entsprechende
    Durchflussgeschwindigkeit und Aufzeizgeschwindigkeit zu kommen kann
    dies aber eine Lösung sein.
  - Den Input kann man verringern indem man während dem Druck am
    Ulticontroller oder in OctoPrint oder aber direkt beim Erzeugen des
    gcodes in Cura den Fluss (Flowrate) verringert (z.B. auf 90 oder
    80%).

Die Strategie wäre erstmal folgendes zu erreichen: Der Input liefert
weniger nach als der Output hergeben könnte. Man könnte also erstmal die
Temperatur erhöhen (sodass das Material leichter herausfließt) und
gleichzeitig den Input über die Flowrate verringern. Wenn man dann
erreicht hat, dass die extrudierten Bahnen lückenhaft sind, (also nicht
direkt aneinander liegen) weiß man genau, dass nun alles heraus fließt,
was der Vorschub in den Extruder hinein schiebt. Dann regelt man die
Flowrate so weit nach, bis die Bahnen wieder geschlossen. Damit hat man
ein perfektes Fließgleichgewicht zwischen Input und Output hergestellt.

**Was man auf keine Fall tun sollte:**

  - Die Flussrate erhöhen, weil ja anscheinend zu wenig heraus kommt.
    Dieser Versuchung muss man tunlichst widerstehen\!
  - Die Temperatur so weit erhöhen, dass das Filament verdampft oder
    dunkel wird
  - Eine hohe Temperatur (über dem Schmelzpunkt) und eine geringe
    Druckgeschwindigkeit zu kombinieren ist auch nicht so gut

## Reste/Verunreinigungen im Extruder

**Das Problem:** Wenn Staubpartikel in den Extruder gelangen können sie
die Düse verstopfen. Probleme hat man auch, wenn der Extruder mal
verstopft war und trotzdem noch eine Weile weiter geheizt wurde (z.B.
weil niemand den Druck beaufsichtigt hat). Dann verkohlt das Filament
und bilded schwarze Ablagerungen. Ein Problem das mit dem neuen
gekühlten E3D Extruder aufgekommen ist, besteht darin dass Filament
beim zurückziehen vom geheizten Bereich in den gekühlten Bereich gezogen
wird und dort an den Wänden erkaltet und hängen bleibt. Das kann beim
Herausziehen/Wechseln des Filaments passieren oder wenn man eine zu
große Retraction für den Druck eingestellt hat. Das erhährtete Filament
an den Extruderwänden kann den Vor- und Rückschub bremsen oder das
Filament sogar komplett festhalten, sodass man es nur noch mit der Zange
aus dem Extruder entfernen kann.

**Lösung:** Verunreinigungen und Reste können aus dem Extruder entfernt
werden mit der Cold-Pull Technik:

  - Man entfernt den Teflonschlauch, indem man die Bowdenkupplung nach
    unten drückt und den Schlauch heraus zieht.
  - Man heizt den Drucker auf Schmelztemperatur und drückt etwas
    Filament durch den Extruder.
  - Dann lässt man den Extruder auf etwa 85°C abkühlen.
  - Ist der Extruder abkekühlt zieht man das Filament (direkt am
    Extruder) mit etwas Gewalt (und vlt. einer Zange) aus dem Extruder.
    Das Filament sollte soweit herabgekühlt sein, dass es ohne zu
    verformen als Ganzes herausgezogen wird.

Hat man Temperatur und Zeitpunkt gut abgepasst, sollte das unverformte
Filament die Innenstruktur des Extruders abbilden, also auch die
Verjüngung an der Spitze. Alle Verunreinigungen, Reste und eventuell
verkohlte Reste von den Wänden sollten dabei mit heraus gezogen werden.
Jodoch sollte man das Ganze einige male wiederholen, bis man sieht, dass
nichts mehr mit heraus kommt.

**Besonders mit unserem neuen E3D Extruder empfiehlt es sich diese
Technik nach jedem Filamentwechsel anzuwenden**, bzw. das Filament
überhaupt erst mit dieser Technik zu entfernen (also nicht im beheizten
Zustand aus dem Extruder zu ziehen).

Ausserdem empfieht es sich diese Technik jedes mal durchzuführen, wenn
der Extruder einmal verstopft war (siehe oben). Verstopfungen lösen sich
i.d.R. nicht von alleine. Reste bleiben immer vorhanden, führen zwar
nicht immer zu weiteren Verstopfungen, aber beeinträchtigen die
Druckqualität.

# Nachweise

<references />

1.  Documentation unter
    <https://github.com/foosel/OctoPrint/wiki/Cookbook:-System-Commands>