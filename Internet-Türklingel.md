Eine "Türklingel", mit der man von unserer Internetseite aus anfragen
kann, ob grad jemand im fablab ist. Also quasi ein Raspberry oder
Arduino mit nem Lautsprecher oder Klingel dran und dann ein paar Knöpfe
"bin noch ne halbe Stunde da" oder "noch drei Stunden". Dann auf der
Internetseite ein Knopf, der die Klingel aktiviert und auf Antwort von
einem Knopfdruck wartet. Vielleicht kann man auch einen Drehknopf mit
variable Zeiteinstellung machen, der dann wie bei einer Eieruhr zurück
läuft. Da könnte man z.B. einen motorisierten Poti nehmen. Oder
tatsächlich eine Eieruhr und müsste dann irgendeinen Abgreifer bauen.

# Informationen

  - <http://arduino.cc/en/Tutorial/Bridge> → Arduino Yun über
    HTTP-Requests steuern

# Diskussion

  -
    Dazu ein paar Ideen/Vorschläge. Da die Anzahl der Schlüsselbesitzer
    begrenzt ist, einfach ein Touchscreen (z.B. den 2.x" von Watterott)
    draufgesteckt und für jeden "Aufseher" eine Schaltfläche an/aus.
    Nützlich wäre auch, wenn man angeben könnte, bis wann garantiert
    jemand da ist. Dann weiss man, ob es sich zeitlich auch lohnt, zum
    Werkeln hinzufahren. Habe eine kleine Touchscreen-Oberfläche, wenig
    RAM-fressend für Arduino geschrieben, könnte die ggfs.
    beisteuern.[Stefan B.](Benutzer:Stefan_B. "wikilink")
    ([Diskussion](Benutzer_Diskussion:Stefan_B. "wikilink")) 21:41, 31.
    Jul. 2014 (CEST)
      -
        Ich hab mir einen Touchscreen aus Hongkong schicken lassen. Hab
        den aber noch nicht sauber zum laufen gebracht. Der Support vom
        Hersteller ist quasi nichtexistent. Dafür gibts ne Menge Leute,
        die sich auch schon damit rumgeärgert haben. Aber die Boards
        scheinen sich auch von Zeit zu Zeit zu ändern, sodass immer
        wieder neue Probleme auftauchen. Vielleicht ist es besser einen
        gut dokumentierten zu kaufen. Aber wenn du Zeit und Lust hast
        dich mit meinem zu beschäftigen - gerne\!
        [Nanu](Benutzer:Nanu "wikilink") 11:56, 3. Aug. 2014 (CEST)
        Ich hatte mir eigentlich vorgestellt mal ein Gerät ohne
        Touchscreen zu bauen. Die gibt es ja mittlerweile überall und
        ich persönlich würde mich über ein haptisches Gerät freuen, mit
        einem etwas ausgefallenen vielleicht auch witzig umgesetzten
        Bedienkonzept. Aber von mir aus können wir es auch effizient,
        unkünstlerisch und mit bewährten Methoden umsetzen. Dann wird es
        wahrscheinlich auch schneller fertig.
        [Nanu](Benutzer:Nanu "wikilink") 11:56, 3. Aug. 2014 (CEST)
        Vielleicht könnte man das Ganze auch kombinieren mit einem
        Kartenleser zur Dokumentation der Werkstattnutzung. Dann muss
        man keine Papierliste führen, sondern zieht einfach beim kommen
        und gehen seine Karte durch. Ein Einstelldialog wie lange man
        dableiben wird und ob man bereit ist anderen Instruktionen zu
        geben oder nur für in Eigenregie arbeitende öffnen möchte wäre
        aber trotzdem nötig. [Nanu](Benutzer:Nanu "wikilink") 11:56, 3.
        Aug. 2014 (CEST)
        Ein paar weitere ungeordnete Gedanken dazu: Ein solches Gerät
        wäre täglich benutzter Teil der Kerninfrastruktur für das
        Projekt. Im Zweifelsfalle also lieber militärisch robust, so
        einfach, ergonomisch, zeitsparend und idiotensicher wie möglich
        zu benutzen. Leicht anpassbar an wechselnde
        Bedürfnisse/Gegebenheiten. Fragt sich allerdings, ob sinnvoll
        ist, wenn auch diejenigen, die nicht
        "Schlüsselinhaber+Betreuer+Aufseher" sind, einer
        "Stempelkartenpflicht" unterliegen sollen oder ob es weniger
        bürokratisch-intrusive Wege gibt, die Werkstattauslastung zu
        messen. Ein Argument für die Registrierung der Werkstattnutzung
        wäre jedenfalls, dass man so auch im Web anzeigen könnte, welche
        Infrastruktur "besetzt" und welche "frei" ist. Das wäre auch
        sehr nützlich, um Enttäuschungen zu vermeiden, wenn zwar offen
        ist, aber man trotzdem nichts machen kann, weil die jeweilige
        Infrastruktur gerade in Benutzung ist. Wichtiger ist ja derzeit
        eher, dass das Fablab mittelfristig möglichst lange
        Öffnungszeiten etabliert, um attraktiver zu werden. Da könnte
        man z.B. gut eine Dokumentation der "Betreuungszeiten"
        gebrauchen, um z.B. freiwillige Betreuer/Aufseher zu belohnen
        oder anderweitig zu motivieren. Im Auge behalten sollte man
        auch, dass als gemeinnütziger Verein prinzipiell die Möglichkeit
        besteht, sich vom Jobcenter "bezahlte Aufseher" stellen zu
        lassen, um ohne allzugrosse Belastung der "Freiwilligen"
        attraktive Öffnungszeiten anbieten zu können. Dafür wäre ein
        solches Registrierungssystem Voraussetzung. Ein ausgebautes
        derartiges System wäre z.B. auch hilfreich, um
        Werkstattplätze/Infrastruktur im Voraus reservieren zu können,
        da sonst Projekte im Fablab zeitlich nicht sicher planbar
        wären.[Stefan B.](Benutzer:Stefan_B. "wikilink")
        ([Diskussion](Benutzer_Diskussion:Stefan_B. "wikilink")) 13:38,
        3. Aug. 2014 (CEST)
        Bei der letzten Besprechung wurde gesagt, dass wir für die
        Versicherung aufschreiben müssen, wer wann in der Werkstatt war.
        [Nanu](Benutzer:Nanu "wikilink") 14:38, 3. Aug. 2014 (CEST)
        Mmh, das habe ich gar nicht mitbekommen. Müsste man also sofort
        als Behelfslösung (und als Fallback, falls die
        "Internet-Türklingel" mal ausfällt) Papierformulare zum
        Selbsteintragen erstellen und am Werkstatteingang anbringen
        (Klammerbrett?). In etwa wie Unterschriftenliste, mit Spalten
        für Name, Beginn und Ende des Werkstattaufenthalts und was wir
        sonst noch lt. Vereinbarung mit der Versicherung
        mitprotokollieren müssen. Das wäre jedenfalls in die Kategorie
        "To-Do-Dringend" einzuordnen. Ähnlich wie "Müll wegbringen",
        "Monitorwandprojekt-Überreste auslagern/entsorgen",
        "Inventurliste erstellen (Geräte, Seriennummern), erstmal per
        Hand" und solche Dinge. Vielleicht wäre eine Wiki-Seite
        "Dringend/Eilt" einzuführen sinnvoll? [Stefan
        B.](Benutzer:Stefan_B. "wikilink")
        ([Diskussion](Benutzer_Diskussion:Stefan_B. "wikilink")) 15:21,
        3. Aug. 2014 (CEST)
        Wenn die Versicherung das vorschreibt, kommen wir ja gar nicht
        darum herum, einen Anwesenheitslogger zu bauen. Die Geburt der
        "FabLab Card"? Oder gibts sowas schon als fertige Lösung? Wenn
        nicht, wär das n Ding, das gut in die "c't Hacks" passen würde.
        Weil, andere Fablabs werden bestimmt ähnliche
        Versicherungsbedingungen haben und sowas gebrauchen können.
        Werbung und Reputation fürs FablabCB wäre ein Gewinn. Klasse
        Idee, je mehr man über diese "Internet-Türklingel" nachdenkt.
        Vielleicht statt mit Karte eben mit 433-MHz Dongle am
        Schlüsselbund? Dann könnte ggf. auch die Bedienung eines
        Kartengeräts entfallen. Man muss sich ja nicht wie ein
        Fabrikarbeiter fühlen :) [Stefan
        B.](Benutzer:Stefan_B. "wikilink")
        ([Diskussion](Benutzer_Diskussion:Stefan_B. "wikilink")) 15:37,
        3. Aug. 2014 (CEST)
        Da würde ich eher 13.56Mhz RFID NFC (Near Field Communication)
        benutzen. Da gibts
        [Schlüsselanghänger](http://www.gearbest.com/development-boards/pp_50129.html)
        oder
        [Aufkleber](http://www.gearbest.com/development-boards/pp_63972.html)
        und manche Handys können das auch. Oder man registriert das
        Bluetooth Signal der Handys. Hilft nur nix, wenn Bluetooth
        ausgeschaltet ist. Ich fänd auch bewusstes ein- und ausloggen
        schöner. Und auf ner Karte könnte man auch noch einen Namen
        aufdrucken. Das fänd ich auch gut. 433Mhz wird glaub ich eher so
        für Geragentoröffner benutzt bzw. Funksteckdosen.
        [Nanu](Benutzer:Nanu "wikilink") 17:00, 3. Aug. 2014 (CEST)

# Material

### vorhanden

  - Arduino Uno
  - Ethernet Shield
  - Touchscreen Shield
  - Summer

### bestellen