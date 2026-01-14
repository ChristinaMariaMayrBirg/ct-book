# Codierung 

In diesem Kapitel haben wir nun eine Reihe von Datentypen kennengelernt: ``int``, ``bool``, ``float`` aber auch zusammengesetzte Datentypen wie ``str`` (Zeichenkette) oder eine Liste von Strings.

Im Kapitel über [Codierung](sec-codierung) haben wir bereits gesehen, dass alle Informationen im Computer als Bitfolgen gespeichert werden und dass eine **Codierung** festlegt, wie diese Bitfolgen zu interpretieren sind.

Wie also werden die Datentypen, die wir in diesem Kapitel kennengelernt haben, abgespeichert?

## Codierung vs. Zahlensysteme

Bevor wir uns den verschiedenen Codierungsverfahren widmen, ist es wichtig, den Unterschied zwischen **Codierung** und **Zahlensystemen** zu verstehen:

```{admonition} Codierung
:name: def-encoding
:class: definition
Eine **Codierung** (engl. *encoding*) legt fest, wie eine Bitfolge zu interpretieren ist.
Sie definiert eine Zuordnung zwischen Bitfolgen und deren Bedeutung.
```

```{admonition} Zahlensystem
:name: def-number-system
:class: definition
Ein **Zahlensystem** ist eine Darstellungsweise von Zahlen.
Es legt fest, wie Zahlen mit Ziffern notiert werden (z.B. Dezimal, Binär, Hexadezimal).
```

**Wichtiger Unterschied:**
- Ein **Zahlensystem** ist nur eine **Notation** oder **Darstellung** von Zahlen. Die Zahl $13_{10}$ kann als $1101_2$ (binär) oder als $D_{16}$ (hexadezimal) geschrieben werden - es ist dieselbe Zahl, nur anders dargestellt.
- Eine **Codierung** legt fest, wie eine **Bitfolge** interpretiert wird. Die Bitfolge `01000001` kann je nach Codierung unterschiedliche Bedeutungen haben:
  - Als Zahl: $65_{10}$ (wenn wir die Bitfolge als Binärzahl interpretieren)
  - Als Buchstabe: "A" (wenn wir die Bitfolge als ASCII-Zeichen interpretieren)

Für Details zur Umrechnung zwischen verschiedenen Zahlensystemen siehe das Kapitel [Zahlensysteme](sec-number-systems).

## Zahlen

Für Zahlen gibt es verschiedene Codierungsverfahren, die je nach Art der Zahl unterschiedlich sind.

### Ganze Zahlen (natürliche Zahlen)

Ganze Zahlen wie z.B. die dezimale $13_{10}$ lassen sich als Bitfolge darstellen, indem wir die Zahl in das Binärsystem umrechnen.
In diesem einfachen Fall nutzen wir das Binärsystem als **Zahlensystem** - wir stellen die Zahl $13_{10}$ als $1101_2$ dar.

Eine Binärzahl $b_{n-1} \ldots b_0$ mit $b_i \in \{0,1\}$ hat den Wert

$$b_{n-1} \cdot 2^{n-1} + \ldots + b_0 \cdot 2^0 = \sum\limits_{i=0}^{n-1} b_i \cdot 2^i.$$

Zum Beispiel hat $1101_2$ den Wert

$$1 \cdot 2^3 + 1 \cdot 2^2 + 0 \cdot 2^1 + 1 \cdot 2^0 = 8 + 4 + 0 + 1 = 13_{10}.$$

Hierbei handelt es sich um einen direkten **Zahlensystemwechsel** - keine spezielle Codierung im eigentlichen Sinne.
Die **Codierung** besteht lediglich darin, dass wir festlegen: "Diese Bitfolge wird als Binärzahl interpretiert."

Für Details zur Umrechnung zwischen Dezimal- und Binärsystem siehe das Kapitel [Zahlensysteme](sec-number-systems).

### Negative Zahlen (Zweierkomplement)

Für die Darstellung von **negativen ganzen Zahlen** wird in Computern das **Zweierkomplement** verwendet.
Hierbei handelt es sich um eine **Codierung**, die festlegt, wie Bitfolgen als negative Zahlen interpretiert werden.

Das höchste Bit wird dabei nicht als einfaches Vorzeichenbit, sondern als negativer Anteil interpretiert.

Im *Zweierkomplement* wird eine Zahl $b_{n-1} \ldots b_0$ wie folgt interpretiert:

```{math}
:label: eq:binary:integer
  b_{n-1} \ldots b_0 = -b_{n-1} \cdot 2^{n-1} + \sum\limits_{i=0}^{n-2} b_i \cdot 2^i.
```

**Beispiel für 8-Bit-Zahlen:**
- $0$-$127$: positive Zahlen (höchstes Bit = 0)
- $128$-$255$: negative Zahlen im Zweierkomplement (höchstes Bit = 1)

So kann mit 8 Bits der Bereich von $-128$ bis $+127$ dargestellt werden.

**Beispiele:**
- $1011_2$ (4 Bits) = $-2^3 \cdot 1 + 2^2 \cdot 0 + 2^1 \cdot 1 + 2^0 \cdot 1 = -8 + 2 + 1 = -5_{10}$
- $111_2$ (3 Bits) = $-2^2 \cdot 1 + 2^1 \cdot 1 + 2^0 \cdot 1 = -4 + 2 + 1 = -1_{10}$

```{admonition} Hinweis: Zweierkomplement
:class: note

Das Zweierkomplement ist eine **Codierung**, die festlegt, wie Bitfolgen als negative Zahlen interpretiert werden.
Es ist mehr als nur ein Zahlensystem - es definiert eine spezielle Interpretation von Bitfolgen für negative Werte.

Für detaillierte Informationen über das Zweierkomplement, die Umrechnung zwischen positiven und negativen Zahlen sowie Addition und Subtraktion im Binärsystem siehe das Kapitel [Zahlensysteme](sec-number-systems).
```

### Gleitkommazahlen (IEEE 754)

Für Zahlen mit Nachkommastellen (z.B. $3.14$ oder $0.0000000001$) reicht ein einfacher Zahlensystemwechsel nicht aus. Hier ist eine spezielle **numerische Codierung** erforderlich, die festlegt, wie das Komma, die Nachkommastellen und Rundungen repräsentiert werden.

Der Standard für die Codierung von Gleitkommazahlen ist **IEEE 754** (Institute of Electrical and Electronics Engineers Standard 754). Dieser Standard legt fest, wie Fließkommazahlen im Computer gespeichert werden.

Gleitkommazahlen werden nach dem IEEE 754-Standard codiert, indem die Zahl in drei Komponenten aufgeteilt wird:

1. **Vorzeichenbit**: Bestimmt, ob die Zahl positiv (0) oder negativ (1) ist
2. **Exponent**: Bestimmt die Größenordnung der Zahl (wo das Komma steht)
3. **Mantisse** (auch Signifikand): Enthält die signifikanten Ziffern der Zahl

Die Idee ist ähnlich der wissenschaftlichen Schreibweise: Eine Zahl wie $1234.56$ kann als $1.23456 \times 10^3$ geschrieben werden. Im Binärsystem funktioniert dies analog mit Potenzen von 2.

In Python werden Fließkommazahlen (``float``) nach dem IEEE 754-Standard mit **64 Bits** (8 Bytes) gespeichert:

- **1 Bit** für das Vorzeichen
- **11 Bits** für den Exponenten
- **52 Bits** für die Mantisse

Diese Aufteilung ermöglicht es, sowohl sehr kleine Zahlen (z.B. $0.0000000001$) als auch sehr große Zahlen (z.B. $10000000.0$) mit der gleichen Anzahl von Bits darzustellen, indem die Position des "Kommas" (genauer: des Binärpunkts) durch den Exponenten verschoben wird.

```{admonition} Wichtig 
:class: important

**Rundungsfehler**: Aufgrund der begrenzten Anzahl von Bits können nicht alle Dezimalzahlen exakt als Gleitkommazahlen dargestellt werden. Dies führt zu Rundungsfehlern, die bei Berechnungen auftreten können.

**Beispiel:**
```python
0.1 + 0.2 == 0.3  # False!
```

Dies liegt daran, dass $0.1$ im Binärsystem eine periodische Zahl ist und nicht exakt dargestellt werden kann. Für die meisten praktischen Anwendungen sind diese Rundungsfehler jedoch vernachlässigbar klein.

**Genauigkeit**: Mit 64 Bits können etwa 15-17 signifikante Dezimalstellen dargestellt werden. Für die meisten technischen Berechnungen ist dies ausreichend.
```

## Text

Text besteht aus Zeichen (Buchstaben, Ziffern, Sonderzeichen), die als Bitfolgen codiert werden müssen. Hierbei handelt es sich um eine **Codierung** im eigentlichen Sinne: Wir legen fest, welche Bitfolge welchem Zeichen entspricht.

Wie wir bereits im Kapitel über [Codierung](sec-codierung) gesehen haben, kann die gleiche Bitfolge `01000001` je nach Codierung unterschiedliche Bedeutungen haben:
- Als Zahl: $65_{10}$ (wenn wir die Bitfolge als Binärzahl interpretieren)
- Als Buchstabe: "A" (wenn wir die Bitfolge als ASCII-Zeichen interpretieren)

### Grundprinzip der Zeichencodierung

Wollen wir die Buchstaben des Alphabets in Binärdarstellung schreiben, so müssen wir uns darauf einigen, welche Binärzahl welchen Buchstaben repräsentiert.
Dies ist eine **Codierung** - wir legen fest, wie Bitfolgen als Zeichen interpretiert werden.

Da das lateinische Alphabet 26 Großbuchstaben enthält, brauchen wir mindestens 5 Bits, denn es gilt:

$$2^4 < 26 \leq 2^5.$$

Mit 5 Bits können wir $2^5 = 32$ verschiedene Zeichen darstellen, was für die 26 Buchstaben ausreicht.

```{exercise} Repräsentation
:label: repraesentation-alphabet-exercise
Wie viele Bits benötigen Sie, wenn Sie die Kleinbuchstaben auch repräsentieren möchten?
```

```{solution} repraesentation-alphabet-exercise
:label: repraesentation-alphabet-solution
:class: dropdown
Mit Kleinbuchstaben haben wir $52$ Elemente und brauchen somit $6$ Bits, denn 

$$2^5 < 52 \leq 2^6$$
```

Ein Wort besteht natürlich aus mehreren Buchstaben.
Zum Beispiel wäre *BAD* repräsentiert durch die Konkatenation der Binärdarstellungen der einzelnen Buchstaben.
Im Computer würden demnach mehrere Bits, die entweder den Zustand **Strom aus** oder **Strom an** haben, das Wort repräsentieren.

Sonderzeichen wie Leerzeichen oder weitere Zeichen müssten wir in unsere Codierung noch einfügen.
Auch könnten wir einen vollkommen anderen Zeichensatz benutzen.
Programme, die auf diesem aufbauen, müssen die Codierung lediglich kennen.

Auch können wir längere Wörter oder ganze Sätze bilden, brauchen dafür natürlich Speicherplatz.
In unserem Beispiel benötigt jeder Buchstabe 5 Bits.
D. h., um einen Text mit, sagen wir 300 Zeichen im Speicher zu halten, brauchen wir die Bauteile für mindestens $300 \times 5 = 1500$ Bits, was wiederum $187.5$ Bytes bzw. $0.1875$ [kiloByte](https://en.wikipedia.org/wiki/Kilobyte) (kB) ($10^3$ Byte) und ca. $0.1831$ [kibiByte](https://en.wikipedia.org/wiki/Kilobyte) (KB/KiB) ($2^{10}$ Byte) sind.

### ASCII

Eine der ersten wichtigen Zeichencodierungen ist **ASCII** (American Standard Code for Information Interchange). ASCII verwendet 7 Bits und kann damit 128 verschiedene Zeichen darstellen (0-127).

ASCII ist eine **Codierung**, die festlegt:
- Welche Bitfolge welchem Zeichen entspricht
- Wie Zeichen als Bitfolgen gespeichert werden

ASCII enthält:
- Lateinische Groß- und Kleinbuchstaben (A-Z, a-z)
- Ziffern (0-9)
- Sonderzeichen und Satzzeichen (!, ?, ., etc.)
- Steuerzeichen (z.B. Zeilenumbruch, Tabulator)

**Beispiel:**
- Der Buchstabe "A" hat den ASCII-Code $65_{10}$, was der Bitfolge `01000001` entspricht
- Der Buchstabe "a" hat den ASCII-Code $97_{10}$

ASCII hat jedoch eine wichtige Limitation: Es kann nur englische Zeichen darstellen. Umlaute (ä, ö, ü), Akzente (é, è, à) oder Zeichen aus anderen Schriftsystemen (z.B. Chinesisch, Arabisch) sind nicht enthalten. Auch Emojis können nicht dargestellt werden.

### Unicode

Um diese Einschränkung zu überwinden, wurde **Unicode** entwickelt – ein universeller Zeichensatz, der Zeichen aus praktisch allen Sprachen und Schriftsystemen der Welt umfasst. Unicode definiert für jedes Zeichen eine eindeutige Nummer, den sogenannten **Code Point**.

Unicode enthält weit mehr Zeichen als ASCII:
- Alle ASCII-Zeichen (Code Points 0-127)
- Umlaute und Akzente (ä, ö, ü, é, è, à, etc.)
- Zeichen aus anderen Schriftsystemen (Chinesisch, Arabisch, Kyrillisch, etc.)
- Emojis und Sonderzeichen (🎉, €, ©, etc.)

Wichtig: Unicode definiert nur, *welche* Zeichen es gibt und welche Nummer (Code Point) jedes Zeichen hat. Es legt jedoch **nicht** fest, wie diese Zeichen als Bitfolgen gespeichert werden sollen. Unicode ist also noch keine vollständige Codierung - es ist eine Zuordnung von Zeichen zu Nummern.

### UTF-8

**UTF-8** (Unicode Transformation Format 8-bit) ist eine **Codierung**, die festlegt, wie Unicode-Zeichen als Bitfolgen gespeichert werden. UTF-8 ist die Standard-Codierung für Python-Strings.

UTF-8 verwendet eine **variable Länge**: Je nach Zeichen werden unterschiedlich viele Bytes verwendet:

- **1 Byte** für ASCII-Zeichen (z.B. "A", "1", "!")
- **2 Bytes** für viele europäische Zeichen (z.B. "ä", "ö", "ü", "é")
- **3 Bytes** für viele andere Zeichen (z.B. "€", "©")
- **4 Bytes** für Emojis und einige seltene Zeichen (z.B. "🎉", "🚀")

**Beispiele:**
- "A" → 1 Byte (gleich wie ASCII)
- "ä" → 2 Bytes
- "€" → 3 Bytes
- "🎉" → 4 Bytes

Ein wichtiger Vorteil von UTF-8 ist die **Rückwärtskompatibilität zu ASCII**: Alle ASCII-Zeichen werden in UTF-8 genauso codiert wie in ASCII. Das bedeutet, dass jeder ASCII-Text automatisch auch ein gültiger UTF-8-Text ist.

```{admonition} Wichtig
:class: important

**Python Strings sind UTF-8**: In Python werden Strings standardmäßig als UTF-8 gespeichert. Sie können mit den Funktionen ``ord()`` und ``chr()`` zwischen Zeichen und ihren Unicode-Code Points umwandeln:

```python
ord('A')    # 65
chr(65)     # 'A'
ord('ä')    # 228
chr(228)    # 'ä'
ord('🎉')   # 127881
```

**Encoding-Probleme**: Bei der Arbeit mit Dateien oder beim Datenaustausch über Netzwerke kann es zu Encoding-Problemen kommen, wenn die Codierung nicht korrekt angegeben wird. Stellen Sie sicher, dass Sie beim Öffnen von Dateien das richtige Encoding angeben (z.B. ``open('datei.txt', encoding='utf-8')``).
```
