Am Lehrstuhl an dem ich arbeite fahren die Kollegen regelmäßig raus, um
Datenlogger auszulesen. Das ist natürlich aufwändig. Ausserdem, wenn man
nur einmal im Monat die Daten abholt, oder einmal die Woche, kann man
schonmal feststellen, dass der Logger oder das Messgerät irgendwann
ausgefallen ist. Im schlimmsten Falle direkt nachdem man das letzte mal
da war. Wenn dadurch Messreihen unterbrochen werden ist das immer
ärgerlich.

Ich frage mich, warum in Zeiten, wo an den meisten Stellen UMTS
verfügbar ist, solche fernübertragenden Datenlogger noch nicht
installiert sind. Selbst nicht am
[Hühnerwasser](http://www.tu-cottbus.de/projekte/de/ecosystem/wassereinzugsgebiet-huehnerwasser.html),
wo haufenweise Messgeräte stehen. Bestimmt liegt das daran, dass
kommerzielle Datenlogger sehr teuer sind. Und dass die meisten nicht
wissen, das es heute billige Minicomputer wie die den [Raspberry
Pi](http://de.wikipedia.org/wiki/Raspberry_Pi) gibt, die prima für so
eine Aufgabe geeignet sind. Und dann muss man sich natürlich ein
bisschen reinfuchsen, wie man aus einem Raspberry Pi einen Datenlogger
mit Fernübertragung macht.

An den Messstellen, die ich kenne, gibt es folgende Vorraussetzungen:

  - Messsignal über serielle Schnittstelle
  - Stromversorgung entweder 220V oder 12V aus Batterie, die mit einem
    Solarpanel aufgeladen wird

# TODO

  - Raspberry Pi mit serieller Schnittstelle ausstatten (entweder über
    USB-Adapter oder über die GPIO-Pins) \[erledigt\]
      - habe ich jetzt mit einem USB-Adapter gemacht

<!-- end list -->

  - Skript zum Ansprechen und auslesen des Messgerätes schreiben, dass
    automatisch gestartet wird, wenn der Raspberry bootet \[50%
    erledigt, mit Fehlern\]
      - Das automatische Starten der Seriellen Verbindung zum Messgerät
        nach Anschluss des USB-Serial-Adapters funktioniert noch nicht
        reibungslos. Das Auslesen brach immer wieder ab. Warum genau ist
        aber noch unklar. Eventuell haben andere USB-Geräte wie der
        UMTS-Stick die Kommunikation gestört, vor allem weil dieser sich
        immer wieder an- und abzumelden scheint. Ich bräuchte vor allem
        mal ein Gerät, mit dem ich das in meinem Büro testen kann.
        Brauche nämlich die Nähe zum Internet, um nach möglichen
        Lösungsansätzen zu suchen ;-)

<!-- end list -->

  - UMTS-Stick installieren \[erledigt\]
      - funktioniert mit
        [sakis3G](https://github.com/trixarian/sakis3g-source) und läuft
        besser als die Vodafone-Software auf meinem Mac.
      - um UMTS-Kosten zu sparen sollte man sich überlegen, bei welcher
        Datenmenge sich der Verbindungsaufbau zur Dropbox lohnt. Es
        werden nämlich eine ganze Menge Daten verschickt, bevor die
        Verbindung überhaupt erstmal besteht. Eventuell wäre z.B. FTP
        auch weniger Datenintensiv.

<!-- end list -->

  - Skript schreiben, dass die IP des Raspberry einem korrespondierenden
    Server bekannt macht (damit man im Notfall den Raspberry ansprechen
    per SSH kann, wenn der sich nicht mehr meldet oder Einstellungen
    vorgenommen werden müssen) \[im Grunde erledigt, aber nicht ganz
    zufriedenstelltend\]
      - Eine wirkliche IP-Adresse gibt es nicht im UMTS-Netz. Lösung war
        jetzt ein [reverse ssh
        tunnel](http://debianforum.de/forum/viewtopic.php?f=32&t=143011).
        Dazu braucht man allerdings wieder einen Server oder Computer,
        der über seine IP frei im Internet erreichbar ist. Also geht
        eine Verbindung direkt ins Uni-Netz leider nicht.
      - Eine gut funktionierende Lösung war, die Daten in eine Dropbox
        hoch zu laden. Das habe ich auch so eingerichtet, dass der Pi in
        der Dropbox nach einem Schell-Script mit einem bestimmten Namen
        schaut in die man den Befehl zum aufbauen des revers tunnel
        schreiben kann. Oder irgend ein anderes Wartungs-Script.

<!-- end list -->

  - Skript schreiben, dass alle paar Minuten oder Stunden die Daten
    verschickt (Cron-Job) \[erledigt\]
      - Daten werden gezippt und unter dem Datum gespeichert. Dann wird
        die Zip in die Dropbox hochgeladen und nach erfolgreichem
        hochladen gelöscht. Wenn die Dropbox-Verbindung nicht aufgebaut
        werden kann, sammeln die Zip-Dateien sich im Ordner an und
        können z.B. über USB abgeholt werden. Wenn die
        Dropbox-Verbindung das nächste mal erfolgreich ist, werden alle
        Zip-Dateien im Ordner hochgeladen (auch die, die das letzte mal
        nicht geladen werden konnten).
      - Eventuell lieber Owncloud oder FTP auf dem fablab-Server
        benutzen. Dann müssen die Daten nicht nach Amerika geschickt
        werden ;-)

<!-- end list -->

  - Routine für das Auslesen per USB schreiben (automatischer Datensync,
    wenn USB-Stick angeschlossen wird) \[erledigt\]
      - udev-Regel reagiert, wenn der USB-Stick angeschlossen wird und
        startet ein Skript zum Kopieren. Die udev-Regel kann auch nur
        auf einen bestimmten USB-Stick eingestellt werden (über dessen
        Seriennummer).
      - Auch auf den Stick kann ein Shell-Script gelegt werden, dass
        beim Anschluss des USB-Sticks ausgeführt wird.
      - Beim Anschluss des USB-Sticks werden bisher nicht die Daten vom
        Datenlogger gelöscht, da man nicht weiß, ob der USB-Stick nicht
        unterwegs verloren gehen könnte. Das Löschen der Dateien könnte
        man dann in das Shell-Script schreiben, sodass die erfolgreich
        Übertragenen Daten beim nächsten Abholen gelöscht werden.

<!-- end list -->

  - 12V-Stromversorgung (Eventuell über Autonetzteil) \[0% erledigt\]

Der Datenlogger sollte eine hohe Redundanz haben, damit ja keine Daten
verloren gehen.

  - Mehre Auslesewege (UMTS, USB-Stick, Auslesung mit Laptop über LAN)
  - keine Daten löschen, bevor nicht bestätigt wurde, dass sie
    ausgelesen wurden und sicher irgendwo angekommen sind

Dann sollte der Datenlogger automatisch Warnungen verschicken, wenn die
Batteriespannung zu gering, der Datenspeicher voll ist oder das
Messgerät nicht mehr arbeitet.

Man muss sich natürlich auch noch Gedanken machen, wie man den Raspberry
wetterfest macht. Manchmal könnte man ihn in bestehende Kästen
integrieren, manchmal bräuchte man aber auch ein Gehäuse wie z.B.
[dieses
hier](https://www.kickstarter.com/projects/1821240043/pice-the-ultimate-case-for-your-raspberry-pi-and-c).

# Was bringt das dem fablab?

  - Ein tolles Bastelprojekt
  - Ein Vorzeigeprojekt
  - Eine erste Bastelanleitung, die wir in unserem Wiki veröffentlichen
    können
  - Ein Ergebnis, dass einige Lehrstühle hier an der Uni gut gebrauchen
    können
  - Deswegen auch wahrscheinlich Unterstützung bzw. Spenden von
    entsprechenden Lehrstühlen
  - Ein Ergebnis, dass vielleicht auch woanders Interessenten findet
  - Folgeprojekte?

# Diskussion

# Übersicht momentane Lösung

In seinem jetzigen Stand erledigt der Raspberry als Datenlogger drei
Aufgaben:

1.  Kommunikation mit dem Messgerät herstellen und Daten loggen
2.  Bei Anschluss eines USB-Stick Daten auf Stick kopieren
3.  Wenn ein Internet-Stick angeschlossen ist Internetverbindung
    herstellen und Dropbox-upload

Hier ein Überblick über die Herausforderungen und die gefundenen
Lösungen:

  - USB-Geräte erkennen und entsprechende Skripte starten → Lösung:
    [UDEV-Regeln](http://wiki.ubuntuusers.de/udev)
  - Serielle Kommunikation zum Messgerät herstellen →
    [`stty`](http://unixhelp.ed.ac.uk/CGI/man-cgi?stty),
    Kommunikationseinstellungen spezifisch für jedes Gerät
  - Messgerät konfigurieren (vor allem Uhrzeit stellen) → [`echo``
     ``-e`](http://unixhelp.ed.ac.uk/CGI/man-cgi?echo) (`-e` to enable
    interpretation of backslash escapes), Befehle nach Handbuch
  - Eingehende Daten in Datei umleiten →
    [`cat`](http://unixhelp.ed.ac.uk/CGI/man-cgi?cat)`
    /dev/USB-Serial-Port >> Datei.txt `

# Erläuterung der momentanen Lösung

Um zu verstehen was der Datenlogger macht und wie man die Skripte
anpassen kann, muss man sich vor allem in drei Themenfelder einarbeiten:

1.  Grundsätzlich: wie schreibt man Shell-Skripte?
2.  Wie schreibt man UDEV-Regeln?
3.  Wie kann man aus der Shell über die serielle Schnittstelle (RS-232)
    mit einem Gerät kommunizieren?

Zum Schreiben von UDEV-Regeln gibt es unter
[hier](http://wiki.ubuntuusers.de/udev) eine schöne Anleitung. Über die
Serielle Schnittstelle hat [hier](http://papers.mpastell.com/serial.pdf)
jemand eine kurze und gut verständliche Anleitung zusammen gestellt.

Zum Aufbau eines Shell-Skriptes sollte man folgendes wissen:

Die erste Zeile des Skripts muss lauten:

` #!/bin/bash`

Diese sogenannte [Shebang-Zeile](https://de.wikipedia.org/wiki/Shebang)
macht das Shell-Skript überhaupt erst als solches erkennbar.

Da die Skripte später nicht mehr vom User direkt, sondern von den
UDEV-Regeln oder Cron-Jobs aufgerufen werden sollen, lohnt sich die
Umleitung aller Meldungen in eine Log-Datei. Dies wird am besten direkt
in den nächten beiden Zeilen veranlasst:

`logfile=/home/pi/logs/usb-serial-log.log &&`
`exec >> $logfile 2>&1`

Nun werden Fehlermeldungen in die definierte Datei geschrieben.
Ausserdem kann man mit `echo` Kommentare über den (reibungslosen) Ablauf
des Skripts in die Log-Datei schreiben. So zum Beispiel:

`echo -e Connecting to parsivel distrometer $(date +"%F %X")`

Alles was normalerweise an den User ausgegeben wird, wird nun in die
Log-Datei geschrieben.

Kommandozeilen in Shell-Skripten sind grundsätzlich wie folgt aufgebaut:
Das erste Wort ist der Befehl, gefolgt von den Optionen, die meist mit
-e beginnen. Der Befehl `cat` kann zum Beispiel den Inhalt einer Datei
anzeigen:

`cat -n MeinText.txt`

Die Option `-n` sorgt dabei dafür, dass eine Zeilennummerierung
dargestellt wird.

Das Ergebnis eines Befehls kann mit `>` umgeleitet werden. Zum Beispiel
in eine Datei:

`cat alte_Datei.txt > neue_Datei.txt`

Da die Kommunikation, die von der seriellen Schnittstelle kommt genauso
zu handhaben ist wie eine Datei, können wir mit:

`cat /dev/USB-Serial-Port >> /home/pi/Documents/Loggerdaten/Loggerdaten.txt`

einkommende Daten in eine Datei schreiben. `>>` statt `>` sorgt dabei
dafür, dass neue Daten an die Datei angehängt werden und nicht ihren
Inhalt ersetzen.

Um diesen Befehl im Hintergrund laufen zu lassen fügt man `&` an den
Befehl an:

`cat /dev/USB-Serial-Port >> /home/pi/Documents/Loggerdaten/Loggerdaten.txt &`

Verwendet man als nächste Zeile

`MeineProzessNR=$!`

hat man die Prozessnummer (PID) in einer Variablen gespeichert, um
später mit

`kill $MeineProzessNR`

den Prozess wieder beenden zu können. Die PID kann man natürlich auch in
eine Datei schreiben, um den Prozess mit einem anderen Skript wieder
beenden zu können.

Für gewöhnlich bauen die Kommandos eines Skriptes aufeinander auf. Das
heißt das die nächste Kommandozeile das erfolgreiche abarbeiten der
vorangehenden Kommandozeile voraussetzt. Um zu vermeiden, dass die
nächste Zeile (bzw. der ganze Rest des Skriptes) ausgeführt wird, wenn
ein Teil davon nicht funktioniert, muss jedes Kommando von einem `&&`
gefolgt werden. `&&` sorgt dafür, dass das Skript nur fortgesetzt wird,
wenn das davorstehende Kommando `0` zurück gibt. Jede andere Rückgabe
bedeutet einen Fehler. Systemkommandos sind alle so eingestellt, dass
sie `0` zurück geben, wenn sie erfolgreich ausgeführt wurden und
ansonsten einen Fehlercode übergeben. In eigenen Skripts kann man das
genauso umsetzen. Mit

`exit 0`

beendet man sein Skript und signalisiert, dass die Ausführung
erfolgreich war. Somit würde ein ganz simples Skript also so aussehen:

`#!/bin/bash`
`cat TestDatei.txt &&`
`echo Hallo Welt &&`
`exit 0`

Wenn Zeile zwei nicht ausgeführt werden kann (z.B. weil die Datei
TestDatei.txt nicht vorhanden ist), wird auch der Rest des Skripts nicht
ausgeführt. Da auch `exit 0` nicht ausgeführt wird, ist klar, dass das
Skript nicht erfolgreich bis zu Ende ausgeführt wurde.

Dabei muss man beachten, dass das Starten von Hintergrundprozessen das
nacheinander abarbeiten der Kommandos mit `&&` unterbricht und zu
unvorhergesehenen Ergebnissen führt. Das Ausführen von:

`echo eins && `
`sleep 5 && echo zwei & `
`echo drei && `
`echo vier`

zum Beispiel führt zu der Ausgabe:

`drei`
`vier`
`eins`
`zwei`

Abhilfe schafft hier Klammersetzung:

`echo eins &&`
`(sleep 5 && echo zwei &)`
`echo drei &&`
`echo vier`

Hier kann man die Prozessnummer wie folgt speichern:

`echo eins &&`
`pid=$(sleep 5 && echo zwei & echo $!)`
`echo drei &&`
`echo vier`

Auf diese Weise wurde z.B. folgende Zeile im Skript `usb-serial.sh`
umgesetzt:

`pid=$( cat /dev/USB-Serial-Port >> $logfile & echo $! )`

# Verwendete Skripte

## Installation

  - [sakis3G](https://github.com/trixarian/sakis3g-source) herunterladen
    und kompilieren.
  - [Dropbox Sync
    installieren](http://raspi.tv/2013/how-to-use-dropbox-with-raspberry-pi)

` # make dropbox available systemwide:`
` sudo ln -s /home/pi/Scripts/Dropbox-Uploader/dropbox_uploader.sh /usr/bin/dropbox`
` # same for sakis3g`
` sudo ln -s /home/pi/Scripts/sakis3g /usr/bin/sakis3g`

Die UDEV-Regeln müssen als Datei in `/etc/udev/rules.d` angelegt werden.
Man kann alle Regeln in eine Datei legen. Eventuell macht man auch einen
Symlink in den Ordner wo man alle Skripte zentral zu liegen hat.

## online upload

### UDEV-Regel beim Anschluss des USB-Modems:

Einfach nur, um dem Gerät einen immer gleichen Namen zu geben:

` ATTRS{idProduct}=="1003", ATTRS{idVendor}=="12d1", ATTRS{bInterfaceNumber}=="00", ACTION=="add", SYMLINK+="umts0"`

Um die Verbindung aufzubauen, sobald das Modem vollständig erkannt ist:

` #ATTRS{idVendor}=="Huawei Technologies Co., Ltd.", ATTRS{idProduct}=="E220 HSDPA Modem / E230/E270/E870 HSDPA/HSUPA Modem"`
` #ATTRS{bInterfaceNumber}=="01",`
` #KERNEL=="ttyUSB?", SUBSYSTEMS=="usb", ATTRS{idProduct}=="1003", ATTRS{bInterfaceNumber}=="01", ACTION=="add", RUN+="/home/pi/test.sh"`
` `
` KERNEL=="ttyUSB*", SUBSYSTEM=="tty", ATTRS{bInterfaceNumber}=="01", ACTION=="add", RUN+="/home/pi/Scripts/3Gconnect.sh"`
` `
` #, ATTRS{idProduct}=="1003", ATTRS{idVendor}=="12d1",`

### 3Gconnect.sh

Aufbau der 3G-Verbindung

` #!/bin/bash`
` `
` logfile=/home/pi/logs/3Gconnect_$$.log`
` exec > $logfile 2>&1`
` #sleep 10s`
` sudo sakis3g SIM_PIN=`<vierstelligePIN>` APN=internet.eplus.de connect`

### cron-job zum starten des Dropbox Sync

`crontab -e` zum editieren der cron-jobs. Folgende Zeilen einfügen:

` 0 7-20   * * *   /home/pi/Scripts/cron-dropbox-sync.sh`
` @reboot  /home/pi/Scripts/cron-dropbox-sync.sh`

### cron-dropbox-sync.sh

Synchronisiert mit der Dropbox

`#!/bin/bash`

`logfile=/home/pi/logs/crontab-dropbox-sync_$$.log`
`exec > $logfile 2>&1 `

`cd /home/pi/Documents/Loggerdaten/ && `

`timestamp=$(date +%Y_%m_%d-%H_%M_%S) &&`

`timestamp >> $logfile`

`file=Loggerdaten_$timestamp.txt`

`cp Loggerdaten.txt $file &&`

`echo Fortsetzung der Messung $(date +"%F %T %Z") > Loggerdaten.txt &&`

`gzip --best $file &&`

`sudo sakis3g SIM_PIN=1328 APN=internet.eplus.de connect`

`/home/pi/Dropbox-Uploader/dropbox_uploader.sh upload Loggerdaten_*.gz Loggerdaten/ &&`

`rm Loggerdaten_*`

`/home/pi/Scripts/cron-dropbox-execute.sh`

`sudo sakis3g disconnect`

### cron-dropbox-execute.sh

Führt das Shell-Script aus, dass von der dropbox geladen wurde

` #!/bin/bash`
` cd /home/pi/executeScript &&`
` `
` /home/pi/Dropbox-Uploader/dropbox_uploader.sh download executeScript/execute.sh ../ &&`
` `
` chmod +x execute.sh &&`
` `
` ./execute.sh &&`
` `
` /home/pi/Dropbox-Uploader/dropbox_uploader.sh delete executeScript/execute.sh`
` `
` /home/pi/Dropbox-Uploader/dropbox_uploader.sh upload * executionLog/ &&`
` `
` rm *`

### execute.sh

Wenn man `execute.sh` in den Ornder "executeScript" in der Dorpbox legt,
wird das Shell-Skript beim Dropbox-Sync ausgeführt und daraufhin in den
Ordner "executionLog" gelegt, zusammen mit dem Log-File der execution.

Die folgende Datei ruft Beispielhaft einen reverse ssh tunnel auf, um
den Raspberry live steuern zu können. Der reverse tunnel öffnet den Port
2222 auf dem Server und leitet eine eingehende ssh-Verbindung an den Pi
weiter. Die Verbindung mit dem Raspberry stellt man also her mit ` ssh
 `<benutzer>`@`<serverIP>`:2222`. Arbeitet man auf dem Server can
"localhost" anstatt der IP verwendet werden.

` #!/bin/bash`
` `
` exec 1>> log.txt 2>&1`
` echo $(date)`
` `
` #-f would be for background`
` ssh -v -N -R 2222:localhost:22 `<benutzer>`@`<ServerIP>` &`
` sshPID=$!`
` # hold the connection open for some time, then close`
` sleep 900`
` kill $sshPID`

## USB download

### UDEV-Regel:

Eventuell kann hier die Seriennummer auch weggelassen werden, wenn man
mit jedem beliebigen USB-Stick zugreifen möchte

`ATTRS{idVendor}=="0951", ATTRS{idProduct}=="1643", ATTRS{serial}=="`<Seriennummer>`", ACTION=="add", MODE="0755", GROUP="plugdev", OWNER="pi", SUBSYSTEMS=="usb", SYMLINK+="commandstick", RUN+="/home/pi/Scripts/mountCommandStick.sh"`
`ENV{DEVLINKS}=="/dev/commandstick", ACTION=="remove", RUN+="/home/pi/Scripts/unmount.sh"`

### mountCommandStick.sh

Mountet den Commandstick

`#!/bin/bash`
`mkdir /media/commandstick`
`mount -o uid=pi,gid=plugdev /dev/commandstick /media/commandstick`

`/media/commandstick/command.sh`

### command.sh

Kommandodatei auf dem Stick:

`#!/bin/bash`

`logfile=/media/commandstick/logs/rsync.log`
`exec >> $logfile 2>&1`

`cd /home/pi/Documents/Loggerdaten/ &&`

`timestamp=$(date +%Y_%m_%d-%H_%M_%S) &&`

`echo -e "\nProtokoll Auslesung" $timestamp "\n"`
`df #to write free diskspace to log file`
`echo " "`

`#file=Loggerdaten_$timestamp.txt`
`#cp Loggerdaten.txt $file &&`
`#echo Fortsetzung der Messung $(date +"%F %T %Z") > Loggerdaten.txt && `


`# Datein auf den Stick kopieren:`
`rsync -r /home/pi/Documents/Loggerdaten/ /media/commandstick/Loggerdaten/ -v`

`# logs auf den Stick kopieren:`
`rsync -r /home/pi/logs/* /media/commandstick/logs/ -v`


`# diese Zeile auskommentiren um dei Daten auf dem Logger zu löschen:`
`#rm /home/pi/Documents/Loggerdaten/Loggerdaten.txt`

### unmount.sh

Unmountet den Commandstick

`#!/bin/bash`
`logfile=/home/pi/logs/unmount_$$.log`
`exec >> $logfile 2>&1`
`umount /media/commandstick`
`rm -r /media/commandstick`

## Serielle Kommunikation

Viele Messgeräte besitzen eine serielle Schnittstelle (z.B. [HeliosMini
Wetterstation/Datenlogger](HeliosMini_Wetterstation/Datenlogger "wikilink")).
In diesem Aufbau wird ein USB zu Seriell Adapter verwendet, um die
Kommunikation herzustellen. Wenn dieser angeschlossen wird, wird eine
UDEV-Regel aktiviert:

### UDEV-Regel:

`# this contains the rules to execute serial comminication with the Parsivel`
`ATTRS{idVendor}=="067b", SUBSYSTEMS=="usb", ATTRS{manufacturer}=="Prolific Technology Inc.", ATTRS{product}=="USB-Serial Controller", ACTION=="add", SYMLINK+="USB-Serial-Port", RUN+="/home/pi/Scripts/usb-serial.sh"`
` `
`ENV{DEVLINKS}=="/dev/USB-Serial-Port", ACTION=="remove", RUN+="/home/pi/Scripts/usb-serial-remove.sh"`

`#ATTRS{serial}=="Prolific_Technology_Inc._USB-Serial_Controller"`

### usb-serial.sh

Macht eine Pipe vom Seriellen Anschluss in die Datei "Loggerdaten.txt".

`#!/bin/bash`

`logfile=/home/pi/logs/usb-serial-log.log &&`
`exec >> $logfile 2>&1`
`echo -e "\nConnecting to parsivel distrometer" $(date +"%F %X") &&`
`#sudo -u pi touch /home/pi/Documents/Loggerdaten/Loggerdaten.txt`

`#for the HeliosMini`
`#stty -F /dev/USB-Serial-Port speed 9600 &&`

`#for Parsivel:`
``#while ! `tty -s`; do sleep 3; done``
`#sleep 120 # necessary to run properly at system start`
`#stty -F /dev/USB-Serial-Port speed 19200 &&`
`# repeated because the first time doesnt work on boot (don't know why)`

`stty -F /dev/USB-Serial-Port speed 19200 raw &&`
`stty -F /dev/USB-Serial-Port -inlcr -icrnl -imaxbel -opost onlcr -isig -icanon -echo &&`

`# Return von Parsivel in logdatei schreiben`
`pid=$( cat /dev/USB-Serial-Port >> $logfile &`
`echo $! ) &&`
`sleep 1 &&`
`#echo $pid &&`

`# turn sdi-12 mode off:`
`echo turn sdi-12 mode off &&`
`echo -e "CS/S/E/0\r" > /dev/USB-Serial-Port &&`
`sleep 1 &&`

`# turn poll mode on for settings:`
`echo "turn poll mode on for settings" &&`
`echo -e "CS/I/0\r" > /dev/USB-Serial-Port &&`
`sleep 3 &&`

`# set time of parsivel:`
`#sudo hwclock -s &&`
`#echo $(TZ="UTC-1" date +"%H:%M:%S") > /home/pi/testlog.txt &&`
`echo "set date to $(date +%d.%m.%Y)" &&`
`echo -e "CS/D/$(date +%d.%m.%Y)\r" > /dev/USB-Serial-Port &&`
`sleep 3 &&`
`echo "set time to $(TZ=UTC-1 date +%H:%M:%S)" &&`
`echo -e "CS/T/$(TZ=UTC-1 date +%H:%M:%S)\r" > /dev/USB-Serial-Port &&`
`sleep 1 &&`

`# Anwendertelegramm anschalten:`
`echo "switch to user data telegram" &&`
`echo -e "CS/M/M/1\r" > /dev/USB-Serial-Port &&`
`sleep 1 &&`

`# Datentelegramm festlegen:`
`echo "define data telegram" &&`
`echo -e "CS/M/S/\r" > /dev/USB-Serial-Port &&`
`sleep 1 &&`
`echo -e "%21;%20;%01;%02;%11;%10;%12;%17;%03;%04;%05;%06;%07;%09;%08;%18;%90;%91;%93;/n\r" > /dev/USB-Serial-Port &&`
`sleep 1 &&`

`# Messintervall auf 60 Sekunden:`
`echo "set sample interval" &&`
`echo -e "CS/I/60\r" > /dev/USB-Serial-Port &&`
`sleep 1 &&`
`# Return nicht mehr in logdatei schreiben`
`kill $pid &&`

`# Daten in Datei speichern`
`(`
`cat /dev/USB-Serial-Port >> /home/pi/Documents/Loggerdaten/Loggerdaten.txt &`
`logging=$! &&`
`echo "started logging with PID $logging"`
`) &&`
`exit 0`

### usb-serial-remove.sh

Wird aufgerufen beim abziehen des Seriellen Adapters. Garantiert, dass
beim nächsten Anstecken die Verbindung wieder hergestellt werden kann

`#!/bin/bash`
`echo -e "\nserial connector removed" $(date +"%F %X") >> /home/pi/logs/usb-serial-log.log &&`
`pkill cat &&`
`exit 0`

## Real Time Clock

Damit der Raspberry auch ohne Internet-Verbindung die richtige Zeit
behält, ist eine Real Time Cloc (RTC) notwendig, die man auf einem
kleinen Chip kaufen kann, der auf die GPIO-Pins des Raspberrys
aufgesteckt wird. Ich hab
[diese](http://www.ebay.de/itm/331215053208?_trksid=p2059210.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT)
gekauft.
[Hier](http://nicegear.co.nz/blog/using-an-i2c-real-time-clock-rtc-with-a-raspberry-pi/)
habe ich eine Anleitung gefunden, um den Raspberry auf die RTC
einzustellen. Konkret habe ich verwendet:

`# Remove the module blacklist entry so it can be loaded on boot`
`sudo sed -i 's/blacklist i2c-bcm2708/#blacklist i2c-bcm2708/' /etc/modprobe.d/raspi-blacklist.conf`
`# Load the module now`
`sudo modprobe i2c-bcm2708`
`# Notify Linux of the Dallas RTC device`
`echo ds1307 0x68 | sudo tee /sys/class/i2c-adapter/i2c-1/new_device`
`# Test whether Linux can see our RTC module.`
`sudo hwclock`

Eine neue Real-Time-Clock muss man wahrscheinlich erstmal auf die
richtige Uhrzeit einstellen. Dazu am besten den Raspberry einmal mit
Internetverbindung booten, damit er sich die Zeit aus dem Internet holt.
Dann mit folgendem Befehl die RTC einstellen:

`sudo hwclock -w`

Nun muss noch eingestellt werden, dass beim nächsten Booten die
Systemzeit von der RTC geholt wird:

`# Add the RTC device on boot`
`sudo sed -i 's#^exit 0$#echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device#' /etc/rc.local`
`echo "sudo hwclock -s" | sudo tee -a /etc/rc.local`
`echo exit 0 | sudo tee -a /etc/rc.local`