---
---

[English translation](/en/howto/regain-light/)

**Kommen wir nun zu Fall 2.: Durchsuchen eines lokalen Web**


Grundsätzlich kann Regain jede [Website](http://de.wikipedia.org/wiki/Website) durchsuchen, die über das Intra- oder das Internet erreichbar ist. In der Regel hat jede Website eine Startseite, von der aus alle restlichen Seiten über Hyperlinks erreichbar sind und beginnt mit http://irgend-ein-bloeder-Name.de/index.htm oder so ähnlich.



In diesem Artikel gehe ich auf die Verwendung von Regain als lokalem [Webserver](http://de.wikipedia.org/wiki/Website) ein. Hier ist die lokale Website dann per Default über http://localhost:8020/irgend-eine-startseite.htm zu erreichen, wenn Regain gestartet wurde.


**''Vorausgesetzt, die Site wurde in den 'web' Ordner von Regain kopiert.''



**



Aha! Das ist also unser erster Schritt nach der Installation! Rein mit der Site in den Ordner `web`. Tipp: wenn beim Kopieren die Frage auftaucht: Wollen Sie die vorhandene Datei ersetzenbla bla Erstmal Abbrechen und noch mal nachdenken!







Schritt 2 besteht daraus, die Datei `CrawlerConfiguration.xml` im Ordner `conf` anzupassen. Bitte diesmal NICHT die `Einstellungseite` verwenden. In der Version 1.1 drohen sonst Einstellungen, die manuell in der CrawlerConfiguration.xml durchgeführt wurden, verloren zu gehen.







In dieser Datei werden nun (mindestens) 3 Punkte angepasst:




    <pre>
    <startlist>
    <start index="false" parse="true"> <nowiki>http://localhost:8020/irgend-eine-startseite.htm
    </nowiki></start>
    </startlist>
    </pre>











Damit sagen wir dem Krauler, wo er loskraulen soll. Er wird dann allen in der Startseite angegebenen Hyperlinks folgen, die wieder auf Seiten mit Hyperlinks verweisen, die wieder mit anderen Worten eine rekursive Suche der kompletten Site durchführen.







Allerdings werden Seiten nur durchgekrault, wenn Sie in der `Whitelist` stehen. Also fix angepasst:




     <pre>
     <whitelist>
     <prefix> http://localhost:8020/</prefix>
     </whitelist>
     </pre>







Wahrscheinlich beginnen alle lokalen Seiten ja mit diesem Präfix. Ansonsten einfach mehrere Präfixe aufnehmen oder gar einen [Regulärer Ausdruck](/de/howto/regulärer_ausdruck/) (RegExp).







Wer jetzt den Crawler auf die Suche nach Inhalten schickt, der wird schnell feststellen, dass dieser sich außerstande sieht seinen Job zu machen. Dies zeigt sich im Log. Der HTML Preparator meckert über seinen nicht vorhandenen Kollegen, den Content Extractor! 







Dies regeln wir schnell, in dem wir die folgende Passage noch in die `CrawlerConfiguration.xml` aufnehmen. (Siehe auch die hilfreiche `CrawlerConfiguration_example.xml`):








    <pre>
    <preparator>
    <class>.HtmlPreparator</class>
       <urlPattern>(^http://[^/]*/?=)|(^http://.*/[^\.]*=)|(^http://.*/=)|(\.
       (html|htm|jsp|php\d?|asp)=)</urlPattern>
       <config>
          <section name="contentExtractor">
            <param name="prefix">http://localhost:8020/</param>
            <param name="headlineRegex">&lt;a name=.*&gt;(.*)&lt;/a&gt;</param>
            <param name="headlineRegex.group">1</param>
          </section>
          <section name="pathExtractor">
            <param name="prefix"> http://localhost:8020/</param>
            <param name="pathNodeRegex">&lt;a.*href="([^"]*)">(.*)&lt;/a></param>
            <param name="pathNodeRegex.urlGroup">1</param>
            <param name="pathNodeRegex.titleGroup">2</param>
          </section>
      </config>
    </preparator>
    </pre>


Wer nicht direkt erkannt hat, was hier konfiguriert wird, der sei auf die tieferen Geheimnisse der [Konfiguration](/de/howto/config/crawlerconfiguration_xml/) verwiesen.







Jedenfalls sind wir jetzt soweit direkt zur `Statusseite` zu gehen, um dort auf `Index aktualisieren` zu klicken. Am einfachsten kommen wir wieder über das kleine [Regain-wiki.png](/de/howto/bild/regain-wiki_png/), unseren Freund in der Taskleiste, dorthin.







Wieder beobachten wir, nach dem Einschalten der automatischen Aktualisierung der Seite, das Log. Es ist mindestens so spannend wie ein prasselndes Kaminfeuer. Ist der Index fertig erstellt heißt es:







Auf die Suche, fertig, LOS!







HINWEIS:



Dem aufmerksamen Leser ist nicht entgangen, dass alle Veränderungen im Regain Verzeichnis vorgenommen worden sind. Die lokale Site liegt unterhalb von `web`. Selbst der erstellte Index liet im Verzeichnis `searchindex`. 







Damit sind grundsätzlich die Voraussetzungen geschaffen, eine `durchsuchbare CD` zu erstellen. Im Artikel [Regain-Light](/de/howto/regain-light/) findet sich dazu Weiteres.







André Kreienbring



















------------------------------







= Regain-Light =



'regain-Light' ist eine abgespeckte (ab 6 MB klein - je nach Indexgröße) regain-Desktop-Version, die dann eingesetzt werden kann, wenn auf die Crawler-Funktionalität verzichtet wird. Zum Beispiel, wenn regain-Index auf eine CD gebrannt und der Index sowieso nicht aktualisierbar ist.



==regain-Light erstellen HowTo==



Begriffsklärung:



**Inhalt:** Es handelt sich um Verzeichnisinhalte oder um Webseiten, die mit Hilfe von Regain indiziert wurden und durchsucht werden sollen.



**Index:** Hier: Der Inhalte des Ordners `searchindex` unterhalb des Regain Verzeichnisses.



**Externer Datenträger:** Wechselmedium, z.B. CD, USB-Stick u.ä.



**Ziel PC:** Der Rechner des Anwenders, der den externen Datenträger einsetzt, um den Inhalt zu durchsuchen.



**Applikation:** Alle Dateien aus denen Regain besteht und das zum Betrieb notwendige [http://de.wikipedia.org/wiki/JRE Java Runtime Environment (JRE)].



**Regain-Verzeichnis:** Dieses Verzeichnis dient als Container. In dem Container wird die Applikation, der Inhalt und der Index vorbereitet. Später wird der Container auf den externen Datenträger übertragen. In der Regel ist die Basis dafür das Verzeichnis, dass aus der Installation von Regain hervorgeht.



`Das Ziel von Regain-Light ist die Verwendung oder Weitergabe von indiziertem, also durchsuchbarem Inhalt und der vollständigen Applikation auf einem externen Datenträger. Dadurch ist auf dem Ziel-PC keinerlei Installation notwendig.`



**Schritt für Schritt:**



Ich gehe in diesem Artikel davon aus, dass die Erstellung von Regain-Light auf Basis des frisch entpackten Regain-Verzeichnisses vorgenommen wird.



**1. Inhalt in das Regain Verzeichnis kopieren:**

Ich empfehle dafür unterhalb es Ordners `web` eine entsprechende Verzeichnisstruktur anzulegen und den Inhalt bereits VOR der Erstellung des Index dort hinein zu kopieren. Auf diese Weise stimmen nach der Indizierung durch den Crawler bereits alle Referenzen auf die Inhalte. Sollte hier anders vorgegangen werden muß der Schritt `Konfiguration der Rewrite Rules` durchgeführt werden.



**2. Index erstellen:**

Der fertige Index wird dabei im Regain-Verzeichnis im Ordner `searchindex` angelegt. 



**3. Anpassung des Look and Feels von Regain**

Das bedeutet im Wesentlichen: Anpassen der Weboberfläche von Regain.



**4. Logging Ausgabe anpassen:**

In der Datei conf/`log4j.properties` die Einstellungen `log4j.rootCategory` ändern in:

 log4j.rootCategory=INFO, stdout

Hiermit wird z.B. verhindert, dass Regain versucht ein Log auf eine CD zu schreiben.



**5. Index Aktualisierungs Intervall:**

Defaultmäßig wird Regain in diesem Intervall den Inhalt neu indizieren. Für Regain-Light gehen wir aber von statischem Inhalt aus. In der Version 1.1 kann die Index-Aktualisierung nicht per Konfiguration unterbunden werden. Das Intervall kann aber in der [DesktopConfiguration.xml](/de/howto/desktopconfiguration_xml/) auf einen sehr hohen Wert eingestellt werden.



**6. Konfiguration der Rewrite Rules:**

Achtung: Nur notwendig, wenn indieziert wurde, BEVOR der Inhalt in das Regain-Verzeichnis übertragen wurde!

Damit die Verweise in der Ergebnisliste der Suche nach dem Speichern auf einem externen Datenträger  funktionsfähig sind, passen Sie die entsprechende _RewriteRules_ in der Datei [searchconfiguration.xml](/de/howto/config/searchconfiguration_xml/) an. Zum Beispiel, die Anweisung


    <rule prefix="file://C:/worker/dokumente" replacement="dokumente"/>

sorgt dafür, dass die zuvor auf der Festplatte C:/ im Ordner `file://C:/worker/dokumente` indexierte Dateien nach dem Speichern im Ordner `X://regain/web/dokumente` der regain-Light-Version auf einem externen Datenträger 'X:/' beim Anklicken in der Ergebnisliste richtig angezeigt werden. Wobei die Datenträgerbezeichnung 'X' an dieser Stelle keine Rolle spielt, da die Linkadressierung der Treffer relativ zum 'localhost' bzw. '127.0.0.1' realisiert wird.


**7. JRE zum Container hinzufügen und den Aufruf von Regain anpassen**

JRE ist auf Ihrem Computer in einem Ordner, der `j2re1.4.2` oder j2reN.N.N heisst,  installiert, sonst wäre Regain nicht funktionsfähig ;-). Diesen Ordner komplett in das Regain-Verzeichnis übertragen. Im Regain-Verzeichnis müssen Sie noch eine Datei mit der .bat-Endung, z.B. `sucheStarten.bat` mit diesem Inhalt



 j2reN.N.N/java -jar regain.jar



erstellen (die N's werden sinnvollerweise mit der Versionsnummer Ihrer JRE ersetzt). 

Dann kann regain mit einem Doppelklick auf die `sucheStarten.bat` vom externen Datenträger gestartet werden. Achtung - JRE beansprucht auf der CD so ab 115 MB Platz!



**8. Container auf externen Datenträger kopieren:**

Da der Index nicht aktualisiert wird, brauchen wir auch keinen Preparator. Also wird abschließend alles, die komplette [Desktop-Suche](/de/howto/de/project_info/variant_comparison/)  ohne den Ordner `regain/**preparator**` auf den gewünschten externen Datenträger kopiert.

