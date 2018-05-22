---
title: "How-To: Dateien aus der Trefferliste direkt öffnen"
---

[English translation](/en/howto/open_file/)

How-To: Dateien aus der Trefferliste direkt öffnen
==================================================

Zusatzfeature
-------------

Mit einem Mausklick eine gefundene Datei zum Bearbeiten öffnen.


Lösungsansatz
-------------

`search.jsp` ändern und Firefox-Einstellungen anpassen, um ein Zugriff auf lokale Dateien zu ermöglichen.


Vorteile
--------

Gefundene Dateien können gleich aus der Trefferliste heraus bearbeitet werden. 


Nachteile
---------

Da die Sicherheitseinstellungen von Firefox gelockert werden, bietet es sich an, für das Surfen mit regain auf eigenem Rechner oder im Intranet ein separates [Firefox-Profil](http://www.firefox-browser.de/wiki/Profil) einzurichten.


Implementierung
---------------

  * in der `search.jsp` den `search:hit_url` -Tag mit einem A-href-Tag ergänzen und so anklickbar machen.
  * [NoScript-Erweiterung](http://www.erweiterungen.de/detail/noscript) in Firefox installieren.
  * In `NoScript`-Einstellungen unter `Erweitert` ein Häkchen für `Links auf lokale Dateien erlauben` setzen.
  * Wie man gewünschte Anwendung für die Bearbeitung der Datei einrichtet, ist im Artikel "[open_file_with](/de/howto/open_file_with/)" beschrieben.

Ergänzen Sie in der Datei `search.jsp` folgende Zeile:

```html
<search:hit_url beautified="true"/>
```

Mit einem Link:

```html
<a href="file://<search:hit_url beautified='true'/>" target="_blank"><search:hit_url beautified="true"/></a>
```


Einschränkungen
---------------

Die Lösung ist nur mit dem Firefox-Browser getestet.


**Autor:** itebob