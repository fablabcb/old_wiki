Wir sind gerade dabei uns einen Mediaserver aufzubauen, der im lokalen
Netzwerk verfügbar ist.

# Anforderungen

  - Media player Musik:
      - Auf Server gespeicherte Musik abspielen
      - Musik an Server streamen, um sie über die Anlage abzuspielen
        (z.B. AirPlay)
      - Eventuell Touchscreen?
      - Steuerung der Musik über Fernbedienung

<!-- end list -->

  - Media Player Bild:
      - Anschluss an Beamer
      - Drahtloses Streamen vom Laptop an Media Player (z.B. für
        Präsentationen)?

<!-- end list -->

  - Dateiserver
      - Erreichbar über FTP, SMB, AFP
      - öffentlicher readonly
      - Vereinsinterner Bereich read, write, kein Überschreiben oder
        Löschen
      - Admin-Account mit Überschreib- und Löschrechten
      - private Benutzer-Ordner

# Hardware

BananaPi mit angeschlossener 2.5 Zoll Sata-Festplatte

# Software

  - OS: [LeMedia](http://www.lemaker.org/resources/9-191/lemedia.html)
    (Debian mit [XBMC/Kodi-Oberfläche](http://kodi.tv) für BananaPi) von
    [lemaker.org](http://lemaker.org)
  - [smb-Server](http://jankarres.de/2013/11/raspberry-pi-samba-server-installieren/)
  - Partitionieren und Formatieren der SATA-Festplatte ist hier
    beschrieben:
    [1](http://banoffeepiserver.com/setup-raspbian-on-a-sata-hard-disk.html),
    [2](http://smallsite.dyndns.org/bananaSSD.php). Eventuell könnte der
    Raspberry auch von der SATA-Festplatte booten. Die Anleitung dazu
    ist auch unter den beiden Links zu finden.