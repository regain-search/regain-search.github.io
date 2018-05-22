---
title: "Breakpoints"
---

[English translation](/en/features/breakpoint/)

Breakpoints
===========

Der [Crawler](/de/components/crawler/) erzeugt regelmäßig so genannte **Breakpoints**. Dabei wird der aktuelle Stand des [Suchindex](/de/components/search_index/) in ein separates Verzeichnis mit dem Namen `breakpoint` kopiert. Wenn die Aktualisierung des Suchindex abgebrochen wird (z.B. indem der Rechner heruntergefahren wird), dann kann der Crawler beim letzten Breakpoint fortfahren, wenn er das nächste mal gestartet wird und muss nicht von vorne beginnen.


Wie kann ich dieses Feature nutzen?
-----------------------------------

Standardmäßig wird alle 10 Minuten ein Breakpoint erstellt. Sie können dieses Intervall über das `<breakpointInterval>`-Tag in der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) verändern, bzw. die Erstellung von Breakpoints ganz abschalten.
