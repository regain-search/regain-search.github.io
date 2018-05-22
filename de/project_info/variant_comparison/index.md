---
title: "Vergleich der regain-Varianten"
---

[English translation](/en/project_info/variant_comparison/)

Vergleich der regain-Varianten
==============================

Es gibt zwei Varianten von regain: Die **Desktop-Suche** und die **Server-Suche**.

Funktionale Unterschiede
------------------------

Die **Desktop-Suche** ist für diejenigen gedacht, die regain auf ihrem Arbeitsplatzrechner nutzen wollen oder regain einfach mal ausprobieren möchten. Die **Server-Suche** ist für Administratoren eines Webservers gedacht, die eine Suche in ihre Webseite oder Intranetseite integrieren wollen. Wobei diese Suche auch Dokumente umfassen kann, die nicht über den Webserver erreichbar sind. So ist es z.B. möglich, eine Suche über Netzlaufwerke anzubieten.

Die folgende Tabelle zeigt die Unterschiede dieser beiden Varianten:

| | regain Desktop-Suche | regain Server-Suche |
| --- | --- | --- |
| Beste Wahl für Einsteiger | ![yes](/images/yes.png) | ![no](/images/no.png) |
| regain [Crawler](/de/components/crawler/) | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| regain [Suchmaske](/de/components/search_mask/) | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Komplette Konfiguration des [Crawler](/de/components/crawler/) über eine XML-Datei | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Einfache Konfiguration des [Crawler](/de/components/crawler/)s über eine Web-Oberfläche | ![yes](/images/yes.png) | ![no](/images/no.png) |
| Komplette Konfiguration der [Suchmaske](/de/components/search_mask/) über eine XML-Datei | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Anpassbares Aussehen der [Suchmaske](/de/components/search_mask/) durch JSPs | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Integrierter Webserver | ![yes](/images/yes.png) | ![no](/images/no.png) |
| Lässt sich in einer Servlet-Engine (z.B. Tomcat) betreiben | ![no](/images/no.png) | ![yes](/images/yes.png) |
| Integration in die (Windows-)Task-Bar | ![yes](/images/yes.png) | ![no](/images/no.png) |

Technische Unterschiede
-----------------------

Im Kern sind beide Varianten gleich. So enthalten beide den [Crawler](/de/components/crawler/), der benötigt wird, um einen [Suchindex](/de/components/search_index/) zu erstellen, sowie die [Suchmaske](/de/components/search_mask/), die benötigt wird, um auf einem Suchindex zu suchen. Auch die Konfiguration der beiden Varianten erfolgt über den gleichen Weg: Die XML-Dateien [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) und [SearchConfiguration.xml](/en/config/searchconfiguration_xml/), wobei die Desktop-Suche eine Web-Oberfläche bereitstellt, die die wichtigsten Einstellungen in diese Dateien einträgt.

Bei der **Desktop-Suche** kommt noch ein kleines Programm hinzu, das die beiden Teile verwaltet. Dieses Programm integriert sich in die Task-Leiste und startet automatisch den Crawler, so dass der Suchindex in regelmäßigen Abständen oder bei einer Änderung der Konfiguration automatisch aktualisiert wird. Außerdem stellt es den Webserver, den die Suchmaske benötigt, um zu funktionieren.

Bei der **Server-Suche** ist der Crawler ein eigenständiges Programm, das der Administrator von Hand (bzw. automatisiert) aufrufen muss, damit der Suchindex aktualisiert wird. Außerdem muss der Admistrator die Suchmaske in einer Servlet-Engine laufen lassen. Der Webserver wird hier nicht von regain mitgeliefert.

Technisch gesehen ist die **Desktop-Suche** eine Stand-Alone-Anwendung. Also eine Anwendung, die -- abgesehen von Java -- keine weiteren Programme benötigt, um zu funktionieren. Die **Server-Suche** teilt sich einerseits in den Crawler, welcher eine Stand-Alone-Kommandozeilen-Anwendung ist, und andererseits in die Suchmaske, die ein .war-Archiv ist und in eine Java-Servlet-Engine (wie z.B. Tomcat) integriert werden muss.
