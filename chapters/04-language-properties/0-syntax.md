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

# Indetation

```{admonition} Behauptung
:class: remark
In Python bestimmt die Formatierung, was passiert.
```

Python nutzt die sogenannte **Off-side rule**: Codeblöcke werden durch Einrückung definiert – nicht durch geschweifte Klammern `{}` oder `begin/end`.
Das heißt, dass die Formatierung bestimmt die Logik. Einrückung ist nicht nur hübsch, sie ist Teil der Sprache!


Mini‑Beispiel: Einrückung ändert Bedeutung

```python
x = 1
if x > 0:
    print("positiv")
    print("immer noch im if-Block")
print("außerhalb")
```

Wenn Sie die Einrückung verändern, ändern Sie den Block – und damit die Programmlogik.

Typischer Fehler: `IndentationError`

```python
if True:
print("oops")
```

Das ist in Python **Syntaxfehler**, nicht nur „schlecht formatiert“.

**Ausnahmen**
Es gibt aber auch Ausnahmen: Leerzeichen um Operatoren (z.B. `+`, `=`, `.`) sind **Stil**. Hier haben die Leerzeichen **keine Bedeutung** für die Programmlogik.

```python
a=1+2
b = 1 + 2
print(a)  # 3
print(b)  # 3
```

Typische Stolperstellen:

- **Tabs vs. Spaces**: Gemischte Einrückung kann zu Fehlern führen (oder zu Code, der „komisch“ aussieht).
- **Kopieren aus PDFs/Websites**: Unsichtbare Whitespaces verursachen manchmal unerwartete `IndentationError`.
- **„Warum ist das in anderen Sprachen egal?“** Dort definieren `{}` die Blöcke; Einrückung ist nur Konvention.

```{admonition} Klarstellung
:class: note
- Einrückung ist in Python Syntax: Sie bestimmt Blöcke und damit Verhalten.
- Nicht jede Formatierung ist semantisch: Leerzeichen um Operatoren sind Stil (z.B. `a=1+2` vs. `a = 1 + 2`).
- Moderne Tools (IDE, Linter, Formatter) helfen, Einrückung konsistent zu halten – aber die Sprache bleibt dabei strikt.
```


