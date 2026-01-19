# Seiteneffekt

```{admonition} Behauptung
:class: remark
In Python verhalten sich Funktionen immer gleich.
```

Eine *Funktion* ist ein benannter Codeblock, den Sie aufrufen können. Typischerweise bekommt sie **Eingaben** (Parameter) und liefert einen **Rückgabewert** zurück. 

Sehen Sie sich das folgende Beispiel an:

```{code-cell} python
def addiere(a, b):
    return a + b  

x = addiere(2, 3)
print("Rückgabewert:", x)
```
In dem Beispiel wird die Funktion `addiere` aufgerufen. Die Werte werden addiert und dann zurückgegeben. Das entspricht im Prinzip der Vorstellung einer mathematischen Funktion: Ich gebe \(x\) hinein und erhalte \(y\) zurück.

In Python kann es jetzt zusätzlich vorkommen, dass eine Funktion \(x\) mitverändert. Man spricht davon dass ein Zustand (\(x\) ) außerhalb der Funktion geändert wird ("Es gibt einen Seiteneffekt"). Das passiert aber nur dann, wenn Sie **veränderliche (mutierbare)** Objekte als \(x\) haben. 

```{admonition} Seiteneffekt
:name: def-side-effect
:class: definition
Ein *Seiteneffekt* liegt vor, wenn die Ausführung einer isolierten Funktionalität (einer Funktion) neben der Berechnung des Rückgabewerts einen Zustand außerhalb ihres Gültigkeitsbereichs verändert und/oder von einem solchen Zustand abhängt.
```

Python übergibt beim Funktionsaufruf **keine Kopien von Objekten**, sondern **Referenzen auf Objekte** (auch: *call‑by‑sharing*, *object references*).
Das heißt: Parameter sind **neue Namen**, die auf **dieselben Objekte** gebunden werden können wie beim Aufrufer. Der Grund dafür wiederum liegt im Python‑Datenmodell: **Namen referenzieren Objekte** und Funktionsaufrufe übergeben nicht die Objekte selbst sondern ebeen die Referenz.

```{admonition} Profiwissen
:name: uebergabemechanismen
:class: tip
Neben Python‑„object references“ gibt es in anderen Sprachen:
- **Pass by Value (Wertübergabe)**: Kopie wird übergeben; Änderungen in der Funktion betreffen das Original nicht.
- **Pass by Reference (Referenzübergabe)**: Eine Referenz/Adresse wird so übergeben, dass die Funktion auch den *Aufrufer‑Bezug* direkt verändern kann (z.B. C++ mit `&`).
```

Zwei Mini‑Beispiele:

Funktion mit Seiteneffekt (mutiert das Argument)

```{code-cell} python
meine_liste = [1, 2, 3]  # Liste außerhalb der Funktion

def erweitere_liste_mit_seiteneffekt(liste, element):
    """Modifiziert die übergebene Liste direkt"""
    liste.append(element)  # Verändert die Liste außerhalb der Funktion!
    return liste

ergebnis = erweitere_liste_mit_seiteneffekt(meine_liste, 4)
print("Ergebnis:", ergebnis)  # Ausgabe: [1, 2, 3, 4]
print("Originale Liste:", meine_liste)  # Ausgabe: [1, 2, 3, 4] - wurde verändert!
```

Funktion ohne Seiteneffekt (arbeitet mit Kopie)

```{code-cell} python
meine_liste = [1, 2, 3]  # Liste außerhalb der Funktion

def erweitere_liste_ohne_seiteneffekt(liste, element):
    """Erstellt eine neue Liste mit dem zusätzlichen Element"""
    neue_liste = liste.copy()  # Kopie der ursprünglichen Liste
    neue_liste.append(element)  # Fügt das Element zur Kopie hinzu
    return neue_liste

ergebnis = erweitere_liste_ohne_seiteneffekt(meine_liste, 4)
print("Ergebnis:", ergebnis)  # Ausgabe: [1, 2, 3, 4]
print("Originale Liste:", meine_liste)  # Ausgabe: [1, 2, 3] - unverändert!
```

In diesem Fall bleibt der Zustand außerhalb der Funktion unverändert – es liegt kein Seiteneffekt vor. In der Informatik spricht man hier auch von reinen (ohne Seiteneffekt) bzw. unreinen Funktionen (mit Seiteneffekt).

Wann tritt ein Seiteneffekt ein?

Drei Voraussetzungen müssen erfüllt sein, damit ein Seiteneffekt entstehen kann:

1. Es gibt einen Zustand (Speicher, Datei, Objekt)
2. Der Zustand kann verändert werden - ob das möglich ist hängt von den Eigenschaften ihres \(x\) ab! 
3. Der Zustand ist geteilt - mehr als ein Programmteil kann denselben Zustand beobachten oder verändern

Stellen Sie sich vor: Wir haben ein Haus (Objekt) in einer Stadt (Speicher). Julia und Hannes haben jeweils einen Zettel, auf dem die Adresse zum Haus steht. Sowohl Julias Zettel (`zettel_julia`) als auch Hannes' Zettel (`zettel_hannes`) referenzieren auf dasselbe Haus. Julia baut das Erdgeschoss um (Seiteneffekt). Hannes kommt zurück und wundert sich, was da passiert ist.

**Wichtig an dieser Stelle:** Beide Zettel zeigen auf dasselbe Objekt (sie referenzieren auf dasselbe). Wenn Julia das Haus verändert, sieht Hannes die Änderung auch, weil beide auf dasselbe Objekt verweisen. Das ist genau das, was bei Python-Objekten passiert, wenn sie per Referenz übergeben werden.

```{code-cell} python
# Analogie: Haus (Objekt) in der Stadt (Speicher)
haus = {"stockwerke": 2, "farbe": "weiß"}  # Das Haus

# Julia und Hannes haben Zettel mit der Adresse (Referenz)
zettel_julia = haus
zettel_hannes = haus

print("Vorher - Julia sieht:", zettel_julia)
print("Vorher - Hannes sieht:", zettel_hannes)

# Julia baut um (Seiteneffekt - verändert das Objekt)
zettel_julia["stockwerke"] = 3
zettel_julia["farbe"] = "gelb"

print("\nNachher - Julia sieht:", zettel_julia)
print("Nachher - Hannes sieht:", zettel_hannes)  # Hannes sieht die Änderung auch!
print("\nBeide zeigen auf dasselbe Objekt:", zettel_julia is zettel_hannes)
```

```{admonition} Klarstellung
:class: note
- Funktionen in Python können Seiteneffekte haben – das ist erlaubt und oft gewollt.
- Seiteneffekte entstehen bei mutierbaren Objekten (z.B. `list`, `dict`). Mehr dazu im Kapitel [Datentypen](../08-python-data-types/0-intro.md).
- Wenn Sie keine Seiteneffekte wollen, arbeiten Sie z.B. mit Kopien.
```

