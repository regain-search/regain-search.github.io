---
title: "regain configuration"
---

[Deutsche Übersetzung](/de/config/)

regain configuration
====================

There are several files where you can change the behavior or the look of regain.


[Crawler](/en/components/crawler/) configuration:
  * The `log4j.properties` contains all settings for the logging. You can define the granularity, the format and the location of your log files. See the [log4j documentation](http://jakarta.apache.org/log4j/docs/manual.html) for details.
  * The [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) contains all settings for the [crawler](/en/components/crawler/).


[Search mask](/en/components/search_mask/) configuration:
  * The `web.xml` defines where the main search configuration file `SearchConfiguration.xml` is located. By default the config is searched in `../conf/regain/SearchConfiguration.xml`. That is if your tomcat directory is `c:\Programme\jakarta-tomcat` you have to put your `SearchConfiguration.xml` to `c:\Programme\jakarta-tomcat\conf\regain`. If you want to use another config location, you have to edit your `web.xml` and change the `searchConfigFile` init parameter.  

     See [How to find the error cause](/en/config/howto_find_error_cause/) if you keep getting error messages.
  * The [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) contains the actual configuration for the [search mask](/en/components/search_mask/).
  * To configure logging (and avoiding an error message at startup) configure a `log4j.properties` file in `webapps/regain`.
