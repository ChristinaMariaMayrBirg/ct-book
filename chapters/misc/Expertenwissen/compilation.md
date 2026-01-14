(sec-compilation-expertenwissen)=
# Kompilieren

Dieses Kapitel ist **Expertenwissen** und vertieft das Verständnis, wie kompilierte Sprachen (z.B. C, C++) von Quellcode zu ausführbarem Maschinencode werden. Es zeigt Schritt für Schritt, wie aus Quellcode letztendlich Maschinencode ("0 und 1") wird.

Wir verwenden durchgehend das folgende einfache Beispiel:

```c
a = b + 3;
```

## 1. Lexikalische Analyse (Lexing)

**Problem:** Der Quellcode ist eine Zeichenkette. Leerzeichen und Zeilenumbrüche tragen keine Rechenbedeutung.

```
a = b + 3
```

**Lösung:** Entfernen der Formatierung, Zerlegung in Tokens.

```
IDENT("a")
ASSIGN("=")
IDENT("b")
PLUS("+")
NUMBER("3")
```

Die lexikalische Analyse zerlegt den Text in einzelne Tokens (Wörter/Symbole), die eine Bedeutung haben.

## 2. Syntaxanalyse (Parsing)

**Problem:** Tokens sind flach – Struktur (was gehört zusammen?) fehlt.

```
IDENT(a) = IDENT(b) + NUMBER(3)
```

**Lösung:** Anwendung der Grammatik, Aufbau eines Syntaxbaums (AST).

```
Assign
├── Name("a")
└── Add
    ├── Name("b")
    └── Const(3)
```

Der Parser erstellt einen abstrakten Syntaxbaum, der die hierarchische Struktur des Programms darstellt.

## 3. Semantische Analyse

**Problem:** Der AST sagt noch nichts über Bedeutung (Typen, Existenz).

**Symboltabelle:**

```
b : int
```

**Lösung:** Typprüfung und Annotation des AST.

```
Assign : int
├── Name("a") : int
└── Add : int
    ├── Name("b") : int
    └── Const(3) : int
```

In dieser Phase wird geprüft, ob alle verwendeten Namen definiert sind, ob die Typen zusammenpassen und ob die Operationen gültig sind.

## 4. Zwischenrepräsentation (IR)

**Problem:** Der AST ist baumförmig und schlecht für Optimierung.

**Lösung:** Lineare, maschinennahe Darstellung.

```
t1 = load b
t2 = const 3
t3 = add t1, t2
store t3 -> a
```

Der AST wird in eine lineare Zwischenrepräsentation (IR) umgewandelt, die besser für Optimierungen geeignet ist.

## 5. Codegenerierung

**Problem:** IR kennt keine echten CPU-Instruktionen.

**Lösung:** Abbildung auf konkrete Architektur (x86-64).

```assembly
mov rax, [b]
add rax, 3
mov [a], rax
```

Die IR wird in Assembler-Code für eine spezifische Prozessorarchitektur übersetzt.

## 6. Assemblierung

**Problem:** Assembler ist für Menschen lesbar, nicht für Hardware.

**Lösung:** Übersetzung in Maschinenbytes.

```
48 8B 05 ?? ?? ?? ??
48 83 C0 03
48 89 05 ?? ?? ?? ??
```

Der Assembler-Code wird in Maschinenbytes (Hexadezimal) übersetzt. Die `??` stellen Platzhalter für Adressen dar, die zur Laufzeit aufgelöst werden.

**Kernbotschaft:**

Dasselbe Programm wird Schritt für Schritt umgeformt. Erst ganz am Ende bleiben rohe 0 und 1, die die CPU ausführt.

## 7. Ausführung (Runtime)

**Problem:** Maschinencode liegt als Datei auf der Festplatte. Die CPU kann nur Code aus dem Speicher ausführen.

**Lösung:** Das Betriebssystem startet das Programm und lädt den Code in den Speicher.

### Schritt 7.1 – Laden: Programmdatei → RAM

Der Maschinencode wird von der Festplatte in den Arbeitsspeicher (RAM) geladen. Code- und Datensegmente werden getrennt geladen.

### Schritt 7.2 – Start: CPU beginnt am Einstiegspunkt

Die CPU beginnt am Einstiegspunkt (Entry Point) mit der Abarbeitung des Programms.

### Schritt 7.3 – CPU-Ausführung

Die CPU führt die Maschinenbefehle Instruktion für Instruktion aus:

1. `mov rax, [b]` → Wert von `b` wird in Register geladen
2. `add rax, 3` → CPU addiert 3 (ALU - Arithmetic Logic Unit)
3. `mov [a], rax` → Ergebnis wird im Speicher abgelegt

**Ergebnis der Ausführung:**

Der Ausdruck `b + 3` wurde physisch von der CPU berechnet. `a` enthält nun das Ergebnis.

## Kernbotschaft

**Kompilieren erzeugt Maschinencode.** Ausführen bedeutet, dass das Betriebssystem diesen Code in den Speicher lädt und die CPU ihn Instruktion für Instruktion abarbeitet.

Im Gegensatz zu interpretierten Sprachen wird bei kompilierten Sprachen der gesamte Code vor der Ausführung in Maschinencode übersetzt. Dieser Maschinencode ist spezifisch für die Zielplattform (Betriebssystem und Prozessorarchitektur) und kann direkt von der CPU ausgeführt werden.
