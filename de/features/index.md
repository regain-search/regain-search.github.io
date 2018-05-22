---
title: "Features"
---

[English translation](/en/features/)

Features
========

Diese Seite fasst die wichtigsten **Features** von regain zusammen.


Steckbrief
----------

  * **regain** ist eine anfrageorientierte, effiziente, weitgehend vom Betriebssystem unabhängige Suchmaschine.
  * Mit regain können große Datenmengen indiziert und dann in Sekundenbruchteilen durchsucht werden.
  * Es können Dateien (Text, HTML, XML, Excel, Powerpoint, Word, PDF, RTF, usw.) lokal, auf Netzlaufwerken oder Intranet-Servern sowie ganze HTTP-Webauftritte/Webserver durchsucht werden.
  * regain ist Open Source, damit kostenlos und unterliegt der [Lesser General Public License](http://de.wikipedia.org/wiki/LGPL) (LGPL)
  * Es gibt eine **Desktop-Variante** als  stand alone-Programm für Arbeitsplatzrechner, sowie eine **Server-Variante**. Siehe: [variant_comparison](/de/project_info/variant_comparison/)
  * Das Aussehen der [Suchmaske](/en/components/search_mask/) ist beliebig anpassbar.
  * Für Anwender und Entwickler gibt es eine ausführliche [Dokumentation](http://regain.sourceforge.net/docs.php)
  * Das deutsch- bzw. englischsprachige [Forum](http://forum.murfman.de/de/viewforum.php?f=13) liefert Hilfe bei Problemen und Fragen.
  * regain ist flexibel, anpassbar und erweiterbar.
  * regain nutzt die mächtige [Suchsyntax von Lucene](http://lucene.apache.org/java/2_3_2/queryparsersyntax.html). Damit lassen sich sehr gezielte Suchanfragen formulieren.


Die Suche
---------

  * Regain nutzt die mächtige Suchsyntax von Lucene. Damit ist es möglich, sehr genaue Suchanfragen zu stellen. Details siehe [searching](/de/usage/searching/).
  * [advanced search](/de/features/advanced_search/): Definieren Sie Ihre Suchanfrage noch genauer, um bessere Treffer zu bekommen.
  * [multi_index_search](/de/features/multi_index_search/): Durchsuchen sie über mehrere Indizes gleichzeitig.
  * URL-Rewriting:  Damit können Dokumente z.B. von `file://c:/www-data/intranet/docs` indiziert und im Browser als `http://intranet.murfman.de/docs` angezeigt werden.
  * [file-to-http-bridge](/de/features/file-to-http-bridge/): Stellt die Dateien, die im Index sind, über das http-Protokoll zur Verfügung.


Festlegung des Suchraums
------------------------

Mit regain können Sie sehr genau festlegen, was wann in den [Suchindex](/de/components/search_index/) kommen soll und was nicht.

  * [white and black list](/de/features/white_and_black_list/): Durch eine White List und eine Black List läßt sich der aufzubereitende Suchraum genau eingrenzen.
  * Mehrere Datenquellen pro Index: Ein Suchindex kann Dokumente von verschiedenen Dateisystemen und / oder Webseiten enthalten.
  * Partielle Indexierung: Die Aktualisierung eines Suchindex kann für die verschiedenen Datenquellen zu unterschiedlichen Zeitpunkten erfolgen.


Indexierung
-----------

  * Hot-Deployment: Der Suchindex kann im laufenden Betrieb erweitert oder gewechselt werden - ohne Neustart des Servers.
  * [terminology](/de/terminology/#stopword-liste): Bestimmen Sie Worte, die nicht indexiert werden sollen.
  * [analysis files](/de/features/analysis_files/): Lassen Sie sich alle Zwischenschritte der Indexierung in Dateien ausgeben.
  * Content-Extraktion für HTML: Indexieren Sie bei Ihren HTML-Dokumenten nur den eigentlichen Inhalt, ohne Navigation und Fußleiste.
  * Pfad-Extraktion für HTML: Zeigen Sie den Navigationspfad Ihrer HTML-Seiten bei den Suchergebnissen.
  * Erkennung von Dead Links: Quasi als Abfallprodukt werden alle gefundenen Dead Links (also Links auf nicht mehr vorhandene Dokumente) ausgegeben.
  * [breakpoint](/de/features/breakpoint/): Der [Crawler](/de/components/crawler/) kopiert während der Indexierung regelmäßig den aktuellen Stand des [Suchindex](/de/components/search_index/) in ein gesondertes Verzeichnis. Bricht die Indexierung ab, kann der Crawler auf dem letzten Breakpoint aufsetzen.
  * [auxiliary fields](/de/features/auxiliary_fields/): Der Index kann um weitere Indexfelder erweitert werden.


Erweiterbarkeit und Anpassung
-----------------------------

  * [Präparatoren](/de/components/preparator/): Sie übernehmen die Aufbereitung und Extrahierung von Texten/Informationen aus den verschiedenen Dateiformaten.
  * TagLibrary für die Suche: Hiermit ist die Anpassung der [Suchmaske](/de/components/search_mask/) an Ihr Design besonders einfach.
  * [Konfigurierbarkeit](/de/config/): regain ist weitgehend anpassbar.
  * [access rights management](/de/features/access_rights_management/): Es sorgt dafür, dass ein Benutzer nur Treffer für Dokumente erhält, für die er auch Leserechte hat.
