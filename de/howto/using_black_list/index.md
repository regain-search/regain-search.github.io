---
title: "How-To: Webseiten ohne Seitennavigation indizieren"
---

[English translation](/en/howto/using_black_list/)

How-To: Webseiten ohne Seitennavigation indizieren
==================================================

FIXME: In diesem How-To werden drei Probleme und drei Lösungen sehr durcheinander beschrieben. Dies sollte klarer formuliert und die Lösung dann getrennt gezeigt werden - am besten an Hand von Beispielen.

Ziele
-----

  - Bei der Erstellung des [Suchindex](/de/components/search_index/) die Besonderheiten der einzelnen Bereiche einer Website berücksichtigen. Es soll nur der eigentliche Inhalt indiziert werden, nicht die Navigationslinks oder dir Fußleiste.
  - Die Index-aktualisierung effizient implementieren


Angaben zur Website
-------------------

Website können folgende Strukturen haben:

  - Einige Webseiten haben eine Art pseudo-frameartige Struktur (Pseudo-Frame): In einer `dateiXY.**htm**` sind eigentliche Seiteninhalte abgelegt und sind jeweils mittels in `dateiXY.**asp**` enthaltenen `include=dateiXY.htm`-Anweisungen eingebunden. Die ASP's beinhalten außerdem seitenbezogene Navigationsleisten, die nicht zu indexieren sind.
  - Andere Webseiten beinhalten echte Framestrukturen (echte Frames).
  - Dann gibt es noch ganz normale HTML-Seiten (easyHTML)

Viele der unter 1. aufgeführten Dokumente werden nochmal im PDF-Format als Druckversion im Webprojekt verlinkt.

Andere Dokumente dagegen werden ausschließlich im PDF-Format veröffentlicht.


Lösungsansätze
--------------

  * Die in jeder Webseite enthaltene Texte in Menüs der linken Spalte und der horizontalen Top-Navigation nicht im regain-Index erfassen.
  * Für die unter 1. aufgeführte Webseiten bietet sich an, nur über die `dateiXY.htm` den regain-Crawler loslassen. Damit linke Navigationsspalte und die horizontale Top-Navigation in den gefundene Treffern korrekt, mit den Navigationsleisten angezeigt werden, im regain-Index `.htm`-Endungen durch `.asp` ersetzen.
  * Die Dokumente, die als HTM und PDF vorliegen, werden nur einmal indiziert.
  * Unter 2. und 3. aufgeführte Webprojekte werden webbasiert mit regain-Standardlösung indiziert.

Die Lösung
----------

Es werden mehrere regain-Indizes erstellt:

  - Alle HTML-Webseiten in 'pseudoFrame'-Projekten, die .htm-Endung haben, werden im Dateisystem in den Index übernommen und dann  werden `.htm`'s durch `.asp` ersetzt - realisierbar mit der Methode `createDocument` (Klasse `net.sf.regain.crawler.document.DocumentFactory`) und dem `file:/_`-Präfix wird mit [rewriteRules](/en/config/searchconfiguration_xml/#rewriterules-tag) durch `http://` ersetzt. Siehe auch im Forum: [Dateiendungen bei der Indexerstellung manipulieren](http://forum.murfman.de/de/viewtopic.php?t=171)

  - Dokumente, die nur im PDF-Format angeboten werden, werden mit Hilfe der [White-List und Black-Liste](/de/features/white_and_black_list/) und dem [urlPattern-Tag](/en/config/crawlerconfiguration_xml/#urlpattern-tag) (`\.pdf`) in einem separaten Index erfasst.

  - 'echte Frames' und 'easy HTML'-Webseiten werden webbasiert mit der regain-Standard-Lösung mit urlPattern-Wert `\.htm` indiziert.

Diese Indizes werden dann in der [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) in die regain-Suche eingebunden.


Elegante Lösung mit Ant-Framework
---------------------------------

Setzt voraus, dass für die oben beschriebene regain-Versionen (z.B. mit der modifzierten `createDocument`-Methode) ein Ant-Projekt mit dem target-Element.

```xml
<target name="index-aktualisieren">
  <exec executable="pseudoFrameIndex.bat"/>
  <exec executable="PDFDocsIndex.bat"/>
  <exec executable="easyHTMLundechteFramesIndex.bat"/>
</target>
```

erstellt wird. In der `pseudoFrameIndex.bat` wird mit 


    %Java_Home%\bin\java -jar regainpseudoFrame-crawler.jar -config CrawlerConfiguration''XX''.xml

eine Crawler-Instanz mit der angepassten `createDocument` gestartet. Alle drei Crawler-Instanzen, die mit den `exec`-Tasks gestartet werden, haben jeweils eine eigene `CrawlerConfiguration**XX**.xml`, die beim Start


    %Java_Home%\bin\java -jar regain-crawler.jar -config CrawlerConfiguration''XX''.xml

mitgegeben wird.

Ich bilde mir ein, dass es möglich ist, dass `regainpseudoFrame-crawler.jar` und `regain-crawler.jar` in einem Ordner gespeichert werden, auf ein gemeinsames Verzeichnis 'preparator' zugreifen und diese drei Ant-Tasks parallel laufen können.


**Autor:** itebob