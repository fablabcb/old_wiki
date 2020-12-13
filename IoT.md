Hier eine Sammlung von Notizen, die hilfreich sind, wenn man Internet of
Things Geräte bauen möchte.

## Wie erreicht man ein IoT Device hinter einer Firewall/NAT?

Ein geläufiges Problem ist dass Geräte nicht aus dem Internet erreichbar
sind. Im Heimnetzwerk sind sie hinter dem NAT des Routers bzw.
DSL-Modems. Dieser hat eine öffentliche IP aber die Rechner im lokalen
Netzwerk haben IPs aus einem privaten Subnetz. Manche Firmennetzwerke
haben zusätzlich noch eine Firewall, die nur bestimmte
Kommunikationsprotokolle (und Ports) zulässt. Geht man per Handynetz ins
Internet, bekommt man auch keine öffentliche IP, mit der man das Gerät
aus dem Internet erreichen könnte. Es gibt einige Methoden, um trotz
fehlender öffentlicher IP Geräte aus dem Internet ansprechen zu können:

  - **Port Forwarding** - dazu muss der Router bzw. das DSL-Modem
    eingestellt werden. Es wird so eingestellt, dass es die Anfragen an
    seine öffentliche IP über bestimmte Ports an bestimmte IPs im
    lokalen Netzwerk weiter leitet. Allerdings ändert sich die IP der
    meisten Router regelmäßig, sodass man noch DynDNS verwenden muss, um
    eine Domain-Weiterleitung auf diese sich ändernde IP einzurichten.
    Ein guter (kostenloser) Anbieter für DynDNS ist z.B.
    [spdyn.de](https://www.spdyn.de/)
  - **UDP** - über UDP können Geräte Ports in Routern selbstständig
    öffnen und eine Weiterleitung erwirken.
  - **Reverse SSH Tunnel** - es ist möglich über SSH sich in einen
    entfernten Rechner einzuwählen und einen lokalen Port des Client
    Rechners auf dem entfernten Rechner verfügbar zu machen. Dieser kann
    dann auf dem entfernten Rechner wie ein lokaler Port genutzt werden.
    So könnte sich z.B. ein Raspberry per SSH in einen Server einwählen
    und dann den lokalen SSH-Port auf dem Server verfügbar machen. Damit
    könnte man vom Server auf den Raspberry per SSH zugreifen, ohne dass
    dieser eine öffentliche IP-Adresse besitzt. Dies nennt sich dann
    Reverse-Tunnel, weil er rückwärts gerichtete Kommunikation zulässt,
    auf den Rechner der eigentlich die Verbindung aufgebaut hat.
  - **VPN-Tunnel** - ein VPN Tunnel leitet jegliche Kommunikation über
    alle Ports an einen entfernten Rechner. Es gibt viele verschiedene
    öffentliche VPN-Anbieter, bei denen man jedoch meist für den
    Service zahlen muss. Über Docker kann man sich relativ easy einen
    eigenen
    [VPN-Server](https://hub.docker.com/r/hwdsl2/ipsec-vpn-server/)
    installieren
  - **1-Klick-Anbieter** - da viele Leute zu kämpfen haben, ihr
    IoT-Gerät ins Internet zu bringen sind einige 1-Klick-Anbieter
    entstanden. So z.B. [dataplicity.com](https://www.dataplicity.com/)