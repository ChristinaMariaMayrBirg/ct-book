---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(sec-memory-management)=
# Garbage Collection

```{admonition} Behauptung
:class: remark
In Python muss ich mich nicht um Speicherverwaltung kümmern. 
```

Sie müssen in Python tatsächlich **keinen Speicher manuell reservieren oder freigeben** (wie z.B. in C mit `malloc`/`free`). Diese Aufgabe übernimmt die Python‑Runtime (inklusive Garbage Collection).

Was bedeutet „Python verwaltet Speicher automatisch“ konkret?

- **Allokation**: Wenn neue Objekte entstehen, reserviert die Runtime Speicher dafür.
- **Freigabe**: Wenn Objekte nicht mehr erreichbar sind, kann ihr Speicher wieder freigegeben werden.

Wie genau das passiert, hängt von der Python‑Implementierung ab.
In **CPython** (der üblichsten Implementierung) passiert das grob so:

- **Referenzzählung (reference counting)**: Jedes Objekt weiß, wie viele Referenzen auf es zeigen. Fällt der Zähler auf 0, kann das Objekt sofort freigegeben werden.
- **Zyklus‑Garbage‑Collector**: Referenzzählung allein findet *Zyklen* nicht (Objekte, die sich gegenseitig referenzieren). Ein zusätzlicher GC erkennt solche Zyklen und räumt sie auf.

Warum merkt man das im Code trotzdem?

Auch wenn Sie Speicher nicht manuell verwalten, beeinflusst das Modell Ihr Programmierverhalten:

- Viele Datenstrukturen sind **dynamisch** (wachsen/schrumpfen zur Laufzeit) und enthalten intern **Referenzen** auf ihre Elemente.
- Teilen mehrere Namen/Programmteile dieselben Objekte, werden Themen wie **Mutabilität** und **Seiteneffekte** relevant.

```{admonition} Klarstellung
:class: note
- Sie müssen Speicher nicht manuell verwalten, aber Python verwaltet ihn natürlich trotzdem.
- In CPython: Referenzzählung + Zyklus‑GC.
```