---
title: "Installation der Desktop-Variante"
---

[English translation](/en/installation/desktop/)

Installation der Desktop-Variante
=================================

Dieser Artikel beschreibt, wie Sie die [Desktop-Variante](/de/project_info/variant_comparison/) von regain installieren.


Installation
------------

Zunächst müssen Sie regain von der [Download-Seite](http://regain.sourceforge.net/download.php) herunterladen.

Unter Windows können Sie den Windows-Installer (.exe) zur Installation benutzen, unter anderen Plattformen muss die Zip-Datei entpackt werden.


regain starten
--------------

regain muss gestartet sein, damit Sie etwas suchen können. Ob regain gestartet ist, erkennen Sie daran, dass in der Taskleiste neben der Uhr das regain-Symbol ![regain-logo-16](/images/regain-logo-16.png) erscheint.

Der Windows-Installer startet regain automatisch. Wenn Sie die Zip-Datei heruntergeladen haben, dann starten Sie regain, indem Sie einen Doppleklick auf die Datei `regain.exe` bzw. `regain.jar` machen.

Falls das nicht funktioniert, geben Sie in der Konsole folgenden Befehl ein:

    cd ''[regain-Verzeichnis]''
    java -jar regain.jar

  * Damit regain bei jedem Neustart wieder geladen wird, machen Sie am besten eine Verknüpfung in Ihrem Autostart-Ordner. Der Windows-Installer macht das für Sie automatisch. 
  * Sie können auch eine Datei `regain.bat` erstellen, die dieses Commando `java -jar regain.jar` enthält. Dann können Sie regain mit einem Doppelklick auf diese Datei jederzeit zeitsparend starten.

Beim ersten Start wird Ihr Browser gestartet und die Willkommen-Seite angezeigt. Um suchen zu können, müssen Sie [regain einrichten](/de/usage/desktop_getting_started/).


Problembehebung beim regain-start
---------------------------------

**Problem:** Beim Start von regain erscheint die Fehlermeldung `Die Seite kann nicht angezeigt werden`.

**Lösung:**
  * Das könnte daran liegen, dass bei einigen Windows-Versionen die Adresse `localhost` nicht richtig aufgelöst wird. Sie können dieses Problem umgehen, indem Sie `127.0.0.1` statt `localhost` verwenden, also z.B. `http://127.0.0.1:8020` in die Adressleiste Ihres Browsers eingeben.
  * Wenn Ihr Rechner in einem Netzwerk über einen [Proxy-Server](http://de.wikipedia.org/wiki/Proxy) mit dem Internet verbunden ist, dann könnte die Fehlermeldung immer noch auftreten. Dies könnte daran liegen, dass Ihr Browser versucht, die Adressen `127.0.0.1` und `localhost` über den Proxy zu laden. In diesem Fall müssen Sie Ihren Browser so einstellen, dass der Proxy für diese Adressen nicht verwendet wird.  

     Die entsprechenden Einstellungen finden Sie hier:

      * Firefox: ''Extras -> Einstellungen -> Verbindungs-Einstellungen -> **Kein Proxy für**''
      * Internet Explorer: ''Extras -> Internetoptionen -> Verbindungen -> Einstellungen -> **Proxy für lokale Adressen umgehen**''
