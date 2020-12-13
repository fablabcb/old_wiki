Unter newwiki.fablab-cottbus.de haben wir den Upgradeprozess auf
MediaWiki 1.23 begonnen.

Anleitungen:

  - <https://www.mediawiki.org/wiki/Manual:Upgrading/de>
  - <https://www.mediawiki.org/wiki/Manual:Upgrading>

Die Extensions sind in den Ordner extension/ geladen. Ob alle
funktionieren ist noch nicht getestet.

  - Einige Extensions haben wir deaktiviert:
      - mimtex (hat nicht funktioniert)
      - simpleAntiSpam (wurde in den Core bewegt)
      - NativeSvgHandler hat wahrscheinlich vorher sowieso nicht
        funktioniert

Die skin "vector" hat sich massiv verändert.

  - screen.less includes multiple other less files
  - most css has moved to the sub files
  - git ist nicht fähig die diffs darzustellen

Todo:

  - Diff aus orignal vector von 1.22 zu Nanus Änderungen erstellen
  - Änderungen anwenden auf vector von 1.23
  - eventuell könntne wir ein semantisches CSS-Diff Tool verwenden:
    <http://stackoverflow.com/questions/7930064/tool-to-parse-and-compare-two-css-stylesheets>
  - testing
      - extensions
      - skin
  - semantic Mediawiki mit Kalender installieren