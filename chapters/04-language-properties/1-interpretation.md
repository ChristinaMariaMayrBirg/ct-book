# Reine Skriptsprache?


Sie kennen sicherlich die Aussage ein Computer kennt nur 0 und 1. Und tatsächlich: ein jedes Computerprogramm ist, wenn es ausgeführt wird, nur eine abfolge von 0 und 1, die auf eine bestimmte Weise verarbeitet werden. Die Abfolge von 0 und 1 wird als Maschinencode bezeichnet.


Üblicherweise geben Programmierer aber keine 0 und 1 in den Computer direkt ein. Warum? Weil er nicht in 0 und 1 denkt, sondern weil ein Mensch üblicherweise anders denkt: wenn bedinung 1 erfüllt ist, dann soll XYZ passieren. Danach soll schritt 2 geschehen. Höhere Programmiersprachen wurden genau zu diesem Zweck entwickelt: sie ermöglichen ein Programm zu entwickeln, das für menschen verständlich ist. Fast alle Programmiersprachen die in der praxis heutzutage anwendung finden sind höhere Programmiersprachen. Python ist eine höhere Programmiersprache.

Die große Frage die bleibt ist allerdings: wenn der Computer am Ende nur 0 und 1 ausführen kann. Wie wird aus aus dem Quelltext, den wir in einer höheren Programmiersprache geschrieben haben, am Ende eine Abfolge von 0 und 1, die der Rechner versteht? Grundsätzlich brauchen wir eine Übersetzung zwischen dem Quelltext und dem Maschinencode (Abfolge von 0 und 1). 

Programmiersprachen werden in zwei Arten eingeteilt, die sich dadurch unterscheiden wann und wie die Übersetzung durchgeführt wird.
- kompilierte Sprachen. Klassische Beispiele hierfür sind C, C++
- Skriptsprachen. Python

Ob ein Programm in einer kompilierten Sprache erstellt wurde, erkennen Sie daran, dass Sie eine ausführbare Datei vor sich haben, die Sie direkt starten können:
```
meine-anwendung.exe
```

Haben Sie ein Programm vor sich liegen, das in einer Skriptsprache entwickelt wurde, dann starten Sie das Programm anders:
```
python3 meine-anwendung.py
```

Der fundamentale Unterschied zwischen den beiden ist, wo der Maschinencode zu finden ist. Im ersten Fall befindet sich der Maschinencode in `meine-anwendung.exe`; im zweiten Fall ist er im Python-Interpreter (`python3`) enthalten. `meine-anwendung.py` liegt weiterhin als Quelltext vor.

**Wichtig zu verstehen:** Bei einer nativ kompilierten Sprache wie C oder C++ enthält die `.exe`-Datei bereits den nativen Maschinencode (0 und 1), der speziell für Ihr Betriebssystem und Ihre Prozessorarchitektur kompiliert wurde. Das Betriebssystem erkennt die `.exe`-Datei an ihrem Dateiformat (z.B. PE-Format bei Windows) und kann sie direkt ausführen - es muss nicht "wissen", in welcher Sprache das Programm ursprünglich geschrieben wurde, da es bereits zu Maschinencode übersetzt wurde. Eine ausführbare Datei kann nur auf dem Betriebssystem und der Prozessorarchitektur ausgeführt werden, für die sie kompiliert wurde (z.B. Windows x64, Linux ARM, etc.).


```{figure} ../../figs/overview/interpretationcompilation.png
---
width: 600px
name: fig-interpretationcompilation
---
Vergleich zwischen Kompilierung und Interpretation
```


Warum sollte man den Unterschied kennen: Der Entwicklungsprozess und auch die möglichen Fehlerquellen in der Programmierung hängen davon ab, ob sie in einer kompilierten Sprache oder einer Skriptsprache entwickeln. Unser ziel ist es in Python zu programmieren: Sie sollten daher verstehen wie aus Ihrem Programm 0 und 1 werden, die vom Rechner ausgeführt werden können. 

## Übersetzung


Sowohl bei Skriptsprachen als auch komipilierten Sprachen muss an irgeneiner Stelle irgendwann eine Übersetzung stattfinden: ein Übersetzer (ein Compiler) übersetzt Quelltext in Maschinencode! Der unterschied ist wann das ganze passiert.

## Was ist nun Python??

## Was ist nun Python?

Python ist eine **hybride Sprache**: Sie wird sowohl kompiliert als auch interpretiert. Der Python-Interpreter (z.B. CPython) kompiliert den Quellcode zunächst in Bytecode (eine Zwischenform), der dann von der Python Virtual Machine (PVM) interpretiert wird.

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