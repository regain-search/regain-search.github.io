---
title: "White and black list"
---

[Deutsche Übersetzung](/de/features/white_and_black_list/)

White and black list
====================

Using the **white and black list** you can specify very precisely, what will get in the index and what not.

The base rule is always: A document gets in the index, if its URL comes up to at least one entry from the white list, but no entry from the black list.


How can I use this feature?
---------------------------

The lists are defined in the `CrawlerConfiguration.xml` by the tags [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/#whitelist-tag) resp. [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/#blacklist-tag).

The following configuration defines for example that all URLs should be taken in that start with `http://www.mydomain.de`, except for those starting with `http://www.mydomain.de/some/dynamic/content/`:
```xml
<whitelist>
  <prefix><nowiki>http://www.mydomain.de</nowiki></prefix>
</whitelist>
<blacklist>
  <prefix><nowiki>http://www.mydomain.de/some/dynamic/content/</nowiki></prefix>
</blacklist>
```

Additionally, a [crawler plugin](/en/features/components/crawler_plugins/#checkdynamicblacklist) may be written in order to blacklist files according to more complex conditions (e.g. filesize).