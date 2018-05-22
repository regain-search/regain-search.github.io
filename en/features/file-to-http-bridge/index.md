---
title: "File-to-http-bridge"
---

[Deutsche Übersetzung](/de/features/file-to-http-bridge/)

File-to-http-bridge
===================

Mozilla browsers have a security mechanism that blocks loading file-URLs from pages loaded via http.

To be able to load files from the search results, regain offers the **file-to-http-bridge** that provides all files that are listed in the index via http.

The [desktop search](/en/project_info/variant_comparison/) allows only an access to those files from the computer where it is running (`localhost`).

You can disable this mechanism in the `SearchConfiguration.xml` using the [&lt;useFileToHttpBridge&gt; tag](/en/config/searchconfiguration_xml/#usefiletohttpbridge-tag).
