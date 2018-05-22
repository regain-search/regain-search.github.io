---
title: "Crawler Plugins"
---

[Deutsche Übersetzung](/de/components/crawler_plugins/)

Crawler Plugins
===============

Crawler Plugins hook into the [crawling process](/en/components/project_info/crawling_process/) in order to add advanced functionality. 

### What can crawler plugins do?
Some examples:


     * Modify the result of preparators
       * by specifying default-values if the chosen preparator does not fill in a certain field (''onBeforePrepare'')
       * by overriding or modyfing the results of whatever preparator was chosen (''onAfterPrepare'')
     * Modify their storage in the lucene index
     * Do sth at every start or end of the crawling process (e.g. inform the administrator via email)


### How to create a crawler plugin

  - Create a class that implements `CrawlerPlugin`.
  - Packaged it (and all its dependencies) as a .jar

      * In the manifest file, the attribute ''Plugin-Class'' must be set to the complete class name of the implementing class.
  - Drop it into the `plugins`-Directory.


### Crawler Plugin API

#### onStartCrawling

`void onStartCrawling(Crawler crawler)`

Called before the crawling process starts (`Crawler::run()`).

This may be called multiple times during the lifetime of a plugin instance,
but [onFinishCrawling()](/en/components/crawler_plugins/#onfinishcrawling) is always called in between.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| crawler             | The crawler instance that is about to begin crawling     | 

#### onFinishCrawling

`void onFinishCrawling(Crawler crawler)`

Called after the crawling process has finished or aborted (because of an exception).

This may be called multiple times during the lifetime of a plugin instance.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| crawler             | The crawler instance that is about to begin crawling     | 

#### checkDynamicBlacklist

`boolean checkDynamicBlacklist(String url, String sourceUrl, String sourceLinkText)`

Allows to blacklist specific URLs.

This function is called when the URL would normally be accepted, i.e. included in whitelist, not included in blacklist.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| url             | URL of the crawling job that should normally be added.     | 
| sourceUrl             | The URL where the url above has been found (&lt;a&gt;-Tag, PDF or similar)     | 
| sourceLinkText | The label of the URL in the document where the url above has been found. |

**Returns**:

`True`: blacklist this URL. `False`: Allow this URL.

If at least one of the crawler plugins returns true, the file will be treated as blacklisted.

#### onAcceptURL

`void onAcceptURL(String url, CrawlerJob job)`

Called during the crawling process when a new URL is added to the processing Queue.

As the queue is filled recursively, these calls can come between prepare Calls.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| url             | URL that just was accepted     | 
| job             | CrawlerJob that was created as a consequence     | 

#### onDeclineURL

`void onDeclineURL(String url)`

Called during the crawling process when a new URL is declined to be added to the processing Queue.

Note that ignored URLs (that is, URL that were already accepted or declined before), do not appear here.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| url             | URL that just was declined     | 

#### onCreateIndexEntry

`void onCreateIndexEntry(Document doc, IndexWriter index)`

Called when a document as added to the index.

This may be a newly indexed document, or a document that has changed since
and, thus, is reindexed.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| doc             | Document to write     |
| index             | Lucene Index Writer     |  

#### onDeleteIndexEntry

`void onDeleteIndexEntry(Document doc, IndexReader index)`

Called when a document is deleted from the index.

Note that when being replaced by another document ("update index"),
the old document is added to index first, deleting is part of the cleaning-up-at-the-end-Phase.

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| doc             | Document to read     |
| index             | Lucene Index Reader     |  

#### onBeforePrepare

`void onBeforePrepare(RawDocument document, WriteablePreparator preparator)`

Called before a document is being prepared to be added to the index.
(Good point to fill in default values.)

**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| document		| Regain document that will be analysed |
| preparator	 | Preperator that was chosen to analyse this document |

#### onAfterPrepare

`void onAfterPrepare(RawDocument document, WriteablePreparator preparator)`

Called after a document is being prepared to be added to the index.
Here you can override the results of the preperator, if necessary.


**Parameters**: 
| Parameter Name       | Description                                              |
| --- | --- |
| document		| Regain document that was analysed |
| preparator	 | Preperator that has analysed this document |


### Existing Plugins

  * **FilesizeFilterPlugin** (included in regain): Blacklist files that have a filesize below or above a certain treshold
  * [JavaThumbnailer](https://github.com/benjamin4ruby/java-thumbnailer): Create Thumbnails of indexed documents

