(sec-interpreter-expertenwissen)=
# Interpretieren

Dieses Kapitel ist **Expertenwissen** und vertieft das Verständnis, wie Python-Code tatsächlich ausgeführt wird. Es zeigt Schritt für Schritt, wie aus Quellcode letztendlich Maschinencode ("0 und 1") wird.

Wir verwenden durchgehend das folgende einfache Beispiel:

```python
b = 10
a = b + 3
```

## 0. Quelltext (Input)

**Problem:** Nur Zeichen/Text – keine Struktur, keine Bedeutung.

```
"b = 10\na = b + 3"
```

Der Quellcode ist zunächst nur eine Zeichenkette ohne strukturelle Information.

## 1. Lexikalische Analyse (Lexing)

**Problem:** Leerzeichen/Zeilenumbrüche/Kommentare sind Formatierung; der Rechner braucht bedeutungstragende Einheiten.

**Lösung:** Text → Tokenliste.

```
NAME(b) ASSIGN NUMBER(10)
NAME(a) ASSIGN NAME(b) PLUS NUMBER(3)
```

Die lexikalische Analyse zerlegt den Text in einzelne Tokens (Wörter/Symbole), die eine Bedeutung haben.

## 2. Syntaxanalyse (Parsing)

**Problem:** Tokenliste ist flach; Struktur (was gehört zusammen?) fehlt.

**Lösung:** Grammatik anwenden → AST (Abstract Syntax Tree).

```
Module
├── Assign: b = Const(10)
└── Assign
    ├── Name("a")
    └── Add
        ├── Name("b")
        └── Const(3)
```

Der Parser erstellt einen abstrakten Syntaxbaum, der die hierarchische Struktur des Programms darstellt.

## 3. (Leicht) Semantik / Namensauflösung

**Problem:** Namen müssen auf Werte zeigen (b existiert?) und Operatoren müssen zu Typen passen.

**Lösung:** Symboltabelle/Laufzeitumgebung wird vorbereitet (b wird angelegt).

**Symboltabelle nach 'b = 10':**

```
b → int(10)
```

In dieser Phase wird geprüft, ob alle verwendeten Namen definiert sind und ob die Operationen für die beteiligten Typen gültig sind.

## 4. AST → Python-Bytecode

**Warum:** Bytecode ist linear und kann effizient in einer Schleife ausgeführt werden (statt AST-Baum ständig zu traversieren).

**Wichtig:** Bytecode ist kein CPU-Maschinencode.

```python
# stark vereinfacht, sinngemäß
LOAD_CONST 10
STORE_NAME b
LOAD_NAME b
LOAD_CONST 3
BINARY_ADD
STORE_NAME a
```

Der AST wird in eine lineare Folge von Bytecode-Anweisungen umgewandelt, die effizient ausgeführt werden können.

## 5. Ausführung des Bytecodes (Interpreter-Loop)

**Problem:** Bytecode ist nur eine Liste von OpCodes – jemand muss sie abarbeiten.

**Lösung:** Der Python-Interpreter (`python.exe`) läuft als Programm und interpretiert die OpCodes.

**Stack-basierte Ausführung:**

```
Stack: []
LOAD_CONST 10     → Stack [10]
STORE_NAME b      → b=10, Stack []
LOAD_NAME b       → Stack [10]
LOAD_CONST 3      → Stack [10, 3]
BINARY_ADD        → Stack [13]
STORE_NAME a      → a=13, Stack []
```

Der Interpreter verwendet einen Stack (Stapel), um Werte zwischenzuspeichern und Operationen durchzuführen.

## 6. Mapping: OpCode → Interpreter-Funktion (C-Code)

**Problem:** Was bedeutet `BINARY_ADD`? (Welche Operation ist gemeint?)

**Lösung:** Im Interpreter-Code gibt es eine Fallunterscheidung: OpCode `BINARY_ADD` ruft eine Additionsroutine auf.

```c
switch(opcode):
    case BINARY_ADD:
        right = pop()
        left = pop()
        result = PyNumber_Add(left, right)
        push(result)
```

Jeder Bytecode-OpCode wird auf eine entsprechende Funktion im Interpreter (geschrieben in C) gemappt.

## 7. Wo kommen die 0 und 1 her?

**Kernaussage:** Die 0 und 1 gehören zum Interpreter, nicht zu deinem Python-Programm.

**Warum:** `python.exe` wurde vorher (z. B. aus C) kompiliert. Der Maschinenbefehl für „addieren" ist darin enthalten.

**Vereinfachter Ablauf:**

```
C im Interpreter:  long r = left + right;
                   ↓ kompiliert zu CPU-Befehl
Assembler:         ADD rax, rbx
                   ↓ als Bytes / Bits
Bytes (Hex):       48 01 D8
Bits (0/1):        01001000 00000001 11011000
```

## Kernbotschaft (zum Merken)

**Beim Interpretieren wird dein Programm nicht zu Maschinencode.** Stattdessen führt die CPU den Maschinencode des Interpreters aus; dein Programm bestimmt nur, welche Interpreter-Routinen (z. B. Addition) ausgeführt werden.

Der Python-Interpreter selbst ist als kompiliertes Programm vorhanden und enthält bereits alle Maschinenbefehle. Ihr Python-Code wird nicht direkt zu Maschinencode kompiliert, sondern steuert, welche Routinen im Interpreter aufgerufen werden.

```{admonition} Hinweis: Zusammenhang mit dem Sprachverarbeitenden System
:name: hinweis-schritte
:class: tip
Die Schritte 1-4 entsprechen der **Compiler-Funktionalität** in der Abbildung {ref}`fig-sprachverarbeitendes-system` (siehe Kapitel [Interpretation](../04-language-properties/1-interpretation.html)). Die Schritte 5-6 entsprechen den Prozessschritten des **Interpreters**.
``` 