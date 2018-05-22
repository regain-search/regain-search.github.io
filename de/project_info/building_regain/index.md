---
title: "regain bauen"
---

[English translation](/en/project_info/building_regain/)

regain bauen
============

Diese Seite zeigt, wie Sie regain selbst aus dem Quellcode bauen können auf der Kommandozeile. (Sie können aber auch einen [Code-Editor](/de/project_info/project_info/howto_regain_in_an_ide/) installieren und konfigurieren.)


Entwicklungsumgebung einrichten
-------------------------------

Um regain bauen zu können, müssen Sie zuerst folgendes installieren:

  * Das [JDK](http://de.wikipedia.org/wiki/J2SDK) (Java SE Development Kit), welches den Java-Compiler und alles, was dieser braucht, enthält. Siehe [Download-Seite des JDK](http://java.sun.com/javase/downloads/index.jsp).
  * [Ant](http://de.wikipedia.org/wiki/Ant) - eine Scriptsprache für Build-Skripte, wie es in regain verwendet wird. Siehe [Download-Seite von Ant](http://ant.apache.org/bindownload.cgi).

Stellen Sie sicher, dass die nötigen [Umgebungsvariablen](http://de.wikipedia.org/wiki/Umgebungsvariable) korrekt gesetzt sind:
  * `JAVA_HOME` muss auf das Verzeichnis zeigen, in dem das JDK installiert ist. Beispiel: `C:/Programme/Java/jdk1.6.0_12`
  * `ANT_HOME` muss auf das Verzeichnis zeigen, in dem Ant installiert ist. Beispiel: `C:\Programme\apache-ant`
  * `PATH` muss die `bin`-Verzeichnisse vom JDK und von Ant enthalten. Beispiel: `%PATH%;%JAVA_HOME%\bin;%ANT_HOME%\bin`

**Tipp:** Unter Windows finden Sie die Umgebungsvariablen folgendermaßen:
  - Tastenkombination `Windows+Pause` drücken.
  - Auf den Tab `Erweitert` wechseln.
  - Knopf `Umgebungsvariablen` drücken.

Im Verzeichnis, in dem sich die `build.xml` befindet:

  * `build.properties.sample` kopieren als `build.properties`. Dort können Parameter verändert werden, java.dir sollte ebenfalls auf den Wert von JAVA_HOME gesetzt werden.

regain bauen
------------

Öffnen Sie eine Konsole (unter Windows: die Eingabeaufforderung, zu finden unter `Start -> Ausführen -> cmd`).

Wechseln Sie in das Verzeichnis, in das Sie den [Quellcode von regain](/en/project_info/sourcecode/) ausgepackt haben - also das Verzeichnis, in dem die Datei `build.xml` liegt.

Beispiel:

    d:
    cd d:\Projekte\regain

Geben Sie nun folgenden Befehl ein, um die Server-Variante von regain zu bauen:

    ant runtime-server

Geben Sie diesen Befehl ein, wenn Sie die Desktop-Variante bauen wollen:

    ant runtime-desktop

Folgender Befehl listet alle Targets auf, die das Ant-Skript von regain zur Verfügung stellt:

    ant

Den gewünschten Befehl dann folgendermaßen ausführen:

    ant [target-Name]


Weblinks
--------

  * Forum: [Wie kann ich regain am einfachsten (mit Ant-Builder) selbst bauen](http://forum.murfman.de/de/viewtopic.php?t=170) (veraltet)
  * [Apache-Ant-Starthilfe](http://www.joller-voss.ch/apache/ant/ApacheAntStarthilfe.pdf#search=%22apache%20ant%20starthilfe%20joller%22) - eine kompakte Ant-Beschreibung 
  * [Programmiersprache Java - Entwicklungsumgebungen](http://de.wikipedia.org/wiki/Programmiersprache_Java#Entwicklungsumgebungen)
