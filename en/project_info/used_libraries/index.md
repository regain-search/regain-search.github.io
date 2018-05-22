---
title: "Libraries used by regain (outdated)"
---

[Deutsche Übersetzung](/de/project_info/used_libraries/)

Libraries used by regain (outdated)
===================================

These are the projects used by regain:

  * Jakarta Regexp 1.3 (`jakarta-regexp-1.3.jar`). Allows using [regular expression](/en/config/regular_expression/)s. See: http://jakarta.apache.org/regexp
  * Jakarta Log4j 1.2.11 (`log4j-1.2.11.jar`). Provides logging. See: http://jakarta.apache.org/log4j
  * Jakarta Lucene 1.4.3 (`lucene-1.4.3.jar`). Contains the core of the search, that is index creation and searching on the index. See http://jakarta.apache.org/lucene
  * Apache XML Xerces 2.6.2 (`xercesImpl.jar` and `xml-apis.jar`). Provides a parser for reading XML files. See http://xml.apache.org/xerces2-j
  * PDFBox 0.7.1 (`PDFBox-0.7.1.jar`). Reads PDF documents. Only works with Java 1.3 and above. See http://pdfbox.apache.org
  * Jakarta POI 3.0 alpha 1 (`poi-3.0-alpha1-20050704.jar` and `poi-scratchpad-3.0-alpha1-20050704.jar`). Reads Microsoft Excel and Microsoft Word documents. Unfortunately the reading of Word files is still in an early development stage. See http://jakarta.apache.org/poi
  * Jacob 1.8 (`jacob.jar` und `jacob.dll`). Allows the access to COM objects from Java. This is used to read Microsoft Office documents, by reading the data directly from the Microsoft Office applications. See http://sourceforge.net/projects/jacob-project
  * Jacobgen (`jacobgen` directory). Code generator for Jacob. Allows a simpler access on COM objects by generating wrapper classes. The used version is a further development of the [STZ-IDA](http://stz-ida.de), based on version 0.3. See http://www.bigatti.it/projects/jacobgen
  * Simple (`simple-2.5.3.jar`). A very slim Java HTTP server. Used by the [desktop search](/en/project_info/variant_comparison/). See also: [search mask](/en/components/search_mask/). See http://simpleweb.sourceforge.net
  * JDIC (`jdic.jar` and `tray.dll`). A tray icon support. See https://jdic.dev.java.net
