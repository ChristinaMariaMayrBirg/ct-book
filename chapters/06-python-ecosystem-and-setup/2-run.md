# Python ausführen

Es gibt verschiedene Möglichkeiten, Python-Code auszuführen. Die drei wichtigsten sind:

- **REPL (Read–Eval–Print Loop, „Lese–Auswerte–Ausgabe–Schleife“)**: einzelne Befehle interaktiv ausprobieren (z. B. `python` oder `ipython`)
- **Skript/Datei**: ein Programm aus einer `.py`-Datei starten (z. B. `python mein_script.py`)
- **Notebook**: Code in Zellen ausführen und dokumentieren (z. B. `jupyter lab`)

Im Praktikum nutzen wir vor allem **Skripte/Dateien** und (für erste Experimente) eine **REPL**.
Notebooks verwenden wir im Kurs hauptsächlich zum Ausprobieren von Beispielen auf der interaktiven Website.


## REPL

### Python

Öffnen Sie Ihre Konsole und rufen

```sh
python
```

auf.
Jetzt können Sie den ``Python``-Code direkt eintippen.
Es wird (in der Regel) das Ergebnis des letzten Ausdrucks ausgegeben.
Zum Beispiel können wir

```python
x = 3 + 6
x + 6
```

rechnen.
Wir können auch Mehrzeilige Befehle abfeuern.
Lassen Sie uns z.B. eine Funktion ``add(x, y)`` definieren:

```python
def add(x, y):
    return x + y

add(9, 5)
```

```{figure} ../../figs/06-python-ecosystem-and-setup/python-tutorial/environment/repl.png
---
width: 800px
name: fig-repl
---
Ausgabe die auf der Konsole durch die oben angegeben Befehle erzeugt wird.
```

Mit ``quit()`` oder ``ctrl + D`` bzw. ``Strg + D`` beenden Sie den Kommandozeileninterpreter.

### IPython

Mit dem Befehl ``ipython`` starten Sie einen anderen Kommandozeileninterpreter zum interaktiven Arbeiten.
Im Unterschied zu ``python`` (Standard-Interpreter) bietet IPython viele Komfortfunktionen für die REPL, z. B. bessere Fehlermeldungen, Autovervollständigung, Command-History, magische Befehle (z. B. ``%time``) und ein angenehmeres interaktives Arbeiten.

```sh
ipython
```

Wir können den selben Code ausführen:

```{figure} ../../figs/06-python-ecosystem-and-setup/python-tutorial/environment/ipython.png
---
width: 800px
name: fig-ipython
---
Ausgabe die auf der Konsole durch die oben angegeben Befehle erzeugt wird.
```


## Jupyter Notebook

Wenn Sie mit diesem interaktiven Lehrbuch in der Web-Version arbeiten, dann nutzen Sie bereits Jupyter Notebooks:
Wenn Sie auf „Live Code“ oder „Jupyter“ klicken, wird im Hintergrund ein Notebook gestartet (nicht auf Ihrem Rechner, sondern auf einem Server). Sie sehen die Ergebnisse über Ihren Browser.

Sie können Jupyter Notebooks auch lokal ausführen. Notebook-Dateien erkennen Sie typischerweise an der Endung `.ipynb`.

Sie starten ein Notebook lokal in der Konsole mit:

```sh
jupyter lab [path/to/notebook/file]
```
Im Rahmen dieser Vorlesung werden Sie Jupyter Notebooks vor allem nutzen, um Code-Beispiele aus der Vorlesung auf der interaktiven Website selbst auszuprobieren.

Falls Sie dennoch mehr über Jupyter Notebooks erfahren möchten, finden Sie dazu Informationen im Expertenwissen: [Jupyter Notebooks](sec-jupyter-notebooks).


## Script / Datei

Die wohl gängigste Technik, Python-Anwendungen zu entwickeln, ist es, Code in **Dateien** (z. B. `mein_script.py`) abzulegen und diese dann vom Python-Interpreter ausführen zu lassen.



Wir öffnen unseren Texteditor unserer Wahl und tippen folgenden Code ein:

```python
import sys

n = int(sys.argv[1])
square_sum = 0

for i in range(n):
    square_sum += (i+1)**2

print(square_sum)
```
Wir speichern die Datei unter dem Namen ``square_sum.py`` im aktuellen Verzeichnis ab.
Was passiert? Das Skript

- berechnet die Summe der Quadratzahlen von 1 bis ``n``, wobei ``n`` das **erste Argument** des Programmaufrufs ist und
- nutzt `sys.argv` (Argumente aus der Kommandozeile).

Das 0. Argument ist immer der Name der Datei in der das ``Python``-Script steht.
Nun führen wir die Datei aus:

```sh
python square_sum.py 100
```
und erhalten als Ausgabe die Summe aller Quadratzahlen von 1 bis einschließlich 100. 

Wie man Skripte sinnvoll strukturiert (Entrypoint/Workflow/Bausteine, Guard, Import) besprechen wir im nächsten Abschnitt: [Python-Skripte](sec-python-scripts).
