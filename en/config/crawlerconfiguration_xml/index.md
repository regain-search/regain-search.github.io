---
title: "CrawlerConfiguration.xml"
---

[Deutsche Übersetzung](/de/config/crawlerconfiguration_xml/)

CrawlerConfiguration.xml
========================

The **CrawlerConfiguration.xml** contains the configuration of the [crawler](/en/components/crawler/).

&lt;startlist&gt; tag
---------------------

**role:** A list of URLs the [crawler](/en/components/crawler/) should start with. You may add any number of start URLs, which allows to add document from several sources in one index.

**values:** Any number of &lt;start&gt; child tags.

**example:**
```xml
<startlist>
   <start> ... </start>
   <start> ... </start>
   ...
</startlist>
```

### &lt;start&gt; tag
Child tag of the [&lt;startlist&gt; tag](/en/config/crawlerconfiguration_xml/#startlist-tag).

**role:** A start URL, the [crawler](/en/components/crawler/) starts with.

**attribute `parse`:** Specifies whether the document should be parsed for URLs.  (**values:** `true` or `false`)

**attribute `index`:** Specifies whether a found document should be indexed.  (**values:** `true` or `false`)

**values:** A URL.

**example:**
```xml
<start parse="true" index="false">http://www.murfman.de/bla/blubb</start>
```
or
```xml
<start parse="true" index="true">file://P:/documents</start>
```

&lt;whitelist&gt; tag
---------------------

**role:** The [white list](/en/config/features/white_and_black_list/). Contains prefixes a URL **must** have to be processed.

**values:** Any number of &lt;prefix&gt; or &lt;regex&gt; child tags.

**example:**
```xml
<whitelist>
  <prefix>http://www.mydomain.de</prefix>
</whitelist>
```

### &lt;prefix&gt; tag
Child tag of the [&lt;whitelist&gt; tag](/en/config/crawlerconfiguration_xml/#whitelist-tag).

**role:** Specifies a URL prefix a URL `must` have in order to be processed by the [crawler](/en/components/crawler/).

**attribute `name`:** The name of the white list entry. This is needed for the partial indexing. (Optional, **values:** A unique name)

**values:** A URL prefix.

**example:**
```xml
<prefix>http://www.murfman.de/bla/blubb</prefix>
```
or
```xml
<prefix name="docs">file://c:/MyDocuments</prefix>
```

### &lt;regex&gt; tag
Child tag of the [&lt;whitelist&gt; tag](/en/config/crawlerconfiguration_xml/#whitelist-tag).

**role:** Specifies a [regular expression](/en/config/regular_expression/) a URL `must` match to in order to be processed by the [crawler](/en/components/crawler/).

**values:** A [regular expression](/en/config/regular_expression/).

**since version:** 1.1 Beta 5

**example:**
```xml
<regex>/docs/[^/]**$</regex>
```

&lt;blacklist&gt; tag
---------------------

**role:** The [black list](/en/features/white_and_black_list/). Contains prefixes a URL must **not** have to be processed.

**values:** Any number of &lt;prefix&gt; or &lt;regex&gt; child tags.

**example:**
```xml
<blacklist>
  <prefix>http://www.mydomain.de/some/dynamic/content/</prefix>
</blacklist>
```

### &lt;prefix&gt; tag
Child tag of the [&lt;blacklist&gt; tag](/en/config/crawlerconfiguration_xml/#blacklist-tag).

**role:** Specifies a URL prefix a URL `must not` have in order to be processed by the [crawler](/en/components/crawler/).

**values:** A URL prefix.

**example:**
```xml
<prefix>http://www.murfman.de/dynamic/content</prefix>
```
or
```xml
<prefix>file://c:/MyDocuments/stuff/I/won't/search/for</prefix>
```

### &lt;regex&gt; tag
Child tag of the [&lt;blacklist&gt; tag](/en/config/crawlerconfiguration_xml/#blacklist-tag).

**role:** Specifies a [regular expression](/en/config/regular_expression/) a URL `must` match to in order to be processed by the [crawler](/en/components/crawler/).

**values:** A [regular expression](/en/config/regular_expression/).

**since version:** 1.1 Beta 5

**example:**
```xml
<regex>/backup/[^/]**$</regex>
```

&lt;proxy&gt; tag
-----------------

**role:** Sets the HTTP proxy that should be used by the crawler.

**values:** Knows the following child tags:
  * `<host>`: The host name of the proxy.
  * `<port>`: The port of the proxy.
  * `<user>`: The user name if authentification is desired.
  * `<password>`: The password if authentification is desired.

All these fields may be left empty, if no proxy or no authentification is desired.

If you don't know, what you should set here, use the settings of your web browser.

**example:**
```xml
<proxy>
  <host>proxy.something.de</host>
  <port>3128</port>
  <user>karl34</user>
  <password>gkxy23</password>
</proxy>
```

### &lt;host&gt; tag
Child tag of the [&lt;proxy&gt; tag](/en/config/crawlerconfiguration_xml/#proxy-tag).

**role:** The host name of the proxy. May be left out if no proxy is desired.

**values:** A host name.

**example:**
```xml
<host>proxy.something.de</host>
```
or
```xml
<host>10.10.10.53</host>
```

### &lt;port&gt; tag
Child tag of the [&lt;proxy&gt; tag](/en/config/crawlerconfiguration_xml/#proxy-tag).

**role:** The port number of the proxy. May be left out if no proxy is desired.

**values:** A number.

**example:**
```xml
<port>8080</port>
```

### &lt;user&gt; tag
Child tag of the [&lt;proxy&gt; tag](/en/config/crawlerconfiguration_xml/#proxy-tag).

**role:** The user name for proxy authentification. May be left out if no proxy authentification is desired.

**values:** A user name.

**example:**
```xml
<user>karl34</user>
```

### &lt;password&gt; tag
Child tag of the [&lt;proxy&gt; tag](/en/config/crawlerconfiguration_xml/#proxy-tag).

**role:** The password for proxy authentification. May be left out if no proxy authentification is desired.

**values:** A password.

**example:**
```xml
<password>i56dFg2s</password>
```

&lt;searchIndex&gt; tag
-----------------------

**role:** Contains all settings according the [search index](/en/components/search_index/).

**values:** Knows the following child tags:
  * `<dir>`: The directory, where the search index should be created.
  * `<buildIndex>`: Specifies whether to create an index at all.
  * `<analyzerType>`: The [terminology](/en/terminology/#analyzer) to use.
  * `<writeAnalysisFiles>`: Specifies whether to create an analysis files.
  * `<maxFailedDocuments>`: Specifies the maximum percentage of failed documents.
  * `<stopwordList>`: A list of words that should not be indexed.
  * `<excludeList>`: A list of words that shouldn't be changed by the [terminology](/en/terminology/#analyzer) before indexing.

**example:**
```xml
<searchIndex>
  <dir>C:\regain\index</dir>
  <buildIndex>true</buildIndex>
  <analyzerType>german</analyzerType>
  <writeAnalysisFiles>false</writeAnalysisFiles>
  <maxFailedDocuments>100</maxFailedDocuments>
  <stopwordList> ... </stopwordList>
  <exclusionList> ... </exclusionList>
</searchIndex>
```

### &lt;dir&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** The directory, where the [search index](/en/components/search_index/) should be created.

**values:** A directory name.

**example:**
```xml
<dir>C:\regain\index</dir>
```

### &lt;buildIndex&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** Specifies whether to create an index at all.

By setting this to `false` you can use the crawler to detect dead links or to fill a server side cache.

**values:** `true` or `false`

**example:**
```xml
<buildIndex>true</buildIndex>
```

### &lt;analyzerType&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** The [terminology](/en/terminology/#analyzer) to use.

**values:** `standard` or `german`

**example:**
```xml
<analyzerType>standard</analyzerType>
```

### &lt;breakpointInterval&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** Specifies the interval between two [breakpoint](/en/features/breakpoint/)s in minutes. If set to 0, no breakpoints will be created.

**values:** A number.

**since version:** 1.1 Beta 6

**example:** With the following the crawler will create a breakpoint every 10 minutes:
```xml
<breakpointInterval>10</breakpointInterval>
```

### &lt;writeAnalysisFiles&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** Specifies whether to create an analysis files.

**values:** `true` or `false`

**example:**
```xml
<writeAnalysisFiles>false</writeAnalysisFiles>
```

### &lt;maxFailedDocuments&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** Specifies the maximum percentage of failed documents.

**values:** A floating point number between `0` and `100`.

**example:**
```xml
<maxFailedDocuments>9.5</maxFailedDocuments>
```

### &lt;stopwordList&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** A list of words that should not be indexed. This list is called [terminology](/en/terminology/#stopword-list).

This list helps keeping the index small. Specify here frequent words noone would search for.

**values:** A space separated list of words.

**example:**
```xml
<stopwordList>we and or without with at in of</stopwordList>
```

### &lt;exclusionList&gt; tag
Child tag of the [&lt;searchIndex&gt; tag](/en/config/crawlerconfiguration_xml/#searchindex-tag).

**role:** A list of words that shouldn't be changed by the [terminology](/en/terminology/#analyzer) before indexing.

The [terminology](/en/terminology/#analyzer) tries to find for every word its base. For some words this may cause problems. Put these words in this list.

**values:** A space separated list of words.

**example:**
```xml
<exclusionList>veryProblematicWord evenMoreProblematicWord</exclusionList>
```

&lt;preparatorList&gt; tag
--------------------------

**role:** Contains the [preparator](/en/config/components/preparator/)s in the order they should be applied. Preparators that aren't listed here will be applied after the listed ones.

You can use this list
  * to define the priority (order) of the preparators
  * to disable preparators
  * to configure preparators

**values:** Any number of &lt;preparator&gt; child tags.

**example:**
```xml
<preparatorList>
  <preparator> ... </preparator>
  <preparator> ... </preparator>
  ...
</preparatorList>
```

### &lt;preparator&gt; tag
Child tag of the [&lt;preparatorList&gt; tag](/en/config/crawlerconfiguration_xml/#preparatorlist-tag).

**role:** Contains the settings for one [preparator](/en/config/components/preparator/).

**attribute `enabled`:** Specifies whether the preparator is enabled. (**value:** `true` or `false`, **default:** `true`)

**values:** Knows the following child tags:
  * `<class>`: The class name of the preparator.
  * `<urlPattern>`: The regular expression a URL must match.
  * `<config>`: The configuration of the preparator.

**example:**
```xml
<preparator>
  <class>de.murfman.mypackage.MyPreparator</class>
  <config> ... </config>
</preparator>
```

#### &lt;class&gt; tag
Child tag of the [&lt;preparator&gt; tag](/en/config/crawlerconfiguration_xml/#preparator-tag).

**role:** The class name of the preparator.

**values:** A fully classified class name. If the class is of the package `net.sf.regain.crawler.preparator`, the package may be abbreviated with a dot.

**example:**
```xml
<class>de.murfman.mypackage.MyPreparator</class>
```
or
```xml
<class>.HtmlPreparator</class>
```

#### &lt;urlPattern&gt; tag
Child tag of the [&lt;preparator&gt; tag](/en/config/crawlerconfiguration_xml/#preparator-tag).

**role:** The regular expression a URL must match to, to be prepared by this preparator. If specified, the regular expression used internally by the preparator is overridden.

**values:** A [regular expression](/en/config/regular_expression/).

**since version:** 1.1 Beta 5

**example:**
```xml
<urlPattern>\.(html|jsp)$</urlPattern>
```

#### &lt;config&gt; tag
Child tag of the [&lt;preparator&gt; tag](/en/config/crawlerconfiguration_xml/#preparator-tag).

**role:** The configuration of the preparator.

**attribute `file`:** If this attribute is set, the preparator configuration is loaded from an extra file (**values:** A file name).

**values:** Any number of &lt;section&gt; child tags.

**example:**
```xml
<config>
  <section> ... </section>
  <section> ... </section>
  ...
</config>
```

##### &lt;section&gt; tag
Child tag of the [&lt;config&gt; tag](/en/config/crawlerconfiguration_xml/#config-tag).

**role:** One section of the preparator configuration.

Which sections are provided depends on the particular preparator.

**attribute `name`:** The name of the section (**values:** A section name).

**values:** Any number of &lt;param&gt; child tags.

**example:**
```xml
<section>
  <param name="parameter1">value1</param>
  <param name="parameter2">value2</param>
  ...
</section>
```

**&lt;param&gt; tag**
Child tag of the [&lt;section&gt; tag](/en/config/crawlerconfiguration_xml/#section-tag).

**role:** A parameter of the preparator configuration.

Which parameters are provided depends on the particular preparator.

**attribute `name`:** The name of the parameter (**values:** A parameter name).

**values:** The configured value.

**example:**
```xml
<param name="aParam">the value</param>
```

&lt;crawlerPluginList&gt; tag
-----------------------------

**role:** Contains the [crawler_plugins](/en/config/components/crawler_plugins/) in the order they should be applied. Plugins that aren't listed here, but present in the folder `/plugins`, will be registered at the end..

You can use this list
  * to define the priority (order) of the plugins
  * to disable plugins
  * to configure plugins

**values:** Any number of &lt;crawlerPlugin&gt; child tags.

**since version:** 1.7.8 Preview

**example:**
```xml
<crawlerPluginList>
  <crawlerPlugin> ... </crawlerPlugin>
  <crawlerPlugin> ... </crawlerPlugin>
  ...
</crawlerPluginList>
```

### &lt;crawlerPlugin&gt; tag
Child tag of the [&lt;crawlerPluginList&gt; tag](/en/config/crawlerconfiguration_xml/#crawlerpluginlist-tag).

**role:** Contains the settings for one [crawler_plugins](/en/config/components/crawler_plugins/).

**attribute `enabled`:** Specifies whether the plugin is enabled. (**value:** `true` or `false`, **default:** `true`)

**values:** Knows the following child tags:
  * `<class>`: The class name of the plugin.
  * `<config>`: The configuration of the plugin.

**since version:** 1.7.8 Preview

**example:**
```xml
<crawlerPlugin>
  <class>de.murfman.mypackage.MyPlugin</class>
  <config> ... </config>
</crawlerPlugin>
```

#### &lt;class&gt; tag
Child tag of the [&lt;crawlerPlugin&gt; tag](/en/config/crawlerconfiguration_xml/#crawlerplugin-tag).

**role:** The class name of the plugin.

**values:** A fully classified class name.

**since version:** 1.7.8 Preview

**example:**
```xml
<class>de.murfman.mypackage.MyPreparator</class>
```

#### &lt;config&gt; tag
Child tag of the [&lt;crawlerPlugin&gt; tag](/en/config/crawlerconfiguration_xml/#crawlerplugin-tag).

**role:** The configuration of the plugin.

**attribute `file`:** If this attribute is set, the plugin configuration is loaded from an extra file (**values:** A file name).

**values:** Any number of &lt;section&gt; child tags.

**since version:** 1.7.8 Preview

**example:**
```xml
<config>
  <section> ... </section>
  <section> ... </section>
  ...
</config>
```

##### &lt;section&gt; tag
Child tag of the [&lt;config&gt; tag](/en/config/crawlerconfiguration_xml/#config-tag).

**role:** One section of the plugin configuration.

Which sections are provided depends on the particular plugin.

**attribute `name`:** The name of the section (**values:** A section name).

**values:** Any number of &lt;param&gt; child tags.

**since version:** 1.7.8 Preview

**example:**
```xml
<section>
  <param name="parameter1">value1</param>
  <param name="parameter2">value2</param>
  ...
</section>
```

**&lt;param&gt; tag**
Child tag of the [&lt;section&gt; tag](/en/config/crawlerconfiguration_xml/#section-tag).

**role:** A parameter of the plugin configuration.

Which parameters are provided depends on the particular plugin.

**attribute `name`:** The name of the parameter (**values:** A parameter name).

**values:** The configured value.

**since version:** 1.7.8 Preview

**example:**
```xml
<param name="aParam">the value</param>
```

&lt;auxiliaryFieldList&gt; tag
------------------------------

**role:** A list of [auxiliary fields](/en/features/auxiliary_fields/).

The [search index](/en/components/search_index/) may be extended by auxiliary fields that are generated from the document's URL.

Example: Assumed you have a directory with a sub directory for every project. Then you can generate an auxiliary field with the project name. When searching for `offer project:otto23` you will only get results from that project directory.

The following tag generates an auxiliary field `project` with the value `otto23` from the URL `file://c:/projects/otto23/docs/Spez.doc`:

```xml
<auxiliaryField name="project" regexGroup="1">
  ^file://c:/projects/([^/]**)
</auxiliaryField>
```

**values:** Any number of &lt;auxiliaryField&gt; child tags.

**example:**
```xml
<auxiliaryFieldList>
  <auxiliaryField> ... </auxiliaryField>
  <auxiliaryField> ... </auxiliaryField>
  ...
</auxiliaryFieldList>
```

### &lt;auxiliaryField&gt; tag
Child tag of the [&lt;auxiliaryFieldList&gt; tag](/en/config/crawlerconfiguration_xml/#auxiliaryfieldlist-tag).

**role:** The definition of an [auxiliary field](/en/features/auxiliary_fields/).

In order to define the value the auxiliary field should get, use either the attribute `value` (for fixed values) or the attribute `regexGroup` (for values extracted from the URL), not both.

**attribute `name`:** The name of the auxiliary field. (**value:** A name, **example:** `project` or `system`)

**attribute `value`:** The value the auxiliary field should get. (**value:** A string, **example:** `letters`, **Since version:** 1.1 Beta 6)

**attribute `regexGroup`:** The number of the [regular expression](/en/config/regular_expression/) group that contains the value the auxiliary field should get. (**value:** A number)

**attribute `toLowerCase`:** Specifies whether the value extracted by `regexGroup` should be converted to lower case. (**value:** `true` or `false` Optional. Default is `true`, **Since version:** 1.1 Beta 6)

**values:** A [regular expression](/en/config/regular_expression/).

**example** (value extracted from the URL):
```xml
<auxiliaryField name="project" regexGroup="1">^file://c:/projects/([^/]**)</auxiliaryField>
```

**example** (fixed value):
```xml
<auxiliaryField name="doctype" value="letters">^file://c:/docs/letters</auxiliaryField>
<auxiliaryField name="doctype" value="images">^file://c:/docs/(images|cliparts)</auxiliaryField>
<auxiliaryField name="doctype" value="photos">^file://c:/docs/photos</auxiliaryField>
```

&lt;loadUnparsedUrls&gt; tag
----------------------------

**role:** Specifies whether URLs should be loaded that are neither parsed nor indexed.

By this means dead links can be detected. This function may also be used to fill the cache of the server.

**values:** `true` or `false`

**example:**
```xml
<loadUnparsedUrls>false</loadUnparsedUrls>
```

&lt;httpTimeout&gt; tag
-----------------------

**role:** Specifies the maximum time in seconds, a HTTP download may take in total.

**values:** A number.

**example:**
```xml
<httpTimeout>180</httpTimeout>
```

&lt;userAgent&gt; tag
---------------------

**role:** Sets the user agent the crawler should use for identifying at the HTTP server(s).

**values:** A string.

**since version:** 1.1 Beta 6

**example:** Use the following userAgent to identify at web servers as Internet Explorer.
```xml
<userAgent>Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)</userAgent>
```

&lt;useLinkTextAsTitleList&gt; tag
----------------------------------

**role:** Contains a list of [regular expression](/en/config/regular_expression/)s that must match to the URL of a document that should use the text of the link that pointed to the document as title instead of the real document title.

**values:** Any number of [&lt;urlPattern&gt; tag](/en/config/crawlerconfiguration_xml/#urlpattern-tag)s.

**example:**
```xml
<useLinkTextAsTitleList>
  <urlPattern> ... </urlPattern>
</useLinkTextAsTitleList>
```

### &lt;urlPattern&gt; tag
Child tag of the [&lt;useLinkTextAsTitleList&gt; tag](/en/config/crawlerconfiguration_xml/#uselinktextastitlelist-tag).

**role:** A [regular expression](/en/config/regular_expression/) that matches to a document that should use the link text as title.

**values:** A [regular expression](/en/config/regular_expression/).

**example:**
```xml
<urlPattern>^http://.**\.(pdf|xls|doc|rtf)$</urlPattern>
```

&lt;controlFiles&gt; tag
------------------------

**role:** Contains the names of the control files.

The control files may be used for controlling a script for instance.

**optional:** This tag is optional.

**values:** Knows the following child tags:
  * `<finishedWithoutFatalsFile>`: The control file for successful index creation.
  * `<finishedWithFatalsFile>`: The control file for failed index creation.

**example:**
```xml
<controlFiles>
  <finishedWithoutFatalsFile>C:\lucene\control\NoFatals</finishedWithoutFatalsFile>
  <finishedWithFatalsFile>C:\lucene\control\WithFatals</finishedWithFatalsFile>
</controlFiles>
```

### &lt;finishedWithoutFatalsFile&gt; tag
Child tag of the [&lt;controlFiles&gt; tag](/en/config/crawlerconfiguration_xml/#controlfiles-tag).

**role:** The control file for successful index creation.

This file is created, if an index was successfully created.

**optional:** This tag is optional.

**values:** A file name.

**example:**
```xml
<finishedWithoutFatalsFile>C:\lucene\control\NoFatals</finishedWithoutFatalsFile>
```

### &lt;finishedWithoutFatalsFile&gt; tag
Child tag of the [&lt;controlFiles&gt; tag](/en/config/crawlerconfiguration_xml/#controlfiles-tag).

**role:** The control file for failed index creation.

This file is created, if an index creation failed.

**optional:** This tag is optional.

**values:** A file name.

**example:**
```xml
<finishedWithoutFatalsFile>C:\lucene\control\WithFatals</finishedWithoutFatalsFile>
```

&lt;crawlerAccessController&gt; tag
-----------------------------------

**role:** The CrawlerAccessController to use.

This is a part of the [access rights management](/en/features/access_rights_management/) that ensures that only those documents are shown in the search results that the user is allowed to read.

If you specify a `CrawlerAccessController`, don't forget to specify the `SearchAccessController` counterpart in the [SearchConfiguration.xml](/en/config/searchconfiguration_xml/#searchaccesscontroller-tag)!

**values:** Knows the following child tags:
  * `<class>`: The class name of the `CrawlerAccessController`.
  * `<config>`: The configuration of the `CrawlerAccessController`.

**since version:** 1.1 Beta 4

**example:**
```xml
<crawlerAccessController>
  <class jar="myAccess.jar">mypackage.MyCrawlerAccessController</class>
  <config> ... </config>
</crawlerAccessController>
```

### &lt;class&gt; tag
Child tag of the [&lt;crawlerAccessController&gt; tag](/en/config/crawlerconfiguration_xml/#crawleraccesscontroller-tag).

**role:** The class name of the `CrawlerAccessController`.

**attribute `jar`:** The name of the jar file, where the `CrawlerAccessController` class is included. May be omitted, if the class is already in the classpath.

**values:** A fully classified class name.

**since version:** 1.1 Beta 4

**example:**
```xml
<class jar="myAccess.jar">mypackage.MyCrawlerAccessController</class>
```

### &lt;config&gt; tag
Child tag of the [&lt;crawlerAccessController&gt; tag](/en/config/crawlerconfiguration_xml/#crawleraccesscontroller-tag).

**role:** The configuration of the `CrawlerAccessController`.

**values:** Any number of &lt;param&gt; child tags.

**since version:** 1.1 Beta 4

**example:**
```xml
<config>
  <param name="param1">value1</param>
  <param name="param2">value2</param>
</config>
```

#### &lt;param&gt; tag
Child tag of the [&lt;config&gt; tag](/en/config/crawlerconfiguration_xml/#config-tag).

**role:** A parameter of the `CrawlerAccessController` configuration.

**attribute `name`:** The name of the parameter (**values:** A parameter name).

**values:** The configured value.

**since version:** 1.1 Beta 4

**example:**
```xml
<param name="scriptPath">c:\regain\access\getGroups.cmd</param>
```

&lt;htmlParserPatternList&gt; tag
---------------------------------

**role:** A list of patterns that are used for identifying URLs when a HTML document is parsed.

**values:** Any number of &lt;pattern&gt; child tags.

**example:**
```xml
<htmlParserPatternList>
  <pattern> ... </pattern>
  <pattern> ... </pattern>
  ...
</htmlParserPatternList>
```

### &lt;pattern&gt; tag
Child tag of the [&lt;htmlParserPatternList&gt; tag](/en/config/crawlerconfiguration_xml/#htmlparserpatternlist-tag).

**role:** A pattern that finds a URL in a HTML document.

**attribute `parse`:** Specifies whether a found document should be parsed for URLs as well.  (**values:** `true` or `false`)

**attribute `index`:** Specifies whether a found document should be indexed.  (**values:** `true` or `false`)

**attribute `regexGroup`:** The number of the [regular expression](/en/config/regular_expression/) group that contains the URL.  (**values:** A number)

**values:** A [regular expression](/en/config/regular_expression/).

**example:**
```xml
<pattern parse="false" index="true" regexGroup="1">="([^"]**\.(doc|pdf|rtf))"</pattern>
```
