---
title: "Installation of the server variant of regain"
---

[Deutsche Übersetzung](/de/installation/server/)

Installation of the server variant of regain
============================================

This article describes, how to install the [server variant](/en/project_info/variant_comparison/) of regain. 

The regain server search consists of two separate applications: The crawler and the search. The crawler creates the search index. The search executes search queries on the finished index and presents the results.


Installation of the crawler
---------------------------
  - Ensure you have the jre installed http://www.java.com At least version 1.6 is required, but the latest version is normally recommended.
  - Download the regain server search from the [download page](http://regain.sourceforge.net/download.php) and unpack it.
  - Create a program directory, e.g. `c:\Program Files\regain\crawler`.
  - Copy the content of the directory `regain\runtime\crawler` from the downloaded zip-file to the program directory.
  - Change the file [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) for your needs.
  - Create the directory where the index should be created, e.g. `c:\Program Files\regain\searchindex`. This isn't done automatically by the crawler for security reasons.

Starting the crawler
--------------------

The crawler is started from the console with the command:
 java -jar regain-crawler.jar

You can specify the following parameters:
  * ­`--help`: Shows the possible parameters.
  * ­`-forceNewIndex`: Forces the creation of a new index. If not specified, the crawler will try to update an existing index.
  * `-retryFailedDocs`: If set, the crawler tries to reindex documents, that failed the last time, too. Normally only those documents are retried, that have changed since the last try. Therefore this parameter only makes sense, if you have changed the configuration of the [preparator](/en/components/preparator/)s, because otherwise these documents will fail again, which costs needlessly time.
  * `-onlyEntries <WhitelistEntry1>,<WhitelistEntry2>`: The list of whitelist entries that should be processed. All other entries of the white list will be left in the index, but not updated.
  * `-config <filename>`: Specifies the configuration file that should be used. Default is `CrawlerConfiguration.xml`.
  * ­`-logConfig <filename>`: Specifies the logging configuration file that should be used. Default is `log4j.properties`.
  * (optional) parameters handled by java, see the Java documentation. This includes for instance `-Xmx256m` (allocate more memory to Java VM) `-Dfile.encoding=8859_1` (file encoding is not the same as the locale)


Example with parameters:

    java -jar regain-crawler.jar -config HomepageConfig.xml

Installation of the search
--------------------------

  - Install Jakarta Tomcat 3.2.3 or higher. You get Tomcat [here](http://tomcat.apache.org/). Of course you may use another servlet engine as well, e.g. [Jetty](http://jetty.mortbay.org/jetty).
  - Copy the file `regain.war` in the tomcat subdirectory `webapps`. You find it in the downloaded zip-file in the directory `regain\runtime\search\webapps`.
  - Copy the file `SearchConfiguration.xml` in the tomcat subdirectory `conf\regain`. You find it in the downloaded zip-file in the directory `regain\runtime\search\conf\regain`.
  - Change the file [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) and specify where the index directory is located, e.g. `c:\Program Files\regain\index`.


Starting the search
-------------------

Start tomcat: Execute `startup` in the tomcat subdirectory `bin`.


**Note:** If you start tomcat as a Windows service you have to set the absolute path to your `webapps/regain` directory in the `web.xml`.

Example:
```xml
<context-param>
  <param-name>webDir</param-name>
  <param-value>c:/Program Files/jakarta-tomcat/webapps/regain</param-value>
</context-param>
```
