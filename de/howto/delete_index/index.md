---
title: "How-To: Erstellung eines komplett neuen Index"
---

[English translation](/en/howto/delete_index/)

How-To: Erstellung eines komplett neuen Index
=============================================

Bei Änderungen an der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) kann es in Ausnahmefällen sein, dass eine Aktualisierung des [Suchindex](/de/components/search_index/) nicht ausreicht, um die Änderungen wirksam zu machen.

Dies ist immer dann der Fall, wenn das Dokument sich nicht verändert hat, jedoch die Einstellungen so verändert wurden, dass dasselbe Dokument anders im Index abgelegt wird. Dies gilt beispielsweise für die Schaffung neuer [Zusatzfelder](/de/features/auxiliary_fields/) oder Änderungen von [Präparator](/de/components/preparator/)-Einstellungen.


Vorgehen bei der Desktop-Variante
---------------------------------

Bei der **Destop-Variante** von regain, müssen Sie in diesem Fall den Index löschen.

So löschen Sie den Index:
  - Beenden Sie regain.
  - Löschen Sie das Indexverzeichnis manuell.
  - Starten Sie regain neu.

regain erstellt nun einen neuen Index.


Vorgehen bei der Server-Variante
--------------------------------

Bei der **Server-Variante** von regain müssen Sie den Index nicht löschen.

Hier reicht es, wenn Sie den [Crawler](/de/components/crawler/) mit dem Parameter `-forceNewIndex` ausführen:

    java -jar regain-crawler.jar -forceNewIndex
