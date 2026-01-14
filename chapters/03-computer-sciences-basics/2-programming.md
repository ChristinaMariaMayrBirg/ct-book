(sec-programming)=
# Programmieren
Programmieren ist eine Tätigkeit bei der wir unsere Ideen und Konzepte in Text überführen.
Ob das Programmieren nun wirklich mit dem Schreiben des Codes beginnt oder wir den ganzen Prozess der Softwareentwicklung als das Programmieren betrachten sei dahingestellt.
Wenn wir vom Programmieren sprechen, meinen wir oft beides:

1. Das Entwerfen eines Algorithmus und
2. dessen Realisierung (*Implementierung*) durch eine Programmiersprache.


Als gute Programmierer\*innen müssen wir 

+ unseren Kontext kennen,
+ logisch und mathematisch Denken können,
+ uns exakt ausdrücken können und uns auch unmissverständlich mit anderen austauschen können und
+ unsere Entwicklungswerkzeuge beherrschen können
  
Wir benötigen ein Grundverständnis davon wie ein [Computer funktioniert](sec-information-processing) und wie wir uns in der abstrakten Welt der [Kontroll-](sec-control-structures) und [Datenstrukturen](sec-data-structures) ausdrücken können.


Im Folgenden wollen wir eine gemeinsame Sprache schaffen und festlegen, was unter *Algorithmus*, *Programmcode* und *Programm*, *Software verstanden wird* .

## Algorithmus

Ein *Algorithmus* ist eine wohldefinierte Sequenz von Anweisungen, welche eine Lösung für ein bestimmtes Problem berechnet. oder auch: Ein *Algorithmus* ist eine endliche Folge von unmissverständlich beschriebenen ausführbaren Anweisung (z.B. Text/Programmcode), um für eine bestimmte endliche Eingabe in endlich vielen Schritten eine endliche Ausgabe zu erzeugen, wobei zu jeder Zeit der Ausführung nur endlich viel Speicherplatz verwendet wird. #todo: cite donald e. knuth.


```{exercise} Beispiel: Euklidischer Algorithmus
:label: euclid-exercise
Problem: 
Gegeben seien zwei natürliche Zahlen $n, m \in \mathbb{N}$.
Wir suchen nach dem größten gemeinsamen Teiler $\text{ggT}(n,m)$ von $n$ und $m$, d.h., die größte natürliche Zahl die sowohl $n$ als auch $m$ teilt.

Algorithmus:
Wir starten mit zwei Zahlen, und ziehen solange immer und immer wieder die kleinere von der größeren ab, bis beide Zahlen gleich sind.
Das Ergebnis ist der größter gemeinsamer Teiler der beiden ursprünglichen Zahlen!
Warum funktioniert das? -> siehe formalen nachweis.
```

Die Realisierung dieses Algorithmus in Python kann so aussehen:

```{code-cell} python3
def gcd(zahl1,zahl2):

    n = zahl1 # Wir starten mit zwei Zahlen
    m = zahl2
    
    while n != m: # solange die zahlen ungleich sein
        n = n - m # ziehen die kleinere von der größeren zahl ab
        if m > n: # bestimme welche aktuell die kleinere der beiden ist 
          t = m  # merke dir die größere zahl
          m = n # speichere den kleineren zahlwert in m
          n = t # speichere den größeren zahlenwert in n
    return m

gcd(544, 119) 
```
Daneben gibt es weitere Realisierungsmöglichkeiten. Wichtig an dieser Stelle ist zu verstehen: wir können ein problem oftmals mit unterschiedlichen algorithmen lösen. Einen weiteren Algorithmus und die mathematische Theorie, warum die Algorithmen "funktionieren", finden Sie im [Expertenwissen](sec-euclid-alg).


```{admonition} Eigenschaften von Algorithmen
:name: def-algorithm
:class: definition

Ein Algorithmus hat folgende Eigenschaften:

**(1) Endlichkeit:** 
: Identisch zur Beschreibung einer [Turingmaschine](info-universal-turing-machine), besteht ein Algorithmus aus endlich vielen Zeichen.
Anders ausgedrückt, können wir ihn in endlich viel Zeit niederschreiben.
Durch die Endlichkeit seiner Beschreibung, kann ein Algorithmus als Programm in einem (endlichen) Speicher abgelegt werden.

**(2) Ausführbarkeit:** 
: Jede Anweisung des Algorithmus muss ausführbar sein.
Das heißt, die [Semantik](def-semantik) einer jeden Anweisung muss im jeweiligen Kontext eindeutig definiert sein.
Es muss in jedem Schritt nicht nur klar sein was zu tun ist, sondern dieses was muss auch tatsächlich möglich sein.

**(3) Gebundenheit:** 
: Während der Ausführung des Algorithmus wird lediglich endlich viel Speicher bzw. eine endliche Anzahl an Variablen benötigt.

**(4) Terminierung:** 
: Die Ausführung eines Algorithmus muss nach endlich vielen Schritten enden.
Die Terminierung ist das Gegenstück zur *Gebundenheit* bezogen auf die Zeit.
**(1)** und **(4)** stellen sicher, dass ein Programm und dessen Ressourcen zusammengenommen nur endlich viel Speicher verbrauchen. 
In der Komplexitätstheorie spricht man hierbei von *dynamischer Finitheit* des Speicherbedarfs.

**(5) Eingabe:** 
: Jeder Algorithmus hat entweder keine oder eine endliche Eingabe.

**(6) Ausgabe:** 
: Jeder Algorithmus liefert mindestens eine Ausgabe, d.h., ein Ergebnis zurück.

Es gibt noch zwei optionale Eigenschaften für Algorithmen, welche oftmals gefordert werden:

**(7) Determiniertheit:** 
: Wir nennen einen Algorithmus **determiniert**, wenn er bei gleicher Eingabe auch die gleiche Ausgabe erzeugt.
Entscheidet ein Algorithmus durch einen *echten Münzwurf* (kein pseudo Zufall sondern echter Zufall) über den Verlauf der Ausführung, so wäre jener Algorithmus nicht determiniert.
Algorithmen basieren wenn überhaupt auf Pseudozufallszahlen, deren Erzeugung mit einem Startwert (*Seed*) initialisiert wird.
Bei gleichem *Seed* und gleicher Eingabe erzeugen diese Algorithmen auch das gleiche Ergebnis.
Da der *Seed* zur Eingabe gehört, sind jene Algorithmen determiniert.

**(8) Determinismus:** 
: Wir nennen einen Algorithmus **deterministisch**, wenn dieser während seiner Ausführung zu jedem Zeitpunkt die nächste Anweisung eindeutig definiert.
Es gibt keine reale digitale Maschine die nichtdeterministische Algorithmen direkt umsetzten kann.
Ein Beispiel für einen nichtdeterministischen Algorithmus wäre die Wanderung durch ein Labyrinth wobei Sie bei jeder Verzweigung beide Wege zeitgleich ablaufen.
Dies ist nicht möglich, da Sie sich klonen müssten bzw. an zwei Orten gleichzeitig sein müssten.
Verwechseln Sie dies nicht mit der **Parallelität**.
Es ist natürlich möglich, dass sich zwei Personen bei einer Abzweigung trennen.
Nichtdeterminismus bedarf jedoch der Kopie des gesamten Zustands der Maschine!

Determinismus und Determiniertheit hängen zusammen, denn Determiniertheit folgt aus dem Determinismus jedoch folgt aus der Determiniertheit nicht unbedingt der Determinismus.


```

## Software vs. Programm

Ein *Programm* ist in einer Programmiersprache wie ``Python`` geschrieben und kann auf einer Maschine ausgeführt werden.

Eine *Software* besteht in der Regel aus einem oder mehreren Programmen sowie deren Konfigurationsdateien und der Dokumentation. Aus der Systemdokumentation können Entwickler den Aufbau der Software verstehen, insbesondere welche Strukturen vorhanden sind, damit verschiedene Programme ausführbar sind. Die Benutzerdokumentation dient dem Anwender, um zu verstehen, wie er von außen das Programm bedient {cite}`sommerville`.

#TODO: add a picture here

*Programmiercode* auch genannt *Quellcode*, *Source Code* oder kurz *Code*, ist das Resultat der *Programmierung* und Teil eines *Programms*.
Das heißt zur Ausführung des *Quellcodes* fehlt möglicherweise ein Teil des gesamten Codes.

## Berechenbarkeit und Turing-Complete

Eine Teildisziplin der Informatik, die theoretische Informatik, beschäftigt sich unter anderem mit der Berechenbarkeit von Problemen.
Die Frage "Was können wir überhaupt mit einem Computer berechnen?" mag zunächst theoretisch klingen, hat aber für die Praxis ganz erhebliche Auswirkungen.

```{admonition} Berechenbarkeit
:name: def-turing-computable
:class: definition

Ein Problem ist *allgemein berechenbar*, wenn es einen Algorithmus gibt, der für jede gültige Eingabe eine Lösung berechnen kann.
```

Das *Halteproblem* ist das bekannteste Beispiel für ein nicht berechenbares Problem: Es gibt keinen Algorithmus, der für ein beliebiges Programm und eine beliebige Eingabe entscheiden kann, ob das Programm mit dieser Eingabe jemals terminiert (anhält) oder in einer Endlosschleife läuft.

**Wann können wir ein Problem auf einem Computer lösen?**

Nehmen Sie Ihren Taschenrechner: Wie unterscheidet sich dieser von Ihrem Computer?
Ein Taschenrechner kann nur eine begrenzte Menge von Operationen ausführen, wie Addition, Subtraktion, Multiplikation, Division oder das Berechnen von Wurzeln und trigonometrischen Funktionen.
Er ist jedoch nicht in der Lage, beliebige Algorithmen (wie den euklidischen Algorithmus oben) zu implementieren—beispielsweise können Sie auf einem Taschenrechner keine Schleifen programmieren, keine bedingten Verzweigungen definieren oder komplexe Datenstrukturen verwalten.
Ein Computer hingegen kann prinzipiell alle berechenbaren Probleme lösen, da er über die notwendigen Operationen verfügt, um beliebige Algorithmen auszuführen.

```{admonition} Turing-Vollständigkeit
:name: def-turing-complete
:class: definition

Ein System oder eine Programmiersprache ist *Turing-vollständig* (engl. *Turing-complete*), wenn sie all das berechnen kann, was eine [Turingmaschine](info-universal-turing-machine) berechnen kann.
Einfach gesprochen bedeutet dies, dass sie sämtliche Operationen zulässt, sodass prinzipiell jedes berechenbare Problem gelöst werden kann.
Die genaue mathematische Definition ist etwas komplexer und basiert auf dem Konzept der Turingmaschine, einem theoretischen Modell der Berechnung.
```

Moderne Computer und die meisten Programmiersprachen sind Turing-vollständig.
Beispiele für Turing-vollständige Programmiersprachen sind ``Python``, ``Java``, ``C``, ``C++``, ``JavaScript``, ``Ruby`` und viele weitere.
Das bedeutet, dass alle diese Sprachen prinzipiell dieselben Probleme lösen können—der Unterschied liegt lediglich in der Art und Weise, wie wir die Lösung formulieren, und in praktischen Aspekten wie Ausführungsgeschwindigkeit oder Speicherverbrauch.
Im Gegensatz dazu sind einfache Taschenrechner oder sehr eingeschränkte Sprachen wie HTML (ohne JavaScript) oder CSS nicht Turing-vollständig.

