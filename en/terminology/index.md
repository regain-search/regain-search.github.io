---
title: "Terminology"
---

[Deutsche Übersetzung](/de/terminology/)

Terminology
===========

This page lists short explanations of special terms regarding regain and search engines.

Analyzer
--------

When the [crawler](/en/components/crawler/) found a document and extracted the text, then it stores that text in the [search index](/en/components/search_index/) using [Lucene](/en/project_info/used_libraries/).

Lucene extract every single word from the document's text. Before the words are stored in the index, they are reduced to their base form using an **analyzer**. So searching for `tree` and `trees` has the same results. 

Query syntax
------------

The syntax of search queries.

Details see [http://jakarta.apache.org/lucene/docs/queryparsersyntax.html](http://jakarta.apache.org/lucene/docs/queryparsersyntax.html)

Stopword list
-------------

Stopwords are words that shouldn't be stored in the index.