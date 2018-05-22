---
title: "Idee: Zugriffsrechte-Management mit Hilfe von Active Directory und Kerberos"
---

[English translation](/en/howto/enterprisesearchaccesscontroller/)

Idee: Zugriffsrechte-Management mit Hilfe von Active Directory und Kerberos
===========================================================================

Zusatzfeature
-------------

In der Trefferliste einer Intranet-Suche erscheinen nur Dokumente, für die der Suchende zumindest Leserechte hat.


Lösungsansatz
-------------

Die Infos darüber, ob ein Benutzer im Intranet angemeldet ist bzw. in welchen Dateien aus dem regain-Index er suchen darf, werden vom im [ADS](http://de.wikipedia.org/wiki/Active_Directory) implementierten  [Kerberos-Protokoll](http://de.wikipedia.org/wiki/Kerberos_(Informatik)) bzw. aus den [ACL](http://de.wikipedia.org/wiki/Access_Control_List) zur Laufzeit ermittelt.


Vorteile
--------

  * Der Index muß nicht jedes mal, nachdem Sie den CrawlerAccessController geändert haben oder nachdem sich die Rechte eines Dokuments oder eines Benutzers geändert haben, neu erstellt werden.
  * Es muss nur ein EnterpriseSearchAccessController programmiert werden.


Implementierung
---------------

**Bei einer Suchanfrage:** 

  * Der `EnterpriseSearchAccessController` bezieht über das [Kerberos-Protokoll](http://de.wikipedia.org/wiki/Kerberos_(Informatik)) Informationen darüber, ob der Suchende im Intranet angemeldet ist.
  * Falls _ja_ werden aus dem regain-Index alle der Suchanfrage entsprechenden Dokumente ausgefiltert.
  * Falls _nicht_ werden aus dem regain-Index Dokumente ausgefiltert, die ein `anonymous`-Besucher sehen darf.
  * In der Trefferliste werden anhand von ACL-Listen nur die Dokumente aufgelistet, für die der Suchende Leserechte hat.


Änderungen im Quellcode
-----------------------

[SearchAccessController](/de//features/access_rights_management/)-API muß vermutlich geändert werden. FIXME: Warum und wie?


Einschränkungen
---------------

  * Der Lösungsansatz ist hier am Beispiel [Active Directory Service](http://de.wikipedia.org/wiki/Active_Directory) beschrieben, gilt aber auch für andere Verzeichnisdienste.
  * Es muss getestet werden, ob die Antwortzeiten der regain-Suche mit dieser Lösung akzeptabel bleiben.


Siehe auch
----------

  * Diskussion zu dieser Idee im Forum: [EnterpriseSearchAccessController](http://forum.murfman.de/de/viewtopic.php?p=1312)
  * [access rights management](/de//features/access_rights_management/)
  * [personalized_search](/de/howto/personalized_search/) - Aufgabenstellung aus Anwender-Sicht, also eine Art "Fachkonzept" für diese Idee.
