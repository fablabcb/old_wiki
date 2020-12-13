Auf dieser Seite wollen wir einige Probleme sammeln, die wir beim
3D-Drucken haben und andererseits Problemstellungen als
Herausforderungen, die man lösen könnte.

# Probleme

  - Flow
  - Flow
  - Flow
  - Haftung auf dem Druckbett
  - Filament verheddert sich auf der Rolle
  - nach dem Springen an einen neuen Druckpunkt fließt plötzlich viel
    mehr Filament (da durch den fehlenden Vorschub beim Sprung mehr
    weich geworden ist als im laufenden Betrieb)-\> Effekt als "Narbe"
    bekannt

# Programmtechnische/mathematische Herausforderungen

  - Bridging beim Abdecken der Füllgitter: Druckkopf zieht die Bridges
    teilweise nicht bis zum nächsten Steg, sondern kehrt auf halber
    Strecke um - Filament fällt in den Zwischenraum.
  - Füllstruktur zur Decke hin verzweigen lassen - für besseres
    Schließen bzw. Bridging an der Oberfläche und größere Abstände im
    Füllgitter im unteren Bereich.
  - Lassen sich die Schmelzprozesse im Druckkopf simulieren? Sodass man
    eventuell die Temperatur dynamisch anpassen kann, dass z.B. bei
    Sprüngen weniger hinaus läuft? Sozusagen Schmelzen nach Bedarf?
  - Könnte man die Schichten mehr verzahnen? Also z-Bewegung um wenige
    mm oder µm in den Druck einbauen? Bräuchte man dafür eine andere
    Spitze oder geht es auch mit den bestehenden Spitzen?
  - Programm lässt potentielle Schwachstellen/Detailgenauigkeit nur
    schwer erkennen (zu dünne Verbindungen, Haftungsfläche auf dem
    Boden)

# Womit sich andere schon beschäftigt haben

  - Herausrechnen der Schwingungen in den Gummi-Riemenantrieben beim
    Richtungswechsel (Quelle?)
  - Es gibt versuche mit unterschiedlichen Druckkopfgrößen und einem
    schnelleren Druckverfahren mit hoher Genauigkeit