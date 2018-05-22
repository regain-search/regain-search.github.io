---
title: "Preparators"
---

[Deutsche Übersetzung](/de/components/preparator/)

Preparators
===========

Before the [crawler](/en/components/crawler/) is able to add any document to the [search index](/en/components/search_index/), its text must be extracted. This is done by so-called **preparators**.

Dedicated preparators are responsible for each document format. For example there is a HTML preparator that is able to read the text from HTML documents, a PDF preparator that is able to read PDFs and so on.

Preparators are implemented using a plugin architecture. That means, the preparators are not integrated part of the main program, but they are located in seperate files in the directory `preparator`. This way regain may be extended easily for handling further data formats  and sources by newly developed preparators and you may specify in a flexible way, which preparator should be used.

Including Preparators
---------------------

A preparator itself knows for which documents it is responsible. In order to make a preparator working it is therefore sufficient to: 
  * store it in the directory `preparator`.
  * make a proper entry in [`preparatorList` tag](/en/config/crawlerconfiguration_xml/#.3cpreparatorlist.3e_tag) of the [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) using regular expressions (see also the optional [`urlPattern` tag](/en/config/crawlerconfiguration_xml/#.3curlpattern.3e_tag)).

You may, however, exactly adjust what preparator should be used for which URL. Some preparators may also be configured with further settings there. For example the HTML preparator may extract only a certain part of HTML documents (e.g. ignoring the navigation part). In addition the try out sequence of several preparators may be declared for the the [crawler](/en/components/crawler/) process.

Preparator´s Precedence
-----------------------
The [crawler](/en/components/crawler/) is using an internal list of all preparators stored in the `preparator` directory. This list starts in the same order with all the preparators appearing in the `preparatorList`-tag of the [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) and is continued in indefinite order by all those preparators not explicitly configured in the `preparatorList`-tag.

The [crawler](/en/components/crawler/) is trying out the preparators according to this list on every document. The first matching preparator is used.

This way you can cascade preparators which are for the same file format. If the first one fails extracting the `content` [field](/en/components/search_index/) the next one might be able to do it.

Excluding a certain Preparator
------------------------------
To avoid [crawling](/en/components/crawler/) a particular file type there are (in addition to the `blacklist`) two ways to de-activate a preparator: 
*either you can remove the belonging `.jar`-file from the
directory `preparator` 
* or you can set the according `preparator` tag attribute `enabled` to `false`.

**Example:** Deactivation of the preparator `JacobMsExcelPreparator`:
```xml
<preparatorList>
  ...
  <preparator enabled="false">
    <class>.JacobMsExcelPreparator</class>
  </preparator>
  ...
</preparatorList>
```

List of available Preparators
-----------------------------

regain comes with the following preparators:

**Preparators for all systems**
  * `HtmlPreparator` - regain-preparator for HTML files.
  * `PdfBoxPreparator` - for portable documents files (PDF), based on [pdfbox](http://www.pdfbox.org).
  * `OpenOfficePreparator` - for OpenOffice files.
  * `PoiMsOfficePreparators` - a set of preparators written in Java, using [POI](http://jakarta.apache.org/poi/) for MS Office files (Word, Excel and Powerpoint). 
  * `PlainTextPreparator` - for simple ASCII text files.
  * `XmlPreparator` - for XML files.
  * `SimpleRtfPreparator` - regain´s own preparator for rich text format files (RTF).
  * `SwingRtfPreparator` - another RTF-preparator based on [JEditorPane](http://java.sun.com/j2se/1.5.0/docs/api/javax/swing/JEditorPane.html) of the Swing framework for Java.
  * `EmptyPreparator` - for storing url/filname and date only, does ignore file content.
  * `ExternalPreparator` - a generic preparator calling any external programm or script for preparation.

**Preparators for MS Windows Systems only**
  * `IfilterPreparator` - a preparator on top of the MS [IFilter-API](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/indexsrv/html/ixrefint_9sfm.asp). The supported range of file formats depends on what IFilter are installed on your system. However, Windows itself has already a number of IFilters. The [IFilter Explorer](http://www.citeknet.com) may be used to list them.
  * `JacobMsOfficePreparators` - this set of preparators for Word, Excel and PowerPoint provides quite good content extraction using [Jacob](http://danadler.com/jacob/). However, an MS Office installation is required, because the Office programs are involved via COM for extraction...
