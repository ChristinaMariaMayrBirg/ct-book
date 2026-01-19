# Datenmodell (Einschub)
(sec-object-model)=

Zahlreiche Eigenschaften von Python sind direkte Folgen des Datenmodells, mit denen wir uns in den kommenden Abschnitten auseinandersetzen werden. Voraussetzung um diese zu verstehen, ist das Verständnis über das Datenmodell. Deshalb gehen wir hier kurz auf Pythons Datenmodell ein. 

Für den Computer sind Daten immer **Bits**. Ob eine Bitfolge „eine Zahl“ oder „Text“ bedeutet, hängt von ihrer **Interpretation** ab.
In Python übernimmt diese Interpretation das Laufzeitsystem – aber nur, weil zu jedem Wert **Typinformationen** existieren.

Genau hier kommt das Datenmodell ins Spiel: In Python werden Werte als Objekte modelliert. Ein Objekt hat (mindestens) einen Wert, einen Typ und eine Identität.
Variablennamen sind dann keine „Speicherzellen“, sondern Bindungen auf solche Objekte. Der Typ des Objekts bestimmt, wie die zugrunde liegenden Bits zu interpretieren sind (z.B. als `int` oder als `str`).

Sehen wir uns hierzu das folgende Code‑Beispiel an:

```{code-cell} ipython3
x = 100
identitaet = id(x)
print("id(x):", identitaet)  # Identität (Adresse/Referenzwert)
print("x:", x)               # Wert
```

Auf den ersten Blick wirkt es so, als würde der Zahlenwert *100* „in“ der Variable `x` abgespeichert werden.
Unter der Haube passiert aber etwas anderes: `x` ist **nur ein Name**, der an ein `int`‑Objekt **gebunden** wird.
Dieses Objekt hat einen Wert („100“), einen Typ (`int`) und eine Identität („dieses konkrete Objekt“). Diese Identität können Sie mit `id(...)` sichtbar machen (in CPython ist das oft die Speicheradresse).

- Ein **Objekt** ist ein Wert *mit Identität* (und Typ).
- Ein **Name** (Variablenname) ist eine **Bindung** auf ein Objekt.
- Beim Zuweisen wird **kein Speicherbereich „gefüllt“**, sondern ein Name wird **neu gebunden**.

Eine *Variable* ist (vereinfacht) also ein **Name**, mit dem Sie ein Objekt wiederfinden können. Mit dem Zuweisungszeichen `=` wird der Name an ein Objekt „gebunden“.


```{figure} ../../figs/overview/object.png
---
width: 550px
name: fig-python-object-model
---
Ein Objekt hat eine Identität (`id`) und einen Wert; Variablennamen sind Bindungen auf Objekte.
```

Das Zuweisungszeichen `=` unterscheidet sich damit vom mathematischen \(=\):

\[
x = 13
\]

In Python bedeutet

```{code-cell} ipython3
x = 13
```

„Binde den Namen `x` an das Objekt `13`“ – nicht „lege 13 in eine Variable ab“.

```{figure} ../../figs/python-tutorial/variables/ram.png
---
width: 400px
name: fig-ram-language-properties
---
Der Arbeitsspeicher ist eine sehr lange Liste bestehend aus Bits.
```

```{figure} ../../figs/python-tutorial/variables/variable.png
---
width: 800px
name: fig-variable-language-properties
---
Eine Variable ist ein Name, der auf einen Speicherbereich (und damit auf ein Objekt) zeigt.
```

Identität vs. Gleichheit: `is` und `==`

Zwei Namen können auf **dasselbe Objekt** zeigen (gleiche Identität) oder auf **zwei verschiedene Objekte**, die zufällig gleich aussehen (gleicher Wert).

```{code-cell} ipython3
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(a == b, a is b)  # gleicher Inhalt, gleiche Identität
print(a == c, a is c)  # gleicher Inhalt, aber andere Identität
```

- `==` prüft (typischerweise) **Wert/Gleichheit**.
- `is` prüft **Identität** („ist es wirklich dasselbe Objekt?“).

```{admonition} Klarstellung
:class: note
- Namen (Variablen) referenzieren Objekte (Binding), Python ist nicht „Variablen = Speicherzellen“.
- Mit `is` prüfen Sie Identität (dasselbe Objekt), mit `==` Gleichheit (gleicher Wert).
```

