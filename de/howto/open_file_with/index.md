---
title: "How-To: Treffer mit der gewünschten Anwendung öffnen"
---

[English translation](/en/howto/open_file_with/)

How-To: Treffer mit der gewünschten Anwendung öffnen
====================================================

Zusatzfeature
-------------
Ein Dokument in der Trefferliste mit der gewünschten Anwendung öffnen.


Lösungsansatz
-------------

`search.jsp` ändern; Firefox-Erweiterungen installieren und konfigurieren


Vorteile
--------

Mit dieser Lösung können Sie die Treffer direkt aus der Trefferliste mit der gewünschten Anwendung öffnen. Mit der Desktop-Variante von regain können die gefundene Dokumente auch gleich bearbeitet werden.


Nachteile
---------

Da die Sicherheitseinstellungen von Firefox gelockert werden, bietet es sich an, für das Surfen mit regain auf eigenem Rechner oder im Intranet ein separates Firefox-Profil einzurichten. 


Implementierung
---------------

### search.jsp anpassen

In der `search.jsp` den `search:hit_url`-Tag mit einem a-href-Tag ergänzen und so anklickbar machen.

Vorher:
```html
<search:hit_url beautified="true"/>
```

Nachher:
```html
<a href="file://<search:hit_url beautified='true'/>" target="_blank">
<search:hit_url beautified="true"/></a>
```


### NoScript-Erweiterung installieren

  * [NoScript-Erweiterung](http://www.erweiterungen.de/detail/noscript) in Firefox installieren.
  * in `NoScript`-Einstellungen unter 'Erweitert' ein Häkchen für 'Links auf lokale Dateien erlauben' setzen.


### ViewSourceWith-Erweiterung installieren

  * [ViewSourceWith](http://www.erweiterungen.de/detail/ViewSourceWith/) installieren.
  * Die gewünschte Anwendung über Extras -&gt; Add-Ons -&gt; ViewSourceWith -&gt; Einstellungen einbinden.
  * Jetzt erscheint im Kontextmenü bei Verweisen ein 'ViewSourceWith'-Eintrag mit der Beschriftung 'Quelltext anzeigen'.


### Launchy-Erweiterung

Alternativ zu ViewSourceWith-Erweiterung:
  * [Launchy-Erweiterung](http://gemal.dk/mozilla/launchy.html) installieren.
  * Im chrome -Ordner ihres [Firefox-Profils](http://gemal.dk/mozilla/profile.html) eine Datei `launchy.xml` mit diesem Inhalt speichern:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configurations xmlns="http://launchy.mozdev.org/configurations">
  <application>
    <!-- Name Ihres Lieblings-Editors -->
    <label>HTML-Kit</label>
    <type>1</type>

    <!-- Im <command>-Tag wird der Pfad zum Editor festgelegt -->
    <!-- Entweder absolut: -->
    <command>C:\Programme\Chami\HTML-Kit\Bin\HTMLKit.exe</command>

    <!-- Oder alternativ in dieser Schreibweise: -->
    <command>%ProgramFiles%\Chami\HTML-Kit\bin\HTMLKit.exe</command>

    <arguments></arguments>

  </application>
</configurations>
```

  * Jetzt erscheint im Kontextmenü bei Verweisen ein 'Launchy'-Eintrag mit dem Menüpunkt 'Link in HTML-Kit öffnen'.


Siehe auch
----------

  * Im Forum: [Diskussion zu diesem How-To](http://forum.murfman.de/de/viewtopic.php?p=2432)


**Autor:** itebob