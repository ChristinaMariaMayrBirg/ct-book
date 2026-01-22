---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(sec-programming-constructs)=
# Programmierkonstrukte

In diesem Kapitel lernen wir die fundamentalen Bausteine der Programmierung kennen: *Kontrollstrukturen* und *Datenstrukturen*.
Diese beiden Konzepte bilden zusammen die Grundlage für alle Algorithmen und Programme.

## Lernziele

Nach diesem Kapitel können Sie …

- erklären, was **Kontrollstrukturen** sind und wozu man **Fallunterscheidungen** und **Wiederholungen** braucht.
- den Unterschied zwischen **Iteration** und **Rekursion** beschreiben und typische Einsatzideen nennen.
- zentrale **Datenstrukturen** (z. B. Stack, Queue, Array, dynamisches Array, verkettete Liste) einordnen und Grundoperationen benennen.
- unterscheiden zwischen **Abstraktem Datentyp (ADT)** und **Implementierung im Speicher**.

## Kontrollstrukturen

Durch [Wiederholung](sec-repetition-and-recursion) in Form von *Schleifen* und *(rekursiven) Funktionen* vermeiden wir es Anweisungen, die wir mehrfach ausführen wollen, auch mehrfach niederzuschreiben.
Erst durch diese fundamentale Eigenschaft, ist es überhaupt möglich, dass wir die Anzahl der ausgeführten Anweisungen von der Länge des Programmcodes entkoppeln.

[Fallunterscheidungen](sec-if-else) erlauben es uns wiederum bestimmte Anweisungen nur dann auszuführen, wenn eine bestimmte Bedingung zur Laufzeit des Programms erfüllt ist.

*Schleifen* und *Fallunterscheidungen* kombiniert mit *Variablen*, bilden bereits alles was wir benötigen.
Um unseren Programmcode zu strukturieren und bestimmte Programmteile an verschiedenen Stellen aufzurufen, gibt es zusätzlich das Konzept der Programmierfunktionen oder kurz *Funktionen*.

```{admonition} Kontrollstrukturen
:name: def-control-structure
:class: definition

*Kontrollstrukturen* sind Anweisungen, welche die Abarbeitungsreihenfolge von anderen Anweisungen, und damit den Programmablauf kontrollieren.
```

Zusammenfassend konzentrieren wir uns auf:

1. Fallunterscheidungen (bedingte Ausführung)
2. Schleifen (Wiederholung)
3. Funktionen (Wiederholung)

Hinweis: Schon wenige Kontrollstrukturen reichen aus, um sehr viele Programme auszudrücken. Die formale Einordnung (Berechenbarkeit, Turing-Vollständigkeit) ist spannend, aber **nicht Kernstoff** dieses Kapitels.
Theoretisch ist es bereits ausreichend wenn eine Programmiersprache 

1. Variablen unterstützt, auf die wir einen konstanten Wert addieren oder subtrahieren können und
2. eine Wiederholung unterstützt, dessen Abbruchbedingung vor dem Eintritt in die Wiederholung unbekannt ist (``while``-Schleife)

Die Fallunterscheidung, lässt sich (in hässlicher Form) durch eine Schleife ausdrücken.

Für die konkrete Syntax und Anwendung dieser Kontrollstrukturen in ``Python`` verweisen wir auf das Kapitel [Kontrollstrukturen](sec-control-statements) im Teil **PYTHON**.

(sec-if-else)=
### Fallunterscheidungen

Die erste Kontrollstruktur realisiert die bedingte Ausführung, das bedeutet, eine bestimmte Sequenz von Anweisungen ``A1, ... ,An`` wird nur dann ausgeführt, wenn eine Bedingung ``B`` zutrifft.

Die Bedingung ``B`` kann nur zu wahr ``True`` oder falsch ``False`` ausgewertet werden.
Gewöhnlich hängt der Wahrheitswert der Bedingung vom Programmablauf ab, d.h., er ist erst zur Laufzeit bekannt.

Es gibt von diesen Fallunterscheidungen verschiedene Varianten, wobei diese lediglich syntaktischer Zucker sind.
Für ``Python`` besprechen wir alle Möglichkeiten im Teil **PYTHON** in [Fallunterscheidungen](sec-cases).

(sec-repetition-and-recursion)=
### Wiederholung

Das fundamentale Prinzip der *Wiederholung* ist zentraler Bestandteil der Programmierung.
Blicken wir in den Werkzeugkasten der Algorithmen so finden wir die Wiederholung überall.
Sortieralgorithmen, die Berechnung eines Gleichungssystems, das Verarbeiten eines Bildes, die Schaltflächen einer App, überall finden wir Schleifen, die unsere Informationen *iterativ* verarbeiten.

Nach der Definition eines Algorithmus muss dieser aus endlich vielen Anweisungen bestehen.
Wenn wir jedoch eine variable Menge an Information verarbeiten wollen, muss ein Algorithmus – abhängig von der Eingabe – unterschiedlich viele Schritte ausführen.
Das erreichen wir durch **Wiederholung**: Wir formulieren einen Teilablauf einmal und lassen ihn (konzeptionell) mehrfach laufen.

In der Praxis ist die Kombination aus **Fallunterscheidung** (Bedingung) und **Wiederholung** der Kern vieler Programme. Die theoretischen Hintergründe dazu sind optional und werden hier nicht weiter vertieft.

Nun haben Sie vielleicht die Hoffnung, Sie müssten nur die [Wiederholung](sec-repetition-and-recursion) und die [Fallunterscheidungen](sec-if-else) beherrschen und können dann jedes Problem lösen.
Leider sind diese beiden Techniken derart grundlegend, dass sie eine notwendige nicht aber ausreichende Bedingung für die Entwicklung von Algorithmen darstellen.
Wir können das mit der Sprache vergleichen.
Nur weil wir Laute von uns geben können, heißt das nicht, dass wir uns in jeder Sprache verständigen können.
Ein weiteres Beispiel wären die Naturwissenschaften.
Nur weil wir die kleinsten Teilchen im Universum verstehen, bedeutet dass nicht, dass wir damit das entstehen von Leben oder andere komplexe Übergängen erklären können.

Wir kennen zwei Arten von Wiederholungen:

1. Die [Iteration](sec-iteration) und 
2. die [Rekursion](sec-recursion).

Auf der konzeptionellen Ebene erscheinen Iteration und Rekursion grundverschieden -- es sind unterschiedliche Denkweisen.
Wir können rekursiv oder iterativ denken.

```{admonition} Iteration und Rekursion
:class: theorem
:name: theorem-iteration-and-recursion

Jede Rekursion kann in eine unbestimmte Iteration und jede (unbestimmte) Iteration in eine Rekursion umgewandelt werden.

```

Mit *unbestimmt* meinen wir, dass bevor die Iteration beginnt nicht bekannt ist, wie viele Wiederholungen nötig sind.

Manche Probleme lassen sich leichter rekursiv und andere leichter iterativ lösen bzw. durchdenken.
In manchen Fällen ist es beispielsweise sinnvoll eine rekursive Lösung zu entwickeln und diese dann in eine iterative umzuwandeln.

Für die konkrete Implementierung von Iterationen und Rekursionen in ``Python`` verweisen wir auf das Kapitel [Schleifen](sec-loops) und [Rekursion](sec-recursive-functions) im Teil **PYTHON**.

(sec-iteration)=
#### Iteration

Wenn Sie Erfahrung im entwickeln von iterativen Algorithmen gesammelt haben und iterative Algorithmen analysiert und verwendet haben, dann werden Sie beginnen in Iterationen zu denken.
Sie werden beginnen in Iterationen von Iterationen von Iterationen zu denken.

Das wohl einfachste Beispiel für eine Iteration ist die Addition einer Menge von Zahlen.
Lassen Sie uns alle geraden Zahlen von ``2`` bis ``n`` addieren.
Hierzu brauchen wir eine Variable ``acc``, welche wir mit dem Wert ``0`` initialisieren und dann iterativ 2 dann 4, und so weiter addieren.

Die konkrete Syntax für Iterationen in ``Python`` (``for``- und ``while``-Schleifen) wird im Kapitel [Schleifen](sec-loops) behandelt.

(sec-recursion)=
#### Rekursion

Rekursion ist dieses scheinbar unverständliche Konzept, welches Mathematiker\*innen lieben und vor dem Programmierer\*innen anfänglich davonlaufen.
Derweil würden wir behaupten, dass die *rekursive Denkweise* uns Menschen näher ist als das Denken in Iterationen.
Rekursive Lösungen sind oft eleganter, kürzer, verständlicher aber leider auch langsamer als iterative Lösungen.
Die Rekursion hängt dabei stark mit der Induktion zusammen, siehe Abschnitt [vollständige Induktion](sec-induction).

Nehmen wir die Berechnung der Fakultät, einmal *iterativ*

$$\text{fac}_\text{it}(n) = n \cdot (n-1) \cdot (n-2) \cdot \ldots \cdot 1 = \prod\limits_{i=1}^n i$$

und einmal *rekursiv*

$$\text{fac}_\text{rec}(n) = \begin{cases} 1 & \text{ falls } n = 0\\ n \cdot \text{fac}_\text{rec}(n-1) & \text{ sonst}\end{cases}$$

Die Rekursion beinhaltet einen Selbstbezug, wohingegen die iterative Lösung diesen ausbreitet bzw. auflöst.
Betrachten wir die rekursive Lösung benötigen wir für die Berechnung lediglich die Multiplikation und den Selbstbezug - keine Schleife, und abgesehen von ``n``, nicht einmal eine Variable.

```{admonition} Rekursion
:name: def-recursion
:class: definition
Als *Rekursion* wird ein Vorgang bezeichnet, welcher sich selbst als Teil enthält oder mithilfe von sich selbst definierbar ist.
```

Für die konkrete Implementierung rekursiver Funktionen in ``Python`` verweisen wir auf das Kapitel [Rekursion](sec-recursive-functions) im Teil **PYTHON**.

## Datenstrukturen


Da sich alle Daten (Programm und dessen Eingabe/Ausgabe) im [Arbeitsspeicher](def-main-memory) befinden, müssen wir begreifen welche Funktionalität diese *konkrete* Datenstruktur bietet.
Alle weiteren *abstrakten* Datenstrukturen bauen auf diesen Möglichkeiten auf.

Es gibt zwei wesentliche Arten, wie Datenstrukturen im Arbeitsspeicher realisiert werden:

(1) Statische Sammlungen
: Die [Sammlung](def-collection) liegt als zusammenhängende Folge von [Bits](def-bit) im Arbeitsspeicher

(2) Dynamische Sammlungen 
: Die [Sammlung](def-collection) besteht aus mehreren zusammenhängenden Folgen von [Bits](def-bit), die voneinander getrennt im Arbeitsspeicher liegen. - wird von Python genutzt.

```{admonition} Statische Sammlungen
:name: def-static-ds
:class: definition
*Statische Sammlungen* können zur Laufzeit des Programms ihre Größe nicht verändern, d.h. ihr Speicherverbrauch kann sich **nicht** verändern. 
Stattdessen muss eine neue Datenstruktur angelegt werden.
```

```{admonition} Dynamische Sammlungen
:name: def-dynamic-ds
:class: definition
*Dynamische Sammlungen* können zur Laufzeit des Programms anwachsen und schrumpfen, d.h. ihr Speicherverbrauch kann sich verändern. Möglich wird dies durch die Verwendung von *[Zeigern](sec-pointer)*. Damit die fragmentierten Teile als ganzes repräsentiert werden können, müssen sie verbunden werden.
Dies wird durch sog. *[Zeiger/Pointer](def-pointer)* realisiert.
Oft spricht man auch von einer *Referenz*.
Dabei ist wichtig, dass ein *Zeiger* wiederum auf einen weiteren *Zeiger* *zeigen/verweisen/referenzieren* kann.
```

```{admonition} Zeiger
:name: def-pointer
:class: definition
Ein *Zeiger* ist ein Objekt welches eine Speicheradresse repräsentiert.
Programmiersprachen bieten die Mittel um Zeiger *aufzulösen*, was den Zugriff auf das Objekt auf das sie verweisen ermöglicht.
```


### Überblick über wichtige Datenstrukturen

In diesem Abschnitt unterscheiden wir zwei Perspektiven:

- **Abstrakte Datentypen (ADT)** beschreiben *das Verhalten* einer Sammlung: welche Operationen erlaubt sind und in welcher Reihenfolge (z. B. FIFO/LIFO).
- **Implementierungen** beschreiben *die Realisierung im Speicher*: liegen Elemente zusammenhängend oder verkettet, statisch oder dynamisch?

Wichtig: **Ein ADT kann durch verschiedene Implementierungen realisiert werden** (z. B. eine Queue als verkettete Liste *oder* auf Basis eines Arrays).

Das folgende Bild gibt einen Überblick über eine **strukturelle** Klassifikation (z. B. linear vs. nicht-linear). Diese Einordnung ist **unabhängig** von der Unterscheidung ADT vs. Implementierung.

- **Lineare Datenstrukturen**: Die Elemente sind in einer bestimmten Reihenfolge angeordnet.
  - **Statische lineare Strukturen**: Die Größe ist fest und kann sich nicht ändern.
  - **Dynamische lineare Strukturen**: Die Größe kann zur Laufzeit verändert werden.
- **Nicht-lineare Datenstrukturen**: Die Elemente sind nicht in einer einfachen Reihenfolge angeordnet.

```{figure} ../../figs/03-computer-sciences-basics/overview/datenstrukturen.png
:name: fig-data-structures-overview
:width: 100%
:align: center

Überblick über wichtige Datenstrukturen
```

#### Abstrakte Datentypen (ADT)

(sec-stack)=
Der *Stapel* (engl. *Stack*) oder auch *Stapelspeicher/Keller* ist einer der einfachsten [dynamischen Sammlungen](def-dynamic-ds), welche dem *Last-In-First-Out (LIFO)* Prinzip folgt.
LIFO bedeutet soviel wie: *zuletzt hinein - zuerst heraus*.
Das was zuletzt hinein gekommen ist, wird auch als erstes herausgenommen.
Stellen Sie sich einen Stapel aus Büchern vor.
Das Buch was Sie zuletzt auf den Bücherstapel gelegt haben liegt zugriffsbereit ganz oben.

Typische Operationen sind: **push** (ablegen), **pop** (entnehmen) und **top/peek** (oberstes Element ansehen).
Ein Stack kann z. B. als Array/dynamisches Array oder als verkettete Liste implementiert werden.

(sec-queue)=
Die *Warteschlange* (engl. *Queue*) ist eine [dynamische Sammlung](def-dynamic-ds) und folgt dem sog. *First-In-First-Out (FIFO)* Prinzip.
FIFO bedeutet soviel wie: *zuerst hinein - zuerst hinaus*.
Das was zuerst hinein gekommen ist, wird auch als erstes herausgenommen.
Der Name rührt daher, dass die Datenstruktur wie eine Warteschlange an der Kasse funktioniert.
Kunden die sich zuerst in die Schlange einreihen, werden auch zuerst bedient.

Typische Operationen sind: **enqueue** (hinten anstellen), **dequeue** (vorne entnehmen) und **front/peek** (vorderstes Element ansehen).
Auch eine Queue kann auf unterschiedliche Weise implementiert werden (z. B. verkettet oder als Ringpuffer auf Basis eines Arrays).

#### Implementierungen (Speicherrepräsentationen)

(sec-array)=
Ein *Array* ist eine [statische Sammlung](def-static-ds) mit direktem Indexzugriff.
Es wird durch einen zusammenhängenden Speicherbereich realisiert.
Ein Array beinhaltet üblicherweise Elemente die alle vom gleichen [Datentyp](def-datatypes) sind.
Arrays bieten effizienten Zugriff über einen Index, können aber ihre Größe nicht dynamisch ändern.

```{admonition} Arrays in Python?
:name: remark-arrays-python
:class: remark
Anders als in den meisten Sprachen, gibt es in ``Python`` keine nativen Arrays.
```

Es gibt sog. [Tupel](sec-tuple), die einem Array nahekommen, jedoch kann man die Elemente eines Tupels nicht verändern.
``Python``-Listen sind hingegen [dynamische Arrays](sec-dynamic-array).
Details zu Tupeln und Listen finden Sie im Kapitel [Tupel](sec-tuple) und [Listen](sec-list).

(sec-dynamic-array)=
*Dynamische Arrays* kombinieren die Vorteile von Arrays (effizienter Indexzugriff) mit der Flexibilität dynamischer Sammlungen (Größenänderung zur Laufzeit).
Sie basieren auf einem zusammenhängenden Speicherbereich, der jedoch bei Bedarf neu angelegt wird.
Die ``Python``-[Liste](sec-list) ist ein *dynamisches Array*.
Details zur Arbeit mit Listen in ``Python`` finden Sie im Kapitel [Listen](sec-list).

(sec-linked-list)=
Eine *verkettete Liste* (engl. *Linked List*) besteht aus Knoten, die durch [Zeiger](def-pointer) verbunden sind.
Jeder Knoten enthält Daten und einen Zeiger auf den nächsten Knoten.
Sie ist eine [dynamische Sammlung](def-dynamic-ds), d.h. sie kann zur Laufzeit vergrößert und verkleinert werden.
Haben wir direkten Zugriff auf einen Knoten so können wir in die *verkettete Liste* ein neues Element effizient einfügen ohne dabei die anderen Elemente der Liste zu verschieben -- ein wesentlicher Vorteil dieser Datenstruktur.



```{admonition} Mehr Hintergrund
:class: note
Mehr Hintergrund zum Thema Speichern von Datenstrukturen finden Sie im [Expertenwissen: Speicherlayout von Datenstrukturen](sec-memory-layout).
```

## Selbstcheck

- Nennen Sie je ein Beispiel für eine **Fallunterscheidung** und eine **Wiederholung** (konzeptionell, ohne Python-Syntax).
- Welche Operationen sind typisch für **Stack** und **Queue**?
- Was bedeutet **ADT** – und warum kann derselbe ADT unterschiedlich implementiert sein?