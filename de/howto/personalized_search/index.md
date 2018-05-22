---
title: "Idee: Personalisierte Suche"
---

[English translation](/en/howto/personalized_search/)

Idee: Personalisierte Suche
===========================

FIXME: Diese Seite hat einen sehr ähnlichen Inhalt wie [enterprisesearchaccesscontroller](/de/howto/de/howto/enterprisesearchaccesscontroller/). Die beiden Seiten sollten zusammengefasst werden.

Zusatzfeature
-------------

In der Trefferliste einer Intranet-Suche erscheinen nur Dokumente, für die der Suchende zumindest Leserechte hat.


Ziel
----

Die in [access rights management](/de/features/access_rights_management/) definierte Funktionalität für ein Netzwerk mit Microsoft Active Directory Service (ADS) zu konzipieren und zu programmieren.


Vorteile
--------

Zeitsparende automatisierte Indexerstellung und Generierung von Trefferlisten passend zum angemeldeten User.


Quellen
-------

Klasse `net.sf.regain.RegainToolkit`:

```java
public static void checkGroupArray(Object accessController, String[] groupArr)
  throws RegainException
{
  if (groupArr == null) {
    // Check for null
    throw new RegainException("Access controller " +
        accessController.getClass().getName() + " returned illegal " +
        "group array: null");
  } else {
    // Check for whitespace
    for (int i = 0; i < groupArr.length; i++) {
      if (RegainToolkit.containsWhitespace(groupArr[i])) {
        throw new RegainException("Access controller " +
            accessController.getClass().getName() + " returned illegal " +
                "group name containing whitespace: '" + groupArr[i] + "'");
      }
    }
  }
}
```

Aufgabenstellung
----------------

Zitat von Til im [Forum](http://forum.murfman.de/de/viewtopic.php?t=157):

> Besser wäre es, wenn dabei auf das echte Rechtesystem, also z.B. die Dateisystemrechte zugegriffen wird. Es wäre wünschenswert, dass der Login des jeweiligen Portals verwendet wird, was sich jedoch nicht allgemein lösen lässt, da dieser bei jedem Portal höchst unterschiedlich umgesetzt ist. Die einzige Möglichkeit, dies allgemein hinzubekommen, wäre, **regain mit einer eigenen Benutzerverwaltung und einer Login-Seite auszustatten, was jedoch relativ aufwändig wäre**.


Lösungsansätze
--------------

`CrawlerAccessController`: Mit der Anweisung in der Kommandozeile


    cacls X:/pfad/dateiname.txt 

kann man in einem Microsoft Active Directory (ADS) für jede im regain-Index erfasste Datei ermitteln, welche Gruppen Vollzugriff(`F`) oder Leserechte(`R`) für diese Datei haben. Also wird zur Laufzeit für jede gerade gecrawlte Datei 


    Runtime.getRuntime().exec("cacls", "X:/pfad/dateiname.txt");

ausgeführt, das Ergebnis wird in den `crawlerAccessController` [eingelesen](http://www.dpunkt.de/java/Programmieren_mit_Java/Die_Umgebung_eines_Java_Programms/2.html) und die Liste von Gruppen, die Leserechte für dieses Dokument haben, wird zurückzugegeben .

`SearchAccessController`: Als Login des jeweiligen Portals wird ein Login im ADS genutzt. Die mit diesem Login initiierte Session wird vom Kerberos-Protokoll gehalten. An regain adressierte Anfrage wird im `SearchAccessController` mit der Kerberos-Schlüssel verglichen. Falls der Nutzer im ADS angemeldet ist, wird die Gruppe zurückgegeben.


Diskussion zur Idee im Forum
----------------------------

  * [personalisierte Suche im internen ADS-Windows-Netzwerk](http://forum.murfman.de/de/viewtopic.php?t=347)
  * [Nutzerberechtigungen mit dem Access-Controller administrieren](http://forum.murfman.de/de/viewtopic.php?t=130)
  * [Mehrere Instanzen oder nutzerabhängiger Index bzw. Suche?](http://forum.murfman.de/de/viewtopic.php?t=157)


Alternative Lösungen
--------------------

**Mehrere Instanzen von Regain mittels Tomcat laufen lassen**

URL-abhängige Lösung. Dabei lässt sich Usermanagement/[Authentifizierung über Tomcat in der web.xml](http://ms2.alien.de/0410/content/view/80/55/) realisieren. Voraussetzung dabei ist, dass man händisch die im Index zu erfassende Dokumente mittels White-List und Black-List pflegt. Akzeptable Lösung, wenn die für unterschiedliche Nutzergruppen zugängliche Daten sauber in unterschiedlichen Verzeichnissen abgelegt sind.

**Mit [smbcacls](http://gertranssmb3.berlios.de/output/smbcacls.1.html) eine Liste von [ACL's](http://de.wikipedia.org/wiki/Access_Control_List) erstellen**

... und diese dann in das [security-constraint-Format](http://ms2.alien.de/0410/content/view/80/55/) überführen. Also was im Absatz oben beschrieben ist, zu automatisieren. Wäre wahrscheinlich nur für User, die Linux haben, machbar. Aber hier kenne ich mich zu wenig aus.


Einschränkungen
---------------

Einschränkungen sind hier wörtlich zu verstehen. Da eine Suche mit Rücksicht auf die Zugangsrechte des Suchenden nur dann möglich ist, wenn er bei der Suche angemeldet ist. Also entweder muss man sich für die Suche bei Tomcat wie oben beschrieben anmelden und dann darf das Browser-Fenster nicht geschlossen werden, bis alle Suchvorgänge durchgeführt sind oder im Intranet wird eine intelligente Lösung realisiert, die dafür sorgt, dass die Anmeldung am Arbeitsplatz-Rechner gleichzeitig als Anmeldung bei der Suche/Tomcat gilt. So eine Lösung ist von der jeweiligen Intranet-Konfiguration abhängig.


Wiederverwendung der Lösung
---------------------------

Da die Crawler-Authentifizierung gegenüber einer Ressource (Netzlaufwerk) für das im Forum-Posting [Wie kann ich eine Seite Login crawlen?](http://forum.murfman.de/de/viewtopic.php?t=350) gewünschtes Feature vermutlich ähnlich umzusetzen ist, wie die in dieser Idee anvisierte Funktionalität, wäre es sinnvoll, die Kräfte zu bündeln.


Siehe auch
----------

  * [OpenID](http://de.wikipedia.org/wiki/OpenID) ist ein Single-Sign-On-System, welches die übliche Anmeldung mit Benutzername und Passwort ersetzt.
  * [Eintrittskarte ins Internet Single-Sign-On mit Kerberos und LDAP](http://www.science-computing.de/downloads/s+c-fachartikel_sso_2006.pdf)
  * [Bestandteile von Samba](http://www.fertig-consulting.de/Linux/pdf/samba.pdf)
  * [Netzwerkprotokoll zum Filesharing zwischen Linuxservern und Windowsclients](http://www-i4.informatik.rwth-aachen.de/content/staff/homes/thissen/DatKom/Heise%20-%20sambaSkript.pdf)
  * [JAAS Tutorial](http://www.oio.de/public/java/jaas/sso-jaas-kerberos-tutorial.htm) (Single Sign-On mit Kerberos) In diesem Artikel wird der Einsatz eines Moduls für Kerberos beschrieben. Das Modul "Krb5LoginModule" bietet die Möglichkeit, Benutzer über deren Windows2000 oder Solaris-Systemlogin zu authentifizieren.
  * [Java Authentication and Authorization Service(JAAS) 1.0](http://transportbroker.vce.de/ressources/documents/Evaluierung_der_JAAS-AP.pdf)
  * [Rechtekonzept für die Mobile Agent System Architecture (MASA)](http://wwwmnmteam.informatik.uni-muenchen.de/pub/Diplomarbeiten/fack01/HTML-Version/main.html) 2.9.1 Die Java Sicherheitsarchitektur
  * [Windows mit externem Kerberos](http://archiv.tu-chemnitz.de/pub/2006/0034/data/html/node44.html)
  * weitere [Lesezeichen, die bei der Lösungssuche gesammelt wurden](http://del.icio.us/itebob/ACL)
  * [Wissensmanagement](http://dmoz.org/World/Deutsch/Wissen/Wissensmanagement/) (u.a. Auflistung der Software zum Content- und Dokumentenmanagement)
  * [Role Based Access Control](http://de.wikipedia.org/wiki/RBAC) (RBAC)
  * [Erweiterung einer Lösung zum Identity und Access Management um eine Berechtigungsverwaltung](http://www11.in.tum.de/publications/pdf/da-strunck2006.pdf) eine Diplomarbeit vom 15.06.2006, TU München, Fakultät für Informatik
  * RBAC ist wichtig und LDAP ist nützlich. In einer konkreten Situation hat Schnedermann Software-Consulting GmbH festgestellt, dass die Mischung von beidem zu Verwicklungen führt. Wie man den Widerspruch auflöst, steht im [IT-Security Whitepaper: RBAC und LDAP](http://www.schnedermann.de/RBAC_LDAP.shtml)
  * [Policies für dynamische Systeme](http://www.telematik.uni-freiburg.de/foliendownload.php?id=381) Sommersemester 2006, Prof. Dr. Günter Müller
  * [Stategien der Zugriffskontrolle](http://www.die.informatik.uni-siegen.de/DIE_BIB/Gestaltungspraktikum/gp_gesamt/home/modulMIP/ch03.html) Die hier vorgestellten Lerneinheiten sind im Rahmen von Gestaltungspraktika  in der Medieninformatik-Lehre der Universität Siegen entstanden. 11.08.2006.
  * [Single-Sign-On on Linux using LDAP with Active Directory](http://www.oo-services.com/en/articles/sso.aspx)
  * [Linkssammlung zum Thema 'Single-Sign-On(SSO)'](http://del.icio.us/breeen/sso)
  * [Portale: Open Source im Anmarsch](http://www.computerwoche.de/index.cfm?pid=381&pk=567617)
  * [Portale: Open Source nur mit Augenmaß](http://www.computerwoche.de/knowledge_center/software/589211/)
  * [Open Source Portale](http://www.oio.de/open-source-portale.htm)

**Autor:** itebob