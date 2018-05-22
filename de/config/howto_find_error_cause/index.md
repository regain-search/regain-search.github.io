---
title: "Wie man die Fehlerursache findet"
---

[English translation](/en/config/howto_find_error_cause/)

Wie man die Fehlerursache findet
================================

Wie man den Stacktrace findet
-----------------------------

### Fehler des Crawlers

Der [Crawler](/de/components/crawler/) protokolliert seine Fehler in der Fehler-Log-Datei. Sie befindet sich im Unterverzeichnis `log`.

### Fehler der Suchmaske

Es gibt zwei mögliche Fehlerseiten, die Sie bekommen können, wenn ein Fehler in der [Suchmaske](/de/components/search_mask/) auftritt: Die regain-Fehlerseite oder die Fehlerseite Ihrer Servlet-Engine (z.B. Tomcat).

Die **regain-Fehlerseite** erkennen Sie daran, dass sie das regain-Logo enthält und die Meldung "Fehler bei Suche nach ..." zeigt. Sie enthält einen versteckten Stacktrace, der die genaue Fehlerursache beschreibt. Der Stacktrace befindet sich am Ende der Seite und ist in weißer Schrift auf weißem Grund geschrieben (versteckt), um zu vermeiden, dass der "normale" Benutzer erschrickt. Sie können ihn sichbar machen, indem Sie die gesamte Seite selektieren, beispielsweise durch Drücken von `Strg+A`.

Die **Fehlerseite Ihrer Servlet-Engine** kann unter Umständen einen Stacktrace zeigen, der nur den internen Fehlerort zeigt und nicht, wo der Fehler in regain ausgelöst wurde. Bei der Servlet-Engine "Tomcat" enthält die Fehlerseite gewöhnlich die Nachricht `Error message: Writing results failed`.

Den regain-Stacktrace erkennen Sie daran, dass er `net.sf.regain.RegainException` enthält. Ist das nicht der Fall, dann müssen Sie einen Blick in die Log-Datei werfen, die ihre Servlet-Engine erzeugt hat. Die Log-Datei, die den benötigten regain-Stacktrace enthält, befindet sich im Unterverzeichnis `logs` des Tomcat-Verzeichnisses. Sie hat den Namen `localhost.xyz.log`, wobei `xyz` das heutige Datum ist. Öffnen Sie diese Datei, scrollen Sie bis zum Ende. Dort sollten Sie den regain-Stacktrace finden.

Wie man den Stacktrace liest
----------------------------

Ein StackTrace besteht aus einem oder mehreren Fehlern, die zeigen, welcher Fehler welchen Folgefehler ausgelöst hat. Zu jedem Fehler wird der Aufruf-Stack aufgelistet.

Beispiel:
```
net.sf.regain.util.sharedtag.taglib.ExtendedJspException: Writing results failed
    at net.sf.regain.util.sharedtag.taglib.SharedTagWrapperTag.doEndTag(SharedTagWrapperTag.java:170)
    at org.apache.jsp.search_jsp._jspx_meth_search_check_0(org.apache.jsp.search_jsp:335)
    at org.apache.jsp.search_jsp._jspService(org.apache.jsp.search_jsp:131)
    at org.apache.jasper.runtime.HttpJspBase.service(HttpJspBase.java:97)
    ... 19 more
Caused by: net.sf.regain.RegainException: Loading configuration file failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
    at net.sf.regain.search.config.DefaultSearchConfigFactory.createSearchConfig(DefaultSearchConfigFactory.java:45)
    at net.sf.regain.search.SearchToolkit.loadConfiguration(SearchToolkit.java:433)
    at net.sf.regain.search.SearchToolkit.getIndexConfigArr(SearchToolkit.java:99)
    at net.sf.regain.search.sharedlib.CheckTag.printEndTag(CheckTag.java:64)
    at net.sf.regain.util.sharedtag.taglib.SharedTagWrapperTag.doEndTag(SharedTagWrapperTag.java:164)
    ... 22 more
Caused by: net.sf.regain.RegainException: Parsing XML failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
    at net.sf.regain.XmlToolkit.loadXmlDocument(XmlToolkit.java:79)
    at net.sf.regain.search.config.XmlSearchConfig.<init>(XmlSearchConfig.java:42)
    at net.sf.regain.search.config.DefaultSearchConfigFactory.createSearchConfig(DefaultSearchConfigFactory.java:42)
    ... 26 more
Caused by: java.io.FileNotFoundException: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml (Path could not be found)
    at java.io.FileInputStream.open(Native Method)
    at java.io.FileInputStream.<init>(FileInputStream.java:106)
    at net.sf.regain.XmlToolkit.loadXmlDocument(XmlToolkit.java:75)
    ... 28 more
```

Der Zeilen eines Aufruf-Stacks beginnen mit `at`, was jedoch nur für den Programmierer relevant ist.

Die Fehlermeldungen hingegen können Ihnen Aufschluss über die Fehlerursache geben.

Für das obige Beispiel sind die Fehlermeldungen:
```
ExtendedJspException: Writing results failed
Caused by: RegainException: Loading configuration file failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
Caused by: RegainException: Parsing XML failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
Caused by: FileNotFoundException: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml (Path could not be found)
```

Diese Fehlermeldung sagt aus, dass das Schreiben der Ergebnisseite fehlschlug: die Konfigurationsdatei konnte nicht geladen werden, weil regain sie nicht finden konnte. In diesem Fall müssten Sie also die `SearchConfiguration.xml` an die richtige Stelle kopieren.

Prüfen des Index
----------------

Mit [lukeall](http://www.dotlucene.net/documentation/ToolforAnalyzingLuceneInd.html) bzw. [Lucene Index Toolbox](http://www.getopt.org/luke/) kann man im [Suchindex](/de/components/search_index/) rumstöbern...
