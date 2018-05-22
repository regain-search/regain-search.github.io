---
title: "Multi index search"
---

[Deutsche Übersetzung](/de/features/multi_index_search/)

Multi index search
==================


The **Multi index search** allows you to search multiple indexes over one search mask. The search query is executed on all indexes and the results are merged afterwards. The merge algorithm merges the results that way, they will stay sorted by relevance. If some results have the same relevance they will be merged in a "fair" way, that is that from every index a hit will be merged in at some time. This prevents that first all hits from one index are listet and then the hits of another index.

**Since version:** 1.1 beta 5


How can I use this feature?
---------------------------

A multi index search is executed, when more than one HTML-parameter `index` is passed.

The following query executes a multi index search for `Test` in the indexes `docs` and `intranet`:

    http://localhost:8020/search.jsp?index=docs&index=intranet&query=Test

Please regard: All indexes must be configured in the [SearchConfiguration.xml](/en/config/searchconfiguration_xml/).
