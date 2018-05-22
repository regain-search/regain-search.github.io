---
title: "How-To: Zugriff auf Desktopsuche von anderen Rechnern aus"
---

[English translation](/en/howto/desktop_external_access/)

How-To: Zugriff auf Desktopsuche von anderen Rechnern aus
=========================================================

Das Problem
-----------

Der Zugriff auf die Desktopsuche ist in der offiziellen regain-Version aus Sicherheitsgründen nur vom lokalen Rechner aus (`localhost`) erlaubt.


Lösungsansatz
-------------

Per Konfiguration den Zugriff auch für externe Aufrufer erlauben.


Vorteile
--------

Die Desktopsuche lässt sich dadurch auch im Netzwerk wie ein Server benutzen.


Nachteile
---------

Jeder Rechner im gleichen Netzwerk hat Zugriff auf alle Dokumente, die im Suchindex enthalten sind. Falls der Rechner mit der regain-Installation direkt im Internet hängt und der von regain verwendete Port nicht durch eine Firewall geschützt ist, dann jeder Rechner im Internet auf alle Dokumente im Index zugreifen!


Implementierung
---------------

In der DesktopConfiguration wurde folgender Tag eingefügt:

```xml
<!-- Allow/Disallow external access to the running desktop instance -->
<allow_external_access>true</allow_external_access>
```


### Änderungen im Quelltext

  * In der Schnittstelle `DesktopConfig.java` hinzufügen:

```java
public boolean getExternalAccessAllowed() throws RegainException;
```

  * In der Klasse `XmlDesktopConfig.java` zu Methode `loadConfig()` hinzufügen:

```java
node = XmlToolkit.getChild(config, "allow_external_access");
mExternalAccessAllowed = ( node == null ) ? false : XmlToolkit.getTextAsBoolean(node);
```

```java
public boolean getExternalAccessAllowed() throws RegainException {
  loadConfig();
  return mExternalAccessAllowed;
}
```

Definition von `mExternalAccessAllowed` als private boolean.

  * In Klasse `FileService.java`:

Ändern Zeile 43 in:
```java
if (!localhost && !DesktopToolkit.getDesktopConfig().getExternalAccessAllowed() ) {
```

  * In Klasse `SharedTagService.java`:

Ändern Zeile 88 in:
```java
if (!localhost && !DesktopToolkit.getDesktopConfig().getExternalAccessAllowed() ) {
```


Umgesetzt in
------------

Branch: `contrib-v1.2.3-thtesche`
Revision: `312`


Einschränkungen
---------------

Defaultmäßig sollte der externe Zugriff nicht erlaubt sein. 


**Autor:** Thomas Tesche, cluster:Consult, http://www.thtesche.com/