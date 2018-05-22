---
title: "How-To: Eigene Tags in der Suchmaske hinzufügen"
---

[English translation](/en/howto/add_custom_tag/)

How-To: Eigene Tags in der Suchmaske hinzufügen
===============================================

**Problem:**

Die vorhandenen Tags und ihre Optionen reichen nicht aus, um dynamisch den richtigen HTML-Code zu generieren.

**Lösungsansatz:**

Neue Tags können via Java hinzugefügt werden und anschließend bei SimpleServer/Tomcat registriert werden.

**Vorteile:**

  * Keine Einschränkungen in der Umsetzbarkeit von dynamisch generierten Inhalten

**Nachteile:**

  * Java-Kenntnisse erforderlich. 

**Autor:**

Benjamin Pick https://github.com/benjaminpick

Download
--------

  * Ein Beispiel der Umsetzung befindet sich unter contrib/crawler-thumbnails.

Anleitung
---------

Angenommen, Sie möchten folgenden Tag in ihren JSPs benutzen:

```xml
<p><my_tag:helloworld/></p>
```

Dafür erstellen wir eine Klasse `HelloworldTag` im package `some.example`. (Der name der Klasse wird durch den Tagnamen festgelegt. &lt;my_tag:hello_world/&gt; wäre Klasse `World` im package `some.example.hello`)

```java
package some.example;

import net.sf.regain.RegainException;
import net.sf.regain.util.sharedtag.PageRequest;
import net.sf.regain.util.sharedtag.PageResponse;
import net.sf.regain.util.sharedtag.SharedTag;

public class HelloworldTag extends SharedTag
{
  public void printEndTag(PageRequest request, PageResponse response) throws RegainException
  {
    response.print("Hello, <span class=\"highlight\">World</span>!");
  }
}
```

Jetzt kompilieren wir diese Klasse mit der verwendeten Regain-Version:


    javac -classpath path/to/build/regain.jar src/some/example/HelloworldTag.java

Das weitere Vorgehen hängt davon ab, ob die Desktop- oder Server-Version verwendet wird. (Natürlich funktioniert auch beides).

### Desktop-Suche
_(benötigt regain Version 1.7.9 oder höher)_

Damit die Desktop-Suche funktioniert, muss der Tag-Namespace ("my_tag") unter [desktopconfiguration.xml](/de/howto/de/config/desktopconfiguration_xml/) hinzugefügt werden:

```xml
<!-- Register namespaces for Simple Server -->
<simple_register_namespace>
  <!-- Default namespaces: search, config, status -->
  <namespace name="search">net.sf.regain.search.sharedlib</namespace>
  <namespace name="config">net.sf.regain.ui.desktop.config.sharedlib</namespace>
  <namespace name="status">net.sf.regain.ui.desktop.status.sharedlib</namespace>
   <namespace name="my_tag">some.example</namespace>
</simple_register_namespace>
```

Damit die generierte .class-Datei geladen wird, können wir sie entweder der regain.jar hinzufügen (wenn Sie sie selbst [building_regain](/de/howto/de/project_info/building_regain/)), oder in als `my_tag.jar` in den `web/taglib`-Ordner stecken.


    jar c0f my_tag.jar some/example/*.class

### Server-Suche

Zuerst müssen wir die neuen Tags deklarieren. Wir erstellen eine Datei `web/taglib/mytag.tld` (Name wählbar). (Siehe `web/server/regain-search.tld` als Template.)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE taglib PUBLIC "-//Sun Microsystems, Inc.//DTD JSP Tag Library 1.1//EN" "http://java.sun.com/dtd/web-jsptaglibrary_1_1.dtd">

<taglib>
  <tlibversion>1.0</tlibversion>
  <jspversion>1.1</jspversion>
  <shortname>my_tag</shortname>
  <info>Example Taglib</info>
  <tag>
    <info>
      Shows "Hello, World!"
    </info>
    <name>helloworld</name>
    <tagclass>some.example.server.HelloworldTag</tagclass>
    <bodycontent>empty</bodycontent>
  </tag>
</taglib>
```

Dann fügen wir diese Deklaration der JSP hinzu (ganz oben):

```xml
<%@taglib uri="taglib/mytag.tld" prefix="my_tag" %>
```

Wir müssen noch eine Wrapper-Klasse schreiben (`some/example/server/HelloworldTag.java`):

```java
package some.example.server;

import net.sf.regain.util.sharedtag.taglib.SharedTagWrapperTag;

public class HelloworldTag extends SharedTagWrapperTag {
  public HelloworldTag() {
    super(new some.example.HelloworldTag());
  }
}
```
(Kompilieren am besten mit den original-Sourcen von Regain ... ant runtime-server und dann build/classes und build/included-lib-classes/common als Classpath verwenden.)

Jetzt muss Regain nur noch (beide) Klassen laden. Entweder in die .war packen, oder nach dem deployen nach `WEB-INF/classes` (some/example/...) oder nach `WEB-INF/lib` (als my_tag.jar) kopieren. Der Servlet-Container muss neu gestartet werden.



Siehe auch
----------

  * [howto](/de/howto/) - Übersicht über alle How-Tos
  * https://github.com/benjamin4ruby/java-thumbnailer - Thumbnails der Dateien erstellen und anzeigen
