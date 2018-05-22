---
title: "How-To: Starten der Desktopsuche ohne TrayIcon"
---

[English translation](/en/howto/desktop_without_tray/)

How-To: Starten der Desktopsuche ohne TrayIcon
==============================================

Problem
-------

Unter Linux funktioniert die Desktopsuche nicht, da das Tray-Icon nicht dargestellt werden kann (ab Java 1.6 mit bestimmten X-Desktops). Dieses Problem tritt auch auf, wenn man die Desktopsuche auf einem headless-System starten will.


Lösungsansatz
-------------

Per Kommandozeilenparameter die Einbindung des Tray-Icons unterbinden.


Vorteile
--------

Die Desktopsuche lässt sich dadurch auch im Netzwerk wie ein Server benutzen. Linux-User können die Desktopsuche unter aktuellen Oberflächen mit Java 1.6 betreiben.


Benutzung
---------

Aufruf mit Parameter `-noTrayIcon`:

    java -jar regain.jar -noTrayIcon


Implementierung
---------------

In der DesktopConfiguration wurde folgender Tag eingefügt:

```xml
<!-- Allow/Disallow external access to the running desktop instance -->
<allow_external_access>true</allow_external_access>
```

In der Klasse `net.sf.regain.ui.desktop.Main` hinzufügen:

```java
public static void main(String[] args) {
  boolean useTrayIcon = true;
  for (int i = 0; i < args.length; i++) {	
    if (args[i].equalsIgnoreCase("-noTrayIcon")) {
     useTrayIcon = false;
    }	
  }
```

Und den TrayIconManager anders aufrufen:

```java
  TrayIconManager.getInstance().init(useTrayIcon);
```

In `net.sf.regain.ui.desktop.TrayIconManager` die `init`-Methode ändern:

```java
public void init(boolean useTrayIcon) {
  boolean active = useTrayIcon;
  if (! active) return;
```


Umgesetzt
---------
Das Feature ist ab Version 1.5.1 in der Distribution enthalten.

**Autor:** Stefan Gottlieb, Thomas Tesche, cluster:Consult, http://www.thtesche.com/
