---
title: "DesktopConfiguration.xml"
---

[Deutsche Übersetzung](/de/config/desktopconfiguration_xml/)

DesktopConfiguration.xml
========================

This page shows the content of the `DesktopConfiguration.xml` - the configuration file of the [desktop variant](/en/project_info/variant_comparison/) of regain.

Typically you don't have to edit this file. You can use the settings page instead.

Example:
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE entities [
 <!ENTITY minus "&#45;">
 <!ENTITY lt "&#60;">
 <!ENTITY gt "&#62;">
]>
<configuration>  
  <interval>1440</interval>
  <port>8020</port>
  <allow_external_access>true</allow_external_access>
  <simple_register_namespace>
    <namespace name="search">net.sf.regain.search.sharedlib</search>
    <namespace name="config">net.sf.regain.ui.desktop.config.sharedlib</config>
    <namespace name="status">net.sf.regain.ui.desktop.status.sharedlib</config>
  </simple_register_namespace>
</configuration>
```

  * configuration file  for [desktop variant](/en/project_info/variant_comparison/) only.
  * `<ENTITY>`-values define some names of common characters inside XML-documents.
  * `<interval>`: the time to wait (in minutes) until the [crawler](/en/components/crawler/) should update the index.
  * `<port>`: the TCP-port to use for the [search mask](/en/components/search_mask/).
  * `<allow_external_access>`: If set to false, the [search mask](/en/components/search_mask/) only accepts queries on the same PC (localhost). If set to true, and the Firewall is configured correctly, other PCs in the network may search and access the files.
  * `<simple_register_namespace>`: Configuration of the JSP Tags (see [custom tags](/en/features/custom_tags/)).