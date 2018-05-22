---
title: "Präparatoren"
---

[English translation](/en/components/preparator/)

Präparatoren
============

Bevor der [Crawler](/de/components/crawler/) ein Dokument in den [Suchindex](/de/components/search_index/) aufnehmen kann, muss zuerst der Text des Dokuments extrahiert werden. Dies wird von s.g. **Präparatoren** übernommen.

Für jedes Datenformat ist immer ein bestimmter Präparator zuständig. So gibt es einen Html-Präparator, der Text aus HTML-Dokumenten lesen kann, einen PDF-Präparator, der PDFs lesen kann, usw.

Präparatoren sind in Form von Plugins realisiert. D.h. die Präparatoren sind nicht in das Hauptprogramm integriert, sondern befinden sich in eigenen Dateien im Verzeichnis `preparator`. So können neuentwickelte Präparatoren für die Behandlung weiterer Datenformate und -quellen leicht in regain eingebunden werden. Außerdem kann man flexibel festlegen, welche Präparatoren regain verwenden soll.


Einbindung von Präparatoren
---------------------------

Ein Präparator weiß eigentlich selbst, für welche Dokumente er zuständig ist. Zur Aktivierung muß man lediglich:
  * den Präparator in das Verzeichnis `preparator` kopieren und
  * im `preparatorList`-Tag der Datei [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) durch [regular expression](/de/config/regular_expression/) festlegen, welcher Präparator für welche URLs verwendet werden soll (s.a. das optionale `urlPattern`-Tag). 

Manche Präparatoren kann man dort noch mit weiteren Einstellungen konfigurieren. Beispielsweise kann man den HTML-Präparator so einstellen, dass er nur einen bestimmten Teil der HTML-Datei auswertet (also z.B. den Navigationsteil ignoriert).


Rangfolge von Präparatoren im Crawler
-------------------------------------

Der [Crawler](/de/components/crawler/) führt intern eine Liste aller Präparatoren im Verzeichnis `preparator`. Am Anfang der Liste stehen die Präparatoren in der Reihenfolge, wie im `preparatorList`-Tag aus der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/). Danach folgen in unbestimmter Ordnung die Präparatoren, die nicht explizit im `preparatorList`-Tag konfiguriert wurden.

Der Crawler probiert bei jedem Dokument die Präparatoren in Reihenfolge dieser Liste. Der erste zur jeweiligen URL passende Präparator wird verwendet. Falls dieser Präparator mit einem Fehler abbricht, probiert der Crawler die Liste weiter, bis wieder ein Präparator zur URL passt.

Auf diese Weise sind Präparatoren, die das gleiche Dateiformat lesen können, kaskadierbar. Falls der erste beim Textextrahieren für das `content`-Feld scheitert, kann es vielleicht der zweite.


Ausschalten bestimmter Präparatoren
-----------------------------------

Um etwa die Aufnahme bestimmter Dateitypen in den Suchindex zu verhindern, können - neben der [Blacklist](/de/features/white_and_black_list/) - auch einzelne Präparatoren deaktiviert werden. Es gibt zwei Möglichkeiten: 
  * Entweder entfernt man die zugehörige `.jar`-Datei aus dem Verzeichnis `preparator`,
  * oder man setzt beim entsprechenden `preparator`-Tag das Attribut `enabled` auf `false`.

**Beispiel:** Deaktivierung des Präparators `JacobMsExcelPreparator`:
```xml
<preparatorList>
  ...
  <preparator enabled="false">
    <class>.JacobMsExcelPreparator</class>
  </preparator>
  ...
</preparatorList>
```


Liste der Präparatoren
----------------------

In regain sind die folgenden Präparatoren enthalten:

**Plattformunabhängige Präparatoren:**
  * `HtmlPreparator` - Präpariert HTML-Dokumente.
  * `PdfBoxPreparator` - Präpariert PDF-Dokumente, basiert auf [pdfbox](http://www.pdfbox.org).
  * `OpenOfficePreparator` - Präpariert OpenOffice-Dokumente.
  * `PoiMsOfficePreparators` - Eine Sammlung von Präparatoren, die die Microsoft-Office-Formate Word, Excel und Powerpoint präparieren können. Diese Präparatoren basierend auf [POI](http://jakarta.apache.org/poi/) sind 100% pure Java und laufen damit auf jeder Plattform.
  * `PlainTextPreparator` - Präpariert einfachen ASCII-Text.
  * `XmlPreparator` - Präpariert XML-Dokumente.
  * `SimpleRtfPreparator` - Präpariert RTF-Dokumente. Nutzt eine eigene RTF-Implementierung.
  * `SwingRtfPreparator` - Präpariert RTF-Dokumente. Nutzt die [RTF-Implementierung](http://java.sun.com/j2se/1.5.0/docs/api/javax/swing/JEditorPane.html) von Java (genauer: Swing).
  * `EmptyPreparator` - indexiert nur die URL/Dateiname, Datum usw. (ignoriert Inhalt)
  * `ExternalPreparator` - Überlässt das Präparieren einem externen Programm oder Script und kann damit für alle möglichen Dateiformate eingesetzt werden.

**Präparatoren, die nur auf Windows-Systemen laufen:**
  * `IfilterPreparator` - Ein Präparator, der die [IFilter-Schnittstelle](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/indexsrv/html/ixrefint_9sfm.asp) von Microsoft nutzt. Dieser Präparator läuft nur unter Windows. Welche Formate unterstützt werden, hängt davon ab, welche IFilter auf dem Windows-System installiert sind. Windows selbst bringt jedoch schon eine sehr große Anzahl an IFiltern für alle gängigen Formate mit. [IFilter Explorer](http://www.citeknet.com) zeigt die installierten Filter an.
  * `JacobMsOfficePreparators` - Eine Sammlung von Präparatoren, die die Microsoft-Office-Formate Word, Excel und Powerpoint präparieren können. Diese Präparatoren nutzen via [Jacob](http://danadler.com/jacob/) die COM-Schnittstelle der Office-Programme zur Extraktion. Sie haben damit eine sehr hohe Erfolgsquote, setzen jedoch ein Windows-System mit installiertem MS-Office voraus.
