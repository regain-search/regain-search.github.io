---
title: "Terminologie"
---

[English translation](/en/terminology/)

Terminologie
============

Diese Seite enthält Kurzbeschreibungen von Begriffen rund um regain und Suchmaschinen.


Analyzer
--------

Wenn der [Crawler](/de/components/crawler/) ein Dokument gefunden und seinen Text extrahiert hat, dann speichert er diesen Text im [Suchindex](/de/components/search_index/) mit Hilfe von [Lucene](/de/project_info/used_libraries/).

Lucene extrahiert die einzelnen Wörter aus dem Text. Bevor das Wort dann in den Index kommt, wird es mit Hilfe eines **Analyzers** in seine Grundform gebracht. Dadurch liefert eine Suche nach `Baum` auch Dokumente, die das Wort `Bäume` enthalten.


Partielle Indexierung
---------------------

Die Aktualisierung eines Suchindex mit dem Crawler muß nicht komplett für alle Datenquellen erfolgen. Dokumente auf bestimmten Netzlaufwerken oder Webseiten können beispielsweise stündlich aktualisiert werden, andere hingegen nur wöchentlich.


Stopword-Liste
--------------

Die **Stopword-Liste** legt fest, welche Wörter _nicht_ im [Suchindex](/de/components/search_index/) gespeichert werden sollen. [Stoppworte](http://de.wikipedia.org/wiki/Stoppwort) sind Wörter, die sehr häufig in Texten vorkommen, aber nicht sinntragend sind. Die Aufnahme dieser Wörter würde nur den Index unnötig vergrößern und gleichzeitig keine Trennschärfe für die Suche liefern.

Typische Stopwords können sein: 
  * Präpositionen: ab, an, außer, bei, bis, statt, trotz, von, vor...
  * Pronomen: alle, dein, der, dich, du, man, sie, ...
  * Artikel: der, die, das, ein, eine, eines, ...
  * Konjunktionen: und, oder, ...

Die Stopword-Liste wird im [&lt;stopwordList&gt;-Tag](/en/config/crawlerconfiguration_xml/#stopwordlist-tag) der `CrawlerConfiguration.xml` angegeben.
