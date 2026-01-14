# Eingaben

Wenn wir in Python Texteingaben über das Command Line Interface (CLI) verarbeiten möchten, verwenden wir die Funktion `input()`.

```python
text = input("Eingabe: ")
```

### Was macht `input()`?

- `input()` liest **Text** von der Standard-Eingabe (`stdin`)
- dieser Text wird **unverändert** an unser Programm übergeben
- der Rückgabewert ist **immer vom Typ `str`**
- `input()` nutzt eine **textbasierte Eingabe-Schnittstelle**, die vom Betriebssystem bereitgestellt wird

---

## Beispiel 1: Zahl einlesen und quadrieren (Typumwandlung)

```python
text = input("Bitte eine Zahl eingeben: ")
zahl = int(text)
print("Quadrat:", zahl ** 2)
```

- `input()` liefert Text
- Typumwandlung kann fehlschlagen (`ValueError`)
- Fehlerbehandlung ist notwendig!!

---

## Beispiel 2: E-Mail-Adresse einlesen (Validierung)

```python
email = input("Bitte E-Mail-Adresse eingeben: ")

if "@" in email:
    print("E-Mail-Adresse sieht gültig aus.")
else:
    print("Ungültige E-Mail-Adresse.")
```

Validierung bedeutet **nicht**, dass eine Eingabe harmlos oder sicher ist.

Beispiel einer formal gültigen, aber potenziell problematischen Adresse:

```
mein-trojanerlegtdeinenpclam@hacking.de
```



```{admonition} Warnung
:name: warning-input-limitations
:class: warning

`input()` ist ein **didaktisches Werkzeug**, kein Praxisstandard. Es kann nur verwendet werden, wenn die Ausführungsumgebung eine Texteingabe-Schnittstelle (STDIN) bereitstellt. Dies ist der Fall:
- wenn Sie oder Ihre Entwicklungsumgebung (IDE) Ihr Programm in einem Terminal starten (Terminal = stdin)
- wenn Sie Ihr Programm in einem Jupyter Notebook ausführen (Notebook web frontend = stdin)

In der Praxis benutzen Endanwender jedoch kein Terminal oder Jupyter Notebook (generell wollen sie von der Programmierung nichts sehen). Vielmehr geben sie ihre Daten in einer grafischen Nutzeroberfläche ein.
```

