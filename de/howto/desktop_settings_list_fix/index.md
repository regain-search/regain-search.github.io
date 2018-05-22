---
title: "How-To: Bug-Fix für White- und Black-List-Bearbeitung in der Einstellungsseite"
---

[English translation](/en/howto/desktop_settings_list_fix/)

How-To: Bug-Fix für White- und Black-List-Bearbeitung in der Einstellungsseite
==============================================================================

Das Problem
-----------

In der Desktop-Variante funktioniert die Editierung der 'startlist' und 'blacklist' in der Einstellungsseite nicht korrekt. Es werden nicht markierte Einträge entfernt, die markierte dagegen bleiben in der Liste.


Lösungsansatz
-------------

Die Bedingung
```javascript
if (list.options[i].value == text)
```

durch eine mit `selected`-Ereignis ersetzen.


Vorteile
--------

Es werden ausschließlich markierte Einträge entfernt.


Nachteile
---------

Falls mehrere Einträge markiert sind, wird nur ein Eintrag entfernt.


Implementierung
---------------

Änderungen in der regain.js:

```javascript
function removeFromList(listName) {
  var field = document.getElementById(listName + "-entry");
  var list = document.getElementById(listName + "-list");

  // Remove marked entries
  for (var i = 0; i < list.length; i++) {
    if (list.options[i].selected) {
      list.options[i] = null;
    }
  }
 }
```


**Autor:** itebob
