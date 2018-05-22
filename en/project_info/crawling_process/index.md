---
title: "Crawling Process"
---

[Deutsche Übersetzung](/de/project_info/crawling_process/)

Crawling Process
================

How does the crawling process work? Where do the [Crawler Plugins](/en/project_info/components/crawler_plugins/) interact?

At the beginning, `__onStartCrawling(Crawler)__` is called for all plugins.

#### 1. Creating the job queue


     * According to the Crawling [[features:white_and_black_list|Whitelist and Blacklist]], the start URLs are added to the job queue (Crawler::addJob) (''__onAcceptURL(String url, CrawlerJob job)__'' or ''__onDeclineURL(String url)__'' is called to inform the plugin)
        * If a job would be accepted, the crawler plugins are asked if they want to blacklist it anyway (''__boolean checkDynamicBlacklist(String url, String sourceUrl, String sourceLinkText)__'' - if at least one of the plugins returns true, the file isn't indexed.)
     * Recursively, all entries are checked: (Crawler::run)
        * If they are folders (and should be indexed), their content is added to the job queue
        * If they are files (and should be parsed), their content is analysed in order to add new URL to the job queue
        * If they are files (and should be indexed), then it is indexed according to the next section.

#### 2. Indexing a single document


     *(Note that a document (RawDocument) may be a file, a file on a network share (smb), a HTTP-Request, or an IMAP-Message).
     * First, verify if the document already exists in the index (IndexWriterManager::addToIndex)
        * If so, check if it was indexed recently (less than a day ago) by comparing their lastModified-time.
           * If it was indexed recently, stop this process and continue with the next document.
           * If it was indexed more than 1 day ago, or this cannot be checked (HTTP), then delete the current entry and proceed (Note: It is not deleted immediatly, but rather at the end of the crawling process (IndexWriterManager::removeObsoleteEntries). That is also when ''__onDeleteIndexEntry(Document doc, IndexReader index)__'' will be called (just before deletion).)
     * Create a new Index entry (IndexWriterManager::createNewIndexEntry)
     * First the document is prepared for indexation (DocumentFactory::createDocument)
        * [[features:auxiliary_fields|Auxiliary Fields]] are calculated.
        * The [[features:access_rights_management|Crawler Access Controller]] (if available) is asked to retrieve the allowed groups.
        * The MIME-Type is identified.(org.semanticdesktop.aperture.mime.identifier.magic.MagicMimeTypeIdentifier::identify())
        * All preparators are collected which accept this MIME-Type.
        * The preparator with the highest priority is executed. (DocumentFactory::createDocument)
          * Before (''__onBeforePrepare(RawDocument document, WriteablePreparator preparator)__'') and after (''__onAfterPrepare(RawDocument document, WriteablePreparator preparator)__'') the actual preparation, the plugins are called. 
        * If he fails, then an empty document is returned (DocumentFactory::createSubstituteDocument).
     * Then it is added to the [[http://lucene.apache.org|Lucene]] [[components:search_index|index]], after notification of the plugins (''__onCreateIndexEntry(Document doc, IndexWriter index)__'').

At the end, `__onFinishCrawling(Crawler)__` is called.