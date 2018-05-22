---
title: "Howto: Wiederverwendbare Zeichenfolgen(Entities) in *.xml-Dateien"
---

[English translation](/en/howto/xml_entities/)

Howto: Wiederverwendbare Zeichenfolgen(Entities) in *.xml-Dateien
=================================================================

Einführungsbeispiel
-------------------

Wenn mehrere Indexe in der Datei `SearchConfiguration.xml` eingebunden und in einem Ordner gespeichert sind, z.B. `C:/Tomcat 5.0/webapps/regain/WEB-INF` dann ist es sinnvoll, am Anfang der `SearchConfiguration.xml` unter der Zeile `<!ENTITY lt ...>` eine Zeile 

```xml
<!ENTITY indexPfad "C:\Tomcat 5.0\webapps\regain\WEB-INF">
```

einzufügen.

Dann können Sie an Stelle 
```xml
<dir>C:/Tomcat 5.0/webapps/regain/WEB-INF/MySearchindex</dir>
```

einfach
```xml
<dir>&indexPfad;/MySearchindex</dir>
```

schreiben. Diese Schreibweise macht  den Quelltext der `SearchConfiguration.xml` übersichtlicher und die Änderungen von Pfadangaben für die Indexe bei der Migration von regain, z.B. aus einer Entwicklungs- in die produktive Umgebung können dann durch Änderung des Werts `indexPfad` an einer Stelle gemacht werden.

Genauso können Sie bei der Definition von `<prefix>`-Werten in `<whitelist>` und `<blacklist>` in der `CrawlerConfiguration.xml` vorgehen.


Entities als Parameter in XML-Elementen einsetzen
-------------------------------------------------

Wenn man solche Entities in der Datei `CrawlerConfiguration.xml` definiert 
```xml
<!ENTITY prefix1 "file://C:/wwwroot/">
<!ENTITY replacement1 "http://meinServer.de/">
```

dann ist auch diese platz- und zeitsparende Schreibweise bei der Definition von `rewriteRules` zulässig:

```xml
<rewriteRules>
  <rule prefix='&prefix1;' replacement='&replacement1;'/>
</rewriteRules>
```


komplette XML-Elemente als Entities
-----------------------------------

Solche Entity-Definition
```xml
<!ENTITY rewriteRules1 "<rewriteRules><rule 
prefix='file://C:/wwwroot/' replacement='&replacement1;'/></rewriteRules>">
```

ist auch zulässig. Sie ist sinnvoll, wenn die `rewriteRules`-Werte für mehrere Suchindexe identisch sind. Dann kann man nach der Definition der `rewriteRules1`-Entity alle Abschnitte 

```xml
<rewriteRules>
  <rule prefix='file://C:/wwwroot/' replacement='http://meinServer.de/' />
</rewriteRules>
```

durch ein Entity-Element

```xml
&rewriteRules1;
```
ersetzen ;-)


verschachtelte Entities
-----------------------

Das Beispiel ist selbsterklärend, nehme ich an 
```xml
<!ENTITY rewriteRules1 "<rewriteRules><rule prefix='&prefix1;' 
replacement='&replacement1;'/></rewriteRules>">
```

Also man darf Entities in Entities verwenden.


Siehe auch
----------

  * [config](/de/config/)
