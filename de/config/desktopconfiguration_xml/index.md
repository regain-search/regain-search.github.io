---
title: "DesktopConfiguration.xml"
---

[English translation](/en/config/desktopconfiguration_xml/)

DesktopConfiguration.xml
========================

Diese Seite zeigt den Inhalt der `DesktopConfiguration.xml` - der Konfigurationsdatei der [Desktop-Variante](/en/project_info/variant_comparison/) von regain.

Normalerweise müssen Sie in dieser Datei keine Änderungen vornehmen. Nutzen Sie die statt dessen die [Einstellungsseite](/de/usage/desktop_getting_started/).

Beispiel:
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
</configuration>
```

  * Die `<ENTITY>`-Werte legen einige Bezeichner für verbreitete Zeichen in XML-Dokumenten fest.
  * Im `<interval>`-Tag wird ein Interval (in Minuten) für die Aktualisierung des Indexes durch den [Crawler](/de/components/crawler/) festgelegt. 
  * Im `<port>`-Element können Sie die [Portnummer](http://de.wikipedia.org/wiki/Port_%28Schnittstelle%29) für die [Suchmaske](/de/components/search_mask/) festlegen.  

     Dabei können Sie im Prinzip jede beliebige Nummer nutzen, mit Ausnahme der [Standardwerte für Portnummer](http://www.greyhat.de/articles/TCP_UDP_Ports.htm), die für bestimmte Programme auf Ihrem PC reserviert sind.
