---
title: "Suchen mit regain"
---

[English translation](/en/usage/searching/)

Suchen mit regain
=================

Diese Seite erklärt, wie Sie mit regain suchen und wie Sie Ihre Suchtreffer weiter eingrenzen können.


Sucharten
---------

In regain stehen Ihnen zwei Sucharten zur Verfügung:

**Standardsuche:** Die Standardsuche ist in der [Suchmaske](/de/components/search_mask/) standardmäßig über den Link `Suchen` verfügbar.
**Erweiterte Suche:** Hier können Sie Ihre Suchanfrage genauer eingrenzen, indem Sie in den Drop-down-Listen die Werte für die zur Verfügung stehenden [Zusatzfelder](/de/features/auxiliary_fields/) auswählen. Standardmäßig ist die Angabe eines bestimmten Dateityps möglich. Je nach Bedarf können weitere Zusatzfelder definiert werden und als [weitere Suchoption](/de/howto/extend_advanced_search/) angeboten werden.


Wie stelle ich eine Suchanfrage?
--------------------------------

Das Prinzip ist hier dasselbe wie bei allen anderen gängigen Suchmaschinen.
  - Tippen Sie Ihre(n) Suchbegriff(e) in das Textfeld ein.
  - Stellen Sie ggf. die Drop-down-Listen ein.
  - Drücken Sie `Enter` oder klicken Sie auf `Suchen`.


Wie definiere ich eine Suchanfrage genauer?
-------------------------------------------

Wenn Ihre Suchanfrage zu viele Treffer verursacht, sollten Sie sie genauer definieren. Hierzu empfiehlt sich im ersten Schritt der Einsatz der `Erweiterten Suche`.

Darüber hinaus können Sie die folgenden Hilfsmittel benutzen:

  * Bool'sche Operatoren: z.B.: "`lucene AND regain`" oder "`+Lucene -Zoe`"
  * [Wildcards](http://de.wikipedia.org/wiki/Wildcard_(Informatik)): z.B.: "`te?t`" oder "`text*`"
  * Phonetische Suche: z.B.: "`Maier~`"
  * Gruppierung: z.B.: "`(Jakarta AND Lucene) OR regain`"
  * Suche in bestimmten [Index-Feldern](/de/components/search_index/#standardfelder): z.B.: "`Lucene title:Seminararbeit`"
  * mit Gänsefüßchen klammern `"Otto Maier"` und damit eine genaue Wortgruppe oder Phrase suchen.


Siehe auch
----------

  * [Suchsyntax von Lucene](http://lucene.apache.org/java/2_4_0/queryparsersyntax.html)
  * unscharfe Ähnlichkeits-Suche via [Qsol](http://famestalker.com/devwiki/index.php?title=Main_Page)
