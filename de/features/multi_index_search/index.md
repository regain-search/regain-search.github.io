---
title: "Multiindex-Suche"
---

[English translation](/en/features/multi_index_search/)

Multiindex-Suche
================

Mit Hilfe der **Multiindex-Suche** können Sie mehrere Indexe über dieselbe Suchmaske durchsuchen. Die Suchanfrage wird auf alle Indizes losgelassen und die Ergebnisse werden anschließend gemischt. Der dafür zuständige Algorithmus mischt die Ergebnisse so, dass sie nach der Relevanz sortiert bleiben. Bei gleicher Relevanz werden die Ergebnisse "fair" gemischt, d.h. dass von jedem Index irgendwann ein Treffer hineingemischt wird. So wird vermieden, dass erst alle Treffer des einen Index und dann die eines anderen Index aufgelistet werden.

**Verfügbar seit:** Version 1.1 beta 5


Wie kann ich dieses Feature nutzen?
-----------------------------------

Eine Multiindex-Suche wird immer dann vorgenommen, wenn mehr als ein HTTP-Parameter `index` an die Such-JSP-Seite übergeben wird.

Die folgende Anfrage führt eine Multiindex-Suche nach `Test` in den Indexen `docs` und `intranet` durch:

    http://localhost:8020/search.jsp?index=docs&index=intranet&query=Test

Bitte beachten: Alle Indizes müssen in der [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) konfiguriert sein.


Diskussionen im Forum
---------------------

  * [Multiindex-Suche-Lösung konfigurieren](http://forum.murfman.de/de/viewtopic.php?t=100)
  * [gezielte Suche](http://forum.murfman.de/de/viewtopic.php?t=226)
