---
title: "regain features"
---

[Deutsche Übersetzung](/de/features/)

regain features
===============

regain offers lots of very useful functions that are important for an effective search engine.


Search
------

  * regain uses the powerful search syntax of Lucene. Thus it is possible to express very specific search queries. The most important possibilities are the following:

      * Boolean operators
      * Wildcards
      * Phonetic search
      * Grouping
      * and much more. You can find more information about the search syntax [[http://jakarta.apache.org/lucene/docs/queryparsersyntax.html|here]].
  * [Multi index search](/en/features/multi_index_search/): Search multiple indexes with one search mask. Totally transparent for the user.
  * URL-Rewriting: You can use URL-Rewriting at your search. This enables you to index documents from `file://c:/www-data/intranet/docs` and show them in the browser as `http://intranet.murfman.de/docs`.
  * Advanced search: All values that are in the index for one field may now be provided as a drop down list on the search page. Particularly together with [auxiliary fields](/en/features/auxiliary_fields/) this is very useful.
  * [File-to-http-bridge](/en/features/file-to-http-bridge/): Some browsers load for security reasons no file links from http pages. Thus all documents that are in the index are now provided over HTTP. Of course this may switched off and at the [desktop search](/en/project_info/variant_comparison/) these documents are only accessible from the local host.

Defining the search space
-------------------------

Using regain you may specify very exactly what should be indexed and what should not.

  * [White and black list](/en/features/white_and_black_list/): With a white list and a black list you may isolate very exactly which documents the crawler should process. E.g. you may index all from `http://www.murfman.de` except for `http://www.murfman.de/dynamiccontent`.
  * Several sources in one index: You may index documents from different file systems and/or web sites in the same search index.
  * Partial indexing: Assumed your search index contains documents from a network drive (file server) and a web page. You may update only the documents from the network drive. In doing so you may update some drives every hour and others only every week.


Indexing
--------

  * Hot deployment: Change on a new search index without restarting your servlet engine (e.g. Tomcat).
  * Stopword list: Defined words are not indexed.
  * [Analysis files](/en/features/analysis_files/): If desired, all intermediate steps of the indexing process can be written out as files. This allows you see exactly what is in the search index.
  * Content extraction for HTML: Index only the actual content of your web pages. regain removes the navigation and footer from your html documents.
  * Path extraction for HTML: Shows the navigation path of your web pages in the search results.
  * Dead link detection: As a sort of by-product all found dead links (links to non-existing documents) are written out.
  * [Breakpoint](/en/features/breakpoint/)s: The crawler creates periodic breakpoints. When doing so, the current state of the search index is copied into a separate directory. If the index update should be cancelled (e.g. if the computer is shut down), the crawler will go on from the last breakpoint the next time it is started.
  * [Auxiliary fields](/en/features/auxiliary_fields/): The index may also be extended by auxiliary fields that are extracted from a document's URL. For example, assuming that you have a directory containing a sub directory for each project, you can generate an auxiliary field using the project name. This allows you to only get documents from individual projects (eg. only obtain documents from the project directory "otto23" when searching for "Offer project:otto23").

Expandability and customization
-------------------------------

regain is designed to be easily adaptable to your needs.

  * [Preparator](/en/components/preparator/)s: The preparation of a certain file format is done by so-called preparators. Thus you are able to specify which preparators regain should use. In addition regain may easily be extended for more file formats.
  * [Tag Library for the search](/en/components/the_search_mask_jsp_pages/): regain offers a Tag Library for creating the Java Server Page for the search. Thus the adaption of the search page to your web page's design is particularly easy.
  * [Configuration](/en/config_/): regain is highly adaptable. The whole configuration of the crawler is in one XML file.
  * [Access rights management](/en/features/access_rights_management/): It is now possible to integrate an access rights management, that ensures that a user only sees results for documents he has reading rights for.
