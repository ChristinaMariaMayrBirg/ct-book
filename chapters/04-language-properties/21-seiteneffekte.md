# Seiteneffekte

Wie wir im Kapitel [Speicherverwaltung in Python](sec-memory-management) gesehen haben, verwendet ``Python`` Zeiger (Referenzen) für die Speicherverwaltung.
Wenn Sie eine Variable erstellen, zeigt diese Variable auf einen Speicherbereich, in dem der Wert gespeichert ist.
Das bedeutet aber auch, dass mehrere Variablen auf denselben Wert zeigen können.

Diese Eigenschaft hat eine wichtige Konsequenz: Wenn mehrere Variablen auf dasselbe Objekt im Speicher zeigen, können alle diese Variablen den Wert unter bestimmten Umständen ändern.
Wenn Sie beispielsweise eine Liste an eine Funktion übergeben, zeigt der Funktionsparameter auf dasselbe Objekt im Speicher wie die ursprüngliche Variable.
Änderungen an der Liste innerhalb der Funktion wirken sich daher auch auf die ursprüngliche Liste aus - dies nennt man einen *Seiteneffekt*.

Python erlaubt Seiteneffekte - im Gegensatz zu Sprachen wie Haskell. Deshalb gehen wir im Folgenden kurz auf dieses wichtige Prinzip ein.

```{admonition} Seiteneffekt
:name: def-side-effect
:class: definition
Ein *Seiteneffekt* liegt vor, wenn die Ausführung einer isolierten Funktionalität (einer Funktion) neben der Berechnung des Rückgabewerts einen Zustand außerhalb ihres Gültigkeitsbereichs verändert und/oder von einem solchen Zustand abhängt.
```

**Beispiel 1: Funktion MIT Seiteneffekt (Standard-Verhalten)**

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
Damit können wir beliebig oft die Liste erweitern. Wenn wir das wollen sind wir fertig.

**Beispiel 2: Funktion OHNE Seiteneffekt**

Was wir damit aber nicht können sind zwei voneinander unabhängige Listen erstellen:

liste1 = 1 2 3 4
liste2 = 1 2 3 5

Um das zu realisieren müssten wir erreichen, dass die ursprüngliche liste verwendet wird, nicht die bereits erweiterte. Auch das ist in python möglich, indem wir eine copy anlegen.


```{code-cell} python
meine_liste = [1, 2, 3]  # Liste außerhalb der Funktion

def erweitere_liste_ohne_seiteneffekt(liste, element):
    """Erstellt eine neue Liste mit dem zusätzlichen Element"""
    neue_liste = liste.copy()  # Erstellt eine Kopie der ursprünglichen Liste
    neue_liste.append(element)  # Fügt das Element zur Kopie hinzu
    return neue_liste

ergebnis = erweitere_liste_ohne_seiteneffekt(meine_liste, 4)
print("Ergebnis:", ergebnis)  # Ausgabe: [1, 2, 3, 4]
print("Originale Liste:", meine_liste)  # Ausgabe: [1, 2, 3] - unverändert!
```

In diesem Fall lässt die Funktion die Ausgangsliste unverändert. In Fachsprache spricht man davon, dass hier kein Seiteneffekt vorliegt.

Anmerkung: In funktionalen Programmiersprachen wie Haskell sind Seiteneffekte nicht erlaubt. Hier sind nur Funktionen ohne Seiteneffekte erlaubt. 

Hinweis:
Funktionen die Seiteneffekt zulassen werde in der Informatik als unreine Funktionen bezeichnet. Funktionen ohne Seiteneffekt als rein.

## Aber warum wollen wir Python Seiteneffekte?

Auf den ersten Blick wirken Seiteneffekte gefährlich: Eine Funktion verändert etwas außerhalb ihres Gültigkeitsbereichs - das kann unerwartet sein und zu Fehlern führen. Warum erlaubt Python sie dann?

**Seiteneffekte sind praktisch, weil:**

1. **Effizienz**: Statt große Datenstrukturen zu kopieren, können wir direkt auf das Original zugreifen und es modifizieren. Das spart Speicher und Rechenzeit.

2. **Natürliche Modellierung**: Viele reale Probleme haben Zustände, die sich ändern (z.B. ein Bankkonto, eine Einkaufsliste, eine Datenbank). Seiteneffekte erlauben es, diese Zustandsänderungen direkt zu modellieren.


**Der Kompromiss:** Python wählt bewusst Flexibilität und Praktikabilität über strikte Reinheit. Sie als Programmierer müssen darauf achten, wann Seiteneffekte auftreten können, um unerwartete Verhaltensweisen zu vermeiden.

Dass Python Seiteneffekte zulässt, ist also eine bewusste Designentscheidung der Entwickler der Programmiersprache. 

## Warum geht das überhaupt in Python?

**Drei Voraussetzungen** müssen erfüllt sein, damit ein Seiteneffekt entstehen kann:

1. Es gibt einen Zustand (Speicher, Datei, Objekt)
2. Der Zustand kann verändert werden
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

In diesem Beispiel haben wir einen Zustand, ein veränderliches object (warum das veränderlich ist lernen Sie im Kapitel Datentypen) + unterschiedliche programmteile die darauf zugreifen können.

