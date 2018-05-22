---
title: "How-To: Zugriff auf Ordner in der Trefferliste"
---

[English translation](/en/howto/open_folder/)

How-To: Zugriff auf Ordner in der Trefferliste
==============================================

Zusatzfeature
-------------

Mit einem Mausklick den Ordner mit der gefundenen Datei zu öffnen.


Lösungsansatz
-------------

Zu jedem Treffer der Desktop-Suche einen Link zum Ordner, ähnlich wie `<search:hit_link/>` in der Trefferliste erstellen.


Vorteile
--------

Zusatzkomfort bei der Verwaltung von Dateien.


Quelltext
---------

```java
package net.sf.regain.search.sharedlib.hit;

import net.sf.regain.RegainException;
import net.sf.regain.search.SearchToolkit;
import net.sf.regain.search.results.SearchResults;
import net.sf.regain.util.sharedtag.PageRequest;
import net.sf.regain.util.sharedtag.PageResponse;
import org.apache.lucene.document.Document;

public class DirTag extends AbstractHitTag {

  protected void printEndTag(PageRequest request, PageResponse response,
    Document hit, int hitIndex)
    throws RegainException
  {
    // Get the search results
    SearchResults results = SearchToolkit.getSearchResults(request);
    String url =  results.getHitUrl(hitIndex);

    // Dir_Verweis_erstellen Anfang
    String url_dir = "";
    String url_array[] = url.split("/");	
    for (int i = 0; i < url_array.length-1; i++) {
      url_dir = url_dir+url_array[i]+"/";
    }

    url =url_dir;

    // Dir_Verweis_erstellen Ende
    response.print(url);
  }
}
```

In der Datei `search.jsp` wird folgender Link plaziert:

```html
<a href="file://<search:hit_dir/>" target="_blank">Link zum Ordner</a>
```


Implementierung
---------------

Eine  Klasse `DirTag`, die von der Klasse `net.sf.regain.search.sharedlib.hit.AbstractHitTag` abgeleitet ist, erstellen und im Ordner `net/sf/regain/search/sharedlib/hit` in der Datei `regain.jar` ablegen. Als fertige Vorlage kann dabei die Klasse `net.sf.regain.search.sharedlib.hit.UrlTag` dienen.


Änderungen im Quelltext
-----------------------

```java
// Dir_Verweis_erstellen Anfang 
String url_dir = "";
String url_array[] = url.split("/");	
for (int i = 0; i < url_array.length-1; i++) {
  url_dir = url_dir+url_array[i]+"/";
}
url =url_dir;

// Dir_Verweis_erstellen Ende  
```


Für Firefox-User
----------------

Falls Sie Firefox unter Windows einsetzen, erscheint im Kontextmenü nach dem Rechtsklick auf den Verweis 'Link zum Ordner' ein Menüpunkt 'Launchy -&gt; Ziel mit Explorer ducrhsuchen', falls Sie die Erweiterung.

[Launchy](http://www.erweiterungen.de/detail/Launchy/) installiert haben. Mit der Auswahl des Menüpunkts öffnet sich der Ordner mit der gefundenen Datei im Windows Explorer. Sie können auch 'Launchy -&gt; Link im Internet Explorer öffnen' auswählen - das Ergebnis ist gleich ;-)

Alternativ kann man [ViewSourceWith](http://www.erweiterungen.de/detail/ViewSourceWith/)-Erweiterung einsetzen, die einfacher zu konfigurieren ist. Siehe dazu: [open_file_with](/de/howto/de/howto/open_file_with/)


Einschränkungen
---------------

  * Im Internet Explorer Version 6.0 SP2 ist es nicht möglich, mit einem Klick auf den Link ein Ordner zu öffnen, falls der Ordner auf dem Laufwerk C:/ oder D:/ liegt. In diesen Fällen kann man den Link zum Ordner mit der rechten Maustaste anklicken, im Kontextmenü 'Verknüpfung kopieren' wählen und diese Verknüpfung in der Adressleiste im Browser direkt eingeben, danach 'Wechseln zu' oder Eingabetaste betätigen.
  * Das hier beschriebene How-To funktioniert am komfortabelsten dann, wenn ein Zugriff auf ein file://-URL im Browser erlaubt ist. Falls dies nicht der Fall ist, kann man den oben beschriebenen Trick mit 'Verknüpfung kopieren' anwenden oder mit Firefox-Browser die Launchy-Erweiterung installieren.
  * Es ist nicht möglich, gleichzeitig dieses How-To in der `search.jsp` und `<rewriteRules>` in der `SearchConfiguration.xml` anzuwenden - außer, wenn das Ergebnis von RewriteRules im Zusammenspiel mit `<search:hit_dir/>` einen Pfad generieren, der zu einem existierenden Ordner führt.

FIXME: Eine step-by-step-Anleitung, die hilft im Browser die oben geschilderte Einschränkung 2 zu beseitigen, wäre sehr wünschenswert.


Siehe auch
----------

  * Im Forum: [Diskussion zum How-To](http://forum.murfman.de/de/viewtopic.php?t=220)
  * [Einen Link auf Ordner und nicht auf Datei](http://www.supportnet.de/fresh/2005/1/id987764.asp)


**Autor:** itebob
