---
title: "Die wichtigsten Komponenten von regain"
---

[English translation](/en/components/)

Die wichtigsten Komponenten von regain
======================================

Grob betrachtet arbeitet regain folgendermaßen: Der **Crawler** sucht nach Dokumenten, extrahiert ihren Text und speichert diesen in einem **Suchindex**. Mit Hilfe dieses Indexes kann die **Suchmaske** Suchanfragen von Benutzern sehr schnell beantworten. Um den Suchindex zu schreiben und zu nutzen verwendet regain eine Bibliothek namens **Lucene**.

[Lucene](http://lucene.apache.org/) verwaltet sehr effizient Suchindizes für große Datenmengen. Lucene bietet lediglich eine Programmierschnittstelle (API) um einen solchen Suchindex zu erzeugen und darin zu suchen. Was in den Index rein soll, oder wann was gesucht werden soll, muss durch ein anderes Programm bestimmt werden: Zum Beispiel regain.

Die wichtigsten Komponenten von regain sind:
  * [Crawler](/de/components/crawler/) - Er sucht nach Dokumenten un extrahiert deren Text mit Hilfe der [Präparatoren](/de/components/preparator/).
  * [Suchindex](/de/components/search_index/) - Der Suchindex ist eine Sammlung von Dateien, welche von Lucene dazu verwendet werden, Suchanfragen zu beantworten.
  * [Suchmaske](/de/components/search_mask/) - Die Suchmaske zeigt dem Benutzer eine Web-Oberfläche, in die er Suchanfragen eingeben und die Suchergebnisse betrachten kann. Die Webseiten werden Hilfe der [JSP-Seiten der Suchmaske](/de/components/search_mask_jsp_pages/) erstellt.
