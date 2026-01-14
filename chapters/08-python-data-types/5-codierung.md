# Codierung 

In diesem Kapitel haben wir nun eine reihe von datentypen kennengelernt: int, bool, float aber auch zusammengesetzte datentypen wie strings (buchstabenkette) oder eine string-liste (mehrere strings nacheinander).


Im Kapitel über Codierung (chapters/03-computer-sciences-basics/1-codierung.md) haben wir bereits gesehen, dass alle Informationen im Computer als Bitfolgen gespeichert werden und dass eine **Codierung** festlegt, wie diese Bitfolgen zu interpretieren sind.

Wie also werden die Datentypen, die wir in diesem Kapitel kennengelernt haben abgespeichert?


## Zahlen

Für Zahlen gibt es verschiedene Codierungsverfahren, die je nach Art der Zahl unterschiedlich sind. 

+ Ganze Zahlen: (natürliche zahlen??): Spezialfall, siehe chapters/03-computer-sciences-basics/1-codierung.md. Ganze Zahlen wie z.B. die dezimale 13 lassen sich als Bitfolge darstellen (codieren), indem Sie die 13 dezimal in binär umrechnen. In diesem einfachen Fall fallen findet keine Codierung im eigentlichen sinne statt.

### Negative Zahlen

Für die Darstellung von **negativen ganzen Zahlen** wird in Computern häufig das **Zweierkomplement** verwendet. Dabei wird das höchste Bit als Vorzeichenbit interpretiert.

**Beispiel für 8-Bit-Zahlen:**
- 0-127: positive Zahlen (höchstes Bit = 0)
- 128-255: negative Zahlen im Zweierkomplement (höchstes Bit = 1)

So kann mit 8 Bits der Bereich von -128 bis +127 dargestellt werden.

```{admonition} Hinweis: Zweierkomplement
:class: note

Die Details des Zweierkomplements werden hier nicht weiter vertieft, da dies ein fortgeschrittenes Thema der numerischen Codierung ist. Für die praktische Programmierung ist es wichtig zu wissen, dass negative ganze Zahlen auf diese Weise dargestellt werden, und dass es einen begrenzten Wertebereich gibt.
```

### Gleitkommazahlen (IEEE 754)

Für Zahlen mit Nachkommastellen (z.B. 3,14 oder 0,0000000001) reicht ein einfacher Zahlensystemwechsel nicht aus. Hier ist eine spezielle **numerische Codierung** erforderlich, die festlegt, wie das Komma, die Nachkommastellen und Rundungen repräsentiert werden.

Der Standard für die Codierung von Gleitkommazahlen ist **IEEE 754** (Institute of Electrical and Electronics Engineers Standard 754). Dieser Standard legt fest, wie Fließkommazahlen im Computer gespeichert werden.

Gleitkommazahlen werden nach dem IEEE 754-Standard codiert, indem die Zahl in drei Komponenten aufgeteilt wird:

1. **Vorzeichenbit**: Bestimmt, ob die Zahl positiv (0) oder negativ (1) ist
2. **Exponent**: Bestimmt die Größenordnung der Zahl (wo das Komma steht)
3. **Mantisse** (auch Signifikand): Enthält die signifikanten Ziffern der Zahl

Die Idee ist ähnlich der wissenschaftlichen Schreibweise: Eine Zahl wie 1234,56 kann als $1,23456 \times 10^3$ geschrieben werden. Im Binärsystem funktioniert dies analog mit Potenzen von 2.

In Python werden Fließkommazahlen (`float`) nach dem IEEE 754-Standard mit **64 Bits** (8 Bytes) gespeichert:

- **1 Bit** für das Vorzeichen
- **11 Bits** für den Exponenten
- **52 Bits** für die Mantisse

Diese Aufteilung ermöglicht es, sowohl sehr kleine Zahlen (z.B. $0.0000000001$) als auch sehr große Zahlen (z.B. $10000000.0$) mit der gleichen Anzahl von Bits darzustellen, indem die Position des "Kommas" (genauer: des Binärpunkts) durch den Exponenten verschoben wird.


#todo add algorithmus der umrechnung 

```{admonition} Wichtig 
:class: important

**Rundungsfehler**: Aufgrund der begrenzten Anzahl von Bits können nicht alle Dezimalzahlen exakt als Gleitkommazahlen dargestellt werden. Dies führt zu Rundungsfehlern, die bei Berechnungen auftreten können.

**Beispiel:**
```python
0.1 + 0.2 == 0.3  # False!
```

Dies liegt daran, dass 0,1 im Binärsystem eine periodische Zahl ist und nicht exakt dargestellt werden kann. Für die meisten praktischen Anwendungen sind diese Rundungsfehler jedoch vernachlässigbar klein.

**Genauigkeit**: Mit 64 Bits können etwa 15-17 signifikante Dezimalstellen dargestellt werden. Für die meisten technischen Berechnungen ist dies ausreichend.


## Text

Text besteht aus Zeichen (Buchstaben, Ziffern, Sonderzeichen), die als Bitfolgen codiert werden müssen. Wie wir bereits im Kapitel über Codierung (chapters/03-computer-sciences-basics/1-codierung.md) gesehen haben, kann die gleiche Bitfolge `01000001` je nach Codierung unterschiedliche Bedeutungen haben – als Zahl 65 oder als Buchstabe "A".

### ASCII

Eine der ersten wichtigen Zeichencodierungen ist **ASCII** (American Standard Code for Information Interchange). ASCII verwendet 7 Bits und kann damit 128 verschiedene Zeichen darstellen (0-127).

ASCII enthält:
- Lateinische Groß- und Kleinbuchstaben (A-Z, a-z)
- Ziffern (0-9)
- Sonderzeichen und Satzzeichen (!, ?, ., etc.)
- Steuerzeichen (z.B. Zeilenumbruch, Tabulator)

**Beispiel:**
- Der Buchstabe "A" hat den ASCII-Code 65, was der Bitfolge `01000001` entspricht
- Der Buchstabe "a" hat den ASCII-Code 97

ASCII hat jedoch eine wichtige Limitation: Es kann nur englische Zeichen darstellen. Umlaute (ä, ö, ü), Akzente (é, è, à) oder Zeichen aus anderen Schriftsystemen (z.B. Chinesisch, Arabisch) sind nicht enthalten. Auch Emojis können nicht dargestellt werden.

### Unicode

Um diese Einschränkung zu überwinden, wurde **Unicode** entwickelt – ein universeller Zeichensatz, der Zeichen aus praktisch allen Sprachen und Schriftsystemen der Welt umfasst. Unicode definiert für jedes Zeichen eine eindeutige Nummer, den sogenannten **Code Point**.

Unicode enthält weit mehr Zeichen als ASCII:
- Alle ASCII-Zeichen (Code Points 0-127)
- Umlaute und Akzente (ä, ö, ü, é, è, à, etc.)
- Zeichen aus anderen Schriftsystemen (Chinesisch, Arabisch, Kyrillisch, etc.)
- Emojis und Sonderzeichen (🎉, €, ©, etc.)

Wichtig: Unicode definiert nur, *welche* Zeichen es gibt und welche Nummer (Code Point) jedes Zeichen hat. Es legt jedoch **nicht** fest, wie diese Zeichen als Bitfolgen gespeichert werden sollen.

### UTF-8

**UTF-8** (Unicode Transformation Format 8-bit) ist eine Codierung, die festlegt, wie Unicode-Zeichen als Bitfolgen gespeichert werden. UTF-8 ist die Standard-Codierung für Python-Strings.

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

**Python Strings sind UTF-8**: In Python werden Strings standardmäßig als UTF-8 gespeichert. Sie können mit den Funktionen `ord()` und `chr()` zwischen Zeichen und ihren Unicode-Code Points umwandeln:

```python
ord('A')    # 65
chr(65)     # 'A'
ord('ä')    # 228
chr(228)    # 'ä'
ord('🎉')   # 127881
```

**Encoding-Probleme**: Bei der Arbeit mit Dateien oder beim Datenaustausch über Netzwerke kann es zu Encoding-Problemen kommen, wenn die Codierung nicht korrekt angegeben wird. Stellen Sie sicher, dass Sie beim Öffnen von Dateien das richtige Encoding angeben (z.B. `open('datei.txt', encoding='utf-8')`).

```


