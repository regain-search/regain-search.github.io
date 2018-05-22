---
title: "White List und Black List"
---

[English translation](/en/features/white_and_black_list/)

White List und Black List
=========================

Mit Hilfe der **White List** und der **Black List** können Sie sehr genau einstellen, was in den Index kommen soll und was nicht.

Die Grundregel dabei ist immer: Ein Dokument kommt in den Index, wenn seine URL mindestens einem Eintrag der White List, aber keinem Eintrag aus der Black List entspricht.


Wie kann ich dieses Feature nutzen?
-----------------------------------

Die Listen werden in der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) durch die Tags `<whitelist>` bzw. `<blacklist>` definiert.

Die folgende Konfiguration bestimmt beispielsweise, dass alle URLs aufgenommen werden, die mit `http://www.mydomain.de` beginnen, außer diejenigen aus `http://www.mydomain.de/some/dynamic/content/`:

```xml
<whitelist>
  <prefix>http://www.mydomain.de</prefix>
</whitelist>

<blacklist>
  <prefix>http://www.mydomain.de/some/dynamic/content/</prefix>
</blacklist>
```
