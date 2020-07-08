---
tags: [allgemein, webentwicklung ]
title: Ein neue Webseite mit Jekyll
---
Die Idee war ein Webauftritt zu entwickeln. Etwas Schlichtes und ohne viel Schnickschnack. Der erste Gedanke war, die Seite in Auftrag zu geben.
Nach Recherchen hat es nicht mehr lange gedauert, bis ich von der Idee der Beauftragung Abstand genommen habe. 

Der Reiz einer selbst entwickelten und selbst gehosteten Internetseite war dann doch zu groß.

Zwei Grundfragen am Anfang standen im Raum, die beantwortet gehörten: 

1. Welche Daten und Inhalte sollen auf der Seite dargestellt werden und wie soll das "Backend" der Seite persistiert und organisiert werden?
2. Welche Bibliotheken und Tools sollen für die Darstellung der Inhalte im Browser verwendet werden und was muss die Oberfläche der Seite aus der Sicht eines modernen Webauftritts als Mindestvoraussetzung erfüllen?

## Backend und Plattform

Für den Zweck Blogeinträge zu erstellen und einige einfache Präsentationsseiten mit relativ überschaubaren Textinhalten zu hinterlegen, fand ich ein CMS System zu überladen. Überladen, weil es viele Zusatzfunktionen eben nicht benötigt werden und ein solches System eben "installiert" und ggf. auch "administriert" werden müsste. Übertragung  zu anderen Hosting-Providern wäre ebenso ein Thema für den Fall, dass ich den Hosting-Provider wechseln sollte. **Meine Idee war eine möglichst einfache und trotzdem noch dynamische Form der Seitenerstellung mit möglichst wenigen Abhängigkeiten (Datenbank, Hosting-Provider, Plattform, usw.)**.

Die Idee die Seite statisch zusammen zu setzen kam mir nach dem ich das Tool `Jekyll` zufällig kennengerlernt habe. Nach einigen Tests und kurze Einarbeitung in die Idee des `Jekyll` als statischen Seitengenerator hab ich mich dafür entschieden meine Webseite mit diesem System zusammen zu stellen.

Aus meiner bescheidenen Sicht sprechen folgende Vorteile für `Jekyll`:

* Der Fokus liegt absolut auf den Inhalt und Struktur der Seite
* Sowohl die Struktur als auch der Inhalt lässt sich auf Dateisystem gut und einfach abbilden und es wird kein zusätzliches Overhead benötigt.
* Das Template System kann durch die Möglichkeit der Vererbung (`_layouts`) und Komposition von Teilinhalten (`include`) auf einer Seite sehr flexibel und erweiterbar umgesetzt werden.
* Blog-Einträge können über das System einfach und übersichtlich abgebildet werden.
* `Sass`, `Liquid` oder `Markdown` sind gängige Standards im Webbereich und werden von `Jekyll` autmatisch unterstützt. 
* Die Seite kann durch die Anbindung an Github-Pages automatisiert von GitHub gehostet und als Repository historisierbar gesichert und sogar gehostet werden.
* Zweckbezogen benötige ich damit kein Datenbanksystem im Hintergrund.
* Sollte der Bedarf an einer Erweiterung und Umstellung auf ein CMS System doch noch bestehen, können die Templates und Inhalte relativ leicht auf ein anderes System übertragen und wiederverwendet werden.
* Gute Dokumentation und schnelle Einarbeitung.
* Deployment und Ausrollung der Seite kann sowohl manuell als auch automatisiert laufen. 

Natürlich gibt es auch gewisse Einschränkungen, die eine statische Website naturgemäß mit sich bringt: 

* Fehlende Möglichkeit Benutzerinteraktionen wie Kontaktformulare oder Kommentarfunktion zu programmieren. (Hierzu kann man allerdings auf extern gehostete Lösungen zurückgreifen)
* Allgemeine fehlende serverseitige Verarbeitung von Geschäftslogik. (Ein Shop-System würde ich vermutlich damit nicht aufbauen)
* Technisches Verständnis für die Erstellung und Ausrollung der Seite wird benötigt.
* Installation und Einrichtung von `Ruby` und `Jekyll` ging anfangs nicht ganz reibungslos. Nach anfänglichen Schwierigkeiten jedoch, war es relativ klar und problemlos.

## Webinterface und Browseroberfläche

Eine moderne und zeitgemäße Html-Seite muss auf allen Endgeräten vernünftig und angepasst dargestellt werden können. Nach dem ich mir einige Templatevorlagen im Netz angesehen habe und diese alle mich nicht zu 100% überzeugt haben, entschied ich mich, mein eigene Html-Vorlage zu entwickeln.

Für den Aufbau der Internetseite greife ich auf folgende Bibliotheken zu:

* **`Bootstrap`**: Eine weit verbreitete CSS Bibliothek für die Erstellung von Endgeräte-unabhängiges Layout. Der Mobile-First Ansatz und die große Bandbereite der Nutzung dieser Bibliothek hat mich überzeugt.
* **`JQuery`**: Quasi standard im Webbereich, wenn es darum geht DOM im Browser zu manipulieren. Langjährig bewährt und von vielen tausenden Web-Entwicklern und Websites erfolgreich im Einsatz.
* **`Font Awesome`**: CSS basierte Icons kann ich damit schnell und deklarativ nutzen.
* **`Google Fonts`**: Schöne Fonts, einfache Einbindung

## Fazit

Und so ist diese Seite eben entstanden. Es gibt mittlerweile sehr viele Möglichkeiten für die Erstellung von Webauftritten. Je nach Anforderung und Gegebenheiten müsste man sich natürlich für das passende System und die bessere Art entscheiden, was einem am meisten den gewünschten Mehrwert bringt.

Mein Ansatz für die Erstellung dieser Seite ist eher vom Pragmatismus geprägt. Es muss für mich nicht immer die technisch beste und umfangreichste Lösung sein. Das gewünschte Ergebnis muss immer der Basispunkt für Entscheidungen sein. Und der Rest ist "Beiwerk" und sollte so einfach und so reduziert wie möglich dem Zweck der Erreichung des gewünschten Ergebnisses dienen.

## Weblinks

* [Jekyll](https://jekyllrb.com) : Software für die Generierung von statischen Blog-Seiten
* [Jekyll Deployment](https://jekyllrb.com/docs/deployment/) : Die Art und Weise der Ausrollung von Jekyll erstellen Seiten
* [Font Awesome](https://fontawesome.com/) : CSS basierte und deklarative Icon Einbindung
* [Markdown](https://daringfireball.net/projects/markdown/) : Eine weit verbreitete und vereinfachte Auszeichnungssprache für Web
* [Sass](https://sass-lang.com/) : CSS-Präprozessor mit Variablen, Schleifen und vielen anderen Funktionen, die Cascading Style Sheets nicht mitbringen
* [Bootstrap](https://getbootstrap.com/) : CSS Framework mit Mobile-First Ansatz.
* [JQuery](https://jquery.com//) : Javascript Bibliothek für die Bearbeitung von DOM und andere Utitlities.
* [Google Fonts](https://fonts.google.com/) : Web Fonts einfach einbinden.
* [Liquid](https://shopify.github.io/liquid/) : Templatesprache für die Erstellung von Html Seiten
* [Ruby](https://www.ruby-lang.org/de/) : Basis-Framework von Jekyll
