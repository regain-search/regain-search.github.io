---
title: "Konfiguration"
---

[English translation](/en/config/)

Konfiguration
=============

Es gibt mehrere Dateien, mit deren Hilfe man das Verhalten oder das Aussehen von regain steuern kann.

Konfiguration des [Crawler](/de/components/crawler/)s:

  * Die `log4j.properties` enthält alle Einstellungen zum Logging. Hier stellen Sie die Granularität, das Format und den Ort ihrer Log-Dateien ein. Details siehe [log4j-Documentation](http://jakarta.apache.org/log4j/docs/manual.html).
  * Die [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) enthält alle Einstellungen des [Crawler](/de/components/crawler/)s.

Konfiguration der [Suchmaske](/de/components/search_mask/):

  * Die `web.xml` bestimmt, wo sich die Konfigurationsdatei `SearchConfiguration.xml` befindet. Standardmäßig wird die Konfigurationsdatei in `../conf/regain/SearchConfiguration.xml` gesucht. Wenn Ihr Tomcat-Verzeichnis `c:\Programme\jakarta-tomcat` ist, dann müssen Sie die `SearchConfiguration.xml` in dem Verzeichnis `c:\Programme\jakarta-tomcat\conf\regain` ablegen. Wenn Sie die Konfigurationsdatei an anderer Stelle ablegen möchten, öffnen Sie die `web.xml` und ändern Sie den Init-Parameter `searchConfigFile`.  

     Siehe [Wie man die Fehlerursache findet](/de/config/howto_find_error_cause/), wenn Sie unverständliche Fehlermeldungen erhalten.
  * Die [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) enthält die eigentliche Konfiguration der [Suchmaske](/de/components/search_mask/).

Siehe auch: [Desktop-Installation](/de/installation/desktop/)
