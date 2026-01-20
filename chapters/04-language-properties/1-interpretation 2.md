# Reine Skriptsprache?


Sie kennen sicherlich die Aussage ein Computer kennt nur 0 und 1. Und tatsächlich: ein jedes Computerprogramm ist, wenn es ausgeführt wird, nur eine abfolge von 0 und 1, die auf eine bestimmte Weise verarbeitet werden. Die Abfolge von 0 und 1 wird als Maschinencode bezeichnet.


Üblicherweise geben Programmierer aber keine 0 und 1 in den Computer direkt ein. Warum? Weil er nicht in 0 und 1 denkt, sondern weil ein Mensch üblicherweise anders denkt: wenn bedinung 1 erfüllt ist, dann soll XYZ passieren. Danach soll schritt 2 geschehen. Höhere Programmiersprachen wurden genau zu diesem Zweck entwickelt: sie ermöglichen ein Programm zu entwickeln, das für menschen verständlich ist. Fast alle Programmiersprachen die in der praxis heutzutage anwendung finden sind höhere Programmiersprachen. Python ist eine höhere Programmiersprache. 



Programmiersprachen werden in zwei Arten eingeteilt, die sich dadurch unterscheiden wann und wie die Übersetzung durchgeführt wird.
- kompilierte Sprachen. Klassische Beispiele hierfür sind C, C++
- Skriptsprachen. Python

Warum sollte man den Unterschied kennen? Der Entwicklungsprozess und auch die möglichen Fehlerquellen in der Programmierung hängen davon ab, ob sie in einer kompilierten Sprache oder einer Skriptsprache entwickeln. Unser ziel ist es in Python zu programmieren: Sie sollten daher verstehen wie aus Ihrem Programm 0 und 1 werden, die vom Rechner ausgeführt werden können. 

Ob ein Programm in einer kompilierten Sprache erstellt wurde, erkennen Sie daran, dass Sie eine ausführbare Datei vor sich haben, die Sie direkt starten können:
```
meine-anwendung.exe
```

Haben Sie ein Programm vor sich liegen, das in einer Skriptsprache entwickelt wurde, dann starten Sie das Programm anders:
```
python3 meine-anwendung.py
```

Der fundamentale Unterschied zwischen den beiden ist, wo der Maschinencode zu finden ist. Im ersten Fall befindet sich der Maschinencode in `meine-anwendung.exe`; im zweiten Fall ist er  in `python3` enthalten. `meine-anwendung.py` liegt weiterhin als Quelltext vor.

**Wichtig zu verstehen:** Bei einer kompilierten Sprache wie C oder C++ enthält die `.exe`-Datei bereits den nativen Maschinencode (0 und 1), der speziell für Ihr Betriebssystem und Ihre Prozessorarchitektur kompiliert wurde. Das Betriebssystem erkennt die `.exe`-Datei an ihrem Dateiformat (z.B. PE-Format bei Windows) und kann sie direkt ausführen - es muss nicht "wissen", in welcher Sprache das Programm ursprünglich geschrieben wurde, da es bereits zu Maschinencode übersetzt wurde. Eine ausführbare Datei kann nur auf dem Betriebssystem und der Prozessorarchitektur ausgeführt werden, für die sie kompiliert wurde (z.B. Windows x64, Linux ARM, etc.).


```{figure} ../../figs/overview/interpretationcompilation.png
---
width: 600px
name: fig-interpretationcompilation
---
Vergleich zwischen Kompilierung und Interpretation
```


## Übersetzung und Interpretation

Die große Frage die bleibt ist allerdings: wenn der Computer am Ende nur 0 und 1 ausführen kann, wie wird aus dem Quelltext, den wir in einer höheren Programmiersprache geschrieben haben, am Ende eine Abfolge von 0 und 1, die der Rechner versteht? Grundsätzlich brauchen wir eine Übersetzung zwischen dem Quelltext und dem Maschinencode (Abfolge von 0 und 1). 

Dieses grundlegende Konzept ist bei allen Programmiersprachen gleich {cite}`sommerville`: Der Quellcode muss in eine Form übersetzt werden, die der Computer verstehen und ausführen kann. Der Unterschied zwischen verschiedenen Programmiersprachen liegt lediglich darin, **wann** und **wie** diese Übersetzung stattfindet - nicht **ob** sie stattfindet.

Das folgende Bild zeigt das allgemeine Konzept eines sprachverarbeitenden Systems: Der Quellcode wird von einem **Übersetzer** (Compiler oder Interpreter) in eine ausführbare Form umgewandelt. Diese ausführbare Form kann entweder direkt Maschinencode sein (bei kompilierten Sprachen) oder eine Zwischenform wie Bytecode (bei manchen interpretierten Sprachen). Ein **Ausführungsmodul** (Interpreter oder Prozessor) führt dann diese Anweisungen aus und produziert das Ergebnis.

Der entscheidende Unterschied zwischen kompilierten und interpretierten Sprachen liegt darin:
- **Kompilierte Sprachen**: Der Übersetzer erstellt direkt Maschinencode, der vom Prozessor (Hardware) ausgeführt wird.
- **Interpretierte Sprachen**: Der Übersetzer erstellt eine Zwischenform, die von einem Interpreter (Software) zur Laufzeit ausgeführt wird.


```{figure} ../../figs/overview/sprachverarbeitendes-system.png
---
width: 600px
name: fig-sprachverarbeitendes-system
---
Sprachverarbeitendes System für eine Programmiersprache
```

## Was ist nun Python?
"Python wird interpretiert" - diese Aussage werden Sie in der Praxis häufig finden. Genau genommen: Wie wir aber schon gesehen haben, wird bei jeder Sprache sowohl kompiliert als auch interpretiert. Diese Aufgaben werden vom sogenannten **Python-Interpreter** durchgeführt.

Der Python-Interpreter (z.B. CPython) übernimmt mehrere Funktionalitäten, für die jeweils verschiedene Komponenten verantwortlich sind. Die **Compiler-Funktionalität** des Interpreters übersetzt den Quellcode zunächst in Bytecode (eine Zwischenform). Ein Compiler, der für Python 3.2 gebaut wurde, wird Ihnen einen anderen Bytecode geben als ein Compiler, der für Python 3.12 gedacht ist. Die **Python Virtual Machine (PVM)** - eine weitere Komponente des Interpreters - wandelt den Bytecode in Maschinencode um, der mit Ihrem Betriebssystem kompatibel ist, und führt ihn aus. 




```{figure} ../../figs/overview/python-einfach.png
---
width: 600px
name: fig-python-einfach
---
Python-Interpreter: Kompilierung und Interpretation
```

Ein detailliertes Beispiel, welche Schritte beim Kompilieren und Interpretieren von Python-Code durchlaufen werden, finden Sie im {ref}`Expertenwissen-Kapitel zur Interpretation <sec-interpreter-expertenwissen>`. Zum Vergleich können Sie auch die Schritte bei einer kompilierten Sprache im {ref}`Expertenwissen-Kapitel zur Kompilierung <sec-compilation-expertenwissen>` nachlesen.



```{admonition} Hinweis
:name: kompilierung-interpretation
:class: remark
In der Praxis wird meist davon gesprochen, dass entweder kompiliert oder interpretiert wird - das hat sich so eingebürgert. Was damit eigentlich gemeint ist: Es findet immer eine Kompilierung und Interpretation statt! Der Unterschied liegt im **wo** und **wann**. 

Wenn wir von **kompilierten Sprachen** sprechen, meinen wir, dass die CPU den Maschinencode direkt ausführt (interpretiert). Wenn wir von **Skriptsprachen** sprechen, meinen wir damit, dass eine virtuelle Maschine eine plattformunabhängige Form von Code in Maschinencode umwandelt und ausführt.
```


```{admonition} Hinweis
:name: interpreter-pvm
:class: remark
In der Praxis werden die Begriffe "Python Interpreter" und "Python Virtual Machine" oft synonym verwendet. Technisch gesehen ist die PVM jedoch nur ein Teil des Interpreters - nämlich die Komponente, die den Bytecode ausführt. Der Interpreter als Ganzes umfasst sowohl die Kompilierung (Quellcode → Bytecode) als auch die Interpretation (Bytecode → Ausführung).
```


**Vorteile dieser Hybridform:**
- Portabilität: Der Bytecode kann auf verschiedenen Plattformen ausgeführt werden
- Schnellere Ausführung als reine Interpretation (Bytecode ist optimiert)
- Flexibilität: Code kann zur Laufzeit geändert werden

```{admonition} Hinweis
:name: python-performance
:class: remark
Manchmal wird die Sprache Python als langsame Sprache bezeichnet.
Präzise ausgedrückt müsste man jedoch sagen, dass:
>Die Python-Implementierungen (Interpreter/Übersetzer) üblicherweise zu einer langsamen Ausführung von Python-Programmen führen.

Oftmals gibt es verschiedene Interpreter oder Übersetzer für ein und dieselbe Sprache.
Wie effizient ein Programm läuft, hängt von der konkreten Maschine und den Maschinenbefehlen ab, in die das Programm übersetzt oder interpretiert wird.
Verwenden wir zwei unterschiedliche Übersetzer für den gleichen Code und lassen den übersetzten Code auf der gleichen Maschine laufen, kann die Laufzeit sehr unterschiedlich sein. Der Standardinterpreter von Python ist in C geschrieben (CPython).
```