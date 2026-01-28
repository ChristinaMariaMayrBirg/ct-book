# Abstraktionsgrad

Wir haben uns angesehen, wie Julia das Problem mithilfe von **High-Level-Funktionen** aus der Fremdbibliothek `pandas` gelöst hat. Diese Funktionen kapseln komplexe Datenstrukturen und statistische Auswertungen – und ermöglichen dadurch eine sehr kompakte Implementierung.

Anschließend wurde betrachtet, wie Julia das Problem mit eigenen Lösungen umgesetzt hat. Dabei kamen überwiegend **Low-Level-Funktionen** zum Einsatz, bei denen einzelne Schritte explizit implementiert wurden. Am Ende wurden hierfür Standardbibliotheken wie `statistics` genutzt, die elementare statistische Funktionen bereitstellen.


```{admonition} Definition
:class: definition

High-Level-Funktionen beschreiben primär, was berechnet werden soll (z. B. „gib mir eine statistische Zusammenfassung“).
Low-Level-Funktionen legen fest, wie etwas berechnet wird (z. B. Schleifen, Zwischenspeicher, Einzelschritte).

Wichtig: Das ist kein Entweder-oder, sondern eher ein Kontinuum – viele Funktionen liegen „dazwischen“.
```

**Beispiele**

- **High-Level**: `DataFrame.describe()` liefert eine komplette statistische Analyse „in einem Aufruf“.
- **Zwischenstufe**: `statistics.median()` liefert eine einzelne Kenngröße – sie ist Baustein einer Analyse, aber nicht die ganze Analyse.
- **Low-Level**: eine eigene Median-/Quartilsberechnung per Sortieren/Indexieren/Schleifen legt die Rechenschritte selbst fest.



Sie müssen Pakete kennen – und Sie müssen erkennen können, **auf welchem Abstraktionsgrad** Sie gerade programmieren: Verwenden Sie Bausteine, die viel „für Sie erledigen“, oder implementieren Sie die einzelnen Schritte selbst?

In der Vorlesung und den Praktika sind Ihnen verschiedenen Python-Bibliotheken begegnet, die sich im Abstraktionsgrad und in ihrem Einsatzzweck unterscheiden. Die Grafik soll Sie dabei unterstützen, diese Bibliotheken einzuordnen und ihre Beziehungen zueinander zu verstehen.

```{figure} ../../figs/13-fallbeispiel/abstraction-degress.png
---
width: 900px
---
Abstraktionsgrad: High-Level beschreibt *was*, Low-Level beschreibt *wie*.
```


Auf der vertikalen Achse ist der Abstraktionsgrad dargestellt: Weiter oben stehen High-Level-Bibliotheken, die viele Details verbergen und schnelle Ergebnisse ermöglichen. Weiter unten befinden sich Low-Level-Bibliotheken, die näher an den grundlegenden Rechenoperationen arbeiten und mehr Kontrolle, aber auch mehr Eigenarbeit erfordern.
Im Bereich Daten / Numerik (links) haben wir in Julias Programmieraufgabe mit pandas auf der höchsten Ebene gearbeitet. Pandas stellt komfortable Datenstrukturen wie DataFrame und Series bereit und eignet sich besonders für Datenanalyse und Auswertung. Intern nutzt pandas NumPy, das eine niedrigere Abstraktionsebene bildet und effiziente numerische Arrays bereitstellt. Noch weiter unten befinden sich die Module statistics und math aus der Python-Standardbibliothek: statistics bietet grundlegende statistische Funktionen für einfache Datenlisten und greift dabei intern auf elementare mathematische Funktionen aus math zurück.
Im Bereich Visualisierung (rechts) haben Sie bereits matplotlib kennengelernt. seaborn kennen Sie noch nicht. seaborn ist eine High-Level-Bibliothek für statistische Visualisierungen und baut direkt auf matplotlib auf. Matplotlib selbst arbeitet auf einer niedrigeren Ebene und bietet feinere Kontrolle über Achsen, Linien und Layouts. Häufig werden dabei pandas-Daten oder NumPy-Arrays als Eingabe verwendet, was in der Grafik durch gestrichelte Pfeile dargestellt ist.

Insgesamt zeigt die Grafik: Die Bibliotheken stehen nicht isoliert nebeneinander, sondern bauen logisch und technisch aufeinander auf. Je höher der Abstraktionsgrad, desto einfacher ist die Nutzung – je niedriger, desto mehr Kontrolle. 

