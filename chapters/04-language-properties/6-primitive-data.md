

# Datentypen

Wie wir im Beispiel mit der Potenzierung der Zahl gesehen haben, macht nicht jede Funktionalität für jeden Datentypen Sinn. Die Potenz einer Zahl macht Sinn, unabhängig davon, ob es eine ganze oder eine Kommazahl ist. Die Potenz eines Textes macht keinen Sinn. Deshalb kommen wir nicht darum herum, uns damit zu beschäftigen, was es denn für Datentypen gibt, wie sie sich unterscheiden und wie ich sie in Python nutze. Wir werden uns im Part "Python anwenden" genauer mit Datentypen beschäftigen. 

An dieser Stelle möchten wir kurz eine Besonderheit von Python ansprechen: In Python gibt es im Gegensatz zu anderen Programmiersprachen keine primitiven Datentypen. 

Es gibt grundsätzlich 5 Arten von Datentypen:

1. **Primitive Datentypen**: Zeichnen sich dadurch aus, dass sie direkt vom Betriebssystem unterstützt werden und eine feste Speichergröße haben. Diese existieren in Python nicht direkt (siehe Erklärung unten). Deshalb hier ein Beispiel in der Sprache C/C++: ein `int` belegt immer 4 Bytes (32 Bit), unabhängig vom Wert.

2. **Atomare Datentypen**: Zeichnen sich dadurch aus, dass sie unteilbare Werte repräsentieren - sie können nicht in kleinere Bestandteile zerlegt werden. Beispiel in Python: `int` (5), `float` (3.14), `bool` (True).

3. **Zusammengesetzte Datentypen**: Zeichnen sich dadurch aus, dass sie mehrere Werte in einer Struktur zusammenfassen. Beispiel in Python: `str` ("Hello" - eine Sequenz von Zeichen), `list` ([1, 2, 3]), `tuple` ((1, 2, 3)), `dict` ({"name": "Alice"}), `set` ({1, 2, 3}).

4. **Built-in Datentypen**: Zeichnen sich dadurch aus, dass sie direkt in der Programmiersprache verfügbar sind, ohne dass sie importiert oder definiert werden müssen. Beispiel in Python: alle oben genannten Typen (`int`, `float`, `list`, `dict`, etc.) sind built-in.

5. **Eigens definierte Datentypen**: Zeichnen sich dadurch aus, dass sie vom Programmierer selbst erstellt werden. Beispiel in Python: eigene Klassen wie `class Person:` mit eigenen Attributen und Methoden.



## Besonderheit in Python

In ``Python`` gibt es keine primitiven Datentypen. ``Python`` kapselt die primitiven Datentypen für uns Programmierer*innen.
Zu unserem eigenen Schutz können wir auf diese nicht direkt zugreifen und mit ihnen nicht direkt arbeiten.
Hinter dem Datentyp ``int`` verbirgt sich ein [atomarer Datentyp](def-atomare-data-types), der es uns leichter macht mit ganzen Zahlen umzugehen.
Implementiert ist dieser Datentyp in der Programmiersprache ``C++``.
``Python`` ruft am Ende des Tages ``C++``-Code auf.
Die Implementierung von ``int`` findet sich in den folgenden Dateien (**bitte lassen Sie sich davon nicht abschrecken, Sie müssen diesen Code nicht verstehen!**)

+ [longobject.c](https://github.com/python/cpython/blob/main/Objects/longobject.c)
+ [longintrepr.h](https://github.com/python/cpython/blob/main/Include/longintrepr.h)
+ [longobject.h](https://github.com/python/cpython/blob/main/Include/longobject.h)


Wichtig:
In ``Python`` benötigt eine ganze Zahl ``int`` nicht immer den gleichen Speicherbereich!
Deshalb ist es, anders als in vielen anderen Sprachen, in ``Python`` möglich mit sehr großen ganzen Zahlen zu rechnen!!!
Wäre ``int`` ein primitiver Datentyp, wie etwa in ``Java``, ``C/C++``, so würde ein ``int`` Wert immer gleich viel Speicherplatz belegen.
