---
title: "The main components of regain"
---

[Deutsche Übersetzung](/de/components/)

The main components of regain
=============================

The basic job done by regain is: The **crawler** searches for documents, extracts their text and stores it in a **search index**. Using this index, the **search mask** can answer search queries from users in nearly no time. For writing and using the search index, regain is using a library called **Lucene**.

The most important components of regain are:
  * [crawler](/en/components/crawler/) - It searches for documents and extracts their text using the [preparator](/en/components/preparator/).
  * [search index](/en/components/search_index/) - The search index is bunch of files which are used by Lucene for answering search queries.
  * [search mask](/en/components/search_mask/) - The search mask shows a web user interface to the user where he can enter search queries and browse through the results. The web pages are rendered using the [search mask jsp pages](/en/components/search_mask_jsp_pages/).
