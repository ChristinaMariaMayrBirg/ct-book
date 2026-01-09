
# Referenzen in Python

In Python sind Variablen **Referenzen** auf Objekte, nicht die Objekte selbst. Das bedeutet: Eine Variable zeigt auf ein Objekt im Speicher, sie ist nicht das Objekt selbst.

## Objekte per Referenz

Wenn Sie in Python eine Variable einer anderen zuweisen, wird nicht das Objekt kopiert, sondern beide Variablen zeigen auf dasselbe Objekt:

```python
a = [1, 2, 3]
b = a  # b zeigt auf dasselbe Objekt wie a
b.append(4)
print(a)  # Ausgabe: [1, 2, 3, 4] - a wurde auch verändert!
```

**Wichtig:** Bei veränderlichen (mutable) Objekten wie Listen oder Dictionaries bedeutet das, dass Änderungen über eine Referenz auch alle anderen Referenzen auf dasselbe Objekt betreffen.

## Unterschied: Mutable vs. Immutable

Bei unveränderlichen (immutable) Objekten wie `int`, `str`, `tuple` verhält es sich anders:

```python
x = 5
y = x  # y zeigt auf dasselbe Objekt (5)
y = 10  # y zeigt jetzt auf ein neues Objekt (10)
print(x)  # Ausgabe: 5 - x wurde nicht verändert!
```

Bei unveränderlichen Objekten kann der Wert nicht geändert werden. Eine neue Zuweisung erstellt ein neues Objekt, die alte Referenz bleibt unverändert.

## Identität prüfen

Mit `id()` können Sie die Identität (Speicheradresse) eines Objekts prüfen:

```python
a = [1, 2, 3]
b = a
print(id(a) == id(b))  # True - beide zeigen auf dasselbe Objekt

x = 5
y = 5
print(id(x) == id(y))  # True - kleine Integer werden gecacht
```

Hinweis:
**Zusammenfassung:** Python verwendet "call by object reference" - Variablen sind Referenzen auf Objekte im Speicher, nicht die Objekte selbst.
