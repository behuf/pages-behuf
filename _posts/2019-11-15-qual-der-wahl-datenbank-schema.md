---
title: Qual der Wahl. Welches Datenbankschema?
tags: [datenbanken, webentwicklung ]
---
Als ich mit der Informatik und Softwareentwicklung angefangen habe, stand eine relativ eindeutige und klare Definition von Datenbanksystemen als das Ideal-Bild einer performanten und strukturierten Geschäftsanwendung.

Der Taktgeber in allen Softwarearchitekturen und Entwicklungsabteilungen war das relationale Datenbankschema in der Kombination mit den allesamt hochgepriesenen und dringend notwendigen `Normalisierung` [Link](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)).

Klar und sinnvoll. Daten systematisch zu speichern und Datenredundanz möglichst zu verhindern war und ist heute noch ein wichtiger Grundsatz des Datenbankdesigns. Das Spannungsfeld zwischen der *Performanceverlust* und Erhöhung der *Komplexität* bei der Verarbeitung der Daten aufgrund der notwendigen Normalisierung einerseits und die *Qualität der persistierten Daten* in einer normalisierten Form andererseits stelle die Entwicklung einer Software und damit einhergehender Entscheidung in der maximal notwendigen Tiefe der Normalisierungstufen immer wieder vor großen Herausforderungen.

Mit der Zeit jedoch entwickelte sich auch die Softwareentwicklung weiter. Internet und damit einhergehenden Möglichkeiten definierten die Softwareentwicklung neu. Neue Architekturansätze kamen vermehrt zum Tragen. Neue Fragestellungen wie die Art und Weise der Organisation der vom Anwender produzierten Daten mussten gelöst werden. Software heute funktioniert vermehrt standortsunabhängig und die Idee der Plattformen nimmt auch für die Geschäftswelt immer mehr Einzug. Der Anspruch schnell auf Veränderungen zu reagieren und gar teile einer Lösung gänzlich durch andere Teillösungen zu ersetzen ist keine Seltenheit. Ebenso und auch aufgrund der hohen Reichweite entstehen große Datenbankmengen, die auch an unterschiedlichen Standorten unterschiedliche Abruffrequenzen aufweisen. Die Softwareprodukte werden immer mehr in ihren Einzelteilen "zerlegt" (Stichwort: MicroServices) und sollten jeweils für sich und autark und möglichst hoch skalierbar und performant lauffähig sein. Tauscht man diese Dienste durch neuere Entwicklungen und Dienste aus, soll dies nicht zum Zusammenbruch des Gesamten Systems führen.

`Dokumentenbasierte Datenbanken` [Link](https://de.wikipedia.org/wiki/Dokumentenorientierte_Datenbank) reihen sich hier als eine sinnvolle Ergänzung und Option ein und bereichen das Leben der Entwickler und man kann durchaus behaupten, dass sie in den letzten Jahren einen phänomenalen Siegeszug feiern konnten.

Datensätze werde nicht mehr als Datensätze mit Spalten und Relationen nach einem festen verbindlichen Schema persistiert. Das Dokument samt Inhalt ist die Maßgabe und wird in einem "Schrank" abgelegt und kann jederzeit abgerufen werden. Schema? Egal!

So und nun kommt natürlich die Frage, für welches Konzept entscheide ich mich als Architekt und Entwickler, wenn ich eine neue Software aufsetzen möchte? Nun eine einfache Antwort auf diese Frage gibt es leider nicht. Im Grunde müsste man diese Frage viel mehr von der Architektur der aufgesetzten Software und existierenden Anforderung abhängig machen.

**Die dokumentenbasierten Datenbanksysteme sehe ich persönlich _nicht_ als eine logische Weiterentwicklung der relationalen Datenbanken, die diese obsolet machen sollte.**

Es ist eine neue Entwicklung als Option. Und dabei würde ich es auch belassen.

Ein für mich sehr wesentlicher Vorteil von dokumentenbasierten Datenbanken ist ihre Schemalosigkeit. Das macht die Entwicklung und Ausrollung von neueren Versionen ohne möglichen Migrationsbrüche flüssiger. Der schemalose Ansatz verlagert mehr und mehr die Logik samt Struktur Richtung Code und Geschäftslogik und macht die Entwicklung unabhängiger von der Persistenzschickt der Softwarelösung. Das ist zweifelsohne ein großer Vorteil.

Natürlich verändert auch eine dokumentenbasierte Ablage der Informationen die Art und Weise der Abfragen und Auswertung der vorhandenen Datensätze. Gerade wenn es darum geht, Datensätze für Auswertungen zusammenzuführen, müssten bei einem nicht relationalen Schema neue Ansätze entwickelt und gefahren werden. Ein einfaches "Join" zwischen den Tabellen und Untertabellen ist nicht mehr der absolute Ansatz für eine von MicroService und Web dominierten Softwarearchitektur. Softwarezellen stehen für sich und autark; samt Daten. 

**Ich nenne diese Entwicklung für mich als eine Art systemische "Denormalisierung" für eine unabhängigere und performantere Datenverarbeitung.**

Der Preis dafür => die einfache Auswertbarkeit der Daten aus unterschiedlichen "Bereichen". Hier müssen die Dienste und Daten aus den jeweiligen Diensten manuell "zusammengetragen" werden. Und das geht nicht mehr per Knopfdruck.

## Fazit

Es ist nicht möglich in einem Artikel auf alle Aspekte dieser Technologie-Entscheidung einzugehen. Relational oder Nicht Relational ist eine Entscheidung, die immer wieder neu bewertet und getroffen werden muss.

Für mich ist die dokumentenbasierte Ablage näher an den Realitäten der Geschäftswelt und spiegelt eher den klassischen Umgang mit Dokumenten und Informationen aus der realen Welt wieder. Mit Vor- und Nachteilen, die es mit sich bringt. Früher haben wir ja unsere Rechnungen genauso in Leitzordnern abgelegt. Schemalos bedeutet für mich auch die konsequente Fortführung dieser altbewährten Art der "Datenverarbeitung". Jedoch digital und systemisch. Bei der richtigen Umsetzung auch auswertbar und im Kern erweiterbar.
