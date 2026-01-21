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

(sec-euclid-alg)=
# Algorithmen - Zusatz

Um 1950 herum deutete der Begriff auf Euklid's berühmten Algorithmus zum finden des größten gemeinsamen Teilers.

Lassen Sie uns den ersten aller noch heute relevanten Algorithmen betrachten: Den *Euklidischen Algorithmus*.

```{exercise} Euklidischer Algorithmus
:label: euclid-exercise

Gegeben seien zwei natürliche Zahlen $n, m \in \mathbb{N}$.
Wir suchen nach dem größten gemeinsamen Teiler $\text{ggT}(n,m)$ von $n$ und $m$, d.h., die größte natürliche Zahl die sowohl $n$ als auch $m$ teilt.
```

Der $\text{ggT}(44,12)$ von $44$ und $12$ ist zum Beispiel $4$.
Wie vieles bei den Griechen ist der Algorithmus geometrisch motiviert.
Euklid berechnet den ggT, indem er nach einem gemeinsamen "Maß" für die Längen zweier Linien sucht.
Dazu zieht er wiederholt die kleiner der beiden Längen von der größeren ab.
Der ggT verändert sich dadurch nicht.

```{admonition} Gesetzt des größter gemeinsamer Teiler
:name: theorem-ggt
:class: theorem

Seien $n$, $m$ zwei natürliche Zahlen mit $n > m$ und $d = n - m$, so ist der *größte gemeinsame Teiler* von $n$, $m$ und $d$ identisch.
```

```{admonition} Beweis
:name: proof-theorem-ggt
:class: proof dropdown

Jede natürliche Zahl kann als Produkt ihrer Primfaktorzerlegung geschrieben werden.
Der $\text{ggT}(n,m)$ ergibt sich aus der Multiplikation aller Primzahlen die in beiden Zerlegungen (möglicherweise mehrfach) vorkommen.

Zum Beispiel ist: $44 = (2 \cdot 2) \cdot 11$ und $12 = (2 \cdot 2) \cdot 3$ und ihr $\text{ggT}(44,12) = 2 \cdot 2$.

Seien nun 

$$n = p_1 \cdot \ldots \cdot p_k \cdot q_1$$ 

und 

$$m = p_1 \cdot \ldots \cdot p_k \cdot q_2,$$

wobei $p_1, \ldots, p_k$ die $k$ gleichen Primzahlen der Zerlegungen sind. Dann folgt 

$$d = n - m = (p_1 \cdot \ldots \cdot p_k) \cdot (q_1 - q_2)$$

und somit gilt 

$$\text{ggT}(n,m) = \text{ggT}(d,m) = \text{ggT}(n,d) = (p_1 \cdot \ldots \cdot p_k).$$
```

## Version 1

Aus dem Gesetz des größter gemeinsamer Teiler, folgt der euklidische Algorithmus.
Wir starten mit zwei Zahlen, und ziehen solange immer und immer wieder die kleinere von der größeren ab, bis beide Zahlen gleich sind.
Das Ergebnis ist der größter gemeinsame Teiler der beiden ursprünglichen Zahlen!

Gehen wir wie Euklid vor und beschreiben diese Vorgehensweise in Pseudocode:

```
n <- c0
m <- c1
Solange m ungleich n:
  n <- n - m
  Falls m > n:
    t <- m
    m <- n
    n <- t
```

Dabei sind ``c0`` und ``c1`` irgendwelche natürliche Zahlen wobei ``c0`` größer gleich ``c1`` sein muss.
Überführen wir diesen Code in ein ``Python``-Programm um.
Durch die [Restwertdivision](def-euclid-division) können ``m nicht n teilt`` in ``Python`` realisieren:

```{code-cell} python3
def gcd(n,m):
    while n != m: # Solange m ungleich n
        n = n - m
        if m > n:
          t = m
          m = n
          n = t
    return m

gcd(544, 119)
```

Die Funktion ``gcd`` hat zwei Parameter ``n`` und ``m`` die mit den Argumenten ``544`` und ``119`` initialisiert werden.
Implizit wird angenommen, dass ``n > m`` gilt.
Nachdem die ``while``-Schleife (Wiederholung) verlassen wird, gibt die Funktion ``m`` zurück.

Zuweisungen werden in den allermeisten Programmiersprachen anstatt mit ``<-`` mit dem ``=`` durchgeführt (siehe auch Abschnitt [Initialisierung und Zuweisung](sec-assignment)).
Das mathematische $=$ wird aufgrund dessen mit ``==`` ausgedrückt.

## Version 2

Da uns die [Restwertdivision](def-euclid-division) als Operation zur Verfügung steht, können wir die wiederholte Subtraktion beschleunigen.
Anstatt zum Beispiel ``43 - 11 - 11 - 11 == 10`` zu rechnen ergibt ``43 % 11 == 10``.
Diese Operation steht Ihnen in allen gängigen Programmiersprachen zur Verfügung und kann auf dem Computer sehr schnell ausgeführt werden.

Dadurch vereinfacht sich der euklidische Algorithmus zu:

```
n <- c0
m <- c1
Solange m > 0:
    r <- n % m
    n <- m
    m <- r
```


Die Anweisungen werden von oben nach unten ausgeführt, wobei ``Solange`` eine Wiederholung markiert.
Alles was unter dieser Anweisung eingerückt steht, wird wiederholt, solange die Bedingung ``m > 0`` gilt.
Nach diesen Schritten ist der Wert auf den die Variable ``n``  verweist, der größten gemeinsamen Teiler (ggT) von ``c0`` und ``c1``.
Die Operation ``n % m`` berechnet den Rest der [Restwertdivision](def-euclid-division).
Unter ``r <- n % m`` verstehen wir die Zuweisung des Wertes ``n % m`` zur Variablen ``r``.

Um einen Algorithmus zu verstehen hilft es oft ihn auszuführen.
Wir möchten den ggT von $544$ und $119$ bestimmen.
Wir beginnen mit 
1. $n \leftarrow 544$
2. $m \leftarrow 119$.
  
Wir treten in die Wiederholung ein, da $m > 0$ gilt. Es ergibt sich:
1. $r \leftarrow 68$ 
2. $n \leftarrow 119$
3. $m \leftarrow 68$

Erneut treten wir in die Wiederholung ein, da weiterhin $m > 0$ gilt. Es ergibt sich:
1. $r \leftarrow 51$ 
2. $n \leftarrow 68$
3. $m \leftarrow 51$

Erneut treten wir in die Wiederholung ein, da weiterhin $m > 0$ gilt. Es ergibt sich:
1. $r \leftarrow 17$ 
2. $n \leftarrow 51$
3. $m \leftarrow 17$

Erneut treten wir in die Wiederholung ein, da weiterhin $m > 0$ gilt. Es ergibt sich:
1. $r \leftarrow 0$ 
2. $n \leftarrow 17$
3. $m \leftarrow 0$

Da nun $m$ den Wert $0$ hat, verlassen wir die Wiederholung und das Ergebnis steht in $n$.

Lassen Sie uns den Algorithmus in reneut in ein ``Python``-Programm überführen:

```{code-cell} python3
def gcd(n,m):
    while m > 0:
        r = n % m
        n = m
        m = r
    return n

gcd(544, 119)
```

Die Funktion ``gcd`` hat zwei Parameter ``n`` und ``m`` die mit den Argumenten ``544`` und ``119`` initialisiert werden.
Nachdem die ``while``-Schleife (Wiederholung) verlassen wird, gibt die Funktion ``n`` zurück.

## Version 3

In ``Python`` können wir das Vertauschen der Variablen durch [Tupel](sec-tuple) und das sog. *Packing/Unpacking* kürzer schreiben.
Auch ist die Bedingung einer ``while``-Schleife wahr sofern eine ganze Zahl nicht gleich 0 ist.
Daraus ergibt sich die sehr kurze Version 3:

```{code-cell} python3
def gcd(a,b):
    while b:
        a, b = b, a % b
    return a

gcd(544, 119)
```

Alle drei Versionen berechnen den ggT, also den gleichen Wert.
Version 1 und 2 unterscheiden sich [semantisch](def-semantik) wohingegen Version 2 und 3 sich lediglich [syntaktisch](def-syntax) unterscheiden.
Das sind also Algorithmen.
