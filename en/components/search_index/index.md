---
title: "Search index"
---

[Deutsche Übersetzung](/de/components/search_index/)

Search index
============

The **search index** stores the data about the documents in a way, so that documents containing a certain key word may be found rapidly on search request. Because of the index's smart design a search over many thousands of documents can be performed in parts of a second.

regain uses [Lucene](http://lucene.apache.org) for the index [creation](/en/components/crawler/) and the index based [search](/en/components/search_mask/). Lucene separates the data about a document in several classified fields. So you may decide which fields shall be queried.

A search request "`regain extension:pdf`" for instance will look for `regain` in the default fields as well as for `pdf` inside the `extension` field.

What fields are [seeked](/en/components/search_mask/) by default, will be configured in file [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) using the [tag `searchFieldList`](/en/config/searchconfiguration_xml/#.3csearchfieldlist.3e_tag). The default search fields are `content`, `title` and `headlines`.

Standard fields
---------------

regain creates the following standard fields:
  * `url` - The document's URL.
  * `content` - The document´s text extracted by the [preparator](/en/components/preparator/). 
  * `title` - The document's title (if it has any).
  * `summary` - The summary shown in the hit list.
  * `headlines` - The headlines (if there are any) contained in the document.
  * `size` - The document's size in bytes (can't be searched).
  * `last-modified` - The date of the last change in the `YYYY-MM-DD HH:MM` format (can't be searched).
  * `path` - The navigation path to the document. (can't be searched)
  * `groups` - Contains the user groups that are allowed to read the document. Is set only when the [access rights management](/en/features/access_rights_management/) is enabled.
  * [Further fields may be added](/en/features/auxiliary_fields/). The default configuration adds a field `extension` storing the document´s file extension (e.g. `pdf`).

Important Notes:
  * If [content extraction](/en/components/preparator/) fails no `content` field is established! Instead of this the `preparation-error` field is created and set to `true`.
  * It depends on the capabilities of the [preparators](/en/components/preparator/) used for [crawling](/en/components/crawler/) the files, what will be finally stored in the default fields (e.g. `content`, `title` and `headlines`)!
  * [lukeall](http://www.dotlucene.net/documentation/ToolforAnalyzingLuceneInd.html) or [Lucene Index Toolbox](http://www.getopt.org/luke/) may be helpfully to have a look inside the index. 

The index directory
-------------------

In the '`index directory`' regain puts the search indexes. The indexes are stored in different sub directories, depending in which phase of their life cycle they are.

regain uses the following sub directories:
  * `temp` - An index in this directory is currently changed by the [crawler](/en/components/crawler/).
  * `breakpoint` - Periodically the crawler creates [breakpoint](/en/features/breakpoint/)s. If the crawler is stopped before it finished the new index (e.g. when the computer is shut down), then it is able to proceed from the last breakpoint when it is started the next time and doesn't have to start from the beginning.
  * `new` - When the crawler finished the index, it renames the diretory to `new`. This directory is the interface between [crawler](/en/components/crawler/) and [search mask](/en/components/search_mask/). The search mask regularily checks, if there is an index with the state `new` in the index directory. If it finds such an index it changes to that index, that is it renames the directory to `index`. In this way the [hot deployment](/en/features/hot_deployment/) is implemented.
  * `quarantine` - If the crawler finished an index but had many errors, the new index doesn't get the state `new` but `quarantine`. In this way the [search mask](/en/components/search_mask/) doesn't change to the faulty index automatically. In this case you should [check the log file](/en/config/howto_find_error_cause/) and, if you want to change to that index, rename the directory to `new`.
  * `index` - This index is currently used by the search mask.
  * `backup` - Before the search mask changes to the new index, it renames the old index to `backup`. If a new index should be faulty, you are able to quickly switch to the previous index by renaming the directory `backup` to `new`.
