# Ausgaben

Wenn wir in Python Daten ausgeben möchten, verwenden wir die Funktion `print()`.

```python
print("Hallo Welt!")
```

## Was macht `print()`?

- `print()` schreibt **Text** auf die Standard-Ausgabe (`stdout`)
- der Text wird **unverändert** an die Ausgabe-Schnittstelle übergeben
- `print()` nutzt eine **textbasierte Ausgabe-Schnittstelle**, die vom Betriebssystem bereitgestellt wird

### Wohin wird ausgegeben?

Die Ausgabe von `print()` geht an die **Standard-Ausgabe** (`stdout`).
Wo diese Ausgabe tatsächlich erscheint, hängt von der Ausführungsumgebung ab:

- **Terminal/Konsole**: Wenn Sie Ihr Programm in einem Terminal starten, erscheint die Ausgabe im Terminal-Fenster
- **Jupyter Notebook**: Wenn Sie Code in einem Jupyter Notebook ausführen, erscheint die Ausgabe unter der Code-Zelle
- **IDE**: In Entwicklungsumgebungen (IDE) erscheint die Ausgabe meist in einem speziellen Ausgabebereich

```{admonition} Hinweis: stdout
:name: tip-stdout
:class: tip

`stdout` (Standard Output) ist ein Konzept aus dem Betriebssystem.
Es bezeichnet den "Standard-Ausgabekanal" eines Programms.
In Python wird `stdout` automatisch mit dem Terminal oder der Notebook-Umgebung verbunden, wenn Sie `print()` verwenden.
```

## Automatische Konvertierung bei `print()`

Eines der wichtigsten Merkmale von `print()` ist die **automatische Konvertierung** aller Datentypen zu Strings.

```python
zahl = 42
print(zahl)  # Die Zahl 42 wird automatisch zu "42" konvertiert

liste = [1, 2, 3]
print(liste)  # Die Liste wird automatisch zu "[1, 2, 3]" konvertiert

woerterbuch = {"name": "Anna", "alter": 25}
print(woerterbuch)  # Das Wörterbuch wird automatisch zu "{'name': 'Anna', 'alter': 25}" konvertiert
```

### Explizite Konvertierung mit `str()`

Wenn Sie eine explizite Konvertierung zu einem String durchführen möchten, können Sie die Funktion `str()` verwenden:

```python
zahl = 42
text = str(zahl)  # Explizite Konvertierung zu String
print(text)       # Ausgabe: 42
print(type(text)) # Ausgabe: <class 'str'>
```

Die Funktion `str()` konvertiert jeden Datentyp zu seiner String-Repräsentation.
Dies ist genau das, was `print()` intern für jeden Wert macht.

## f-Strings (Formatted String Literals)

f-Strings sind eine elegante Möglichkeit, Variablen und Ausdrücke direkt in Strings einzubinden.

### Syntax

Ein f-String beginnt mit `f` oder `F` vor den Anführungszeichen:

```python
name = "Anna"
alter = 25
text = f"Mein Name ist {name} und ich bin {alter} Jahre alt."
print(text)  # Ausgabe: Mein Name ist Anna und ich bin 25 Jahre alt.
```

### Variablen einbinden

Sie können beliebige Variablen in geschweiften Klammern `{}` einbinden:

```python
zahl = 42
print(f"Die Antwort ist {zahl}")  # Ausgabe: Die Antwort ist 42
```

### Ausdrücke in f-Strings

Sie können nicht nur Variablen, sondern auch **Ausdrücke** in f-Strings verwenden:

```python
x = 5
y = 3
print(f"Die Summe von {x} und {y} ist {x + y}")  # Ausgabe: Die Summe von 5 und 3 ist 8
print(f"Das Quadrat von {x} ist {x ** 2}")      # Ausgabe: Das Quadrat von 5 ist 25
```

### Formatierung mit f-Strings

f-Strings unterstützen auch **Formatierungsoptionen**:

```python
# Dezimalstellen bei Fließkommazahlen
pi = 3.14159265359
print(f"Pi auf 2 Dezimalstellen: {pi:.2f}")  # Ausgabe: Pi auf 2 Dezimalstellen: 3.14
print(f"Pi auf 4 Dezimalstellen: {pi:.4f}")  # Ausgabe: Pi auf 4 Dezimalstellen: 3.1416

# Zahlen mit Tausendertrennzeichen
große_zahl = 1234567
print(f"Zahl mit Trennzeichen: {große_zahl:,}")  # Ausgabe: Zahl mit Trennzeichen: 1,234,567

# Prozentangaben
anteil = 0.75
print(f"Anteil als Prozent: {anteil:.1%}")  # Ausgabe: Anteil als Prozent: 75.0%
```

### Datentypkonvertierung in f-Strings

Auch in f-Strings werden alle Werte automatisch zu Strings konvertiert:

```python
zahl = 42
liste = [1, 2, 3]
woerterbuch = {"a": 1, "b": 2}

print(f"Zahl: {zahl}, Liste: {liste}, Wörterbuch: {woerterbuch}")
# Ausgabe: Zahl: 42, Liste: [1, 2, 3], Wörterbuch: {'a': 1, 'b': 2}
```

## Praktische Beispiele

### Beispiel 1: Kombination von Eingabe und Ausgabe

```python
name = input("Wie heißen Sie? ")
alter_text = input("Wie alt sind Sie? ")
alter = int(alter_text)

print(f"Hallo {name}! Sie sind {alter} Jahre alt.")
print(f"In 10 Jahren werden Sie {alter + 10} Jahre alt sein.")
```

### Beispiel 2: Formatierte Tabellenausgabe

```python
produkte = [
    {"name": "Apfel", "preis": 1.50, "anzahl": 10},
    {"name": "Banane", "preis": 2.00, "anzahl": 5},
    {"name": "Orange", "preis": 1.75, "anzahl": 8}
]

print("Produkt\t\tPreis\tAnzahl")
print("-" * 30)
for produkt in produkte:
    print(f"{produkt['name']}\t\t{produkt['preis']:.2f}€\t{produkt['anzahl']}")
```

### Beispiel 3: Fehlermeldungen ausgeben

```python
zahl_text = input("Bitte eine Zahl eingeben: ")
try:
    zahl = int(zahl_text)
    print(f"Die eingegebene Zahl ist: {zahl}")
except ValueError:
    print(f"Fehler: '{zahl_text}' ist keine gültige ganze Zahl!")
```

## Zusammenfassung

- `print()` gibt Text auf die Standard-Ausgabe (`stdout`) aus
- Alle Datentypen werden bei `print()` automatisch zu Strings konvertiert
- f-Strings (`f"..."`) ermöglichen elegante String-Formatierung mit Variablen und Ausdrücken
- f-Strings unterstützen Formatierungsoptionen für Zahlen, Dezimalstellen, etc.
- Die Kombination von Eingabe (`input()`) und Ausgabe (`print()`) mit f-Strings ermöglicht interaktive Programme

