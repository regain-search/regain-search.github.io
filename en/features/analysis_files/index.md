---
title: "Analysis files"
---

[Deutsche Übersetzung](/de/features/analysis_files/)

Analysis files
==============

**Analysis files** are files that are created by the [crawler](/en/components/crawler/) if the [&lt;writeAnalysisFiles&gt; tag](/en/config/crawlerconfiguration_xml/#writeanalysisfiles-tag) was set to `true`.

They show the [preparation](/en/components/preparator_/) steps and help to check the quality of the index by showing exactly what is indexed.


How can I use this feature?
---------------------------

Just set the [&lt;writeAnalysisFiles&gt; tag](/en/config/crawlerconfiguration_xml/#writeanalysisfiles-tag) to `true`.

After the [crawler](/en/components/crawler/) is finished, the analysis files are located in the [index directory](/en/components/search_index/#the_index_directory) in the subdirectory `new/analysis` or `index/analysis`, depending on whether the [search mask](/en/components/search_mask/) has already [switched to the new index](/en/features/hot_deployment_/).
