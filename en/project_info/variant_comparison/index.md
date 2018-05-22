---
title: "Comparison of the regain variants"
---

[Deutsche Übersetzung](/de/project_info/variant_comparison/)

Comparison of the regain variants
=================================

There are two variants of regain: The **desktop search** and the **server search**.

Funktional differences
----------------------

The **desktop search** is meant for those who want to use regain on their workstation, or who want to give regain a try. The **server search** is meant for administrators of a web server, who want to integrate a search in their web site or intranet site. Such a search may also include documents that are not accessible over the web server. For example it is possible to offer a search for net drives.

So if you are not sure which variant you should download, take the **desktop search**.

The following table shows the differences of the two variants:

| | regain desktop search | regain server search |
| --- | --- | --- |
| Best choice for newbies | ![yes](/images/yes.png) | ![no](/images/no.png) |
| regain [crawler](/en/components/crawler/) | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| regain [search mask](/en/components/search_mask/) | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Complete configuration of the [crawler](/en/componenents/crawler/) in one XML file | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Simple configuration of the [crawler](/en/componenents/crawler/) over a web interface | ![yes](/images/yes.png) | ![no](/images/no.png) |
| Complete configuration of the [search mask](/en/componenents/search_mask/) in one XML file | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Customizable look of the [search mask](/en/componenents/search_mask/) by JSPs | ![yes](/images/yes.png) | ![yes](/images/yes.png) |
| Integrated web server | ![yes](/images/yes.png) | ![no](/images/no.png) |
| Runs in a servlet engine (e.g. Tomcat) | ![no](/images/no.png) | ![yes](/images/yes.png) |
| Integration in the task bar | ![yes](/images/yes.png) | ![no](/images/no.png) |

Technical differences
---------------------

The core of both variants is the same. Both include the [crawler](/en/components/crawler/), which is needed to create the [search index](/en/components/search_index/), and the [search mask](/en/components/search_mask/), which is needed for searching on a search index. Also the configuration of both variants is done on the same way: The XML files [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) and [SearchConfiguration.xml](/en/config/searchconfiguration_xml/), but the desktop search offers a web interface, that writes the most important settings to these two files.

The **desktop search** also comes with a small program that manages these two parts. This program integrates itself in the task bar and automatically starts the crawler, so the search index is updated regularily or whenever the configuration has changed. Furthermore it provides a web server, which is needed by the search mask in order to work.

At the **server search** the crawler is an independent program, which the administrator has to call by hand (or automated) in order to update the search index. Furthermore the admistrator has to run the search mask in a servlet engine. The web server is not delivered with regain.

Technically speaking the **desktop search** is a stand-alone application. That is an application that needs -- aside from Java -- no more programs to work. The **server search** is split in the crawler on the one hand, which is a stand-alone console application, and the search mask on the other hand, which is a .war archive that has to be integrated in a Java servlet engine (like Tomcat).
