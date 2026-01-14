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

(sec-string)=
# Zeichenketten - str

Eine Zeichenkette (engl. [String](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)) ``str`` ist eine [Sequenzen](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range) von Zeichen.
Wie ein [Tupel](sec-tuple), ist auch eine Zeichenkette **unveränderlich** (engl. immutable).
So kann eine Zeichenkette als ein besonderes Tupel, welches nur Zeichen enthält, gedeutet werden.

``Python`` bietet uns viele nützliche Funktionen um auf Zeichenketten zu operieren.
Zeichenketten können durch einfache oder doppelte Anführungszeichen umschlossen sein.

```{code-cell} python3
text = 'Hello World!'
text = "Hello World!"
```

Was wir bereits exzessive genutzt haben ist die Ausgabe von Zeichenketten durch die *built-in* Funktion ``print``.

```{code-cell} python3
text = 'Hello World!'
print(text)
```

Um Variablen oder Werte anderer Datentypen mit ``print`` auszugeben, mussten wir diese immer mit der *built-in Funktion* ``str`` in eine Zeichenkette umwandeln.
Da dies so häufig gemacht werden muss, haben die Entwickler\*innen von ``Python`` sich etwas einfallen lassen.
Stellen wir vor unsere Zeichenkette ein ``f``, so handelt es sich um eine sog. *formatierte Zeichenkette*.
Diese helfen uns Variablen oder Werte direkt in eine Zeichenkette einzufügen.
Vergleichen Sie folgenden Code:

```{code-cell} python3
x = 5
y = 10
print('x + y = ' + str(x) + ' + ' + str(y) + ' = ' + str(x+y)) # ugly
print(f'x + y = {x} + {y} = {x+y}')                            # beautiful
```

Das vereinfacht das Schreiben und Lesen solcher Ausgaben ungemein.
Sie können formatierte Zeichenketten auch ohne ``print`` verwenden.

```{code-cell} python3
x = 5
y = 10
formatted_str = f'x + y = {x} + {y} = {x+y}'
formatted_str
```

Zwei Zeichenketten lassen sich mit dem ``+``-Operator verketten.

```{code-cell} python3
prefix = 'Hello'
suffix = ' Welt!'
text = prefix + suffix
print(prefix)
print(suffix)
print(text)
```

Bestimmte Zeichen kontrollieren die Darstellung des Textes, z.B. ob eine Leerzeile ein Leerzeichen oder ein Tab eingefügt werden soll.

```{code-cell} python3
space = ' '
space_line = '\n'

print('Hello' + space + 'World' + space_line + '!')
```

Die *leere Zeichenkette* verändert bei der Verkettung eine andere Zeichenkette nicht.
Es ist das neutrale Element der Zeichenverkettung.

```{code-cell} python3
empty_str = ''

print('The correct answer is 42!')
print('The correct' + empty_str + empty_str + empty_str + ' answer is 42!')

'Hello' == 'Hello' + empty_str
```

Zeichenketten lassen sich wie Listen und Tupel [indexieren](sec-list-index),
Mit der *built-in Funktion* ``len``, kann man die Länge einer Zeichenkette erfragen.
Folgender Code gibt jedes einzelne Zeichen einer Zeichenkette aus.

```{code-cell} python3
text = 'Hello World!'

for i in range(len(text)):
  print(text[i])
```

Das lässt sich jedoch auch einfacher schreiben:

```{code-cell} python3
text = 'Hello World!'

for char in text:
  print(char)
```

Auch bei Zeichenketten können wir negative Indices verwenden.
``text[-1]`` gibt uns das letzte und ``text[-2]`` das vorletzte Zeichen.

```{code-cell} python3
text = 'Zeichensalat'

print(text[-1])
print(text[-2])
```

Lassen Sie uns eine Zeichenkette umdrehen:


```{code-cell} python3
text = 'Zeichensalat'
reverse_text = ''

for i in range(len(text)):
  reverse_text += text[-(i+1)]

print(text)
print(reverse_text)
```

Genau wie [Listen](sec-list) und [Tupeln](sec-tuple), lassen sich auch Zeichenketten zerschneiden ([indexieren](sec-list-index)).

```{code-cell} python3
text = 'Zeichensalat'
print(text[0:2])
print(text[0:len(text)])   # take it all
print(text[0:-3])          # negative indexing
print(text[1:-1])          # skip first and last
print(text[-3:-1])         # negative indexing
print(text[2:])            # skip the first 2 and take the rest
```

Dabei ist ``text[2:]`` eine Kurzschreibweise für ``text[2:len(text)]`` und ``text[:2]`` für ``text[0:2]``.

Hin und wieder kann es vorkommen, dass Sie Zeichen schreiben möchten, welche bereits in ``Python`` mit einer Bedeutung belegt sind.
Wie schreiben wir beispielsweise ``Anna sagte: 'Wie geht es dir'``?
Dafür müssen wir das ``'``-Zeichen mit einem ``\`` *maskieren*:

```{code-cell} python3
print('Anna sagte: \'Wie geht es dir\'')
```

Zeichenketten sind Objekte die uns viele nützliche Funktionen anbieten.
Zu beachten ist, dass Zeichenketten **unveränderlich** sind, d.h. die Funktionen liefern neue Zeichenkette zurück, die ursprüngliche bleibt unverändert.

Mit ``text.upper()`` können wir beispielsweise alle Zeichen einer Zeichenkette in Großbuchstaben transformieren.

```{code-cell} python3
text = 'Zeichensalat'
text_upper = text.upper()
print(text)
print(text_upper)
```

Wir können die Vorkommnisse eines Zeichen in einer Zeichenkette zählen oder ganze Zeichenfolgen ersetzten:

```{code-cell} python3
text = 'Zeichensalat'
print(text.count('a'))
print(text.replace('salat', 'spinat'))
```

Es würde zu weit gehen alle Funktionen zu besprechen -- das wäre auch ziemlich langweilig.
Schauen Sie sich einfach die [Dokumentation](https://docs.python.org/3/library/string.html) an oder verwenden Sie die eingebaute Hilfe ``help(str)``.

## Formatierte Zeichenketten (f-Strings) - Vertiefung

Wie bereits oben erwähnt, sind **f-Strings** (formatted string literals) eine elegante Möglichkeit, Variablen und Ausdrücke direkt in Zeichenketten einzubetten. Das ``f`` vor der Zeichenkette aktiviert diese Funktionalität.

### Grundlegende Syntax

Innerhalb von geschweiften Klammern ``{}`` können Sie beliebige Python-Ausdrücke schreiben:

```{code-cell} python3
name = 'Anna'
alter = 25
print(f'Mein Name ist {name} und ich bin {alter} Jahre alt.')
```

### Ausdrücke in f-Strings

Sie können nicht nur Variablen, sondern auch komplexe Ausdrücke verwenden:

```{code-cell} python3
x = 10
y = 5
print(f'Das Ergebnis von {x} + {y} ist {x + y}')
print(f'Das Quadrat von {x} ist {x ** 2}')
```

### Methodenaufrufe

Auch Methodenaufrufe sind innerhalb von f-Strings möglich:

```{code-cell} python3
text = 'Python'
print(f'Der Text "{text}" hat {len(text)} Zeichen.')
print(f'In Großbuchstaben: {text.upper()}')
```

### Formatierung von Zahlen

Für technische Anwendungen ist es oft wichtig, Zahlen in einem bestimmten Format darzustellen. f-Strings bieten hierfür mächtige Formatierungsoptionen:

**Dezimalstellen begrenzen:**

```{code-cell} python3
pi = 3.14159265359
print(f'Pi auf 2 Dezimalstellen: {pi:.2f}')
print(f'Pi auf 4 Dezimalstellen: {pi:.4f}')
```

**Wissenschaftliche Notation:**

```{code-cell} python3
große_zahl = 1234567890
print(f'Wissenschaftliche Notation: {große_zahl:e}')
print(f'Wissenschaftliche Notation mit 2 Dezimalstellen: {große_zahl:.2e}')
```

**Ausrichtung und Breite:**

```{code-cell} python3
zahl = 42
print(f'Rechtsbündig (10 Zeichen): {zahl:>10}')
print(f'Linksbündig (10 Zeichen): {zahl:<10}')
print(f'Zentriert (10 Zeichen): {zahl:^10}')
```

**Mit führenden Nullen:**

```{code-cell} python3
zahl = 42
print(f'Mit führenden Nullen: {zahl:05d}')
```

**Tausender-Trennzeichen:**

```{code-cell} python3
große_zahl = 1234567
print(f'Mit Tausender-Trennzeichen: {große_zahl:,}')
```

### Praktisches Beispiel für Maschinenbauer

```{code-cell} python3
# Berechnung einer Kraft
masse = 10.5  # kg
beschleunigung = 9.81  # m/s²
kraft = masse * beschleunigung

print(f'Berechnung der Gewichtskraft:')
print(f'Masse: {masse} kg')
print(f'Erdbeschleunigung: {beschleunigung} m/s²')
print(f'Kraft: {kraft:.2f} N')
print(f'Kraft (wissenschaftlich): {kraft:.2e} N')
```

### Verschachtelte Anführungszeichen

Bei f-Strings können Sie einfache oder doppelte Anführungszeichen verwenden, was hilfreich ist, wenn Sie Anführungszeichen im Text benötigen:

```{code-cell} python3
name = 'Anna'
print(f"Sie sagte: 'Hallo, {name}!'")
print(f'Er antwortete: "Guten Tag, {name}!"')
```

### Mehrzeilige f-Strings

f-Strings können auch über mehrere Zeilen gehen:

```{code-cell} python3
name = 'Anna'
alter = 25
beruf = 'Ingenieurin'

text = f"""
Name: {name}
Alter: {alter}
Beruf: {beruf}
"""
print(text)
```

```{admonition} Wichtig
:class: important

- f-Strings wurden in Python 3.6 eingeführt und sind die modernste und empfohlene Methode zur String-Formatierung.
- Sie sind effizienter als die älteren Methoden (``.format()`` oder ``%``-Formatierung).
- Die Ausdrücke in ``{}`` werden zur Laufzeit ausgewertet, was bedeutet, dass Sie auch Funktionen aufrufen können.
- Für komplexe Formatierungen können Sie Format-Spezifikationen nach einem Doppelpunkt ``:`` verwenden (z.B. ``{zahl:.2f}``).
```

f-Strings machen die String-Formatierung in Python deutlich lesbarer und einfacher zu verwenden, besonders wenn Sie Variablen und berechnete Werte in Textausgaben einbetten möchten.