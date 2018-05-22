---
title: "Auxiliary fields"
---

[Deutsche Übersetzung](/de/features/auxiliary_fields/)

Auxiliary fields
================

In the [search index](/en/components/search_index/) the data about a document is stored in separate fields. This way you can decide which fields you want to be regarded when searching.

Using **auxiliary fields** you're able to define more fields besides the [standard fields](/en/components/search_index/#standard_fields). This helps you to search more precisely.

How can I use this feature?
---------------------------

### Example 1: Generate an auxiliary field from the URL

Assumed you have a network drive with a projects folder, which contains a sub folder for each project.


    c:
    +-- projects
        +-- gullivers
        +-- regain
        +-- marvin
        +-- blubb
        +-- ...

In this case you may for example add an auxiliary field `project`, which contains for each document the name of the project the document belongs to. A search for "manual project:regain" would the search for the keyword "manual" in all documents in the project folder `regain`.

For this auxiliary field you even may add a list box to the advanced search. This way you're able to select directly a certain project to search in.

To realize that example, you have to add the following entry to the [`auxiliaryFieldList` tag](/en/config/crawlerconfiguration_xml/#.3cauxiliaryfieldlist.3e_tag) in the [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/):
```xml
<auxiliaryFieldList>
  <auxiliaryField name="project" regexGroup="1">
    <regex>^file://c:/projects/([^/]*)</regex>
  </auxiliaryField>
</auxiliaryFieldList>
```

The [regular expression](/en/config/regular_expression/) defines, which documents are provided with the auxiliary field. The attribute `regexGroup` causes that the value of the auxiliary field is extracted from the first regex group: `([^/]*)`.

With the URL `file://c:/projects/marvin/docs/manual.pdf` the auxiliary field `project` gets the value `marvin`.

The URL `file://c:/docs/letter.doc` does not match the regular expression and therefore gets no auxiliary field `project`.

### Example 2: Sub collection

Instead of extracting the value of the auxiliary field from the URL, you may also specify a fixed value.

Assumed you have stored certain document types in certain folders on a network drive. E.g. your letters are stored in three different places. Using auxiliary fields you may limit a search on one document type. For example you may only search in your letters.

The according entry in the [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) may look like this:
```xml
<auxiliaryFieldList>
  <auxiliaryField name="doctype" value="letter">
    <regex>^file://c:/projects/letters</regex>
  </auxiliaryField>

  <auxiliaryField name="doctype" value="letter">
    <regex>^file://e:/office/customer/(letters|correspondence)</regex>
  </auxiliaryField>

  <auxiliaryField name="doctype" value="offer">
    <regex>^file://e:/office/customer/offers/</regex>
  </auxiliaryField>

  <auxiliaryField name="doctype" value="specs">
    <regex>/spec(ification)?/</regex>
  </auxiliaryField>
</auxiliaryFieldList>
```

With the first two entries all documents in `c:/projects/letters`, `e:/office/customer/letters` and `e:/office/customer/correspondence` get an auxiliary field `doctype` with the value `letter`.

The third entry causes that all documents in `e:/office/customer/offers` get an auxiliary field `doctype` with the value `offer`.

With the last entry all documents having `anywhere` in their URL a `/spec/` or a `/specification/` get an auxiliary field `doctype` with the value `specs`.

All other document get no auxiliary field `doctype`.
