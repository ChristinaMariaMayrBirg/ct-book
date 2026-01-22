# Performance

```{admonition} Behauptung
:class: remark
„Python ist langsam.“
```

Diese Aussage taucht in der Praxis häufig auf – und führt schnell zu Missverständnissen. Denn: Ob „Python langsam“ ist, hängt davon ab, **was** Ihr Programm macht und **wie** der Python-Code ausgeführt wird.

Reiner Python-Code (z.B. Schleifen, viele kleine Funktionsaufrufe, dynamische Typprüfungen) ist oft langsamer als nativer Maschinencode aus einer kompilierten Sprache wie C/C++. Gleichzeitig laufen viele „Python‑Programme“ schnell, weil sie intern hochoptimierte Bibliotheken nutzen, die wiederum in C/C++ (oder ähnlichen Sprachen) implementiert sind.

**Was steckt dahinter?**

Ein Computer führt am Ende Maschinencode aus (0 und 1). Quellcode in einer höheren Programmiersprache muss daher in eine ausführbare Form übersetzt werden. Dieses Grundprinzip ist bei allen Sprachen gleich {cite}`sommerville`. Der Unterschied liegt darin, wann und wo diese Übersetzung passiert – nicht darin, ob sie passiert.

Kompiliert vs. „Skript“: Wo liegt der Maschinencode?

Wenn ein Programm in einer kompilierten Sprache erstellt wurde, erhalten Sie typischerweise eine ausführbare Datei:

```
meine-anwendung.exe
```

Bei einer „Skriptsprache“ starten Sie Quelltext üblicherweise über ein Ausführungsprogramm:

```
python3 meine-anwendung.py
```

Der wichtige Unterschied ist dabei: 
- Bei kompilierten Programmen liegt der Maschinencode in der erzeugten Binärdatei**
- bei Skript-/Interpreter-Setups steckt ein großer Teil der Ausführung in `python3` (dem Interpreter), während Ihr `.py`-File als Quelltext bestehen bleibt.


```{figure} ../../figs/04-language-properties/overview/interpretationcompilation.png
---
width: 600px
name: fig-interpretationcompilation
---
Vergleich zwischen Kompilierung und Interpretation
```

**Was passiert bei Python konkret?**

Die Aussage „Python wird interpretiert“ ist als Vereinfachung weit verbreitet – technisch ist es besser, Python als **Hybrid** zu verstehen:

- Der **Python-Interpreter** (z.B. CPython) enthält eine Compiler-Komponente, die Quelltext in **Bytecode** übersetzt (Zwischenform).
- Eine Ausführungs-Komponente (oft als **Python Virtual Machine / PVM** beschrieben) führt diesen Bytecode aus.

```{figure} ../../figs/04-language-properties/overview/python-einfach.png
---
width: 600px
name: fig-python-einfach
---
Python-Interpreter: Kompilierung und Interpretation
```

Ein detailliertes Schritt-für-Schritt-Beispiel finden Sie im {ref}`Expertenwissen-Kapitel zur Interpretation <sec-interpreter-expertenwissen>` (und als Vergleich im {ref}`Expertenwissen-Kapitel zur Kompilierung <sec-compilation-expertenwissen>`).

```{admonition} Merke
:name: kompilierung-interpretation
:class: remark
In der Praxis heißt es oft „entweder kompiliert oder interpretiert“. Streng genommen findet bei Programmiersprachen immer eine Form von Übersetzung **und** Ausführung statt. Der Unterschied liegt im **wo** und **wann**.
```

```{admonition} Merke
:name: interpreter-pvm
:class: remark
„Python-Interpreter“ und „Python Virtual Machine“ werden oft synonym verwendet. Technisch ist die PVM jedoch nur der Teil, der den Bytecode ausführt; der Interpreter umfasst zusätzlich das Übersetzen (Quelltext → Bytecode).
```


```{admonition} Klarstellung
:class: note
„Python ist langsam“ ist weder komplett richtig noch komplett falsch.

- Wenn ein Programm vor allem rechnet (z.B. viele Schleifen, viele kleine Operationen in reinem Python), ist es im Vergleich zu nativ kompiliertem Code (z.B. C/C++) oft langsamer.
- Wenn ein Programm vor allem wartet (z.B. Datei lesen/schreiben, Netzwerk), ist es häufig nicht durch Python selbst limitiert.
- Viele Python‑Workflows sind schnell, weil sie Bibliotheken verwenden, die intern hochoptimiert sind.
- „Python‑Performance“ hängt auch von der Implementierung ab: Verschiedene Interpreter/Übersetzer können denselben Code unterschiedlich schnell ausführen (Standard: CPython, in C implementiert).
```

```{admonition} Exkurs: Performance messen (Profiling)
:class: tip
„Performance“ kann sich auf verschiedene Dinge beziehen – z.B. **Laufzeit**, **Speicherverbrauch (RAM)** oder **I/O-Verhalten** (Warten auf Dateien/Netzwerk). Welche Kennzahl relevant ist, hängt vom Programm ab.

**Einfache Zeitmessung in Python**

```python
import time

start = time.perf_counter()   # alternativ: time.time()
# ... Code, den Sie messen wollen ...
dauer = time.perf_counter() - start
print(f"{dauer:.3f}s")
```

**Profiling**
Profiling ist mehr als eine einzelne Zeitmessung: Es hilft Ihnen zu verstehen, **welche Funktionen** wie viel Zeit (oder Speicher) verbrauchen – also **wo** der Engpass wirklich liegt. 

- **CPU-Profiling (Standardbibliothek)**: `cProfile` (+ Auswertung mit `pstats`)
- **Visualisierung**: z.B. `snakeviz` (zeigt `cProfile`-Ausgaben grafisch)
- **Sampling-Profiler (geringer Overhead)**: z.B. `py-spy` (läuft auch an laufenden Prozessen)
- **Line-by-line**: z.B. `line_profiler` (sehr konkret, aber mehr Overhead)
- **Speicher/Allokationen**: `tracemalloc` (Standardbibliothek), optional `memory_profiler`

Tipp: Messen Sie mit **realistischen Eingaben** und achten Sie darauf, ob Ihr Programm eher **CPU-bound** (Rechnung) oder **I/O-bound** (Warten) ist.
```