# Datei / Skripte (Details)

(sec-python-scripts)=

Im vorherigen Abschnitt haben wir eine python-Datei erzeugt und ausgeführt.
Wir haben also "ein Programm" ausgeführt. Im Kapitel chapters/03-computer-sciences-basics/2-programming.md haben wir bereits gelernt, dass software meistens mehrere programme enthalten und auch wir werden im Laufe der vorlesung und des praktikums mehrere programme schreiben, die unterschiedliche dinge tun. 

## Wo und wie legen wir Python-Dateien ab? 

Python-Projekte (klein wie groß) trennen typischerweise drei Dinge:

- **Entrypoint (Startpunkt)**: *Wie* wird ein Programm gestartet? (z. B. `python ...`, ein CLI-Kommando, ein GUI-Button)
- **Geschäftslogik / Workflow**: *Welche Schritte passieren in welcher Reihenfolge?* (A → B → C)
- **Bausteine (Funktionen/Module)**: wiederverwendbare Teile, die die Geschäftslogik aufruft

In großen Softwareprojekten werden diese Dinge oft auf **Unterordner und Dateien** verteilt. In dieser Vorlesung halten wir die Struktur bewusst klein – aber die Problemstellung bleibt dieselbe: Wir müssen festlegen, **wo der Startpunkt ist**, **wo der Ablauf steht** und **wo Bausteine liegen**, damit wir sie später wiederverwenden können.

```text
my_app/
├─ README.md                   # Einstieg: Was ist das Projekt? Wie nutze ich es?
├─ bin/                        # Entrypoints (Startskripte)
│  ├─ run_design_gui.py        # startet Programm A (interaktiv, ggf. GUI)
│  └─ run_optimize.py          # startet Programm B (Batch/Optimierung, ohne GUI)
├─ src/
│  └─ my_app/                  # Python-Paket (wiederverwendbarer Quellcode)
│     ├─ __init__.py
│     ├─ shared_logic/
│     │  └─ simulator.py       # gemeinsamer Kern: Simulation/Berechnung
│     └─ programs/
│        ├─ design.py          # Geschäftslogik A: „Auslegung/Interaktion“
│        └─ optimize.py        # Geschäftslogik B: „Optimierung/Batch“
├─ configs/
│  └─ default.yaml             # Konfiguration (z. B. Parameterprofile)
├─ data/
│  └─ input.csv                # Beispieldaten
└─ results/
   └─ output.csv               # Ergebnisdaten (z. B. vom Batch-Lauf erzeugt)
```

- **`bin/`**: enthält *Entrypoints* (oft kleine Startskripte)
- **`src/my_app/`**: enthält *Bausteine* und ggf. mehrere *Workflows/Programme*
- **`configs/`**, **`data/`**, **`results/`**: trennen Konfiguration, Input und Output

## Was wir im Kurs machen (vereinfacht: eine Datei)

Damit Sie sich auf Programmierkonzepte konzentrieren können, arbeiten wir häufig mit **einer Python-Datei**.
Auch in einer Datei können (und sollten) Sie gedanklich trennen:

- **Entrypoint**: *wo startet der Ablauf?*
- **Workflow/Geschäftslogik**: A → B → C
- **Bausteine**: z. B. kleine Hilfsfunktionen

Wichtig: Wenn Sie eine Datei direkt ausführen (`python mein_script.py`), arbeitet Python sie **von oben nach unten** ab.

Der *Entrypoint* ist dabei **nicht** „die erste Zeile“, sondern der **Programmstart** (der Aufruf in der Konsole: `python mein_script.py`).

### Einfaches Skript 

Im folgenden Beispiel wird..  Die Pythonbefehle werden in der datei main_script.py abgespeichert. Wir können das skript ausführen über `python mein_script.py` (entweder in der console oder über einen button in der IDE, der den consolenaufruf für Sie übernimmt)

```python
# Datei: mein_script.py
# Entrypoint: Start mit: python mein_script.py

print("Programm startet")

# Workflow/Geschäftslogik (A → B → C) als einfacher Ablauf:
x = 10
y = x * 2

x2 = 11
y2 = x2 * 2

x3 = 14
y3 = x3 * 2

ergebnis = y + y2 + y3
print("Ergebnis:", ergebnis)
```
Sie sehen, dass im Skript die Logik „mal zwei nehmen“  mehrfach kopiert ist.

### Beispiel 2: Skript mit Funktion (Baustein)

Wir wollen den Code nicht kopieren, weil ...
Deshalb lagern wir ihn in eine funktion aus.


```python
# Datei: mein_script.py
# Entrypoint: Start mit: python mein_script.py

def mal_zwei(zahl: int) -> int:
    """Baustein: wiederverwendbare Funktion."""
    return zahl * 2

print("Programm startet")

# Workflow/Geschäftslogik:
y = mal_zwei(10)
y2 = mal_zwei(11)
y3 = mal_zwei(14)

ergebnis = y + y2 + y3
print("Ergebnis:", ergebnis)
```

Die Funktion ein **Baustein** und der restliche Code ist der **Workflow**.


## Empfohlene Datei-Struktur



Sobald Sie Bausteine aus einer Datei in einer anderen Datei wiederbenutzen möchten, verwenden Sie in Python typischerweise einen **Import**.
Ein *Import* bedeutet: Code aus einer anderen Datei (z. B. eine Funktion) wird in der aktuellen Datei verfügbar gemacht.
Wichtig dabei: Beim Import wird die andere Datei einmal **geladen** – und dabei wird ihr **Top-Level-Code** ausgeführt.

Damit beim Importieren nicht automatisch der ganze Workflow startet, nutzen wir einen Guard:

 `if __name__ == "__main__":` 

Wie sieht das in einem Skript aus?

```python
# Datei: skript1.py

def mal_zwei(zahl: int) -> int:
    return zahl * 2

def main() -> None:
    # Workflow/Geschäftslogik:
    ergebnis = mal_zwei(10) + mal_zwei(11) + mal_zwei(14)
    print("Ergebnis:", ergebnis)

if __name__ == "__main__":  # Entrypoint für dieses Skript
    main()

```

Wenn wir `skript1.py` direkt aufrufen (Entrypoint = `skript1.py`), wird `main()` ausgeführt und das Ergebnis ausgegeben.

Ein anderes Skript (`skript2.py`) kann den Baustein importieren, ohne die Geschäftslogik auszulösen:

```python
# Datei: skript2.py
from skript1 import mal_zwei

print(mal_zwei(7))
```
Warum? Wir rufen `skript2.py` auf (Entrypoint = `skript2.py`). Dabei wird `skript1.py` importiert, aber `main()` in `skript1.py` wird **nicht** ausgeführt, weil der Guard `if __name__ == "__main__":` nur beim direkten Start von `skript1.py` greift.

## Merksatz fürs Praktikum (empfohlenes Muster)

- Schreiben Sie Bausteine als **Funktionen** (und später ggf. als Module).
- Schreiben Sie den Ablauf unter if __name__ == "__main__":

```python

## hier bausteine

# ------- ###
if __name__ == "__main__":
    # Geschäftslogik:
    # Schritt 1
    # Schritt 2
    #Schritt 3
```


