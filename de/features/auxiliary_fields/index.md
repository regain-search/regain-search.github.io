---
title: "Zusatzfelder"
---

[English translation](/en/features/auxiliary_fields/)

Zusatzfelder
============

Die Daten über ein Dokument werden im [Suchindex](/de/components/search_index/) in getrennten Feldern abgespeichert. So kann später bei der Suche entschieden werden, welche dieser Felder durchsucht werden sollen.

Über **Zusatzfelder** können Sie neben den [Standardfeldern](/de/components/search_index/#standardfelder) weitere Felder anlegen. Dadurch können Sie noch zielgerichteter suchen.


Wie kann ich dieses Feature nutzen?
-----------------------------------

### Beispiel 1: Zusatzfeld aus URL generieren

Angenommen Sie haben ein Netzlaufwerk mit einem Projekte-Verzeichnis, unter dem Sie für jedes Projekt ein Unterverzeichnis angelegt haben.


    c:
    +-- projects
        +-- gullivers
        +-- regain
        +-- marvin
        +-- blubb
        +-- ...

Hier könnten Sie z.B. ein Zusatzfeld `project` anlegen, das bei jedem Dokument den Namen des Projektes enthält, zu dem das Dokument gehört. Eine Suche nach "Handbuch project:regain" würde nach dem Stichwort "Handbuch" suchen und zwar nur in den Dokumenten im Projekte-Order `regain`.

Für dieses Zusatzfeld könnten Sie in der Erweiterten Suche auch ein eigenes Auswahlfeld anlegen, so dass man bei der Erweiterten Suche direkt ein bestimmtes Projekt auswählen kann.

Um dieses Beispiel umzusetzen, müssen Sie in der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) folgenden Eintrag im `auxiliaryFieldList`-Tag hinzufügen:
```xml
<auxiliaryFieldList>
  <auxiliaryField name="project" regexGroup="1">
    <regex>^file://c:/projects/([^/]*)</regex>
  </auxiliaryField>
</auxiliaryFieldList>
```

Der [reguläre Ausdruck](/de/config/regular_expression/) bestimmt, welche Dokumente mit dem Zusatzfeld versehen werden sollen. Das Attribut `regexGroup` bewirkt, dass der Wert des Zusatzfeldes aus der ersten Regex-Gruppe gewonnen wird: `([^/]*)`.

Bei der URL `file://c:/projects/marvin/docs/manual.pdf` bekommt das Zusatzfeld `project` den Wert `marvin` zugewiesen.

Die URL `file://c:/docs/letter.doc` entspricht nicht dem regulären Ausdruck und bekommt daher kein `project`-Zusatzfeld.


### Beispiel 2: Teilsammlung

Anstatt den Wert des Zusatzfeldes aus der URL zu generieren, können Sie auch einen festen Wert vorgeben.

Angenommen Sie haben in einem Netzlaufwerk bestimmte Dokumententypen in verschiedenen Verzeichnissen abgelegt, z.B. sind Ihre Briefe an drei verschiedenen Orten gespeichert. Mit Hilfe der Zusatzfelder können Sie die Suche auf einen Dokumenttyp beschränken, also z.B. nur alle Ihre Briefe durchsuchen.

Der entsprechende Eintrag in der [CrawlerConfiguration.xml](/en/config/crawlerconfiguration_xml/) könnte z.B. so aussehen:
```xml
<auxiliaryFieldList>
  <auxiliaryField name="doctype" value="letter">
    <regex>^file://c:/projects/letters</regex>
  </auxiliaryField>

  <auxiliaryField name="doctype" value="letter">
    <regex>^file://e:/office/customer/(letters|correspondence)</regex>
  </auxiliaryField>

  <auxiliaryField name="doctype" value="offer">
    <regex>^file://e:/office/customer/offers/</regex>
  </auxiliaryField>

  <auxiliaryField name="doctype" value="specs">
    <regex>/spec(ification)?/</regex>
  </auxiliaryField>
</auxiliaryFieldList>
```

Durch die ersten beiden Einträge bekommen alle Dokumente unterhalb von `c:/projects/letters`, `e:/office/customer/letters` und `e:/office/customer/correspondence` ein `doctype`-Zusatzfeld mit dem Wert `letter`.

Der dritte Eintrag bewirkt das alle Dokumente unterhalb von `e:/office/customer/offers` ein `doctype`-Zusatzfeld mit dem Wert `offer` erhalten.

Durch den letzten Eintrag bekommen alle Dokumente, die `irgendwo` in ihrer URL `/spec/` oder `/specification/` enthalten ein `doctype`-Zusatzfeld mit dem Wert `specs`.

Alle anderen Dokumente bekommen kein `doctype`-Zusatzfeld.


Hinweise
--------

Um die Änderungen an Zusatzfeldern wirksam zu machen, müssen Sie den [Index löschen](/de/howto/delete_index/) und dann [neu erstellen](/de//usage/desktop_getting_started/#index-neu-erstellen) lassen.


Siehe auch
----------

  * [extend_advanced_search](/de/howto/extend_advanced_search/)
