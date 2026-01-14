# Codierung

Ein Computer arbeitet mit elektrischen Signalen, also physikalischen Zuständen.
Diese Zustände werden durch Milliarden von Transistoren gespeichert und über Bussysteme übertragen.
Ein Transistor kann dabei vereinfacht betrachtet zwei Zustände annehmen: *an* oder *aus*.

```{figure} ../../figs/digital-computer/representation/lamps.png
---
width: 200px
name: fig-lamps
---
Eine Lampe, die entweder aus (links) oder an (rechts) geschaltet sein kann.
```

Diese beiden Zustände werden üblicherweise durch die Zahlen **0** und **1** repräsentiert.
Damit entsteht eine Folge von Bits.

Alle Informationen, die ein Computer verarbeitet, liegen letztlich als solche Bitfolgen vor.
Für sich genommen haben diese Bitfolgen jedoch **keine Bedeutung**.

Erst durch eine **Codierung** wird festgelegt, wie eine bestimmte Folge von 0 und 1 zu interpretieren ist.


## Bedeutung entsteht durch Codierung

Die gleiche Bitfolge kann – je nach Kontext – völlig unterschiedliche Bedeutungen haben.

Beispiel:  
Die Bitfolge `01000001` kann bedeuten:
- die Zahl **65** (numerische Codierung)
- den Buchstaben **"A"** (ASCII-Codierung)
- einen Farbwert in einem Bild
- einen Teil eines Maschinenbefehls

Welche Bedeutung gilt, wird **nicht durch die Bitfolge selbst**,  
sondern durch die verwendete **Codierung** festgelegt.

---

## Zahlen

Sollen Bitfolgen als **numerische Werte** interpretiert werden,  
muss zunächst festgelegt werden, dass eine bestimmte Bitfolge überhaupt eine **Zahl** darstellt.

Diese Festlegung nennt man **numerische Codierung**.
Sie bestimmt zum Beispiel:
- ob es sich um eine Ganzzahl oder eine Gleitkommazahl handelt,
- ob Vorzeichen erlaubt sind,
- welcher Wertebereich darstellbar ist.

Beispiele für numerische Codierungen sind:
- vorzeichenlose Ganzzahlen,
- vorzeichenbehaftete Ganzzahlen (z. B. Zweierkomplement),
- Gleitkommazahlen (z. B. IEEE 754).

---

### Rolle der Zahlensysteme

Ein **Zahlensystem** ist ein Bestandteil der numerischen Codierung.
Es legt fest, **wie eine Zahl symbolisch dargestellt und gelesen wird**,
also welches Stellenwertsystem verwendet wird (z. B. Basis 2 oder Basis 10).

Die gleiche Zahl kann in verschiedenen Zahlensystemen unterschiedlich dargestellt werden.
Beispiel: die Zahl **13**:

- **13** im Dezimalsystem (Basis 10, Alltagsschreibweise)
- **1101** im Binärsystem (Basis 2)
- **D** im Hexadezimalsystem (Basis 16)

Alle diese Darstellungen stehen für **dieselbe numerische Bedeutung**.
Nur die **Darstellung** unterscheidet sich.

Ihre Aufgabe als Programmiererin oder Programmierer ist es,
sich von unterschiedlichen Darstellungen **nicht verwirren zu lassen**,
sondern sie korrekt einzuordnen und zu interpretieren. In der Praxis begegnet Ihnen das zum Beispiel, wenn:
- Debugger Speicheradressen oder Registerwerte in **Hexadezimaldarstellung** anzeigen,
- Fehlermeldungen **Bitmasken** oder **Statusflags** in binärer oder hexadezimaler Form enthalten,
- technische Dokumentationen Werte in verschiedenen Zahlensystemen beschreiben,
- Sie mit hardwarenahen Programmiersprachen oder Systemen arbeiten.

Deshalb lohnt es sich, Zahlensysteme zu verstehen und sicher zwischen verschiedenen Darstellungen wechseln zu können. Dabei geht es **nicht** darum, Zahlen ständig von Hand umzurechnen, sondern darum, Darstellungen richtig zu erkennen,
einzuordnen und bei Bedarf nachvollziehen zu können.


> **Zahlensysteme ändern die Darstellung einer Zahl, nicht ihre Bedeutung.**

```{admonition} Spezialfall: Ganze Zahlen 
:class: important

Gehen wir von einer bereits bekannten **ganzen Zahl** aus (z. B. der Zahl 13) und möchten diese als Bitfolge darstellen, dann ist die numerische Bedeutung der Zahl bereits festgelegt.

In diesem Spezialfall fällt der Codierungsschritt mit dem **Wechsel des Zahlensystems** zusammen:
- Die Wahl des Zahlensystems (z. B. Binär, Dezimal, Hexadezimal) bestimmt direkt die Darstellung der Zahl als Bitfolge.

Dies gilt jedoch **nur für ganze Zahlen**! Sollen Zahlen mit Nachkommastellen (z. B. 3,14) dargestellt werden, reicht ein Zahlensystem allein nicht aus.
Dann ist eine zusätzliche **numerische Codierung** erforderlich, die festlegt, wie das Komma, die Nachkommastellen und Rundungen repräsentiert werden (z. B. Gleitkommacodierungen wie IEEE 754).

Im **allgemeinen Fall** erzeugt die Codierung die Bitfolge, nicht das Zahlensystem!

```

---

## Text, Bilder und Töne

Neben Zahlen müssen auch andere Arten von Information codiert werden:

- **Text**  
  Zeichen werden über Zeichencodierungen (z. B. ASCII, UTF-8) auf Bitfolgen abgebildet.

- **Bilder**  
  Bilder bestehen aus Pixeln, deren Farbwerte numerisch codiert sind – also wiederum Zahlen.

- **Töne**  
  Schall wird abgetastet und als Folge numerischer Werte gespeichert – auch Töne werden letztlich als Zahlen dargestellt.

Alle diese Darstellungen beruhen auf Bitfolgen.
Die jeweilige **Codierung** bestimmt, wie diese Bitfolgen interpretiert werden.


```{admonition} Merksatz
:class: important

**Codierungen** legen fest, *dass* eine Bitfolge eine bestimmte Bedeutung hat  
(z. B. Zahl, Zeichen, Farbe).

**Zahlensysteme** legen fest, *wie* eine Zahl dargestellt und gelesen wird  
(z. B. zur Basis 2, 10 oder 16).

```





