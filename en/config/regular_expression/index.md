---
title: "Regular expressions"
---

[Deutsche Übersetzung](/de/config/regular_expression/)

Regular expressions
===================

The [configuration](/en/config_/) of regain works with regular expressions. Regular expressions (short: regex) are very powerfull wildcards and the are well appropriate to describe any string patterns, e.g. URLs.

If you are not familiar with this technique you find a very detailed description [here](http://en.wikipedia.org/wiki/Regular_expression). If you want a more compact intruduction just google for `regex`, you will be covered with them.

**Note:** regain uses the regex dialect of Java, which is the same as the one of Perl.

**Regard:** In the XML configuration files [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) and [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) all XML characters like `&`, `<` or `>` must be replaced by the according entities (`&amp;`, `<` or `>`)!

**Example:** The regex `<a[^>]*>The&nbsp;link</a>` must be specified as `<a[^>]*<The&amp;nbsp;link</a<`. (This example is extrem, of corse...)


Regex groups
------------

Parts of regular expressions may be combined to groups. A group is marked by a left and a right parenthesis. Each group has a unique number, used to identify it.

Groups are numbered by its left parenthesis: The whole regex has the number `0`. The group with the first left parenthesis in the string has the number `1`. The group with the second left parenthesis has the number `2`, and so on.

**Example:**

    a(b(a(b|c)a)a(b|e)*)c   - Number 0
     (b(a(b|c)a)a(b|e)*)    - Number 1
       (a(b|c)a)            - Number 2
         (b|c)              - Number 3
                 (b|e)      - Number 4


Weblinks
--------

  * [Regular expression](http://en.wikipedia.org/wiki/Regular_expression) article in Wikipedia
