---
title: "SearchConfiguration.xml"
---

[Deutsche Übersetzung](/de/config/searchconfiguration_xml/)

SearchConfiguration.xml
=======================

The **SearchConfiguration.xml** contains the configuration of the [search mask](/en/components/search_mask/).


Cascaded settings
-----------------
The search mask provides searching several [indices](/en/components/search_index_/). For each index you can specify, where it is located and how the results of this index should be presented.

All settings, except of the index location, may be specified as cascaded settings. I.e. if you didn't specify a setting in the particular `<index>` tag, the search mask checks whether you specified it in the `<defaultSettings>` tag. If it is missing here too, the default setting is used.

That way you can specifiy default settings that apply for all indices. If you want another setting for one index however, you can override the default setting by specifying something else in the particular `<index>` tag.


The location of the SearchConfiguration.xml
-------------------------------------------
In order to load the `SearchConfiguration.xml`, the [search mask](/en/components/search_mask/) must know where it is located. The [desktop search](/en/project_info/variant_comparison/) expects the `SearchConfiguration.xml` in the `conf` sub directory. The [server search](/en/project_info/variant_comparison/) takes the location from the `web.xml`. The default expects it in the `conf/regain` of the tomcat directory.


&lt;indexList&gt; tag
---------------------
**role:** Contains the settings for the indices.

**values:** Knows the following child tags:
  * `<defaultSettings>`: The cascaded default settings.
  * `<index>`: The settings for one index.

**example:**
```xml
<indexList>
  <defaultSettings> ... </defaultSettings>
  <index> ... </index>
  <index> ... </index>
  ...
</indexList>
```


### &lt;defaultSettings&gt; tag
Child tag of the [&lt;indexList&gt; tag](/en/config/searchconfiguration_xml/#indexlist-tag).

**role:** The cascaded default settings.

**values:** All tags that are allowed in the [&lt;index&gt; tag](/en/config/crawlerconfiguration_xml/#index-tag), except for the [&lt;dir&gt; tag](/en/config/crawlerconfiguration_xml/#dir-tag).

**example:**
```xml
<defaultSettings>
  <openInNewWindowRegex>.(pdf|rtf|doc|xls|ppt|docx|xlsx|pptx)$</openInNewWindowRegex>
  <useFileToHttpBridge>true</useFileToHttpBridge>
  <searchFieldList>content title headlines location filename</searchFieldList>
  <rewriteRules> ... </rewriteRules>
  <Highlighting>true</Highlighting>
  <sortResults showsortfieldcontent="false">
    <sortEntry id='1' description='relevance desc' order='desc' field='relevance' />
    <sortEntry id='2' description='last modified date asc' order='asc' field='last-modified' />
    <sortEntry id='3' description='last modified date desc' order='desc' field='last-modified' />
  </sortResults>
</defaultSettings>
```

#### &lt;Highlighting&gt; tag
**role:** Enables or disables the highlighting of the search terms in title and summary of a search hit. Highlighting doesn't work for wildcard searches e.g. regai*.

**values:** true or false

#### &lt;sortResults&gt; tag
**role:** Defines the sorting options for the search mask. 

**attribute `showsortfieldcontent`:** A flag for displaying the content of the sort field on the current document. Possible values are **`true`** and **`false`**. Default setting is **`false`**.

**values:**
```xml
      <sortEntry id='' description='' order='' field='' />
      <sortEntry id='' description='' order='' field='' />
      ....
```
Each &lt;sortEntry/&gt; defines an entry in the dropdown list on every search page. 

**attribute `id`:** The entries in the dropdown list are sorted by `id`. The ids must be positive. 

**attribute `description`:** The shown description in the dropdown list.

**attribute `order`:** The sorting order for lucene. Possible values are **`asc`** and **`desc`**

**attribute `field`:** The document field name on which the sort will be performed. Possible values are:

  * **`relevance`** (the scoring of the hit regarding to index size and matching on different fields)
  * **`size`** (the document size) 
  * **`last-modified`** (the last modification date of the document, in case of an web document: the crawling date)
  * **`filename_sort`** (the filename of the document, without the path)
  * **`mimetype`** (the detected mimetype of the document)
  * **`title_sort`** (the title of the document, mostly set for web documents)
  * **`path_sort`** (the path of the document)

**example:**
```xml
  <sortResults showsortfieldcontent="false">
    <sortEntry id='1' description='relevance desc' order='desc' field='relevance' />
    <sortEntry id='2' description='last modified date asc' order='asc' field='last-modified' />
    <sortEntry id='3' description='last modified date desc' order='desc' field='last-modified' />
    <sortEntry id='4' description='document size asc' order='asc' field='size' />
    <sortEntry id='5' description='document size desc' order='desc' field='size' />
    <sortEntry id='6' description='file name asc' order='asc' field='filename_sort' />
    <sortEntry id='7' description='file name desc' order='desc' field='filename_sort' />
    <sortEntry id='8' description='mimetype asc' order='asc' field='mimetype' />
    <sortEntry id='9' description='mimetype desc' order='desc' field='mimetype' />
    <sortEntry id='10' description='title asc' order='asc' field='title_sort' />
    <sortEntry id='11' description='titel desc' order='desc' field='title_sort' />
    <sortEntry id='12' description='path asc' order='asc' field='path_sort' />
    <sortEntry id='13' description='path desc' order='desc' field='path_sort' />
  </sortResults>
```


### &lt;index&gt; tag
Child tag of the [&lt;indexList&gt; tag](/en/config/searchconfiguration_xml/#indexlist-tag).

**role:** The settings for one [search index](/en/components/search_index/).

**attribute `name`:** The name of the index. (**values:** A unique name, **example:** `mydocs`)

**values:** Knows the following child tags:
  * `<dir>`: The directory where the [search index](/en/components/search_index/) is located.
  * `<openInNewWindowRegex>`: The [regular expression](/en/config/regular_expression/) that matches URLs that should be opened in a new browser window.
  * `<useFileToHttpBridge>`: Specifies whether the [file-to-http-bridge](/en/features/file-to-http-bridge/) should be used for file-URLs.
  * `<searchFieldList>`: The [index field](/en/components/search_index/)s that should be searched by default.
  * `<rewriteRules>`: The rules for the url rewriting.

**example:**
```xml
<index name="intranet">
  <dir>C:\regain\index</dir>
  <openInNewWindowRegex> ... </openInNewWindowRegex>
  <useFileToHttpBridge>true</useFileToHttpBridge>
  <searchFieldList> ... </searchFieldList>
  <rewriteRules> ... </rewriteRules>
</index>
```
or just:
```xml
<index name="mydocs">
  <dir>C:\regain\index_mydocs</dir>
</index>
```


#### &lt;dir&gt; tag
Child tag of the [&lt;index&gt; tag](/en/config/searchconfiguration_xml/#index-tag).

**role:** The directory where the [search index](/en/components/search_index/) is located.

**values:** A directory.

**example:**
```xml
<dir>C:\regain\index</dir>
```


#### &lt;openInNewWindowRegex&gt; tag
Child tag of the [&lt;index&gt; tag](/en/config/searchconfiguration_xml/#index-tag) or the [&lt;defaultSettings&gt; tag](/en/config/searchconfiguration_xml/#defaultsettings-tag).

**role:** The [regular expression](/en/config/regular_expression/) that matches URLs that should be opened in a new browser window.

**values:** A [regular expression](/en/config/regular_expression/).

**example:**
```xml
<openInNewWindowRegex>.(pdf|rtf|doc|xls|ppt)$</openInNewWindowRegex>
```


#### &lt;useFileToHttpBridge&gt; tag
Child tag of the [&lt;index&gt; tag](/en/config/searchconfiguration_xml/#index-tag) or the [&lt;defaultSettings&gt; tag](/en/config/searchconfiguration_xml/#defaultsettings-tag).

**role:** Specifies whether the [file-to-http-bridge](/en/features/file-to-http-bridge/) should be used for file-URLs.

**values:** `true` or `false`.

**since version:** 1.1 Beta 5

**example:**
```xml
<useFileToHttpBridge>true</useFileToHttpBridge>
```


#### &lt;searchFieldList&gt; tag
Child tag of the [&lt;index&gt; tag](/en/config/searchconfiguration_xml/#index-tag) or the [&lt;defaultSettings&gt; tag](/en/config/searchconfiguration_xml/#defaultsettings-tag).

**role:** The [index field](/en/components/search_index/)s that should be searched by default.

`Note:` The user may also search in other fields using the field operator. See [terminology](/en/terminology/#query-syntax) for details.

**values:** A space seaparated list of index field names.

**example:**
```xml
<searchFieldList>content title headlines</searchFieldList>
```


#### &lt;rewriteRules&gt; tag
Child tag of the [&lt;index&gt; tag](/en/config/searchconfiguration_xml/#index-tag) or the [&lt;defaultSettings&gt; tag](/en/config/searchconfiguration_xml/#defaultsettings-tag).

**role:** The rules for the url rewriting.

For the result presentation you can use the so called URL-rewriting. I.e. that the URL of the document is changed.

This way you can index documents in `file://c:/www‑data/intranet/docs` and show the documents in the browser as `http://intranet.murfman.de/docs`.

If none of the rule matches to a URL, it will remain unchanged.

**values:** Knows the following child tags:
  * `<rule>`: A replacement rule.

**example:**
```xml
<rewriteRules>
  <nowiki><rule prefix="file://c:/example/www-data" replacement="http://www.mydomain.de"/></nowiki>
</rewriteRules>
```


##### &lt;rule&gt; tag
Child tag of the [&lt;rewriteRules&gt; tag](/en/config/searchconfiguration_xml/#rewriterules-tag).

**role:** A replacement rule for the url rewriting.

**attribute `prefix`:** The URL prefix to replace. (**values:** A URL prefix, **example:** `file://c:/www‑data/intranet/docs`)

**attribute `replacement`:** The URL prefix that should be shown instead. (**values:** A URL prefix, **example:** `http://intranet.murfman.de/docs`)

**example:** With these example attribute values the URL `file://c:/www‑data/intranet/docs/manual/regain.pdf` will be changed in `http://intranet.murfman.de/docs/manual/regain.pdf`.
```xml
<rule prefix="file://c:/example/www-data" replacement="http://www.mydomain.de"/>
```


#### &lt;searchAccessController&gt; tag
Child tag of the [&lt;index&gt; tag](/en/config/searchconfiguration_xml/#index-tag) or the [&lt;defaultSettings&gt; tag](/en/config/searchconfiguration_xml/#defaultsettings-tag).

**role:** The SearchAccessController to use.

This is a part of the [access rights management](/en/features/access_rights_management/) that ensures that only those documents are shown in the search results that the user is allowed to read.

If you specify a `SearchAccessController`, don't forget to specify the `CrawlerAccessController` counterpart in the [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/#crawleraccesscontroller-tag)!

**values:** Knows the following child tags:
  * `<class>`: The class name of the `SearchAccessController`.
  * `<config>`: The configuration of the `SearchAccessController`.

**since version:** 1.1 Beta 4

**example:**
```xml
<searchAccessController>
  <class jar="myAccess.jar">mypackage.MySearchAccessController</class>
  <config> ... </config>
</searchAccessController>
```


##### &lt;class&gt; tag
Child tag of the [&lt;searchAccessController&gt; tag](/en/config/searchconfiguration_xml/#searchaccesscontroller-tag).

**role:** The class name of the `SearchAccessController`.

**attribute `jar`:** The name of the jar file, where the `SearchAccessController` class is included. May be omitted, if the class is already in the classpath.

**values:** A fully classified class name.

**since version:** 1.1 Beta 4

**example:**
```xml
<class jar="myAccess.jar">mypackage.MySearchAccessController</class>
```


##### &lt;config&gt; tag
Child tag of the [&lt;crawlerAccessController&gt; tag](/en/config/searchconfiguration_xml/#crawleraccesscontroller-tag).

**role:** The configuration of the `SearchAccessController`.

**values:** Any number of &lt;param&gt; child tags.

**since version:** 1.1 Beta 4

**example:**
```xml
<config>
  <param name="param1">value1</param>
  <param name="param2">value2</param>
</config>
```


**&lt;param&gt; tag**
Child tag of the [&lt;config&gt; tag](/en/config/searchconfiguration_xml/#config-tag).

**role:** A parameter of the `SearchAccessController` configuration.

**attribute `name`:** The name of the parameter (**values:** A parameter name).

**values:** The configured value.

**since version:** 1.1 Beta 4

**example:**
```xml
<param name="scriptPath">c:\regain\access\getUserGroups.cmd</param>
```
