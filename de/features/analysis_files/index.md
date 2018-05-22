---
title: "Analyse-Dateien"
---

[English translation](/en/features/analysis_files/)

Analyse-Dateien
===============

**Analyse-Dateien** werden vom [Crawler](/de/components/crawler/) erstellt, wenn das `<writeAnalysisFiles>`-Tag in der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) auf `true` gesetzt wurde.

Sie zeigen die einzelnen Verarbeitungsschritte der [Präparatoren](/de/components/preparator/) und helfen dadurch, die Qualität des Index zu prüfen, indem sie zeigen, was genau in den Index gekommen ist.


Wie kann ich dieses Feature nutzen?
-----------------------------------

Setzen sie das `<writeAnalysisFiles>`-Tag in der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) auf `true`.

Nachdem der [Crawler](/de/components/crawler/) fertig durchgelaufen ist, befinden sich die Analyse-Dateien im [Index-Verzeichnis](/de/components/search_index/#das_indexverzeichnis) im Unterverzeichnis `new/analysis` oder `index/analysis`, je nachdem, ob die [Suchmaske](/de/components/search_mask/) den neuen Index bereits übernommen hat.
