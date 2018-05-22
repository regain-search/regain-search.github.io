---
title: "Access rights management"
---

[Deutsche Übersetzung](/de/features/access_rights_management/)

Access rights management
========================

The **Access rights management** ensures that a user only sees documents in his search results he has reading rights for.

How can I use this feature?
---------------------------

### Step 1: Implementing the access controllers

In order to use this feature, you have to implement two interfaces:
  * `CrawlerAccessController` from the package `net.sf.regain.crawler.access`. It gets a document and must be able to return a list of groups that have reading rights for that document.
  * `SearchAccessController` from the package `net.sf.regain.search.access`. It gets a page request and must be able to identify, which user initiated that request and to which groups this user belongs.

Your classes have to provide a standard constructor (a constructor that takes no parameters) and should be packed in a .jar-file.

How you identify, which user has initiated a request, depends on your web application where you integrated regain. Normally you do this by checking, whether there is a valid session and to which user this session belongs.

How you get the groups of a document or of a user, depends on your filesystem. So you have to call a script or something else that returns you the groups.

### Step 2: Configuring the access controllers

The `CrawlerAccessController` is used by the [crawler](/en/components/crawler/), the `SearchAccessController` is used by the [search mask](/en/components/search_mask/).

You tell the crawler, which `CrawlerAccessController` to use, by providing a `<crawlerAccessController>`-tag in the [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/). In this tag you specify the class name of your `CrawlerAccessController` and you may provide it with parameters.

**Example:**
```xml
<crawlerAccessController>
  <class jar="myAccess.jar">mypackage.MyCrawlerAccessController</class>
  <config>
    <param name="scriptPath">c:\regain\access\getDocumentGroups.cmd</param>
  </config>
</crawlerAccessController>
```

**Important:** Each time after you've changed the `CrawlerAccessController` or after the rights of a document or of a user have changed, you have to create a new index.

In order to tell the search mask, which `SearchAccessController` to use, you have to add a `<searchAccessController>`-tag in your [SearchConfiguration.xml](/en/config/searchconfiguration_xml/). This tag has the same structure as the one for the crawler.

**Example:**
```xml
<searchAccessController>
  <class jar="myAccess.jar">mypackage.MySearchAccessController</class>
  <config>
    <param name="scriptPath">c:\regain\access\getUserGroups.cmd</param>
  </config>
</searchAccessController>
```
