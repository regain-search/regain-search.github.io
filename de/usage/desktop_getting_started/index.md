---
title: "Erste Schritte mit der Desktop-Variante"
---

[English translation](/en/usage/desktop_getting_started/)

Erste Schritte mit der Desktop-Variante
=======================================

Diese Seite richtet sich vor allem an Anwender, die [Desktop-Variante](/de/project_info/variant_comparison/) von regain frisch installiert haben und nun die nötigen Einstellungen vornehmen und schließlich in ihren Dokumenten suchen wollen.

Falls Sie regain noch nicht installiert haben, dann befolgen Sie bitte zunächst die [Installationsanleitung](/de/installation/desktop/).

Beim ersten Start von regain, wird im Browser die Startseite gezeigt. Da es bisher noch keinen [Suchindex](/de/components/search_index/) gibt, müssen wir diesen erst erstellen. Folgen Sie also der Aufforderung auf der Startseite und wechseln Sie zur Einstellungsseite.

  - Klicken Sie im Browser-Fenster in der Fußzeile einer regain-Seite auf den Link `Einstellungen` oder machen Sie einen rechten Mausklick auf das regain-Logo ![regain-logo-16](/images/regain-logo-16.png) rechts unten in der Taskleiste und klicken Sie dort auf `Einstellungen`.
  - Geben Sie unter `Indexierungsintervall` an, wie oft der Suchindex erneuert werden soll.

      * Für den Alltagsgebrauch ist die Einstellung "Eine Woche" hier empfehlenswert.
  - Geben Sie in den weiteren Feldern an, welche Verzeichnisse / Webseiten zur Suche verfügbar sein sollen und welche davon ausgeschlossen sein sollen.

      * Zum Beispiel "''E:\Dokumente\Rechnungen''".
  - Klicken Sie auf `Einstellungen speichern`, um Ihre Einstellungen zu speichern. Je nach dem, welche Änderungen Sie vorgenommen haben, wird nun automatisch ein neuer Suchindex erstellt.

Der [Crawler](/de/components/crawler/) durchsucht nun das Startverzeichnis und alle seine Unterverzeichnisse nach Dokumenten und packt diese in den Suchindex. Solange der Crawler indiziert, läuft eine grüne Scan-Linie über das regain-Logo in der Task-Leiste.

**Hinweis:** Auf der Statusseite können Sie die Erstellung des Index mitverfolgen.

Sobald die Indexierung abgeschlossen ist, können Sie mit der Suche loslegen. Sie können die Suchmaske öffnen, indem Sie entweder auf den Link in der Fußzeile der Statusseite klicken oder indem Sie auf das regain-Logo in der Taskleiste klicken.


Bestehenden Index aktualisieren
-------------------------------

Sie haben Änderungen an den Einstellungen vorgenommen. Um diese Änderungen sofort wirksam zu machen, müssen Sie den Index neu erstellen.
  - Klicken Sie im Browser-Fenster in der Fußzeile einer regain-Seite auf den Link `Status` oder machen Sie einen rechten Mausklick auf das regain-Logo ![regain-logo-16](/images/regain-logo-16.png) rechts unten in der Taskleiste und klicken Sie dort auf `Status`.
  - Klicken Sie auf den Button `Starten` neben Indexaktualisierung.

regain startet nun eine neue Indexierung.


Siehe auch
----------

  * [delete_index](/de/howto/delete_index/)
