## Mögliche Fehler

### Linux

#### Netzwerkeinstellungen überpfüfen

Druckerkonfiguration: Beim Suchen nach dem Drucker kommt folgende
Fehlermeldung: `FirewallD is not running. Network printer detection
needs services mdns, ipp, ipp-client and samba-client enabled on
firewall.`

Hier sollten die Netzwerkeinstellungen überprüft werden. Es kann sein,
dass PC-Direktverbindung eingeschaltet ist.

#### Interessante Befehle in Linux zum Ducker:

  - Ansicht über die Druckerpfade: `smbtree`
  - Suchen nach Drucker im Netzwerk mit `avahi-browse -all`.

Manuelle Konfiguration grundsätzlich über Webinterface möglich:

  - <http://localhost:631/admin>