Es gibt einige
[Kalenderplugins](https://www.mediawiki.org/wiki/Extension:Calendar) für
MediaWiki, aber keines gefällt mir so ganz. Die Frage ist auch, welche
Kalenderdarstellung wir überhaupt wünschen, was unsere Anforderungen
sind. Hier eine Diskussionsseite darüber.

# Anforderungen

  - kleiner, übersichtlicher Kalender auf der Startseite (eventuell auch
    einfach als Liste)
  - Großformatiger Kalender für ausführliche Informationen
  - Eine Listenansicht um für die Events in den nächsten Wochen Werbung
    zu machen
  - Weiterleitung auf Event-Wikiseite, wenn man auf den Titel eines
    Events klickt

# Möglichkeiten

## Semantic MediaWiki

Mit der Erweiterung [Semantic
MediaWiki](https://semantic-mediawiki.org/wiki/Help:Introduction_to_Semantic_MediaWiki)
kann man in Wikipediaseiten Schlüsselworte bzw. Tags einbauen, die
nachher benutzt werden können, um eine Indexseite zu erstellen. Das
könnte man auch nutzen, um in Seiten, die ein Ereignis oder einen
Workshop beschreiben das Datum als Datum zu markieren und dann in einer
Übersicht aufzuführen. Die Übersicht wäre dann unser Kalender und ließe
sich auch in einem Rahmen auf der Hauptseite einblenden. Es gibt sogar
schon eine Semantic um solche [Kalender
einzubauen](https://semantic-mediawiki.org/wiki/Event_calendar), mit
Kalenderansichten wie 'month', 'basicweek', 'basicday', 'agendaweek',
'agendaday'. Man kann anscheinend Mehrtägige Ereignisse definieren und
[wiederkehrenden
Events](https://semantic-mediawiki.org/wiki/Help:Recurring_events) (hier
eine [Demo](https://semantic-mediawiki.org/wiki/Demo:Recurring_events))
und Bingo\! ein [iCal export
format](https://semantic-mediawiki.org/wiki/Help:ICalendar_format), dass
sich nutzen lässt um die Events mit dem Handy oder Computer zu
synchronisieren\! Man kann sogar auch ein [Formular zum Eintragen von
Events](https://semantic-mediawiki.org/wiki/Demo:Event_calendar/Create_events_using_a_form)
nutzen und ansonsten halt einfach auf einer Wiki-Seite markieren, dass
sie ein Event beschreibt.

Die
[Installation](https://semantic-mediawiki.org/wiki/Help:Installation)
ist jedoch etwas umfassender als eine kleinere Extension. Dafür könnte
die Semantic auch an anderen Stellen sehr nützlich sein, z.B. um umser
Werkzeug zu indexieren.

  -
    Die Nutzung der Semantic-Erweiterung finde ich persönlich am
    Überzeugendsten - [Nanu](Benutzer:Nanu "wikilink") 21:27, 23. Okt.
    2014 (CEST)
    Ich glaube dieses Plugin für Semantic MediaWiki müssten wir für den
    Kalender installieren:
    <https://semantic-mediawiki.org/wiki/Semantic_Result_Formats>
    Zumindest steht hier: "Semantic Result Formats is an extension to
    Semantic MediaWiki (SMW) that adds a large number of further result
    formats to inline queries, including formats for calendars,
    timelines, charts, graphs and mathematical functions."