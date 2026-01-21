---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(sec-memory-management)=
# Speicherverwaltung in Python

In ``Python`` müssen sich Programmierer\*innen um Speicheradressen, das Reservieren und Freigeben von Speicher nicht kümmern! 
Das übernimmt der sog. [Garbage Collector](def-garbage-collector). 

Aber wie funktioniert das eigentlich? Und was bedeutet das für Sie als Programmierer\*in?

## Dynamische Speicherverwaltung

``Python`` verwendet das Konzept der *[dynamischen Sammlungen](def-dynamic-ds)* für die Speicherverwaltung.
Das bedeutet, dass Datenstrukturen in ``Python`` (wie Listen, Tupel, Dictionaries, etc.) nicht als zusammenhängende Speicherbereiche im Arbeitsspeicher abgelegt werden müssen, sondern dass ihre Elemente an verschiedenen Stellen im Speicher liegen können.

### Zeiger und Referenzen

Damit diese fragmentierten Speicherbereiche als zusammenhängende Datenstruktur funktionieren können, verwendet ``Python`` *[Zeiger](def-pointer)* (auch *Referenzen* genannt).

```{admonition} Zeiger
:name: def-pointer
:class: definition
Ein *Zeiger* ist ein Objekt welches eine Speicheradresse repräsentiert.
Programmiersprachen bieten die Mittel um Zeiger *aufzulösen*, was den Zugriff auf das Objekt auf das sie verweisen ermöglicht.
```

```{admonition} Wichtig: Variablen als Zeiger
:name: remark-variables-as-pointers
:class: attention

In ``Python`` werden Variablen durch Zeiger realisiert.
Wenn Sie eine Variable erstellen, zeigt diese Variable auf einen Speicherbereich, in dem der Wert gespeichert ist.
Das bedeutet, dass mehrere Variablen auf denselben Wert zeigen können. 
```

### Was bedeutet das für uns Programmierer?

**Vorteile:**

1. **Automatische Speicherverwaltung**: Sie müssen sich nicht darum kümmern, Speicher zu reservieren oder freizugeben.
   Der Garbage Collector erkennt automatisch, wenn ein Objekt nicht mehr verwendet wird und gibt den Speicher frei.

2. **Flexible Datenstrukturen**: Datenstrukturen können zur Laufzeit wachsen und schrumpfen, ohne dass Sie sich um die Speicherverwaltung kümmern müssen.
   Eine Liste kann z.B. dynamisch Elemente hinzufügen oder entfernen.

3. **Einfache Syntax**: Sie müssen keine expliziten Zeigeroperationen durchführen.
   ``Python`` kümmert sich automatisch um die Verwaltung der Zeiger.

**Was Sie beachten sollten:**

1. **Speicherverbrauch**: Dynamische Sammlungen benötigen zusätzlichen Speicher für die Zeiger.
   Bei sehr großen Datenmengen kann dies relevant sein.

2. **Performance**: Der Zugriff über Zeiger kann etwas langsamer sein als direkter Zugriff auf zusammenhängende Speicherbereiche.
   In der Praxis ist dieser Unterschied jedoch meist vernachlässigbar.

1. **Referenzen vs. Kopien**: Da Variablen in ``Python`` Zeiger sind, bedeutet das Zuweisen einer Liste zu einer neuen Variable nicht automatisch eine Kopie. Welche Auswirkung das hat besprechen wir in den kommenden Abschnitten. 



