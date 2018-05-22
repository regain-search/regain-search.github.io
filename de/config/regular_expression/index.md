---
title: "Reguläre Ausdrücke"
---

[English translation](/en/config/regular_expression/)

Reguläre Ausdrücke
==================

Die [regain-Konfiguration](/de/config/) arbeitet sehr viel mit regulären Ausdrücken. **Reguläre Ausdrücke** (kurz: Regex) sind sehr mächtige Platzhalter (Wildcards) und eignen sich sehr gut dazu, Zeichenketten wie z.B. URLs zu beschreiben.

Wenn Sie mit dieser Technik noch nicht vertraut sind, dann finden Sie [hier eine Beschreibung](http://de.selfhtml.org/perl/sprache/regexpr.htm). Eine weitere etwas akademischere Beschreibung ist [hier zu finden](http://de.wikipedia.org/wiki/Regul%C3%A4rer_Ausdruck). Eine bessere aber englische Beschreibung finden Sie [hier](http://en.wikipedia.org/wiki/Regular_expression). Kürzere Einführungen finden Sie zu Hauf, wenn Sie nach `regex` googlen.

**Hinweis:** regain nutzt den Regex-Dialekt von Java, welcher der gleiche wie von Perl ist.

**Achtung:** In den XML-Konfigurationsdateien [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) und [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) müssen alle XML-Zeichen wie `&`, `<` oder `>` durch die entsprechenden Entities (`&amp;`, `<` bzw. `>`) ersetzt werden!

**Beispiel:** Die Regex `<a[^>]*>The&nbsp;link</a>` muss folgendermaßen angegeben werden: `<a[^>]*<The&amp;nbsp;link</a<`. (Das ist natürlich ein extremes Beispiel)

Regex-Gruppen
-------------

Teile von regulären Ausdrücken können zu Gruppen zusammengefasst werden. Eine Gruppe wird durch eine aufgehende und eine zugehende runde Klammer markiert. Jede Gruppe hat eine eindeutige Nummer, über die sie identifiziert werden kann.

Gruppen werden nach der aufgehenden Klammer durchnummeriert: Die gesamte Regex hat die Nummer `0`. Die Gruppe mit der ersten aufgehenden Klammer von links hat die Nummer `1`. Die Gruppe mit der zweiten aufgehenden Klammer hat die Nummer `2` und so weiter.

`Beispiel:`

    a(b(a(b|c)a)a(b|e)*)c   - Nummer 0
     (b(a(b|c)a)a(b|e)*)    - Nummer 1
       (a(b|c)a)            - Nummer 2
         (b|c)              - Nummer 3
                 (b|e)      - Nummer 4

Weblinks
--------

  * Ein Online-Regex-Tester: http://www.regex-tester.de/regex.html
