---
title: "Verwendete Bibliotheken"
---

[English translation](/en/project_info/used_libraries/)

Verwendete Bibliotheken
=======================

Dies sind die Bibliotheken, die von regain verwendet werden:
  * Jakarta Regexp 1.3 (`jakarta-regexp-1.3.jar`). Ermöglicht die Nutzung von regulären Ausdrücken. Siehe: http://jakarta.apache.org/regexp
  * Jakarta Log4j 1.2.11 (`log4j-1.2.11.jar`). Stellt die Protokollierung zur Verfügung. Siehe: http://jakarta.apache.org/log4j
  * Jakarta Lucene 1.4.3 (`lucene-1.4.3.jar`). Enthält den Kern der Suche, also Indexerstellung und Suche auf dem Index. Siehe http://jakarta.apache.org/lucene
  * Apache XML Xerces 2.6.2 (`xercesImpl.jar` und `xml-apis.jar`). Bietet einen Parser zum Lesen von XML-Dateien. Siehe http://xml.apache.org/xerces2-j
  * PDFBox 0.7.1 (`PDFBox-0.7.1.jar`). Ermöglicht das Lesen von PDF-Dokumenten. Läuft nur unter Java 1.3 oder darüber. Siehe http://pdfbox.org
  * Jakarta POI 3.0 alpha 1 (`poi-3.0-alpha1-20050704.jar` und `poi-scratchpad-3.0-alpha1-20050704.jar`). Ermöglicht das Lesen von Microsoft-Excel-Dokumenten und Microsoft-Word-Dokumenten. Das Lesen von Word-Dokumenten ist dabei leider noch in einem sehr frühen Entwicklungsstadium. Siehe http://jakarta.apache.org/poi
  * Jacob 1.8 (`jacob.jar` und `jacob.dll`). Ermöglicht den Zugriff auf COM-Objekte von Java aus. Damit ist das Auslesen von Microsoft Office Dokumenten implementiert, indem die Daten direkt aus den Office-Anwendungen gelesen werden. Siehe http://sourceforge.net/projects/jacob-project
  * Jacobgen (Verzeichnis `jacobgen`). Codegenerator für Jacob. Ermöglicht einen einfacheren Zugriff auf COM-Objekte durch die Generierung von Wrapper-Klassen. Die verwendete Version ist eine Weiterentwicklung des [STZ-IDA](http://stz-ida.de), aufbauend auf der Version 0.3. Siehe http://www.bigatti.it/projects/jacobgen
  * Simple (`simple-2.5.3.jar`). Ein sehr schlanker Java-HTTP-Server. Wird von der [Desktop-Suche](/de/project_info/variant_comparison/) eingesetzt. Siehe auch [Suchmaske](/de/components/search_mask/). Siehe http://simpleweb.sourceforge.net
