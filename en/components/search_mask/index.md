---
title: "Search mask"
---

[Deutsche Übersetzung](/de/components/search_mask/)

Search mask
===========

The **search mask** is a web interface that receives search queries, executes them and shows the results page by page.

Before you can search something with the search mask, you have to create a [search index](/en/components/search_index/) using the [crawler](/en/components/crawler/).

Technically speaking, the search mask is a set of Java Server Pages, that use a tag library for the dynamic parts. If you want to [use regain on a web server](/en/project_info/variant_comparison/), you therefore need a servlet engine like [Tomcat](http://jakarta.apache.org/tomcat) or [Jetty](http://jetty.mortbay.org/jetty) to run the search mask. The [desktop search](/en/project_info/variant_comparison/) uses a particularly developed, very slim JSP engine, which is based on [Simple](http://simpleweb.sourceforge.net). However, it is only able to process TagLib-tags, no Java Code that was embedded in JSPs. In exchange it is only 200 kB in size and not over 10 MB as "real" servlet engines, which would have been simply to much for a desktop search.
