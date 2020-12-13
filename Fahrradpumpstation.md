### Projektbeschreibung:

Die solare Fahrradpumpstation ist eines der ersten Projekte des FabLabs
gewesen und hat sich über einen längeren Zeitraum entwickelt. Ziel war
es eine Pumpstation aufzubauen, die autark arbeiten kann mit
Sonnenenergie betrieben. Hier wird insbesondere die Elektronik erklärt.
Das fertige Modell ist eine individuelle anfertigung aus vielen
Restbauteilen und kann leider nicht als eine Anleitung dokumentiert
werden.

### Das Konzept

Für die Funktion der Station benötigt man einen Energiegenerator (das
Solarmodul), einen Energiespeicher (die Batterie) und einen Verbraucher
(die elektrische Pumpe). Diese Geräte werden über einen Laderegler, der
die Lade - und Entladeströme regelt (z.B. die Batterie vor
Tiefenentladung schützt) verbunden. Das System arbeitet
Batteriefreundlich im 12V Spannungsbereich. Dadurch entstehen für die
Pumpe (bis zu 240W Leistung) sehr hohe Verbraucherströme (bis 20A), die
nicht vom Laderegler unterstützt werden. Zur Lösung des Problems wurde
ein SolidState Releais mit Optokoppler eingebaut, der es ermöglicht den
Strom direkt von der Batterie abzunehmen, aber gleichzeitig über den
Ladreregler zu konrollieren (Realaisfunktion).

![Konzept_Fahrradpumpstation.png](Konzept_Fahrradpumpstation.png
"Konzept_Fahrradpumpstation.png")

### Einkaufsliste

  - 2-Zylinder-Hochleistungs-Kompressor-12-V
  - 50W Solar-Set BIG 50 Ah 12V
  - Solid State Relay SSR-25 DD DC-DC 25A