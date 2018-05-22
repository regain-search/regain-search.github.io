---
title: "File-zu-Http-Brücke"
---

[English translation](/en/features/file-to-http-bridge/)

File-zu-Http-Brücke
===================

Einige Browser enthalten einen Sicherheitsmechanismus, der das Laden von file-URLs von Seiten, die über HTTP geladen wurden, verhindert.

Damit diese Dateien von den Suchergebnissen aus geladen werden können, bietet regain eine **File-zu-Http-Brücke** an, die alle Dateien über HTTP zur Verfügung stellt, die sich im Index befinden.

Die [Desktop-Suche](/de/project_info/variant_comparison/) erlaubt dabei nur Zugriffe von lokalen Rechner aus (localhost).

Sie können diesen Mechanismus in der [SearchConfiguration.xml](/en/config/searchconfiguration_xml/) mit Hilfe des `<useFileToHttpBridge>`-Tags an- und abschalten.
