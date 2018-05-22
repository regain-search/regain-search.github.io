---
title: "Die Suchmaske"
---

[English translation](/en/components/search_mask/)

Die Suchmaske
=============

Die **Suchmaske** ist eine Web-Oberfläche, die Suchanfragen entgegennimmt, sie ausführt und die Ergebnisse seitenweise anzeigt. In der **Desktop-Variante** von regain (siehe [variant_comparison](/de/project_info/variant_comparison/)) kann über die Suchmaske auch der [Crawler](/de/components/crawler/) konfiguriert und überwacht werden.

Bevor man mit der Suchmaske etwas suchen kann, muss erst mit Hilfe des [Crawler](/de/components/crawler/)s ein [Suchindex](/de/components/search_index/) erstellt werden.

Technisch gesehen ist die Suchmaske eine Reihe von JSP-Seiten, die eine TagLibrary für die dynamischen Teile nutzen. Diese JSP-Seiten brauchen einen Server, der auf Anfragen wartet und dann die JSP-Seiten ausführt.

Bei der **Server-Variante** von regain muss man die Suchmaske auf einem Webserver mit Servlet-Engine deployen - z.B. [Tomcat](http://jakarta.apache.org/tomcat) oder [Jetty](http://jetty.mortbay.org/jetty). 

Bei der **Desktop-Variante** von regain ist bereits ein solcher Server integriert. Dieser nutzt eine eigens entwickelte, sehr schlanke JSP-Engine, die auf [Simple](http://simpleweb.sourceforge.net) aufbaut. Diese kann jedoch nur TagLib-Tags verarbeiten, keinen in JSPs eingebundenen Java-Code. Dafür hat sie auch eine Größe von nur rund 200kB und nicht von über 10MB, wie bei "echten" Servlet-Engines, was für eine Desktop-Suche einfach zu viel wäre.


JSP-Seiten der Web-Oberfläche
-----------------------------

Die relevanten Dateien der Web-Oberfläche sind:
  * `search.jsp`: Die eigentliche Suchmaske
  * `advancedsearch.jsp`: Die [Erweiterte Suche](/de/features/advanced_search/)
  * `index.jsp` bzw. `..web/searchinput.jsp`: Die Startseite
  * `status.jsp`: Zeigt den Status des [Crawler](/de/components/crawler/)s (nur bei der Desktop-Variante)
  * `config.jsp`: Konfigurationsseite für den [Crawler](/de/components/crawler/) (nur bei der Desktop-Variante)
  * `search_xml.jsp`: XML-Schnittstelle, die diesselben Daten enthält wie `search.jsp`.

Die Dateien liegen bei der Desktop-Variante im Unterverzeichnis `web`, bei der Server-Variante in  `runtime/search/webapps/regain.war`. Siehe [variant_comparison](/de/project_info/variant_comparison/)


Die Tag-Library der Suchmaske
-----------------------------

Die dynamischen Teile der Suchmaske werden von Tags der [Tag-Library](http://de.wikipedia.org/wiki/Tag-Library) von regain gefüllt.

Die Tags, die von dieser Tag-Library bereit gestellt werden sind hier dokumentiert:
  * [Tag-Library-Dokumentation zu regain 1.1](http://regain.sourceforge.net/doc/1.1/tlddoc/index.html)

[add_custom_tag](/de/components/de/howto/add_custom_tag/)

Ausführliche Informationen zum Thema JSP und TagLibs findet man hier:
  * [Tag-Bibliotheken](http://de.wikipedia.org/wiki/Jsp#Tag-Bibliotheken)
  * Sun Developer Network-Server: [JavaServer Pages](http://java.sun.com/products/jsp/jstl/reference/docs/index.html) (englisch).


Parameter der Suchmaske
-----------------------

Die `search.jsp` (und `search_xml.jsp`) versteht folgende [GET-Parameter](http://de.wikipedia.org/wiki/Hypertext_Transfer_Protocol#HTTP_GET):
  * `index` - der Index oder eine Aufzählung von Indexen, wo gesucht wird
  * `query` - die eigentliche Suchanfrage
  * `field.` - Das Präfix `field.` bezieht weitere [Suchfelder](/de/components/search_index/#standardfelder) des Suchindex ein.  

     Z.B. entspricht die URL `...?query=test&field.extension=pdf&field.title=otto`  

     der Anfrage `test extension:"pdf" title:"otto"`.
  * `maxresults` - Anzahl Suchergebnisse pro Seite (Voreinstellung ist `10`).
  * `fromresult` - Index des ersten Suchergebnisses (beginnend bei `0`).
