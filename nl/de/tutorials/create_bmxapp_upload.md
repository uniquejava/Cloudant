---

copyright:
  years: 2017, 2018
lastupdated: "2017-11-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-11 -->

# Einfache {{site.data.keyword.Bluemix_notm}}-Anwendung für den Zugriff auf eine {{site.data.keyword.cloudant_short_notm}}-Datenbank erstellen: Anwendung hochladen

In diesem Abschnitt des Lernprogramms wird beschrieben, wie Sie eine {{site.data.keyword.Bluemix}}-Anwendung hochladen.
{:shortdesc}

<div id="uploading"></div>

## Verbindung zu {{site.data.keyword.Bluemix_notm}} herstellen

Die erste Task ist das Herstellen einer Verbindung mit {{site.data.keyword.Bluemix_notm}}.

Das [{{site.data.keyword.Bluemix_notm}}-Toolkit](create_bmxapp_appenv.html#toolkits) unterstützt Sie dabei.

Cloud Foundry muss die URL kennen, die für API-Aufrufe verwendet werden soll, z. B. wenn Sie eine Anwendung hochladen.
Das {{site.data.keyword.Bluemix_notm}}-Toolkit verwendet den Befehl `cf api`, um den API-Endpunkt zu verwalten.
Weitere Informationen zum Befehl `cf api` sind
[verfügbar ![Symbol für externen Link](../images/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/docs/cli/reference/cfcommands/index.html#cf_api){:new_window}.

Setzen Sie den folgenden Befehl ab, um Cloud Foundry die zu verwendende URL bereitzustellen:

```sh
bluemix api https://api.ng.bluemix.net
```
{:pre}

Ihre Ausgabe wird ungefähr wie folgt aussehen:

```
Invoking 'cf api https://api.ng.bluemix.net'...

Setting api endpoint to https://api.ng.bluemix.net...
OK

API endpoint:   https://api.ng.bluemix.net
API version:    2.54.0
Not logged in. Use 'bluemix login' to log in.
```
{:codeblock}

Cloud Foundry weiß jetzt, wohin API-Aufrufe zur Verwaltung von Anwendungen gesendet werden sollen.

Der nächste Schritt besteht darin, sich bei Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendungsumgebung anzumelden.
Sie müssen die folgenden Kontodetails angeben:

-   Ihren Benutzernamen, angegeben als Parameter `-u`.
-   Ihr Organisationsname, angegeben als Parameter `-o`.
-   Ihr Bereich, angegeben als Parameter `-s`.

>   **Hinweis**: Die Kontodetails sind in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard verfügbar,
    wenn Sie sich, wie im folgenden Beispiel gezeigt, über einen Web-Browser anmelden:<br/>
    ![{{site.data.keyword.Bluemix_notm}}-Kontodetails suchen](images/img0035.png)

Verwenden Sie einen Befehl ähnlich dem folgenden, um sich bei Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendungsumgebung anzumelden.
Beachten Sie, dass Sie aufgefordert werden, Ihr Kontokennwort einzugeben.

```sh
bluemix login -u Adrian.Warman@uk.ibm.com -o Adrian.Warman@uk.ibm.com -s dev
```
{:pre}

Ihre Ausgabe wird ungefähr wie folgt aussehen:

```
Invoking 'cf login -u Adrian.Warman@uk.ibm.com -o Adrian.Warman@uk.ibm.com -s dev'...

API endpoint: https://api.ng.bluemix.net

Password> 
Authenticating...
OK

Targeted org Adrian.Warman@uk.ibm.com

Targeted space dev
                
API endpoint:   https://api.ng.bluemix.net (API version: 2.54.0)
User:           adrian.warman@uk.ibm.com
Org:            Adrian.Warman@uk.ibm.com
Space:          dev
```
{:codeblock}

## Anwendung hochladen

Das {{site.data.keyword.cloudant_short_notm}} Foundry-Toolkit weiß jetzt, wie es eine Verbindung zur {{site.data.keyword.Bluemix_notm}}-Umgebung herstellt.

Der nächste Schritt besteht darin, die Anwendung selbst hochzuladen.
Details einer {{site.data.keyword.Bluemix_notm}}-Anwendung werden in der [Manifestdatei](create_bmxapp_appenv.html#manifest) bereitgestellt.

Die Manifestdatei für die Lernprogrammanwendung wurde wie [hier](create_bmxapp_createapp.html#essential-files) beschrieben aktualisiert.

Verwenden Sie einen Befehl ähnlich dem folgenden, um sich anzumelden und Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung hochzuladen.

```sh
cf push "Cloudant Python"
```
{:pre}

Eine Folge von Ergebnisnachrichten wird angezeigt.

```
Using manifest file /..../BMXDemo/manifest.yml

Updating app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK
```
{:codeblock}

Das Cloud Foundry-Toolkit hat die Manifestdatei ausfindig gemacht und bereitet den Upload
der Anwendung mithilfe der Verbindungs- und Identifikationsdetails, die Sie [zuvor](#uploading) bereitgestellt haben, vor.

```
Using route Cloudant-Python.mybluemix.net
Uploading Cloudant Python...
Uploading app files from: /..../BMXDemo
Uploading 1.5K, 3 files
Done uploading
OK
Binding service {{site.data.keyword.cloudant_short_notm}} Service 2017 to app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK
```
{:codeblock}

Die Anwendung wurde erfolgreich hochgeladen und eine Verbindung mit der {{site.data.keyword.cloudant_short_notm}}-Datenbankinstanz hergestellt.

```
Starting app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
-----> Downloaded app package (4.0K)
-----> Downloaded app buildpack cache (29M)
-------> Buildpack version 1.5.5
     $ pip install -r requirements.txt
DEPRECATION: --allow-all-external has been deprecated and will be removed in the future. Due to changes in the repository protocol, it no longer has any effect.
       Collecting cloudant==2.3.1 (from -r requirements.txt (line 1))
         Downloading cloudant-2.3.1-py2-none-any.whl (63kB)
       Collecting requests<3.0.0,>=2.7.0 (from cloudant==2.3.1->-r requirements.txt (line 1))
         Downloading requests-2.12.4-py2.py3-none-any.whl (576kB)
       Installing collected packages: requests, cloudant
       Successfully installed cloudant-2.3.1 requests-2.12.4
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
-----> Uploading droplet (30M)

0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App {{site.data.keyword.cloudant_short_notm}} Python was started using this command `python server.py`
```
{:codeblock}

Die Anwendung wird automatisch gestartet.
Beim Start wird geprüft,
ob alle Anforderungen erfüllt sind, indem der Inhalt der [Datei 'requirements.txt'](create_bmxapp_appenv.html#requirements) ausgewertet wird.
Die Anwendung erfordert Zugriff auf die {{site.data.keyword.cloudant_short_notm}}-Bibliothek,
die beim Erstellen der Anwendung [angegeben](create_bmxapp_createapp.html#essential-files) wurde.

Nachdem Sie die Anwendung hochgeladen und gestartet haben,
werden einige Systemprüfungen ausgeführt, um zu bestätigen, dass die Anwendung bezüglich {{site.data.keyword.Bluemix_notm}} ordnungsgemäß ausgeführt wird.

```
Showing health and status for app {{site.data.keyword.cloudant_short_notm}} Python in org Adrian.Warman@uk.ibm.com / space dev as Adrian.Warman@uk.ibm.com...
OK

requested state: started
instances: 1/1
usage: 128M x 1 instances
urls: Cloudant-Python.mybluemix.net
last uploaded: Thu Dec 22 15:58:18 UTC 2016
stack: cflinuxfs2
buildpack: python 1.5.5

     state     since                    cpu    memory          disk           details
#0   running   2016-12-22 03:59:21 PM   0.0%   49.9M of 128M   110.6M of 1G
```
{:codeblock}

## Beispielanwendung testen

Wenn die {{site.data.keyword.Bluemix_notm}}-Anwendungsumgebung das erste Mal erstellt wird,
enthält das Dashboard einen Link in der Spalte `Route` für die Anwendung:<br/>
![Screenshot des Dashboards für die Anwendung](images/img0017.png)

Wenn Sie auf den Link klicken, wird ein Browserfenster geöffnet,
das Daten von der Anwendung anfordert, die am entsprechenden Port empfangsbereit ist.
Die Anwendung reagiert, indem der Inhalt der Protokolldatei zurückgegeben wird,
die beim Start der Anwendung generiert wurde:<br/>
![Beim Start der Lernprogrammanwendung generierte Protokolldatei](images/img0030.png)

Der Inhalt dieser Protokolldatei ist interessant.
Die Start- und Endzeiten sind deutlich hervorgehoben.
Dazwischen zeichnet das Protokoll alle Details auf, während die Verbindungsinformationen
für {{site.data.keyword.cloudant_short_notm}} abgerufen wurden.
Die tatsächlichen Werte der Verbindung sind nicht wichtig.
Das Protokoll zeigt, dass die Lernprogrammanwendung diese Werte finden,
abrufen und verwenden konnte, um ein neues Dokument in der
{{site.data.keyword.cloudant_short_notm}}-Datenbank abzurufen.

### Datenbankdetails bestätigen

Beginnen Sie, indem Sie das {{site.data.keyword.cloudant_short_notm}}-Dashboard öffnen.
Klicken Sie auf das Symbol `Starten` auf der Registerkarte `Verwalten` der
{{site.data.keyword.cloudant_short_notm}}-Serviceseite:<br/>
![Startsymbol auf der {{site.data.keyword.cloudant_short_notm}}-Serviceseite](images/img0036.png)

> **Hinweis**: Wo Sie Ihre {{site.data.keyword.cloudant_short_notm}}-Serviceseite finden,
  ist in den Details im
  [Lernprogramm '{{site.data.keyword.cloudant_short_notm}}-Instanz erstellen' angegeben](create_service.html#locating-your-service-credentials).

Wenn das Dashboard geöffnet wird, können Sie sehen, dass die Anwendung
die Datenbank `databasedemo` erstellt hat:<br/>
![{{site.data.keyword.cloudant_short_notm}}-Dashboard mit der neuen Datenbank](images/img0031.png)

Die Datenbank enthält ein einzelnes Dokument, das von der Anwendung erstellt wurde.
Klicken Sie auf den Datenbanknamen
im Dashboard, um das Vorhandensein des Dokuments zu prüfen.
Eine Liste von Optionen für die Datenbank wird angezeigt.
Wenn Sie die Registerkarte `Alle Dokumente` auswählen,
werden die Details zu einem einzelnen Dokument angezeigt:<br/>
![Einzelnes Dokument in der neuen Datenbank](images/img0032.png)

Wenn Sie den Inhalt des Dokuments sehen möchten,
klicken Sie auf das Symbol `Bearbeiten`, das
die Form eines Bleistifts hat:<br/>
![Details des Dokuments](images/img0033.png)

Wenn der Inhalt des Dokuments angezeigt wird,
können Sie die einzelnen Felder sehen, die von der Lernprogrammanwendung erstellt wurden.<br/>
![Felder im Dokument](images/img0034.png)<br/>
Insbesondere enthält das Feld `rightNow` das Datum und die Uhrzeit der Erstellung des Dokuments.
Dieser Wert entspricht der Uhrzeit, die in der
[Anwendungsprotokolldatei](#testing-the-sample-application) aufgezeichnet wurde.

## Der nächste Schritt

Der nächste Schritt im Lernprogramm besteht darin, [die Anwendung auszuführen und zu warten](create_bmxapp_maintain.html), z. B. wenn Sie die Anwendung starten, stoppen und debuggen.
