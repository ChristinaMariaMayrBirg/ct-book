# Zahlensysteme

```{admonition} Hausaufgabe
:class: note

Dieses Kapitel ist als **Hausaufgabe** gedacht. Sie sollten sich die Inhalte selbstständig erarbeiten und die Umrechnungen zwischen den verschiedenen Zahlensystemen üben. Die hier dargestellten Algorithmen und Tabellen helfen Ihnen dabei, die Umrechnungen zu verstehen und durchzuführen.
```

Im vorherigen Kapitel haben wir gesehen, dass es möglich ist, Zahlen unterschiedlich darzustellen.

- **13** im Dezimalsystem (Basis 10, Alltagsschreibweise) - das verwenden wir im Alltag, wenn wir von der Zahl 13 sprechen
- **1101** im Binärsystem (Basis 2)
- **D** im Hexadezimalsystem (Basis 16)

Alle drei Zahlensysteme sind **Stellenwertsysteme**. Das bedeutet, dass der Wert einer Ziffer von ihrer Position abhängt.

- **Dezimal (Basis 10)**: Jede Stelle kann Werte von 0-9 annehmen. Die Stellenwerte sind: ..., 10³, 10², 10¹, 10⁰
- **Binär (Basis 2)**: Jede Stelle kann Werte von 0-1 annehmen. Die Stellenwerte sind: ..., 2³, 2², 2¹, 2⁰
- **Hexadezimal (Basis 16)**: Jede Stelle kann Werte von 0-9 und A-F annehmen. Die Stellenwerte sind: ..., 16³, 16², 16¹, 16⁰

Sie sollten in der Lage sein, eine Zahl aus einem dieser drei Zahlensysteme in ein anderes überführen zu können.
Dafür gibt es zwei Wege:
- Sie lernen den Algorithmus, also wie umgerechnet wird
- Sie lernen die Ergebnisse des Algorithmus für bestimmte Zahlen auswendig. Diese Ergebnisse werden meist in Tabellen dargestellt. Hierfür gibt es bereits Tabellen. Allerdings sind da nur ein paar Zahlen immer dargestellt. Das heißt, Sie sollten trotzdem den Algorithmus lernen.

## Umrechnung

### Dezimal → Binär

Um eine Dezimalzahl in eine Binärzahl umzuwandeln, teilen Sie die Zahl wiederholt durch 2 und notieren Sie die Reste. Die Binärzahl ergibt sich, indem Sie die Reste von unten nach oben lesen.

**Beispiel: 13 in Binär umwandeln**

```
13 ÷ 2 = 6  Rest: 1  ← letzte Stelle
 6 ÷ 2 = 3  Rest: 0
 3 ÷ 2 = 1  Rest: 1
 1 ÷ 2 = 0  Rest: 1  ← erste Stelle
```

Von unten nach oben gelesen: **1101**₂

### Binär → Dezimal

Um eine Binärzahl in eine Dezimalzahl umzuwandeln, multiplizieren Sie jede Stelle mit ihrer Stellenwertigkeit (2^Position) und addieren Sie die Ergebnisse.

**Beispiel: 1101₂ in Dezimal umwandeln**

```
1 × 2³ + 1 × 2² + 0 × 2¹ + 1 × 2⁰
= 1 × 8 + 1 × 4 + 0 × 2 + 1 × 1
= 8 + 4 + 0 + 1
= 13
```

### Dezimal → Hexadezimal

Um eine Dezimalzahl in eine Hexadezimalzahl umzuwandeln, teilen Sie die Zahl wiederholt durch 16 und notieren Sie die Reste. Reste größer als 9 werden durch Buchstaben ersetzt (10=A, 11=B, 12=C, 13=D, 14=E, 15=F).

**Beispiel: 13 in Hexadezimal umwandeln**

```
13 ÷ 16 = 0  Rest: 13 (= D)  ← letzte Stelle
```

Ergebnis: **D**₁₆

**Beispiel: 255 in Hexadezimal umwandeln**

```
255 ÷ 16 = 15  Rest: 15 (= F)  ← letzte Stelle
 15 ÷ 16 = 0   Rest: 15 (= F)  ← erste Stelle
```

Von unten nach oben gelesen: **FF**₁₆

### Hexadezimal → Dezimal

Um eine Hexadezimalzahl in eine Dezimalzahl umzuwandeln, multiplizieren Sie jede Stelle mit ihrer Stellenwertigkeit (16^Position) und addieren Sie die Ergebnisse. Buchstaben werden zuerst in Zahlen umgewandelt (A=10, B=11, C=12, D=13, E=14, F=15).

**Beispiel: D₁₆ in Dezimal umwandeln**

```
D × 16⁰ = 13 × 1 = 13
```

**Beispiel: FF₁₆ in Dezimal umwandeln**

```
F × 16¹ + F × 16⁰
= 15 × 16 + 15 × 1
= 240 + 15
= 255
```

### Binär ↔ Hexadezimal

Die Umrechnung zwischen Binär und Hexadezimal ist besonders einfach, da 16 = 2⁴ ist. Sie können jede Hexadezimalziffer direkt durch 4 Binärziffern ersetzen und umgekehrt.

**Beispiel: D₁₆ in Binär umwandeln**

```
D = 13 = 1101₂
```

**Beispiel: 1101₂ in Hexadezimal umwandeln**

```
1101₂ = D₁₆
```

**Beispiel: FF₁₆ in Binär umwandeln**

```
F = 1111₂, also FF₁₆ = 11111111₂
```

**Beispiel: 10101101₂ in Hexadezimal umwandeln**

```
Von rechts nach links in Gruppen zu 4:
1010 1101
 A    D
```

Ergebnis: **AD**₁₆

## Tabellen

Die folgenden Tabellen helfen Ihnen, häufig vorkommende Zahlen schnell zu erkennen und einzuordnen.

### Tabelle: Dezimal, Binär und Hexadezimal (0-15)

| Dezimal | Binär | Hexadezimal |
|---------|-------|-------------|
| 0       | 0000  | 0           |
| 1       | 0001  | 1           |
| 2       | 0010  | 2           |
| 3       | 0011  | 3           |
| 4       | 0100  | 4           |
| 5       | 0101  | 5           |
| 6       | 0110  | 6           |
| 7       | 0111  | 7           |
| 8       | 1000  | 8           |
| 9       | 1001  | 9           |
| 10      | 1010  | A           |
| 11      | 1011  | B           |
| 12      | 1100  | C           |
| 13      | 1101  | D           |
| 14      | 1110  | E           |
| 15      | 1111  | F           |

### Tabelle: Wichtige Zahlen in der Informatik

Diese Zahlen sind besonders wichtig, da sie häufig in der Informatik vorkommen (z.B. bei Speicheradressen, Farbwerten, Bitmasken).

| Dezimal | Binär      | Hexadezimal |
|---------|------------|-------------|
| 0       | 00000000   | 00          |
| 16      | 00010000   | 10          |
| 24      | 00011000   | 18          |
| 32      | 00100000   | 20          |
| 64      | 01000000   | 40          |
| 100     | 01100100   | 64          |
| 128     | 10000000   | 80          |
| 192     | 11000000   | C0          |
| 200     | 11001000   | C8          |
| 224     | 11100000   | E0          |
| 240     | 11110000   | F0          |
| 255     | 11111111   | FF          |

## Rechenregeln

### Addition und Subtraktion

Die **Rechenregeln** für Addition und Subtraktion ändern sich **nicht**, wenn Sie verschiedene Zahlensysteme verwenden. Nur die **Darstellung** der Zahlen ändert sich.

**Beispiel: Addition**

```
Dezimal:    13 + 5 = 18
Binär:      1101₂ + 101₂ = 10010₂
Hexadezimal: D₁₆ + 5₁₆ = 12₁₆
```

Alle drei Darstellungen beschreiben dieselbe Rechnung. Die Addition funktioniert in allen Stellenwertsystemen gleich: Sie addieren stellenweise von rechts nach links und übertragen Überträge zur nächsten Stelle, wenn die Summe die Basis überschreitet.

**Beispiel: Binäre Addition**

```
  1101₂  (13)
+  101₂  ( 5)
------
 10010₂  (18)

Erklärung:
- Rechts: 1 + 1 = 2 = 10₂ → 0 schreiben, 1 übertragen
- Nächste Stelle: 0 + 0 + 1 (Übertrag) = 1
- Nächste Stelle: 1 + 1 = 2 = 10₂ → 0 schreiben, 1 übertragen
- Nächste Stelle: 1 + 0 + 1 (Übertrag) = 2 = 10₂ → 0 schreiben, 1 übertragen
- Letzte Stelle: 1 (Übertrag) = 1
```

Die Subtraktion funktioniert analog: Sie subtrahieren stellenweise und "borgen" von der nächsten Stelle, wenn nötig.

### Byte und Hexadezimal

```{admonition} Byte
:name: def-byte
:class: definition

Ein **Byte** besteht aus **8 Bits**. Ein Byte kann Werte von 0 bis 255 darstellen.
```

Ein Byte entspricht genau **zwei Hexadezimalziffern**:
- **00**₁₆ = 0₁₀ = 00000000₂ (kleinster Wert)
- **FF**₁₆ = 255₁₀ = 11111111₂ (größter Wert)

Diese Beziehung macht Hexadezimal besonders praktisch für die Darstellung von Bytes: Jede Hexadezimalziffer repräsentiert genau 4 Bits (eine "Nibble"), und zwei Hexadezimalziffern repräsentieren genau ein Byte.

**Beispiele:**
- Ein Byte mit dem Wert 13₁₀ = **0D**₁₆ (führende Null nicht weglassen, wenn man explizit ein Byte darstellt)
- Ein Byte mit dem Wert 255₁₀ = **FF**₁₆
- Die Speicheradresse eines Bytes wird oft in Hexadezimal angegeben, z.B. `0x0042` für Byte an Adresse 66

### Praktische Tipps

1. **Binär ↔ Hexadezimal**: Nutzen Sie die einfache Umrechnung über 4er-Gruppen. Dies ist der schnellste Weg zwischen diesen beiden Systemen.

2. **Potenzen von 2**: In der Informatik sind Potenzen von 2 besonders wichtig:
   - 2⁰ = 1
   - 2¹ = 2
   - 2² = 4
   - 2³ = 8
   - 2⁴ = 16
   - 2⁵ = 32
   - 2⁶ = 64
   - 2⁷ = 128
   - 2⁸ = 256

3. **Hexadezimalziffern**: Die Hexadezimalziffern A-F entsprechen den Dezimalwerten 10-15. Diese Zuordnung sollten Sie auswendig kennen.

4. **8-Bit-Bereich**: Zahlen von 0-255 können mit 8 Bits dargestellt werden. Dies entspricht zwei Hexadezimalziffern (00-FF). Dieser Bereich ist besonders wichtig für Farbwerte und viele andere Anwendungen.



```{admonition} Hinweis
:class: important

In der Praxis müssen Sie nicht ständig Zahlen von Hand umrechnen. Wichtig ist jedoch:
- Die verschiedenen Darstellungen zu **erkennen** (z.B. in Debugger-Ausgaben oder technischen Dokumentationen)
- Die **Bedeutung** zu verstehen (z.B. dass FF₁₆ = 255₁₀ = 11111111₂ dieselbe Zahl ist)
- Bei Bedarf die Umrechnung **nachvollziehen** zu können

Viele Entwicklungsumgebungen und Taschenrechner bieten Umrechnungsfunktionen. Das Verständnis der Zahlensysteme hilft Ihnen jedoch, Fehler zu erkennen und technische Dokumentationen besser zu verstehen.
```

