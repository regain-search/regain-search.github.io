---
title: "Crawler"
---

[English translation](/en/components/crawler/)

Crawler
=======

Der **Crawler** ist das Programm, das den [Suchindex](/de/components/search_index/) erstellt. Dieser Index wird von der [Suchmaske](/de/components/search_mask/) benötigt, um schließlich Suchen durchführen zu können.

Er durchsucht die in der Konfigurationsdatei [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) angegebenen Verzeichnisse und Webseiten nach Dokumenten. Bei jedem Dokument, das noch nicht im Index ist, wird mit Hilfe des passenden [Präparators](/de/components/preparator/)  der eigentliche Text extrahiert, welcher dann in den Index aufgenommen wird.

Technisch gesehen ist der Crawler eine Java-Stand-Alone-Applikation (`regain-crawler.jar`), die auf der Konsole läuft, also ohne graphische Benutzeroberfläche. Er kann damit also auch automatisiert gestartet werden, beispielsweise durch einen cron-Job. 

Bei der [Desktop-Suche](/de/project_info/variant_comparison/) wird der Crawler in regelmäßigen Abständen gestartet, er muss also nicht von Hand aufgerufen werden. Dies kann in der Einstellungen-Seite oder direkt in der [DesktopConfiguration.xml](/de/config/desktopconfiguration_xml/) eingestellt werden. Bei der Server-Suche muss der Crawler von Hand aufgerufen werden. Weitere Details zu den Unterschieden der beiden Varianten siehe [Vergleich der regain-Varianten](/de/project_info/variant_comparison/).

Der Crawler muss in dem Verzeichnis aufgerufen werden, in dem er installiert wurde, sonst kann er nicht auf seine Ressourcen (log-Verzeichnis, [Präparatoren](/de/components/preparator/), etc) zugreifen. Unter Windows also beispielsweise so:

    c:
    cd C:\Programme\regain\crawler
    java -jar regain-crawler.jar

**Tipp:**
Der Crawler muß nicht unbedingt auf dem Rechner laufen, auf dem die Servlet-Engine mit der [Suchmaske](/de/components/search_mask/) ausgeführt wird. Man könnte also (zumindest teilweise) die Indizierung mit den umfangreicheren [Präparatoren](/de/components/preparator/#liste-der-präparatoren) unter Windows realisieren...
