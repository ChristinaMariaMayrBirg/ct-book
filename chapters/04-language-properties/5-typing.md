# Typisierung


## Hintergrund

Ausgangslage: der computer kennt nur 0 und 1 (an/aus-zustände). Wie bereits beschrieben ist es für einen menschen schwierig einen algorithmus in maschinencode auszudrücken. vielmehr wird er eine höherere programmiersprache verwenden. wir haben bereits darüber gesprochen, dass sich compiler und interpreter darum kümmern, dass der quelltext in maschinencode umgewandelt wird. was wir noch nicht besprochen haben ist das wie. 



**Beispiel:** Wir addieren die Zahlen 5000 und 2500 auf einem Rechner mit einer 8-Bit-CPU. 8-Bit-CPU bedeutet: 8 Bits können vom Arbeitsspeicher auf einmal in die CPU verschoben werden.

Auf einem rechner werden zahlen im binärsystem representiert.

5000 entspricht 1001110001000 im dualsystem (13 Stellen)
2500 entspricht 100111000100 im dualsystem (12 Stellen)

Das Programm sieht in Maschinencode aus, wenn es in den Arbeitsspeicher geladen wurde, wie folgt aus:

```
00111110₂  Befehl, der das nächste Byte in die CPU verschiebt
10001000₂  Low-Byte von der Zahl 5000
11000110₂  Befehl, der das nächste Byte zum Wert in die CPU addiert
11000100₂  Low-Byte von 2500
00110010₂  Befehl, der das Ergebnis an der Speicheradresse (nächste zwei Bytes) ablegt
00010000₂  Speicheradresse - Part 2
00000000₂  Speicheradresse - Part 1
00111110₂  Befehl, der das nächste Byte in die CPU verschiebt
00010011₂  High-Byte von 5000
11001110₂  Befehl, der das nächste Byte mit Übertrag zum Wert in die CPU addiert
00001001₂  High-Byte von 2500
00110010₂  Befehl, der das Ergebnis an der Speicheradresse (nächste zwei Bytes) ablegt
00010001₂  Speicheradresse Teil 2
00000000₂  Speicheradresse Teil 1
01110110₂  Befehl zum Anhalten der CPU
00000000₂
00000000₂  Speicherstelle für das Ergebnis
00000000₂  Speicherstelle für das Ergebnis
```


Wir sehen, dass in dem Maschinencode sowohl Befehle als auch Daten abgelegt sind. Je nachdem welchen Chip man vor sich hat, unterscheiden sich diese Befehle. Die Entwicklung von Befehlssätzen ist eine eigene Ingenieursdisziplin. Wenn Sie als Ingenieur Programme entwickeln, werden Sie nur selten damit in Berührung kommen. Womit Sie allerdings in Berührung kommen können, ist die Art, wie Daten im Datenspeicher abgelegt werden.

**Was fällt an dem Beispiel auf?**

1. **Mehrbyte-Zahlen:** Wir haben gesehen, dass die Zahl 5000 in binär 13 Stellen hat: `1001110001000₂`. Da in unserem Beispiel immer nur 8 Bits auf einmal von der CPU verarbeitet werden können, müssen wir die Zahl in zwei Portionen an die CPU übergeben. Das ist unschön, weshalb man inzwischen 64 und auch 128 Bit nutzt (aber auch hier haben wir das Problem - wenn etwas größer ist, müssen wir aufteilen).

2. **Endianness:** Die Reihenfolge, wie die Portionen auf einem Rechner abgelegt sind (1-2-3 oder 3-2-1), bezeichnet man als **Big-Endian** und **Little-Endian**.

3. **Hexadezimaldarstellung:** Die 0 und 1 nehmen relativ viel Platz ein und man übersieht einmal schnell eine 0 oder 1. Man verwendet daher in der Regel nicht die Repräsentation im Binärsystem, sondern im Hexadezimalsystem.

```{admonition} Hinweis
:name: number-representation
:class: remark
Sie haben gerade gesehen, wie wir Zahlen unterschiedlich repräsentieren können. Wenn wir im Alltag von der Zahl 5000 sprechen, meinen wir damit eigentlich 5000 im Dezimalsystem. Genauso gut können Sie die Zahl binär oder auch hexadezimal darstellen - Sie müssen nur die Umrechnung kennen. In höheren Programmiersprachen werden Sie damit nur selten in Berührung kommen. Falls doch: Seien Sie nicht überrascht.
``` 


**Wichtig:** Wir haben gesehen, wie eine Dezimalzahl auf einem Rechner abgebildet wird:
- `5000` (dezimal) → `1001110001000₂` (binär)

**Aber was ist, wenn wir einen Text auf einem Rechner abbilden wollen?**
- `"hello!"` → ??

Wie viele 0 und 1 brauche ich und in welcher Reihenfolge muss ich sie anordnen?

**Antwort:** Es gibt dafür verschiedene Lösungen (verschiedene Zeichenkodierungen). 

**Beispiel mit Multibyte-Zeichen: "Hello 中"**

**"Hello 中" in UTF-8:**
- H (U+0048): 01001000₂
- e (U+0065): 01100101₂
- l (U+006C): 01101100₂
- l (U+006C): 01101100₂
- o (U+006F): 01101111₂
- Leerzeichen (U+0020): 00100000₂
- 中 (U+4E2D): 11100100 10111000 10101101₂

Gesamt: 11 Bytes = 88 Bits (5 ASCII-Zeichen à 1 Byte + 1 Leerzeichen à 1 Byte + 1 chinesisches Zeichen à 3 Bytes)

**"Hello 中" in UTF-16:**
- H (U+0048): 00000000 01001000₂
- e (U+0065): 00000000 01100101₂
- l (U+006C): 00000000 01101100₂
- l (U+006C): 00000000 01101100₂
- o (U+006F): 00000000 01101111₂
- Leerzeichen (U+0020): 00000000 00100000₂
- 中 (U+4E2D): 01001110 00101101₂

Gesamt: 14 Bytes = 112 Bits (7 Zeichen à 2 Bytes)

Wir sehen: UTF-8 verwendet für ASCII-Zeichen 1 Byte, für das chinesische Zeichen 3 Bytes (variabel). UTF-16 verwendet für alle Zeichen im Basic Multilingual Plane (BMP) fest 2 Bytes pro Zeichen.

**Kernbotschaft:** Jeder Buchstabe wird wieder durch eine Abfolge von Bits realisiert.

```{admonition} Hinweis
:name: bit-abstraction
:class: remark
Mit Ausnahme der Bitoperationen bieten Hochsprachen wie Python, Java, JavaScript bewusst kaum die Möglichkeit, direkt mit den Bits im Speicher zu interagieren.
Wir ändern Zahlen, Text und anderes und die Hochsprachen kümmern sich darum, dass die Werte im Speicher dementsprechend angepasst werden.
Diese Abstraktion schützt Programmierer\*innen vor Fehlern und erhöht die Lesbarkeit des Quellcodes.
```

**Was wir auch gesehen haben:** Es gibt unterschiedliche Arten, wie man die Abfolge von Bits realisieren kann. Idealerweise wollen wir keine Bits verschwenden. Im Textbeispiel sehen wir, dass die Buchstaben bei UTF-16 im ersten Bereich immer null sind. In UTF-8 wird das vermieden, indem man eine Art Meta-Information hinzufügt: Bestimmte Zeichen sind dann länger (die, die nicht so oft vorkommen).

**Was macht der Compiler oder Interpreter?** Er kümmert sich darum, dass die Objekte (Zahlen, Text, etc.) in 0 und 1 überführt werden. Für einige Objekttypen ist klar, wie diese abgelegt werden (ganze Zahlen), für einige Objekttypen (Text) gibt es hierfür mehrere Wege. Unabhängig davon muss der Compiler/Interpreter wissen, was er da vor sich hat: Zahl oder Text, weil abhängig davon muss er ja ein unterschiedliches Verfahren zum Übersetzen auswählen.

## Dynamische Typisierung

Aber woher weiß der Compiler/Interpreter, was er da vor sich hat? Hier gibt es zwei Wege:

1. **Statische Typisierung:** Der Datentyp wird im Quellcode explizit festgelegt (z.B. in Java, C++).
2. **Dynamische Typisierung:** Der Datentyp wird nicht festgelegt und der Interpreter/Just-in-Time-Compiler muss während der Laufzeit bestimmen, was es ist (z.B. in Python).

Python besitzt eine **dynamische Typisierung**, d.h. Sie können theoretisch mit Python programmieren, ohne dass Sie sich groß darüber Gedanken machen müssen, ob Sie jetzt ganze Zahlen oder Gleitkommazahlen miteinander addieren wollen.

```python
def potenz(basis, exponent):
    return basis ** exponent

if __name__ == "__main__":
    # Mit ganzen Zahlen
    ergebnis_ganz = potenz(3, 4)
    print(ergebnis_ganz)  # Ausgabe: 81
    
    # Mit Gleitkommazahlen
    ergebnis_komma = potenz(3.0, 2.0)
    print(ergebnis_komma)  # Ausgabe: 9.0
    
    # Mit Strings - FEHLER!
    ergebnis_string = potenz("text1", "text2")
    # TypeError: unsupported operand type(s) for ** or pow(): 'str' and 'str'
```

**Problem:** Es gibt keine Potenzen von einem Text. Deshalb gibt es einen Runtime-Error. Das Problem in Python: Wir können grundsätzlich mal alles übergeben, aber ob das klappt, wissen wir erst bei der Ausführung. Bei fremdem komplizierten Quellcode müssen Sie raten und testen, was Sie übergeben dürfen. Das ist nicht effizient, weshalb man in Python üblicherweise auch den Datentyp angibt (dies dient zur Dokumentation und besseren Fehlererkennung).

**Lösung: Type Hints in Python**

```python
def potenz(basis: float, exponent: float) -> float:
    """Berechnet die Potenz von basis^exponent. Nur für Zahlen!"""
    return basis ** exponent

if __name__ == "__main__":
    ergebnis = potenz(3, 4)
    print(ergebnis)  # Ausgabe: 81
    
    # IDE/Type Checker warnt: potenz("text", 2) ist nicht erlaubt!
```

```python
from typing import Union

def addition(a: Union[int, float, str], b: Union[int, float, str]) -> Union[int, float, str]:
    """Addiert Zahlen oder verkettet Strings."""
    return a + b

if __name__ == "__main__":
    # Funktioniert mit Zahlen
    ergebnis_zahl = addition(3, 4)
    print(ergebnis_zahl)  # Ausgabe: 7
    
    # Funktioniert mit Strings
    ergebnis_string = addition("text1 ", "text2")
    print(ergebnis_string)  # Ausgabe: "text1 text2"
```

**Vorteil von Type Hints:**
- Code ist selbstdokumentierend: Man sieht sofort, welche Typen erwartet werden
- IDEs können Fehler bereits beim Schreiben erkennen
- Type Checker (z.B. `mypy`) können den Code analysieren, ohne ihn auszuführen
- Bessere Unterstützung durch Code-Vervollständigung in IDEs

**Haupterkenntnis:** Python zwingt uns nicht dazu, dass wir einen Datentyp festlegen. Ich kann einfach sagen:

```python
x = 3 
x = 4.0
```

Python erkennt automatisch, dass es eine ganze Zahl oder eine Gleitkommazahl ist und speichert das entsprechende Objekt möglichst effizient für uns ab. Da der Typ während der Laufzeit bestimmt wird, spricht man von **dynamischer Typisierung**.

## Starke Typisierung

Python ist außerdem **stark typisiert** (stark und dynamische Typisierung), d.h. dass der Typ einer Variable nicht einfach umgewandelt werden kann.

**Beispiel schwach typisierte Sprache (JavaScript):**
```javascript
x = "5"
y = 2 + x  // Addition einer Zahl 2 mit einem String, der in eine Zahl umgewandelt wird
// Ergebnis: y = "25" (String-Konkatenation) oder y = 7 (je nach Kontext)
```

**In Python schlägt das fehl:**
```python
x = "5"
y = 2 + x  # TypeError: unsupported operand type(s) for +: 'int' and 'str'
``` 

```{admonition} Hinweis
:name: python-typing-performance
:class: remark
Python ist dynamisch und stark getypt.
Jedoch ruft Python intern C/C++ Code auf und dieser ist statisch getypt!
Python ist immer dann schnell, wenn der statisch getypte Code aufgerufen wird und immer dann langsam, wenn wir lange im Python-Code selbst (der dynamisch getypt ist) verweilen.
```


