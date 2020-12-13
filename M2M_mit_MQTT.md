[MQTT](http://mqtt.org) ist eines der Protokolle, die für das
aufkommende ["Internet der
Dinge"](https://de.wikipedia.org/wiki/Internet_der_Dinge) (IoT) genutzt
werden. Es macht die sogenannte Machine-to-Machine (M2M) Kommunikation
möglich.

Machine-to-Machine (M2M) steht für den automatisierten
Informationsaustausch zwischen Endgeräten wie Maschinen, Automaten,
Fahrzeugen oder Containern untereinander oder mit einer zentralen
Leitstelle, zunehmend unter Nutzung des Internets und den verschiedenen
Zugangsnetzen, wie dem Mobilfunknetz. Eine Anwendung ist die
Fernüberwachung, -kontrolle und -wartung von Maschinen, Anlagen und
Systemen, die traditionell als Telemetrie bezeichnet wird.\[1\]

# Warum ein neues Protokoll?

  - **MQTT arbeitet sehr sparsam** (minimal on-the-wire footprint).
      - Normale HTTP-Requests brauchen sehr viel Daten für das
        Protokoll. Wenn z.B. nur ein Temperaturwert gesendet werden
        soll, kann es sein dass fürs Protokoll mehr Daten verwendet
        werden als für den eigentlichen Inhalt der Mitteilung.
      - Das ist wichtig z.B. in Mobilfunknetzen, wo jedes kB kostet.
        Sollen eine ganze Reihe solcher Geräte über GSM betrieben
        werden, addieren sich die Kosten monatlich schnell zu großen
        Summen.
      - Andererseits ist es wichtig für batteriebetriebene Geräte, um
        Energie zu sparen.
      - MQTT realisiert echte Push-Benachrichtigungen. Clients müssen
        nicht regelmäßig anfragen, ob es Neuigkeiten gibt.

<!-- end list -->

  - In vielen Netzen haben Geräte **keine feste IP-Adresse**. Die
    dynamischen IP-Adressen sind meist von Außen nicht ansprechbar.
      - Im Client-Broker System von MQTT braucht nur der Broker eine
        feste IP-Adresse. Alle Clients verbinden sich zum Broker und
        können ab da an Push-Benachrichtigungen vom Broker erhalten.
        Dazu brauchen sie keine feste IP-Adresse und können z.B. hinter
        einem NAT oder einer Firewall liegen.

<!-- end list -->

  - Im Mobilfunknetz ist die **Übertragungsqualität oft schlecht**,
    Datenpakete gehen verloren, Übertragungsgeschwindigkeiten sind
    langsam und Verbindungen brechen ab.
      - Quality of Service (QoS) Levels legen fest, ob die sparsame
        Datenübertragung oder die Sicherheit der Datenübertragung im
        Vordergrund stehen
      - Clients melden sich regelmäßig beim Broker um zu signalisieren,
        dass sie noch verbunden sind.
      - Für den Fall, dass die Verbindung abbricht kann jeder Client
        seinen letzten Willen hinterlassen (Last Will and Testament,
        LWT), der vom Broker ausgeführt wird sobald der Client sich
        nicht mehr meldet.
      - **Timeouts** sind bei MQTT sehr hoch, sodass auch Nachrichten
        mit langer Verzögerung ankommen.

<!-- end list -->

  - Internet of Things-Geräte haben oft **wenig Rechenleistung**, die
    für das HTTP-Protokoll teilweise nicht ausreicht. MQTT ist auch
    sparsamer in der nötigen Rechenleistung.

→ Mehr zu den [Design Prinzipien von
MQTT](https://github.com/mqtt/mqtt.github.io/wiki/Design%20Principles)
im Wiki von mqtt.org.

# Wie funktioniert MQTT?

  - Es gibt einen **Broker** (Server), der über eine feste IP-Adresse
    erreichbar ist.
  - Geräte, die Daten senden wollen (Messgeräte, Anlagenmonitoring,
    IoT-Geräte) verbinden sich zum Broker.
  - Einmal verbunden können diese Geräte Nachrichten an verschiedene
    "**Topics**" auf dem Broker senden (**publish**). Ein Topic könnte
    z.B. Wohnzimmer/Temperatur sein.
  - Geräte, die Daten erhalten wollen (Laptop, Smartphone,
    Datenbankserver), verbinden sich ebenso zum Broker und
    **abonnieren** Topics (**subscribe**).
  - Der Broker pusht Nachrichten, die er von Clients erhält an die
    Clients, die das Topic abonniert haben. Das funktioniert in
    **Echtzeit**, aber auch zwischengespeichert (**Retained Message**),
    falls der lesende Client sich erst später verbindet.
  - Auch Clients die hauptsächlich zum Datenauslesen bzw. -visualisieren
    gedacht sind (z.B. Smartphone) können Nachrichten an den Broker
    senden und auch Messgeräte können Nachrichten abbonieren. So können
    z.B. auch Befehle an das Messgerät übermittelt werden (z.B. ein
    Befehl um das Messintervall zu verändern).
  - Geräte melden sich regelmäßig beim Broker, um zu signalisieren, dass
    sie noch verbunden sind. So kann auch wenn keine Daten gesendet
    werden mit minimalem Daten- und Energieverbrauch sichergestellt
    werden, dass das Gerät noch funktioniert und sendebereit ist.
  - Beim Verbinden können Geräte einen **Last Will and Testament (LWT)**
    verschicken. Dieser wird vom Broker ausgeführt, falls der Client
    nicht mehr erreichbar ist. So kann z.B. bei einem Verbindungsabbruch
    das Topic Anlage1/Sensor4/status auf "offline" gesetzt werden.

→ Weitere Informationen findet man auf der [mosquitto mqtt man
page](http://mosquitto.org/man/mqtt-7.html) oder in den Tutorials auf
[hivemq.com](http://www.hivemq.com/blog/mqtt-essentials/)

# Siehe

  - [mqtt.org](http://mqtt.org)
  - [Wikipedia: M2M](https://de.wikipedia.org/wiki/Machine_to_Machine)
  - [mqtt man page
    (mosquitto.org)](http://mosquitto.org/man/mqtt-7.html)
  - [mqtt-essentials
    (hivemq.com)](http://www.hivemq.com/blog/mqtt-essentials/)

# Anleitungen

  - [mqtt with paho - Vortrag mit Java Codebeispielen von der
    eclipsecon2013](https://github.com/dc-square/mqtt-with-paho-eclipsecon2013)
  - [Überblick über Broker und Client
    Software](https://github.com/mqtt/mqtt.github.io/wiki/software?id=software)
  - [Mosquitto (MQTT Server und/oder Client) auf dem Raspberry
    Pi](http://jpmens.net/2013/09/01/installing-mosquitto-on-a-raspberry-pi/)

# Beispielprojekte

  - [Einfaches Arduino MQTT
    Projekt](http://m2mio.tumblr.com/post/30048662088/a-simple-example-arduino-mqtt-m2mio)
  - [Geofencing with the FONA 808 & Adafruit
    IO](https://learn.adafruit.com/geofencing-with-the-fona-808-and-adafruit-io/introduction)
  - [Ultra-Low Power \#ESP8266, solar power only driven
    \#SENSableTHING](https://www.hackster.io/fablabeu/esp8266-thing-by-sparkfun-982bc6)
  - [Nachtlicht mit Arduino und MQTT über openHAB
    steuern](http://blue-pc.net/2014/10/21/nachtlicht-mit-arduino-und-mqtt-ueber-openhab-steuern/)
  - Im Wiki von mqtt.org sind einige [weitere
    Anwendungsbeispiele](https://github.com/mqtt/mqtt.github.io/wiki/Example%20Uses)
    genannt.
  - [Python-Implementierung](http://jpmens.net/2013/02/25/lots-of-messages-mqtt-pub-sub-and-the-mosquitto-broker/)
    mit mosquitto library.
  - [Bridge between two
    datacenters](http://jpmens.net/2013/02/25/lots-of-messages-mqtt-pub-sub-and-the-mosquitto-broker/)

# Broker

[Liste von Brokern/Servern auf
mqtt.org](https://github.com/mqtt/mqtt.github.io/wiki/servers)

für eigene Installationen:

  - [Mosquitto: Open Source MQTT Broker (Server)](http://mosquitto.org)
      - [SSL-Zertifikat
        einrichten](http://mosquitto.org/2015/12/using-lets-encrypt-certificates-with-mosquitto/)

public platform:

  - [adafruit.io](https://io.adafruit.com)
  - [mqtt.io](http://www.mqtt.io)
  - [public test
    brokers](https://github.com/mqtt/mqtt.github.io/wiki/public_brokers)
  - [thingspeak.com](https://thingspeak.com/pages/how_to#analyze)

# Clients

Arduino:

  - [Adafruit MQTT
    Library](https://github.com/adafruit/Adafruit_MQTT_Library)
  - [Arduino client library](http://pubsubclient.knolleary.net)
  - [Paho Javascript
    client](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.javascript.git/plain/src/mqttws31.js)
    über Websockets (Datei mqttws31.js).
      - Dazu muss der Broker Websockets unterstützen.
        [Hier](http://goochgooch.co.uk/2014/08/01/building-mosquitto-1-4/),
        [hier](https://harizanov.com/wiki/wiki-home/raspberry-pi/how-to-rasbperry-pi-install-mosquitto-with-websockets-enable/)
        oder
        [hier](http://qiita.com/aquaviter/items/cb3051cf42a3a3c4a4d9)
        z.B. eine Anleitungen um mosquitto mit Websocket-Unterstützung
        ([libwebsockets](https://libwebsockets.org/index.html)) zu
        kompilieren.
      - Eine Beispielkonfiguration für einen Broker mit
        Websocket-Unterstützung findet sich
        [hier](http://jpmens.net/2014/07/03/the-mosquitto-mqtt-broker-gets-websockets-support/).
      - [HiveQM Javascipt websocket client
        Beispiel](http://www.hivemq.com/demos/websocket-client/)

Raspberry:

  - [Mosquitto: Open Source MQTT Broker und
    Client](http://mosquitto.org)

Dashboards:

  - [thinstudio.io](http://www.thingstud.io)
  - [io.adafruit.com](http://io.adafruit.com)
  - [MyMQTT](https://play.google.com/store/apps/details?id=at.tripwire.mqtt.client)
    – Android-App
  - [IoT
    Manager](http://www.amazon.de/Victor-Brutskiy-IoT-Manager/dp/B016YW21KE)
    - Android App im Amazon Appstore
  - ["Seven best MQTT client
    tools"](http://www.hivemq.com/blog/seven-best-mqtt-client-tools)

# Postprocessing, Datenauswertung, Datenspeicherung, Interface zu anderen Diensten

  - [mqttwarn](https://github.com/jpmens/mqttwarn) kann die Nachrichten,
    die es als MQTT-Client erhält zu anderen Diensten wie linuxnotify,
    osxnotify, mysql, smtp, slack, twitter und vielen anderen weiter
    pushen.
  - [republisher
    daemon](https://github.com/bluewindthings/mqtt-republisher-daemon)
  - Mit [Node-RED](http://nodered.org) kann man die Datenstreams wie in
    einem Fließdiagramm weiterverarbeiten, zusammenführen, an
    verschiedene Dienste weiterleiten und auch in Dateien oder
    Datenbanken speichern.

# Hardware

  - [hackster.io](http://hackster.io/platforms) bietet einen [Überblick
    über alle Hardware-Plattformen](https://www.hackster.io/platforms)
    mit denen sich IoT-Projekte realisieren lassen.
  - [Übersicht über die
    Arduino-Produkte](https://www.arduino.cc/en/Main/Products) und deren
    Einsatzgebiete

GSM

  - shields
      - [Adafroit Fona 808 GSM shield (with
        GPS)](https://www.adafruit.com/products/2542)
      - [Adafruit Fona 800 GSM
        Shield](https://shop.pimoroni.de/products/adafruit-fona-800-shield-voice-data-cellular-gsm-for-arduino)
        49€
      - [Mini GSM/GPRS+GPS Board - SIM808
        Breakout](https://www.tindie.com/products/Deray/mini-gsmgprsgps-board-sim808-breakout/?pt=full_prod_search)
        35€
      - [SparkFun Cellular Shield -
        MG2639](https://www.sparkfun.com/products/13120) 66€

<!-- end list -->

  - devboards
      - [Particle
        Electron](https://store.particle.io/?utm_source=homesite&utm_medium=Nav&utm_campaign=TopMenu#electron)
        – STM32F205 ARM Cortex M3, 1MB Flash, 128K RAM, cloud zum
        programmieren, 2G 39€, 3G 59€
      - [Adafruit Feather Fona](https://www.adafruit.com/products/3027)
        – ATmega32u4 @ 8MHz, 45 $
      - [CellStick Cellular (GSM/GPRS) IoT
        Platform](https://www.tindie.com/products/tinkeringtech/cellular-gsmgprs-board-with-at328au-and-built-in-ftdi/?pt=full_prod_search)
        60€ (+23€ Versandt)
      - [Hologram Dash](https://hologram.io/store/hologram-global-dash)
        GPRS/EDGE/UMTS/HSPA, analog inputs 69€

Wifi

  - [ESP8266 WiFi SoC](https://www.sparkfun.com/products/13231) 15€ -
    Microcontroller mit Wifi; für energie- und rechensparsame Things
  - [Particle Photon](https://www.sparkfun.com/products/13345) 18€ -
    Devboard mit 120Mhz ARM Cortex M3 microcontroller mit integriertem
    Wifi; für rechenintensive Things
  - [Adafruit HUZZAH ESP8266
    Breakout](https://www.adafruit.com/product/2471)
    [10€](http://www.flikto.de/products/adafruit-huzzah-esp8266-breakout)
    - 80Mhz microcontroller mit Wifi
  - [WIFI development module - ESP8266
    based](https://www.tindie.com/products/Knewron/smartwifi-development-module-esp8266-based/)
    9€
  - [Cactus Micro Rev2 Arduino compatible plus
    esp8266](https://www.tindie.com/products/AprilBrother/cactus-micro-rev2-arduino-compatible-plus-esp8266/)
    10€ (nur 5€ Versandt\!)

<!-- end list -->

  - [WiFi Module - ESP8266](https://www.sparkfun.com/products/13678)
    6,50€ - zur Wifi-Anbindung jedes Arduinos

# M2M Mobilfunk Tarife

Für M2M-Anwendungen sollten die Mobilfunk-Tarife möglichst geringe
Grundkosten haben, damit man mit sparsamer Datenübertragung auch
wirklich kosten sparen kann. Auch die Kosten pro MB gesendeter Daten
sollten möglichst gering sein. Wenn man ganze Netze aus über Mobilfunk
angebundenen Geräten betreiben möchte akkumulieren sich die Kosten sonst
nämlich recht schnell. Darüber hinaus enthalten normale Mobilfunktarife
in den Vertragsbedingungen Klauseln, die besagen, dass dieser Tarif
nicht für reine Datenübertragungen benutzt werden darf, also
hauptsächlich zum telefonieren benutzt werden soll.

Mittlerweile gibt es von einigen Mobilfunkanbietern Tarife, die speziell
auf M2M-Anwendungen zugeschnitten sind. Einige Anbieter richten sich da
eher an Großkunden und verkaufen z.B. 500 Simkarten mit speziell
zugeschnittenem M2M-Tarif. Preise werden hier auf Anfrage gemacht und
sind sicherlich für Großabnehmer billiger. Dies ist interessant z.B. für
Entwickler, die ihre Geräte inklusive einjährige mobiler Cloud-Anbindung
ausliefern, also die Sim-Karte mit dem Gerät ausliefern und alle Kosten
bereits im voraus bezahlt haben. Andererseits kann so z.B. ein
Fuhrunternehmen seine ganze Fahrzeugflotte mit GPS-Trackern ausstatten.

Manche solcher Tarifen bieten weitere Vorteile: z.B. Gleichbleibende
Preise im Ausland oder die Nutzung anderer Netze, falls das eigentliche
Netz nicht verfügbar ist. Vodafone bietet z.B. alternativ zur Sim-Karte
einen Mikrochip, der fest verlötet werden kann und damit
korrosionsbeständiger ist, eine längere Lebensdauer hat und höhere
Temperaturschwankungen aushält.

Solche Tarife findet man eigentlich bei allen gängigen Anbietern. Z.B.:

  - T-Mobile: [1](http://m2m.t-mobile.com) [2](http://m2m.t-mobile.com)
  - Vodafone:
    [3](https://www.vodafone.de/business/firmenkunden/loesungen/m2m-machine-to-machine.html)
    [4](http://www.vodafone.com/business/m2m)
  - O2: [5](http://o2.m2m.com)

Ich habe jedoch auch einen Anbieter gefunden, bei dem man als
Kleinabnehmer zu einem definierten Tarif einzelne Karten kaufen kann:

  - [m2m-mobil.de](https://www.m2m-mobil.de/ueber-uns-datentarif-machine-to-machine)
    im O2-Netz.
    \[<https://www.m2m-mobil.de/m2m-mobilfunk-tarif-preis-informationen?m2m-mobil=4cmd9e8gma2onduhnq5fsu5ru70,95>€
    montl. Grundpreis\], 1MB inkl., 5 MB = 1,07€, 100 MB = 4,64€. Es
    gibt auch einen Tarif im Vodafone-Netz.

[hologram.io](https://hologram.io/iot-sim-card/) ist ein Anbieter aus
den USA, der Tarife ohne monatliche Mindestgebühr anbietet. Ausserdem
sind die Karten (fast) weltweit ohne Roaming-Gebühren gültig. Allerdings
fallen Kosten für den Zoll an, weil die Karten aus den USA importiert
werden müssen. Es gibt einen [Shop in
Österreich](http://www.4bees.at/shop?p_p_id=KonaKart_Storefront_WAR_konakart&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&p_p_col_id=column-1&p_p_col_count=1&_KonaKart_Storefront_WAR_konakart_struts.portlet.action=%2FSelectProd.action&_KonaKart_Storefront_WAR_konakart_struts.portlet.mode=view&_KonaKart_Storefront_WAR_konakart_prodId=96),
der die Karten in Europa vertreibt.

# Referenzen

<references />

1.  <https://de.wikipedia.org/wiki/Machine_to_Machine>