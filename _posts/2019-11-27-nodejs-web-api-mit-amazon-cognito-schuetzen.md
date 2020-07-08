---
tags: [webentwicklung ]
title: NodeJS - Web API mit Amazon Cognito schützen
---
Die Authentifizierung eines Benutzers ist ein zentraler Bestandteil jeder modernen und sicheren Softwarelösung. AWS bietet mit dem Service Cognito einen zuverlässigen und skalierbarten Identity-Dienst.
 
Die Art und Weise der Anbindung ist vielseitig und flexibel. Den "Standard" Fall einer Authentifizierung und Schutz der existierenden API's einer Web-Lösung kann man wie unten stehend exemplarisch umsetzen.

### 1. Amazon Cognito Benutzerpool vorbereiten

* **Benutzerpool anlegen:** Auf der AWS Managementkonsole in die Verwaltung für `AWS Cognito` wechseln und dort einen neuen Benutzerpool (achtung  kein Identitätenpool) mit minimalen Einstellungen anlegen.
* **App-Client anlegen:** Nach der Erstellung des Benutzerpools für das erstelle Benutzerpool unter dem Navigationseintrag `App-Clients` eine Anwendung unter der Angabe eines App-Namens anlegen und speichern.
* **App-Client-Settings:** Nach der Erstellung des App-Clients stellen Sie die Einstellungen für den App-Client wie in der Abbildung dargestellt ein. Hintergrund dieser Anpassung ist die Aktivierung von OAuth2 und die Zulassung dieser Abläufe.  

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/web-api-nodejs-aws-cognito/appclient-settings.png" class="img-fluid center-block border border-dark"  />
</div>

* **Domäne für App-Client anlegen**: Unter `App-Integration > Domännamen` eine gültige und freie domäne für die Apps angeben und speichern.

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/web-api-nodejs-aws-cognito/app-integration-domain-anlegen.png" class="img-fluid center-block border border-dark"  />
</div>

* **Gehostete Benutzeroberfläche starten und testen**: Unter App-Client-Einstellungen relativ weit unten ist ein Link platziert zum Aufrufen der gehosteten Benutzeroberfläche für die Benutzeranmeldung und -registrierung. Diese Oberfläche sollte aufrufbar und funktional sein.

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/web-api-nodejs-aws-cognito/app-integration-hostet-login-page.png" class="img-fluid center-block border border-dark"  />
</div>


* **Testbenutzer anlegen:** Unter dem Navigationseintrag `Benutzer und Gruppen` einen Testbenutzer anlegen und aktivieren. Dieser Benutzer dienst später für die Tests und Zugriff auf die geschützten Urls Ihrer Anwendung. Hierzu nutzen wir exemplarisch die Software `postman`.

* **Benutzerpool-Id und Benutzerpool-Region:** Notieren Sie sich diese zwei Angaben aus Ihren Benutzerpool-Einstellungen. Diese zwei Angaben habe ich aus der Abbildung unkenntlich gemacht.

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/web-api-nodejs-aws-cognito/aws-cognito-benutzerpool-id-region.png" class="img-fluid center-block border border-dark"  />
</div>

Versuchen Sie an dieser Stelle möglichst Minimal-Einstellungen vorzunehmen. Diese Schritte sollten somit auch ausreichen, damit eine Kommunikation er von Ihnen erstellen Web-API in Express mit AWS sauber funktioniert.

### 2. npm Projekt mit typescript Unterstützung vorbereiten

Als erstes legen wir ein neues npm Projekt an.

<kbd>> mkdir example-nodejs-express-api-aws-cognito</kbd>
<br/>
<kbd>> cd example-nodejs-express-api-aws-cognito</kbd>
<br/>
<kbd>> npm init -y</kbd>

Damit der Code in Typescript geschrieben werden kann, aktiviere ich typescript für die Anwendung.

<kbd>> npm install typescript @types/typescript --save-dev</kbd><br/>
<kbd>> tsc --init</kbd>

Die vom System erzeugte `tsconfig.json` Datei habe ich auf das Nötigste reduziert. Änderungen in der `Ordnerstruktur` des Projektes und Anpassungen in der `package.json` Datei können Sie aus der Github-Repository entnehmen.

### 3. Benötigte npm-Module installieren

in diesem Beispiel setzei ch drei npm-Module ein: 

* `express` für die Bereitstellung der Http-Dienste 
* `express-jwt` middleware zum Validieren von JsonWebToken (JWT)
* `jwks-rsa` eine Bibliothek zum empfangen von mit RSA signierten Schlüssel von einem JWKS (JSON Web Key Set) Endpunkt
* `dotenv` die Bibliothek zum Laden der in der `.env` definierten Variablen über `process.env`

<kbd>> npm install dotenv express express-jwt jwks-rsa --save</kbd>

Die index.ts Datei schaut dann wie folgt aus: 
<script src="https://gist.github.com/behuf/952cd07be2ac14ddf6f37be48ebe3caa.js"></script>




### Test mit Postman

um den Zugriffsschutz zu testen, nutze ich `postman`. Hierzu muss neben der Angabe der Test-Url ein Authorization-Token erstellt und mit dem Request übergeben werden.

Hierzu sind folgende Angaben im Fenster für Access Token nötig:

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/web-api-nodejs-aws-cognito/get-access-token-with-postman-over-aws-cognito.png" class="img-fluid center-block border border-dark"  />
</div>
<br>

Die Besonderheit an dieser Stelle ist die Url für den Aufruf des gehosteten Anmeldungsseite für die App-Client. In diesem Beispiel "beispiel-api".

<kbd>https://beispiel-api.auth.`{AWS_Region}`.amazoncognito.com/login</kbd>

Nach dem Klick auf Request Token, sollte die gehostete Anmeldeseite von AWS Cognito erscheinen. In diesem Fenster muss dann die in Cognito hinterlegten Zugangsdaten (Diese müssen Sie noch in Ihrem Benutzerpool anlegen) eingeben und sich anmelden.

Die geschützte Url `http://localhost:3000/about` sollte nur mit einem gültigen Access Token ein Ergebnis zurückliefern.

Im Request Object `req` wird zudem automatisch das verifizierte `user`-object bereitgestellt.

<div class="col d-flex align-items-center justify-content-center">
    <img src="/assets/images/posts/web-api-nodejs-aws-cognito/aws-cognito-express-request-user-object.png" class="img-fluid center-block border border-dark"  />
</div>
<br>

### Quellcode

Den vollständigen Code finden Sie unter [example-nodejs-express-api-aws-cognito](https://github.com/behuf/example-nodejs-express-api-aws-cognito)

## Weblinks

* [OAuth2](https://oauth.net/2/) : Protokoll für Benutzer-Autorisierung
* [OpenID Connect](https://openid.net/connect/) : Authentifizierungsschicht, die auf dem Autorisierungsprotokoll OAuth 2.0 basiert.
* [Identity Server 4](https://identityserver.io/) : Identity und Authorization Bibliothek auf .NET Basis
* [oidc-provider](https://github.com/panva/node-oidc-provider) : Identity und Authorization Bibliothek auf Node.js Basis
* [Auth0](https://auth0.com/de/) : Dienstanbieter und -hoster für Authentifizierung in eigenen Softwareprodukten
* [Amazon Cognito](https://aws.amazon.com/de/cognito/) : Dienstanbieter Authentifizierung in eigenen Softwareprodukten
* [Azure App Center Auth](https://docs.microsoft.com/en-us/appcenter/auth/) : Dienstanbieter für Authentifizierung in eigenen Softwareprodukten
* [Google Identity](https://cloud.google.com/identity) : Eine einheitliche Plattform für Identitäts-, Zugriffs-, Anwendungs- und Geräteverwaltung
* [Begriffsklärung](https://www.datenschutzbeauftragter-info.de/authentisierung-authentifizierung-und-autorisierung/) : Authentifizierung vs. Autorisierung