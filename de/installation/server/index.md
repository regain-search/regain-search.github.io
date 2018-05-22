---
title: "Installation der Server-Variante"
---

[English translation](/en/installation/server/)

Installation der Server-Variante
================================

Die regain Server-Suche besteht aus zwei getrennten Anwendungen: Dem [Crawler](/de/components/crawler/) und der [Suchmaske](/de/components/search_mask/). Der Crawler hat die Aufgabe, den Suchindex zu erstellen. Die Suche führt auf dem fertigen Index Suchen aus und stellt das Ergebnis dar.


Installation des Crawlers
-------------------------

  - Laden Sie die regain Server-Suche von der [Download-Seite](http://regain.sourceforge.net/download.php) herunter und entpacken Sie sie.
  - Legen Sie ein Programmverzeichnis an, z.B. `c:\Programme\regain\crawler`. 
  - Kopieren sie den Inhalt des Verzeichnisses `regain\runtime\crawler` aus der heruntergeladenen Zip-Datei in das Programmverzeichnis.
  - Ändern Sie die Datei [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) nach Ihren Bedürfnissen.
  - Erstellen Sie das Verzeichnis, in dem der Index erstellt werden soll, z.B. `c:\Programme\regain\crawler\searchindex`. Dies wird aus Sicherheitsgründen nicht vom Crawler erledigt.
  - Erstellen Sie das Verzeichnis, in dem die Logfiles erstellt werden sollen, z.B. `c:\Programme\regain\crawler\log`.


Starten des Crawlers
--------------------

Öffnen Sie die Konsole (Unter Windows: Eingabeaufforderung) und wechseln Sie in das Verzeichnis, in dem Sie den Crawler installiert haben:

    c:
    cd c:\Programme\regain\crawler

Starten Sie den Crawler von der Konsole mit folgendem Befehl:

    java -jar regain-crawler.jar

Dabei können folgende Parameter angegeben werden:
  * `--help`: Zeigt die möglichen Aufrufparameter.
  * `-forceNewIndex`: Erzwingt die Erstellung eines neuen Index. Anderenfalls wird versucht, einen bereits bestehenden Index zu aktualisieren.
  * `-retryFailedDocs`: Wenn dieser Parameter gesetzt ist, dann versucht regain, auch jene Dokumente neu zu indizieren, die beim letzten Mal nicht indiziert werden konnten. Normalerweise werden nur die Dokumente neu indiziert, die seit dem letzten Indizierungsversuch geändert wurden. Dieser Parameter macht also nur Sinn, wenn Sie an der Konfiguration der [Präparatoren](/de/components/preparator/) etwas verändert haben, denn sonst können diese Dokumente wieder nicht indiziert werden und dies kostet nur unnötig Zeit.
  * `-onlyEntries <WhitelistEintrag1>,< WhitelistEintrag2>`: Die Liste der Whitelist-Einträge, die bearbeitet werden sollen. Alle anderen Einträge in der [Weißen Liste](/de/features/white_and_black_list/) werden zwar im Index belassen, jedoch nicht aktualisiert.
  * `-config <Dateiname>`: Gibt die zu nutzende Konfigurationsdatei an. Default ist: `CrawlerConfiguration.xml`.
  * `-logConfig <Dateiname>`: Gibt die zu nutzende Logging-Konfigurationsdatei an. Default ist: `log4j.properties`.
  * `-Xmx`: maximale Heapsize für die virtuelle Maschine z.B. `-Xmx512M`
  * `-Xss`: maximale Stacksize für die virtuelle Maschine z.B. `-Xss20M` (empfehlenswert bei großen Dokumenten, vielen Termen/Links)

**Achtung** Alle relativ konfigurierten Pfade (Index, Log) gehen immer vom Startverzeichnis aus (dem Verzeichnis, in welchem obiger Aufruf ausgeführt wurde).

Beispiel mit Parametern:

    java -jar regain-crawler.jar -config HomepageConfig.xml


Installation der Suche
----------------------

  - Installieren Sie Jakarta Tomcat 3.2.3 oder höher. Tomcat bekommen Sie auf der [Tomcat-Seite](http://jakarta.apache.org/tomcat). Selbstverständlich können Sie auch eine andere Servlet-Engine verwenden, wie z.B. [Jetty](http://jetty.mortbay.org/jetty) oder [Glassfish](http://glassfish.dev.java.net/public/downloadsindex.html). Dies könnte helfen, falls Sie bei der Verwendung von Tomcat Probleme mit Zeichensätzen haben.
  - Kopieren Sie die Datei `regain.war` in das Tomcat-Unterverzeichnis `webapps`. Sie befindet sich in der heruntergeladenen Zip-Datei im Verzeichnis `regain\runtime\search\webapps`.
  - Kopieren Sie die Datei `SearchConfiguration.xml` in das Tomcat-Unterverzeichnis `conf\regain`. Sie befindet sich in der heruntergeladenen Zip-Datei im Verzeichnis `regain\runtime\search\conf\regain`. Bei Verwendung von Glassfish und der Standarddomain domain1 erstellen Sie unter `GLASSFISHINSTDIR\domains\domain1\applications\` das Verzeichnis `conf\regain\`.
  - Ändern Sie die Datei [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) und stellen Sie ein, wo sich das Index-Verzeichnis befindet, z.B. `c:\Programme\regain\index`.


Starten der Suche
-----------------

Starten Sie Tomcat. Führen Sie dazu `startup` im Tomcat-Unterverzeichnis `bin` aus.