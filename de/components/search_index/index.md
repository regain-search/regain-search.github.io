---
title: "Der Suchindex"
---

[English translation](/en/components/search_index/)

Der Suchindex
=============

Im **Suchindex** werden die Daten über die Dokumente so gespeichert, dass bei einer [Suche](/de/components/search_mask/) schnell die Dokumente gefunden werden, die ein bestimmtes Stichwort enthalten. Dank des geschickten Aufbaus des Suchindex, ist eine Suche über viele tausend Dokumente in Sekundenbruchteilen durchführbar.

regain setzt zur [Erstellung](/de/components/crawler/) und für die [Suche](/de/components/search_mask/) auf dem Suchindex [Lucene](http://lucene.apache.org) ein. Lucene speichert die Daten über ein Dokument klassifiziert in getrennten Feldern. Bei der Suchanfrage kann so entschieden werden, welche Felder durchsucht werden sollen.((Via [Clustering Lucene](http://search.blogger.com/?as_q=lucene+terracotta&ie=UTF-8&ui=blg&bl_url=orionl.blogspot.com&x=0&y=0) sind auch extreme Datenbestände hocheffizient verwaltbar!))

Eine Suche nach "`regain extension:pdf`" sucht beispielsweise nach `regain` in den Standardfeldern sowie nach `pdf` im Feld `extension`.

Welche Felder standardmäßig durchsucht werden, wird in der Datei [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) im `searchFieldList`-Tag eingestellt. Standardmäßig sind das die Felder `content`, `title` und `headlines`.


Standardfelder
--------------

regain legt folgende Standardfelder an:
  * `url` - Die URL des Dokuments.
  * `content` - Der von den [Präparatoren](/de/components/preparator/) extrahierte Text des Dokuments. 
  * `title` - Der Titel des Dokuments (wenn der zuständige Präparator einen Titel extrahieren konnte).
  * `summary` - Die Zusammenfassung, die in der Trefferliste gezeigt wird.
  * `headlines` - Überschriften (die im Dokument gefunden wurden).
  * `size` - Die Größe des Dokuments in Bytes (kann nicht durchsucht werden).
  * `last-modified` - Das Datum der letzten Änderung im Format `JJJJ-MM-TT SS:MM` (kann nicht durchsucht werden).
  * `path` - Der Navigationspfad zum Dokument.
  * `groups` - Die Benutzergruppen, die das Dokument lesen dürfen. (Nur bei aktiviertem [Zugriffsrechte-Management](/de/features/access_rights_management/)).
  * [Weitere Felder können hinzugefügt werden](/de/features/auxiliary_fields/). So wird in der Default-Konfiguration das Feld `extension` für die Dateiendung hinzugefügt(z.B. `pdf`).

Wichtig:
  * Bei Fehlern während der [Textextraktion](/de/components/preparator/) wird kein Feld `content` angelegt, sondern stattdessen ein Feld `preparation-error` mit dem Wert `true`.
  * Die Fähigkeiten der beim [Indizieren](/de/components/crawler/) genutzten [Präparatoren](/de/components/preparator/) bestimmen, was letztendlich in die Standardfelder `content`, `title` und `headlines` eingetragen wird!
  * Mit [lukeall](http://www.dotlucene.net/documentation/ToolforAnalyzingLuceneInd.html) bzw. [Lucene Index Toolbox](http://www.getopt.org/luke/) kann man den Index detailliert untersuchen.


Das Indexverzeichnis
--------------------

Im **Indexverzeichnis** legt regain die einzelnen Suchindizes ab. Die Indizes werden in verschiedenen Unterverzeichnissen abgelegt, je nachdem in welcher Phase sie sich in ihrem Lebenszyklus befinden.

regain nutzt die folgenden Unterverzeichnisse:
  * `temp` - Ein Index in diesem Verzeichnis wird gerade vom [Crawler](/de/components/crawler/) verändert.
  * `breakpoint` - In regelmäßigen Zeitabständen erzeugt der Crawler [Breakpoint](/de/features/breakpoint/)s. Falls der Crawler beendet wird, bevor der neue Index fertiggestellt wurde (z.B. beim Herunterfahren des Rechners), dann kann er beim nächsten Start beim letzten Breakpoint fortfahren und muss nicht von vorne beginnen.
  * `new` - Sobald der Crawler den Index fertiggestellt hat, benennt er das Verzeichnis nach `new` um. Dieses Verzeichnis stellt die Schnittstelle zwischen [Crawler](/de/components/crawler/) und [Suchmaske](/de/components/search_mask/) dar. Die Suchmaske prüft regelmäßig, ob es im Indexverzeichnis einen Index im Status `new` gibt. Sobald sie einen solchen Index findet, wechselt sie zu diesem Index, d.h. sie nennt das Verzeichnis nach `index` um. Auf diese Weise ist das **Hot Deployment** umgesetzt.
  * `quarantine` - Falls der Crawler einen Index fertiggestellt hat, dabei jedoch sehr viele Fehler hatte, dann bekommt dieser Index nicht den Status `new`, sondern `quarantine`. Auf diese Weise wechselt die [Suchmaske](/de/components/search_mask/) nicht automatisch auf den fehlerhaften Index. In einem solchen Fall sollten Sie [die Log-Datei prüfen](/de/config/howto_find_error_cause/) und, wenn Sie auf den Index wechseln wollen, das Verzeichnis nach `new` umbenennen.
  * `index` - Dieser Index wird momentan von der Suchmaske verwendet.
  * `backup` - Bevor die Suchmaske auf einen neuen Index wechselt, benennt sie den alten Index nach `backup` um. Falls ein neu erstellter Index fehlerhaft sein sollte, können Sie schnell wieder auf den vorigen Index gewechselt werden, indem Sie das Verzeichnis `backup` nach `new` umbenennen.
