---
title: "How-To: Zusatzfelder als Drop-Down in Erweiterte Suche einbinden"
---

[English translation](/en/howto/extend_advanced_search/)

How-To: Zusatzfelder als Drop-Down in Erweiterte Suche einbinden
================================================================

Sie möchten weitere [Zusatzfelder](/de/features/auxiliary_fields/), in die [Erweiterte Suche](/de/features/advanced_search/) einbinden, um den Benutzern mehr Möglichkeiten zur Eingrenzung der Suche zu geben.

Hierzu müssen Sie die `advancedsearch.jsp` entsprechend verändern.


Beispiel: Drop-down-Liste mit Dokumenttyp
-----------------------------------------

Angenommen Sie haben ein [Zusatzfeld für Dokumenttypen angelegt](/de/features/auxiliary_fields/#beispiel-2:-teilsammlung) und möchten nun eine Drop-down-Liste als zusätzliche Suchoption in der Erweiterten Suche anbieten, die alle im [Suchindex](/de/components/search_index/) vorhandenen Dokumenttypen enthält.

  * Öffnen Sie die `advancedsearch.jsp` in einem Editor.
  * Navigieren Sie zu folgendem Code, der die Drop-down-Liste für Dateiendungen definiert:

```html
<tr>
  <td><search:msg key="fileExtension"/>:</td>
   <td><search:input_fieldlist field="extension" allMsg="{msg:allItem}"/></td>
</tr> 
```

  * Fügen Sie dahinter nun den folgenden Code ein.

```html
<tr>
  <td>Dokumententyp:</td>
  <td><search:input_fieldlist field="doctype" allMsg="{msg:allItem}"/></td>
</tr>
```

Mit dem `search:input_fieldlist`-Tag definieren Sie eine neue Drop-down-Liste, die alle Inhalte des Zusatzfeldes "doctype" zur Sucheingrenzung anbietet. Die Anordnung bezieht sich in diesem Beispiel auf das Standardlayout von regain.
