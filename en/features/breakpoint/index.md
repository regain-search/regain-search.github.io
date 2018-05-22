---
title: "Breakpoints"
---

[Deutsche Übersetzung](/de/features/breakpoint/)

Breakpoints
===========

The [crawler](/en/components/crawler/) creates periodically so called **breakpoints**. When doing so, the current state of the [search index](/en/components/search_index/) is copied into a separate directory called `breakpoint`. If the index update should be cancelled (e.g. if the computer is shut down), the crawler will go on from the last breakpoint the next time it is started and doesn't have to start at the beginning.

How can I use this feature?
---------------------------

By default breakpoints are created every 10 minutes. You can change the interval or disable breakpoints using the [&lt;breakpointInterval&gt; tag](/en/config/crawlerconfiguration_xml/#breakpointinterval-tag) in the `CrawlerConfiguration.xml`.
