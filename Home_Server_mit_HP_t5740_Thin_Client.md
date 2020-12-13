Hier lernt ihr, wie man einen gebrauchten [Thin
Client](https://de.wikipedia.org/wiki/Thin_Client) zu einem Heimserver
umfunktionieren kann. In dieser Anleitung verwenden wir den HP t5740e,
der auf Ebay gebraucht für unter 20€ zu haben ist. Mit anderen Thin
Clients sollte es jedoch ähnlich funktionieren.

## Was ist ein Thin Client?

Der t5740e ist ein kleiner lüfterloser Computer der meistens als
sogenannter [Thin Client](https://de.wikipedia.org/wiki/Thin_Client)
eingesetzt wird. Bei Thin Clients läuft die gesamte Software auf einem
Server im Rechenzentrum und der Thin Client stellt die Applikationen nur
dar. Meistens wird das [Remote Desktop Protocol
(RDP)](https://de.wikipedia.org/wiki/Remote_Desktop_Protocol) verwendet,
um eine Windows-Oberfläche auf dem Thin Client darzustellen. Diese
Maschinen sind weit verbreitet in Unternehmen, Behörden etc. Am
Schreibtisch des Bearbeiters steht in diesem Falle nur der kleine und
leise Thin Client, während die eigentliche Rechenarbeit zentral im
Rechenzentrum geleistet wird.

Da große Firmen diese Thin Clients immer wieder in großen Chargen
aussondern, sind sie relativ billig auf Ebay zu bekommen. Während sie
neu einige hundert Euro kosten, lassen sie sich auf Ebay teilweise unter
20€ ergattern. Wir wollen dies nutzen, um uns einen billigen
Media-Server aufzubauen.

## Warum kein Raspberry?

Wenn es um die Einrichtung eines Heimservers ging, fiel meine Wahl
bisher immer auf einen Raspberry Pi. Raspberries sind billig, klein,
energiesparend und es gibt unzählige Anleitungen für alle möglichen
Projekte. Allerdings kann man auch an die Grenzen des Raspberry Pi
kommen. So kann man z.B. Festplatten nur über USB anschließen. Außerdem
ist der Arbeitsspeicher mit 1GB (Raspberry 3) relativ begrenzt. Und dann
ist da das grundlegende Problem mit dem Prozessor: weil der Raspberry
einen
[ARM-Cortex-Prozessor](https://de.wikipedia.org/wiki/ARM-Architektur)
besitzt, kann man auf ihm bestimmte Software nicht installieren. So
hatte ich z.B. kürzlich das Problem, dass ich einen Drucker-Treiber
nicht installieren konnte, weil der Hersteller diesen nur für [i386
Prozessor-Architekturen](https://de.wikipedia.org/wiki/Intel_80386)
anbietet. Ausserdem läuft [Wine](http://winehq.org) nicht auf
ARM-Cortex-Prozessoren. Windows-Software unter Wine auf dem Raspberry
zum laufen zu bringen ist daher nicht so einfach möglich.

Für mich war vor allem die RAM-Begrenzung und die Prozessor-Architektur
ausschlaggebend um nach einem anderen energiesparenden und geräuschlosen
Rechner für meinen Heimserver zu suchen. Es gibt da z.B. den [Intel
NUC](https://www.intel.com/content/www/us/en/products/boards-kits/nuc.html)
oder
[Lattepanda](https://www.kickstarter.com/projects/139108638/lattepanda-a-45-win10-computer-for-everything/description).
Die sind mir jedoch beide zu teuer. Zwar gibt es eine Menge andere
Einplatinencomputer, z.B.
[PandaBoard](https://de.wikipedia.org/wiki/PandaBoard),
[ODROID](https://de.wikipedia.org/wiki/ODROID) oder den [Banana
Pi](https://de.wikipedia.org/wiki/Banana_Pi), jedoch haben diese alle
auch einen ARM-Cortex-Prozessor. Im Neuzustand war kein Gerät mit
i368-Prozessor unter 30€ zu haben.

Fündig geworden bin ich auf dem Gebrauchtmarkt bei einer Geräteklasse,
an die ich nicht direkt gedacht hatte. Ausserdem war nicht ganz klar, ob
diese Geräte eine neue Lunix-Installtion zulassen. Anleitungen zu dem
speziellen Gerät waren auch nicht zu finden. Es hieß also auf gut Glück
bestellen und ausprobieren. Erfreulicherweise hat alles reibungslos und
sehr zu meiner Zufriedenheit funktioniert\!

## Die Vorteile des t5740e

  - Es lässt sich problemlos ein beliebiges Linux von USB-Stick
    installieren (keine fehlenden Treiber oder ähnliches).
  - Mit bis zu 4GB Arbeitsspeicher liegt der t5740e weit über dem RAM
    eines Raspberries.
  - Der Intel Atom N280 mit zwei Kernen und 1,66 Taktfrequenz bringt
    vergleichbare Leistungen wie der 4-Kern 1,2Ghz Prozessor im
    Raspberry 3. Beim Internet-Surfen mit Firefox fand ich den t5740
    sogar schneller.
  - Die Prozessor-Architektur ist i386 und damit geeignet für die
    Installation von Programmen, wie sie auf üblichen Laptops laufen.
  - Es gibt 8 USB-Anschlüsse, zwei davon sogar verschlossen im Gehäuse.
  - Es kann eine Festplatte über SATA angeschlossen werden.
  - Das Gehäuse kann modular erweitert werden. Im Anbauteil ist genügend
    Platz für eine Festplatte und mehr (z.B. USB-Geräte, die über die
    versteckten USB-Anschlüsse verkabelt sind).
  - Der t5740e ist gebraucht für unter 20€ zu haben. Nimmt man mehrere
    kann man sie manchmal schon für 10€ kriegen.

## Installation

Im ersten Test habe ich [Lubunt 16.04.1 in der alternate- und
i368-Variante](https://wiki.ubuntuusers.de/Alternate_Installation/)
installiert. Die alternate-Variante ist spezialisiert für alte Hardware
mit wenig RAM. Die Installation von USB-Stick konnte ich problemlos
durchklicken. Der Flash-Speicher war zu klein und ich hatte kein
SATA-Kabel zur Hand. Daher habe ich das Betriebssystem vorerst auf einem
USB-Stick installiert. Die Installation dauerte ewig, das System bootet
jedoch jetzt relativ schnell. Ob die Installation (und das Booten und
Laden von Programmen) auf einer Festplatte schneller geht, bleibt noch
zu testen. Dies sollte eigentlich zu erwarten sein. Um den USB-Stick zu
schonen habe ich den integrierten Flash-Speicher des t5740e als SWAP
deklariert.

## erste Erfahrungen

Das Betriebssystem läuft vergleichbar wie auf einem Raspberry Pi. Man
muss halt manchmal warten, bis etwas zuende gerechnet hat. Im Gegensatz
zum Raspberry Pi konnte ich mir sogar Youtube-Videos anschauen. Der
Prozessor geht natürlich phasenweise ans Maximum, fährt jedoch auch
immer wieder auf 10 bis 20% runter, wenn man gerade nichts kompliziertes
macht. Mein 1GB Arbeitsspeicher wurde beim Web-Surfen nicht nennenswert
ausgelastet.

### Benchmarks

Unter Systemwerkzeuge \> System Profiler and Benchmark lassen sich ein
paar Benchmarks durchführen:

|                |            |
| -------------- | ---------- |
| CPU Blowfish   | 19.76s     |
| CPU CryptoHash | 64.09MiB/s |
| CPU Fibonaci   | 9.48s      |
| CPU N-Queens   | 16.51s     |
| FPU FFT        | 17.15s     |
| FPU Raytracing | 41.63s     |

Weitere Tests werden folgen.

## Handbücher und Anleitungen

  - [Quick Specs Overview](http://www.arp.com/medias/13709300.pdf)

<!-- end list -->

  - [Troubleshooting
    Guide](http://h10032.www1.hp.com/ctg/Manual/c01924799.pdf) mit
    Anleitung zum Auseinandernehmen und Ein- und Ausbau von Hardware

<!-- end list -->

  - [Bios Setup](https://support.hp.com/de-de/document/c03289222)

<!-- end list -->

  - [Offizielle Liste von
    Ersatzteilen](https://support.hp.com/ca-en/document/c03066253)

<!-- end list -->

  - [Sammlung von Handbüchern vom
    Hersteller](https://support.hp.com/in-en/product/hp-t5740-thin-client/3996155/manuals)

<!-- end list -->

  - Gut dokumentierte [Hacks zum
    t5740](http://parkytowers.me.uk/thin/hp/t5740/index.shtml) und
    [anderen Thin
    Clients](http://parkytowers.me.uk/thin/hware/hardware.shtml)

## Hardware-Erweiterungen

### RAM

Es gibt spezielle RAM-Bausteine für den t5740e. Diese kosten jedoch
meist mehr als das ganze Gerät gebraucht. Es lohnt sich also direkt
einen gebrauchten mit maximalem RAM-Ausbau zu kaufen. Allerdings
funktionieren standard DDR3 SODIMM RAM-Bausteine genauso gut. Da RAM in
der Taktfrequenz abwärtskompatibel ist, kann man einen beliebigen
PC3-10600 SODIMM DDR3-RAM mit Frequenz \>667MHz nehmen, z.B. aus einem
alten Laptop. Nach Herstellerangaben wird ist die Maximale Ausbaustufe
4GB (2x 2GB).

### Flash-Speicher

Der Flash-Speicher ist bei manchen Ausführungen mit 1GB sehr klein.
Darauf lassen sich nur bestimmte Linux-Varianten installieren. Einen
Flash-Umbau habe ich bisher noch nicht getestet. Man benötigt einen
[44-pin IDE flash
memory](https://www.ebay.de/sch/i.html?_from=R40&_trksid=p2380057.m570.l1313.TR0.TRC0.H0.X44-pin+IDE+flash+memory.TRS0&_nkw=44-pin+IDE+flash+memory&_sacat=0).
1GB bekommt man ab ca 8€, 2GB oder 4GB gehen schon gegen 20€. Daher
lohnt es sich auch hier eher, direkt einen t5740e mit maximalem
Flash-Speicher von 4GB zu kaufen.

## Bios Update für Windows 7

Wenn man Windows 7 auf dem t7540 installieren möchte, muss man erst das
Bios auf die Version 1.04 updaten. Andernfalls stoppt die Installation
schon ganz am Anfang nach "Windows wird gestartet" mit einem leeren
schwarzen Bildschirm.

Die Datei
[sp55460.exe](http://ftp.hp.com/pub/softpaq/sp55001-55500/sp55460.exe),
die auf der
[HP-Support-Seite](https://support.hp.com/de-de/drivers/selfservice/hp-t5740-thin-client/3996155)
erhältlich ist, enthält das HP Compaq Thin Client Series System BIOS
(786R9 BIOS) 1.04 Rev. D. Die .exe muss man zuerst auf einem beliebigen
Windows-Computer (oder sogar unter Wine auf Linux) ausführen. Alles was
sie macht ist einen Ordner entpacken, in dem das eigentliche Programm
zum installieren des Bios enthalten ist. Diesen muss man dann auf den
Thin-Client kopieren und dort ausführen. Die Readme-Dateien in den
entsprechenden Ordnern erklären das Prozedere. Man soll wohl das
Bios-Update auch unter Linux und unter DOS ausführen können
(entsprechende Ordner mit eigenen Readmes sind enthalten). Bei mir hat
aber beides nicht geklappt. Daher musste ich zuerst Windows XP
installieren, nur um unter XP das Bios-Update zu machen. Anschließend
konnte ich problemlos Windows 7 installieren (natürlich die 32bit
Version).

## Treiber unter Windows

Eine Liste mit Treibern findet sich auf
[driverscape.com](http://www.driverscape.com/manufacturers/hp/laptops-desktops/hp-t5740e-thin-client/35140).
In meinem Falle musste ich nur den [Broadcom NetLink Gigabit Ethernet
Netzwerkadapter](http://www.driverscape.com/files/netcard/Broadcom_win_k57_32-15.6.0.2.zip)
nachinstallieren. Auf [driverpacks.net](http://driverpacks.net/) kann
man sich ganze Verzeichnisse mit Treibern herunterladen, sodass sich
Windows automatisch den richtigen Treiber aussuchen kann.

## Besonderheiten von Windows Embedded

![Hp_t5740_hp_Easy_Tools.png](Hp_t5740_hp_Easy_Tools.png
"Hp_t5740_hp_Easy_Tools.png") Im originalen Windows 7 Embedded für den
t5740 öffnet sich beim Einloggen in den Administratoraccount (Default
Passwort: "Administrator") die [hp Easy
Tools](http://h10032.www1.hp.com/ctg/Manual/c04471750). Mit diesem Tool
können einige Einstellungen gemacht werden (wie z.B. Sprache und
Keyboard Layout) und es kann ein image des ThinClients erstellt werden.
Das Tool begrüßt einen mit der Meldung "Auf diesem Gerät ist ein
Schreibfilter aktiviert. Bevor Sie eine neue Konfiguration übernehmen
können, müssen Sie den Filter erst deaktivieren." Auch wenn man ohne
das hp-Tool etwas dauerhaft installieren möchte, muss man diesen
Schreibfilter deaktivieren. Was ist das für ein Filter? In der
Standard-Einstellung für den ThinClient werden keine Informationen auf
die Festplatte geschrieben. Da die Festplatte keine herkömmliche
Festplatte ist, sondern ein Flash-Modul, würden ständige Schreibvorgänge
die Lebensdauer des Speichers enorm herab setzen (wir haben es hier mit
einer sehr frühen Variante des Flash-Speichers zu tun). Daher erzeugt
der ThinClient eine virtuelle Festplatte im Ram-Speicher. Dort werden
alle Daten, die im laufenden Betrieb erzeugt werden gespeichert. Diese
Daten werden durch einen Neustart gelöscht. Ist der Schreibfilter (EWF
ofder FBW) aktiviert, kann der Benutzer also keine Daten dauerhaft
speichern (und auch keine Konfigurationen oder Installationen). Den
Schreibfilter deaktivieren kann man nur als Administrator und möchte man
irgendetwas dauerhaft installieren oder konfigurieren, muss man den
Schreibfilter deaktvieren.

Im Handbuch ist der Schreibfilter wie folgt beschrieben:

> A write filter protects the contents of and decreases wear on the
> flash drive of a thin client by redirecting and caching writes in an
> overlay. An overlay is a virtual storage space in RAM that tracks
> changes to a protected volume (the flash drive). The user experience
> in Windows is unaffected because the operating system maintains the
> appearance of writing to the flash drive. When a system restart
> occurs, the overlay cache is cleared, and any changes made since the
> last system startup are lost permanently. If it is necessary to make
> permanent system configurations, an administrator can commit (persist
> by writing through to the protected volume) changes stored in the
> overlay cache prior to a system restart.

(Entnommen dem [Handbuch für den hp
t620](http://h10032.www1.hp.com/ctg/Manual/c04945312#WF))

Wie deaktiviert man den Schreibfilter? Wenn man als Administrator
angemeldet ist, kann man auf das Schloss in der Startmenü-Leiste unten
rechts klicken:
![Hp_t5740_Schreibfilter_Icon.png](Hp_t5740_Schreibfilter_Icon.png
"Hp_t5740_Schreibfilter_Icon.png")

Mit einem Rechtsklick öffnet man das Menü zum deaktivieren des
Schreibfilters. Hat man ihn deaktiviert, muss man neu starten.
![Hp_t5740_Disable_Schreibfilter.png](Hp_t5740_Disable_Schreibfilter.png
"Hp_t5740_Disable_Schreibfilter.png")

Aktivieren kann man den Schreibfilter auf die gleiche Weise. Dabei kann
man zwei verschiedene Varianten des Schreibfilters auswählen: Enhanced
Write Filter (EWF) und File-Based Write Filter (FBWF). Im Grunde ist es
egal, welchen von beiden man aktiviert.