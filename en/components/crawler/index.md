---
title: "Crawler"
---

[Deutsche Übersetzung](/de/components/crawler/)

Crawler
=======

The **crawler** is the program that creates the [search index](/en/components/search_index/). This index is needed by the [search mask](/en/components/search_mask/) in order to perform searches.

It crawles the directories and web sites specified in the configuration file [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) for documents. With each document, that is not yet in the search index, the text is extracted using the suitable [preparator](/en/components/preparator/). This text is included in the index.

Technically spoken the crawler is a Java stand-alone application (`regain-crawler.jar`), that runs on the console, that is without a graphical user interface. Thereby it may be started automated, e.g. by a cron job. 

The [desktop search](/en/project_info/variant_comparison/) starts the crawler periodically, so there is no need to execute it by hand.
The intervall may be set via configuration page as well as inside [DesktopConfiguration.xml](/en/config/desktopconfiguration_xml/).

Crawler call should be perfomed from its installation directory, otherwise it may fail on accessing the ressources (e.g. log file, [Preparator](/en/components/preparator/)en, etc.). A typical call on Windows-Systems is:

    c:
    cd C:\Program files\regain\crawler
    java -jar regain-crawler.jar

Hints:
  * Crawler is not restricted to run on the same engine like the Servlet-Engine with [search mask](/en/components/search_mask/) ist running.
  * So you may build (parts of) the [search index](/en/components/search_index/) using the [Preparator](/en/components/preparator/)s available for Windows only...

[Developer's Documentation of the Crawling Process](/en/components/project_info/crawling_process/)
