---
title: "Zugriffsrechte-Management"
---

[English translation](/en/features/access_rights_management/)

Zugriffsrechte-Management
=========================

Das **Zugriffsrechte-Management** sorgt dafür, dass ein Benutzer nur Dokumente in seinen Suchergebnissen sieht, für die er auch Leserechte hat.

Wie kann ich dieses Feature nutzen?
-----------------------------------

### Schritt 1: Implementierung der Access-Controller

Um dieses Feature nutzen zu können, müssen Sie zwei Klassen erstellen, die je eine der folgenden Schnittstellen implementieren:

  * `CrawlerAccessController` aus dem Package `net.sf.regain.crawler.access`. Es bekommt ein Dokument übergeben und muss in der Lage sein, eine Liste von Gruppen zurückzugeben, die Leserechte für dieses Dokument haben.
  * `SearchAccessController` aus dem Package `net.sf.regain.search.access`. Es bekommt einen Page-Request übergeben und muss in der Lage sein, den Benutzer zu identifizieren, der diesen Request geschickt hat und zu welchen Gruppen er gehört.

Ihre Klassen müssen einen Standard-Konstruktor zur Verfügung stellen (einen Konstruktor, der keine Parameter nimmt) und sie sollten in eine .jar-Datei gepackt werden.

Wie Sie den Benutzer identifizieren, der einen Request abgeschickt hat, hängt von Ihrer Web-Applikation ab, in die Sie regain eingebunden haben. Normalerweise müssen Sie dazu prüfen, ob es eine gültige Session gibt und zu welchem Benutzer diese gehört.

Wie Sie die Gruppen eines Dokuments oder Benutzers bekommen, hängt von Ihrem Dateisystem ab. Sie müssen also ein Skript oder sonst etwas aufrufen, das Ihnen die Gruppen zurückgibt.


### Schritt 2: Konfigurieren der Access-Controller

Der `CrawlerAccessController` wird vom [Crawler](/de/components/crawler/) genutzt, der `SearchAccessController` von der [Suchmaske](/de/components/search_mask/).

Sie sagen dem Crawler, welchen `CrawlerAccessController` er nutzen soll, indem Sie ein `<crawlerAccessController>`-Tag in die [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) einfügen. In diesem Tag geben Sie den Namen Ihrer `CrawlerAccessController`-Klasse an und können sie mit Parametern versorgen.

**Beispiel:**
```xml
<crawlerAccessController>
  <class jar="myAccess.jar">mypackage.MyCrawlerAccessController</class>
  <config>
    <param name="scriptPath">c:\regain\access\getDocumentGroups.cmd</param>
  </config>
</crawlerAccessController>
```

**Wichtig:** Jedes mal, nachdem Sie den `CrawlerAccessController` geändert haben oder nachdem sich die Rechte eines Dokuments oder eines Benutzers geändert haben, müssen Sie einen neuen Index erstellen.

Um der Suchmaske zu sagen, welchen `SearchAccessController` sie nutzen soll, müssen Sie ein `<searchAccessController>`-Tag ihrer [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) angeben. Dieses Tag hat die selbe Struktur wie das des Crawlers.

**Beispiel:**
```xml
<searchAccessController>
  <class jar="myAccess.jar">mypackage.MySearchAccessController</class>
  <config>
    <param name="scriptPath">c:\regain\access\getUserGroups.cmd</param>
  </config>
</searchAccessController>
```
