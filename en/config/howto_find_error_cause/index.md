---
title: "How to find the error cause"
---

[Deutsche Übersetzung](/de/config/howto_find_error_cause/)

How to find the error cause
===========================

If regain shows an error then there is propably something wrong with your [configuration](/en/config/). This page shows you how to find the cause of an error.


How to find the stack trace
---------------------------

### Crawler errors

The [Crawler](/en/components/crawler/) logs its errors to the error log file. It is located in the `log` subdirectory.


### Search mask errors

There are two possible error pages you may get when an error occurs in the [search mask](/en/components/search_mask/): The regain error page or the error page of your servlet-engine (e.g. Tomcat).

The regain error page contains the regain logo and show the message "Error when searching for ...". It contains a hidden stack trace that shows the exact error cause. The stack trace is located at the end of the error page and it written in white text on a white background (hidden) to avoid shocking the "normal" users. You can make it visible by selecting the whole page, for example by pressing `Ctrl+A`.

The error page of your servlet-engine may contain a stack trace that only shows the internal error location in the servlet-engine and not the location, where the error was caused in regain. You recognise the regain stack trace, if it contains `net.sf.regain.RegainException`. If this is not the case, you have to look in the log file created by your servlet-engine.

With the servlet-engine "Tomcat" this page contains normally the message `Error message: Writing results failed`. The log file that contains the regain stack trace you need, is located in the subdirectory `logs` of the Tomcat-Directory. It has the name `localhost.xyz.log`, where `xyz` is today's date. Open that file, scroll to the end and you should find the regain stack trace.


How to read the stack trace
---------------------------

A stack trace consists of one or more errors that show which error has caused another error. For each error the call stack is listed.

Example:
```
net.sf.regain.util.sharedtag.taglib.ExtendedJspException: Writing results failed
    at net.sf.regain.util.sharedtag.taglib.SharedTagWrapperTag.doEndTag(SharedTagWrapperTag.java:170)
    at org.apache.jsp.search_jsp._jspx_meth_search_check_0(org.apache.jsp.search_jsp:335)
    at org.apache.jsp.search_jsp._jspService(org.apache.jsp.search_jsp:131)
    at org.apache.jasper.runtime.HttpJspBase.service(HttpJspBase.java:97)
    ... 19 more
Caused by: net.sf.regain.RegainException: Loading configuration file failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
    at net.sf.regain.search.config.DefaultSearchConfigFactory.createSearchConfig(DefaultSearchConfigFactory.java:45)
    at net.sf.regain.search.SearchToolkit.loadConfiguration(SearchToolkit.java:433)
    at net.sf.regain.search.SearchToolkit.getIndexConfigArr(SearchToolkit.java:99)
    at net.sf.regain.search.sharedlib.CheckTag.printEndTag(CheckTag.java:64)
    at net.sf.regain.util.sharedtag.taglib.SharedTagWrapperTag.doEndTag(SharedTagWrapperTag.java:164)
    ... 22 more
Caused by: net.sf.regain.RegainException: Parsing XML failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
    at net.sf.regain.XmlToolkit.loadXmlDocument(XmlToolkit.java:79)
    at net.sf.regain.search.config.XmlSearchConfig.<init>(XmlSearchConfig.java:42)
    at net.sf.regain.search.config.DefaultSearchConfigFactory.createSearchConfig(DefaultSearchConfigFactory.java:42)
    ... 26 more
Caused by: java.io.FileNotFoundException: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml (Path could not be found)
    at java.io.FileInputStream.open(Native Method)
    at java.io.FileInputStream.<init>(FileInputStream.java:106)
    at net.sf.regain.XmlToolkit.loadXmlDocument(XmlToolkit.java:75)
    ... 28 more
```

The call stack lines begin with `at`. Forget these lines. They show the programmer where in the source code the error was caused.

The part that is interesting for you are the error messages.

For the above example the error messages are:

```
ExtendedJspException: Writing results failed
Caused by: RegainException: Loading configuration file failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
Caused by: RegainException: Parsing XML failed: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml
Caused by: FileNotFoundException: C:\Programme\Tomcat 5.5\conf\regain\SearchConfiguration.xml (Path could not be found)
```

It says that the result page could not be written, because the configuration file could not be loaded, because the configuration file was not found. In this case you should copy the SearchConfiguration.xml to the right location.

Check the index
---------------
The Regain index is a standard Lucene index. A tool to check the information is [lukeall](http://www.dotlucene.net/documentation/ToolforAnalyzingLuceneInd.html). With [Lucene Index Toolbox](http://www.getopt.org/luke/) you can modify the search index...

Enable Debug Logging
--------------------

In `log4.properties` (in `crawler/` or `desktop/conf`), uncomment the following lines (removing the `#`):

```
log4j.category.net.sf.regain=DEBUG
log4j.category.net.sf.regain.crawler.Crawler=DEBUG
```

This will greatly increase the verbosity of the logging output concerning regain issues.