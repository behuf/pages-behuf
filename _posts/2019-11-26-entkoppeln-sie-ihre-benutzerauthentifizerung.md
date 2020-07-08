---
tags: [webentwicklung ]
title: Entkoppeln Sie Ihre Benutzerauthentifizierung
---
Die Authentifizierung eines Benutzers ist ein zentraler Bestandteil jeder modernen und sicheren Softwarelösung.

Das Thema hat sich ebenso in den letzten Jahren entscheidend weiterentwickelt. Gerade bei Weblösungen und serviceorientierten Softwarearchitekturen steht man als Entwickler vor grundlegenden Pflichtanforderungen und Erfordernissen, wenn es um Benutzeranmeldung und Authentifizierung geht.

Die Fragen und die zu lösenden Problemstellungen für die Authentifizierung eines Benutzers, Verwalten der angemeldeten Benutzer und Einbindung von verschiedenen Anbietern wie Google, Apple und ähnliches stellt sich unabhängig von der zu lösenden Softwarelösung und muss immer wieder neu erdacht und auch umgesetzt werden. Im Grunde müssen alle Dienste und Systeme in ähnlicher Weise die Frage nach Benutzeranmeldung lösen.

Einige Anforderungen aus diesem Bereich könnte man wie folgt auflisten:

1. Benutzer muss sich optional registrieren können
2. Anmeldung des Benutzers
3. Sicherheitsrelevante Themen wie die Verifizierung der Echtheit des Benutzers (Stichwort: Zwei-Faktoren-Authentifzierung oder Email-Echtheitsverifizierung)
4. Password-Vergessen Funktion
5. Einbindung und Integration von Benutzeranmeldungen von sozialen Netzwerken und ähnlichen Diensten (Google, Amazon, Facebook usw.)
6. Verwalten und Administration von angemeldeten Benutzern
7. Geräte-unabhängige Authentifizierungsinfrastruktur. (Mobile First Ansatz)
8. Zeitgemäße Infrastruktur und Einhaltung der neuesten sicherheitsrelevanten Richtlinien und Konzepte (Stichwort: OAuth, OpenID Connect, zeitgemäße Verschlüsselung usw.)

um hier nur einige Themen zu nennen. Dieses Themenfeld in die Tiefe gedacht, kann ebenso auch komplex werden und umfangreiche Ausmaße annehmen, wenn es um verteile Systeme geht und auch darum die neuesten Technologien zum Einsatz zu bringen.

Es wäre also wichtig an dieser Stelle  diesen Bereich autark von der zu lösenden Software zu betrachten. Typischerweise sollte es egal sein, welche Software einen authentifizierten Benutzer benötigt. Die Dienststelle für die Benutzer-Authentifizierung sollte als ein separates "Modul" bzw. Dienst diese Aufgabe übernehmen. Die Softwaremodule, die diesen Dienst in Anspruch nehmen wollen bzw. ihre Funktionalität nur authentifizierten Benutzern zur Verfügung stellen wollen, müssen dann nur noch bei der Authentifizierungsstelle die "Echtheit" der ihnen übergebenen "Eintrittskarte" des Benutzers erfragen, sofern nötig. Somit lässt sich die Anmeldung separat behandeln und muss nicht für jede neu zu entwickelnde Softwarelösung neu erdacht und entwickelt werden. **Die Grundprämisse in diesem Architekturansatz ist das Vertrauensverhältnis zwischen den `einzelnen Softwaremodulen` und die `Authentifizierungsstelle`.**

Dieser Ansatz der Entkoppelung lässt sich vereinfacht wie folgt visuell darstellen:

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/benutzerauthentifizierung/diagramm-benutzerauthentifizierung.png" class="img-fluid center-block"  />
</div>

Bei den Softwaremodulen `Zeiterfassung` und `Abrechnung` handelt es sich um zwei autark und voneinander unabhängigen Softwaremodulen mit separaten Datenbanksystemen. Jedoch und das ist der entscheidender Punkt, vertrauen sie jeweils derselben Authentifizierungsstelle bzw. -dienst. Ein Benutzer, der sich über das Module `Benutzeranmeldung` einloggt, bekommt nach erfolgreicher Verifizierung ein "Ticket" übergeben. Mit diesem Ticket kann sich der Benutzer sowohl in der Zeiterfassung als auch in der Abrechnung anmelden und mit den Softwareprodukten arbeiten, obwohl diese zwei Systeme voneinander nichts wissen.

## Basistechnologie und mögliche Implementierungsansätze

Technologisch betrachtet kann die `OAuth2` in der Kombination mit `OpenId Connect` als eine Basistechnologie für einen solchen zentralen und integrativen Authentifizierungsansatz genutzt werden. Es gibt hierzu auch für unterschiedliche Entwicklungsplattformen bereits gute und bewährte Implementierungen und Bibliotheken, die genutzt und in Softwareprojekten integriert werden können.

Ebenso ist es wichtig zwischen der `Authentifizierung` und `Autorisierung` eines Benutzers zu unterscheiden. Während die Authentifizierung sich mit der reinen "Identitätsprüfung" befasst, geht es bei der Autorisierung um Berechtigungsprüfungen innerhalb einer Softwarelogik für einen bereits authentifizierten Benutzer. Der in diesem Artikel beschriebener Ansatz beschränkt sich ausschließlich auf die Authentifizierung eines Benutzers und behandelt somit nicht die Autorisierung.

## Auslagern der Implementierung

Auch die Idee der technologischen Auslagerung der Benutzerauthentifizierung bei den entsprechenden "Providern" ist ein denkbarer Ansatz. Eine quasi Outsourcing dieser Idee. Die Integration von "fertigen" Lösungen bringt sehr viele Vorteile mit sich und macht Sie in der Entwicklung effizienter und hilft Ihnen dabei, sich auf Ihre Kernkompetenz und die eigentliche Softwarelogik zu konzentrieren. Es gibt hierzu zahlreiche Anbieter, die Cloud-Lösungen anbieten. Die meines Erachtens zwei wichtigsten und mir bekannten Systeme und Anbieter hab ich unten verlinkt. Mutig behaupte ich persönlich, dass der Ansatz der ausgelagerten und gehosteten Authentifizierung in den Softwarelösungen der Zukunft durchsetzen wird.

## Weblinks

* [OAuth2](https://oauth.net/2/) : Protokoll für Benutzer-Autorisierung
* [OpenID Connect](https://openid.net/connect/) : Authentifizierungsschicht, die auf dem Autorisierungsprotokoll OAuth 2.0 basiert.
* [Identity Server 4](https://identityserver.io/) : Identity und Authorization Bibliothek auf .NET Basis
* [oidc-provider](https://github.com/panva/node-oidc-provider) : Identity und Authorization Bibliothek auf Node.js Basis
* [Auth0](https://auth0.com/de/) : Dienstanbieter und -hoster für Authentifizierung in eigenen Softwareprodukten
* [Amazon Cognito](https://aws.amazon.com/de/cognito/) : Dienstanbieter Authentifizierung in eigenen Softwareprodukten
* [Azure App Center Auth](https://docs.microsoft.com/en-us/appcenter/auth/) : Dienstanbieter für Authentifizierung in eigenen Softwareprodukten
* [Google Identity](https://cloud.google.com/identity) : Eine einheitliche Plattform für Identitäts-, Zugriffs-, Anwendungs- und Geräteverwaltung
* [Begriffseklärung](https://www.datenschutzbeauftragter-info.de/authentisierung-authentifizierung-und-autorisierung/) : Authentifizierung vs. Autorisierung.