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

(sec-visualization)=
# Kommunikation von Software

Wie kann ich anderen Personen verständlich machen, was mein Programm macht? Wie kann ich anderen Menschen beschreiben, was eine Software tut? Diese Frage steht im Zentrum der Softwareentwicklung, denn Programmieren ist immer auch Kommunikation. Sie wollen einem anderen Menschen Ihre Idee, Ihr Konzept begreiflich machen.

## Lernziele

Nach diesem Abschnitt können Sie …

- erklären, warum Programmieren auch **Kommunikation** ist (Zielgruppe, Zweck, Abstraktionsgrad).
- einen einfachen Algorithmus in **Pseudocode** ausdrücken.
- die Grundideen von **Struktogrammen** (Sequenz, Fallunterscheidung, Schleife) erkennen und einsetzen.
- das passende Kommunikationsmedium (Code, Skizze, Diagramm) für eine Situation begründet auswählen.

Es gibt viele verschiedene Wege, Software und Algorithmen zu kommunizieren.
Jede Methode hat ihre Stärken und ist für bestimmte Aspekte und Zielgruppen geeignet:

- **Flussdiagramme**: Visuelle Darstellung des Programmablaufs mit verschiedenen Symbolen. Gut für den Überblick über den gesamten Ablauf, weniger geeignet für komplexe verschachtelte Strukturen.

- **Pseudocode**: Eine einfache, weniger strikte Beschreibung eines Algorithmus in einer Sprache, die der natürlichen Sprache ähnelt (siehe [Definition](def-pseudocode)). Ideal, wenn Sie sprachenübergreifend kommunizieren möchten oder den Algorithmus konzeptionell beschreiben wollen.

- **Struktogramme** (Nassi-Shneiderman-Diagramme): Visuelle Darstellung strukturierter Algorithmen, bei der die Kontrollstruktur und der Ablauf auf einen Blick erkennbar sind. Besonders geeignet für strukturierte Algorithmen mit wenigen Schritten.

- **Skizzen**: Freihand-Zeichnungen, die schnell erstellt werden können. Perfekt für den ersten Entwurf, Brainstorming und die Kommunikation mit nicht-technischen Stakeholdern. **Malen Sie!**

- **Videos**: Bewegte Darstellungen, z.B. durch Tanzen (hier ein [Sortieralgorithmus](https://youtu.be/lyZQPjUT5B4?si=CaIJa_HSt4pSRtwi)). Sehr anschaulich, aber aufwendig zu erstellen.

- **Sequenzdiagramme**: Zeigen die Interaktion zwischen verschiedenen Komponenten oder Objekten über die Zeit. Ideal für die Kommunikation von Systemarchitekturen und Kommunikationsabläufen.

- **Komponentendarstellungen**: Zeigen die Struktur und Beziehungen zwischen verschiedenen Komponenten einer Software. Gut für die Architekturkommunikation.

- **Klassendiagramme**: Zeigen die Struktur von Klassen und deren Beziehungen in objektorientierten Systemen. Wichtig für die Kommunikation von Softwarearchitekturen.

- **Programmcode**: Wenn Ihr Gegenüber die gleiche Programmiersprache beherrscht, kann der Code selbst die beste Kommunikationsform sein. Direkt ausführbar und unmissverständlich.

Eine Übersicht über Diagramme, die im Systems und Software Engineering klassischerweise zum Einsatz kommen, finden Sie beispielsweise in der [Systems Modeling Language (SysML)](https://de.wikipedia.org/wiki/Systems_Modeling_Language).

```{admonition} Wahl des Kommunikationsmediums
:name: hint-kommunikationsmedium
:class: hint

Die Wahl des Kommunikationsmediums hängt dabei von zwei zentralen Faktoren ab:

1. **Was möchte ich kommunizieren?** 
   - Die Gesamtarchitektur einer Software?
   - Den Ablauf eines Algorithmus?
   - Einen Teilablauf oder eine spezifische Funktion?
   - Die Datenstrukturen und deren Beziehungen?
   - Die Interaktion zwischen Komponenten?

2. **Was kennt mein Publikum?**
   - Beherrscht mein Gegenüber die gleiche Programmiersprache?
   - Kennt mein Gegenüber Struktogramme, Flussdiagramme oder UML?
   - Ist mein Gegenüber ein Programmieranfänger oder erfahrener Entwickler?
   - Arbeitet mein Gegenüber eher visuell oder textuell?

Je nach Zweck und Zielgruppe werden Sie ein bestimmtes Kommunikationsmedium auswählen: 
Wenn Ihr Gegenüber keine Struktogramme kennt, aber Sie beide in der gleichen Programmiersprache programmieren: Warum nicht einfach den Algorithmus in Ihrer Programmiersprache ausdrücken?
```

Im Rahmen dieser Vorlesung lernen wir Struktogramme und Pseudocode als Kommunikationswege kennen. Diese eignen sich für strukturierte Algorithmen, bei denen nur wenige Schritte nacheinander ausgeführt werden. 

## Struktogramme

Struktogramme, auch Nassi-Shneiderman-Diagramme genannt, sind eine visuelle Darstellungsform für strukturierte Algorithmen.
Sie ermöglichen es, mit dem Auge schnell zu erkennen, wie die Kontrollstruktur und der Ablauf in einem Programm aussehen.
Die Grundidee ist, dass jede Kontrollstruktur durch ein Rechteck dargestellt wird, das wiederum andere Rechtecke enthalten kann.
Die Verschachtelung macht die Struktur des Algorithmus visuell erkennbar.

Struktogramme verwenden folgende Grundstrukturen:

1. **Sequenz**: Anweisungen werden nacheinander in einem Rechteck untereinander geschrieben.
2. **Fallunterscheidung**: Ein Rechteck wird durch eine Bedingung geteilt; der obere Teil enthält die Bedingung, der untere Teil die Anweisungen für den Fall, dass die Bedingung erfüllt ist.
3. **Schleife**: Ein Rechteck mit einer Bedingung, die angibt, wann die Schleife wiederholt wird.

```{figure} ../../figs/struktogrammtypen.png
---
width: 600px
name: fig-struktogrammtypen
---
Die Grundstrukturen von Struktogrammen: Sequenz, Fallunterscheidung und Schleife.
```

```{admonition} Achtung
:name: warning-struktogramme
:class: warning

Struktogramme sind Entwurfswerkzeuge für strukturierte Algorithmen (wenige, nacheinander ablaufende Schritte). Sie werden in der strukturierten Programmierung eingesetzt, eine der drei "Programmierstile".

Struktogramme sind weniger geeignet für:
- Sehr komplexe, tief verschachtelte Algorithmen (werden schnell unübersichtlich)!!
```

```{admonition} Achtung
:name: warning-struktogramme-pruefung
:class: warning

Struktogramme sind prüfungsrelevant!
```


## Pseudocode

*Pseudocode* ist eine einfache, weniger strikte Beschreibung eines Algorithmus in einer Sprache, die der natürlichen Sprache ähnelt (siehe [Definition](def-pseudocode)).
Mit Pseudocode können wir einen Algorithmus in einer Sprache beschreiben, die keine bestimmte Programmiersprache zur Basis hat.

Pseudocode steht zwischen der natürlichen Sprache und einer Programmiersprache:
- Er ist präziser als natürliche Sprache, aber weniger strikt als Programmcode
- Er orientiert sich an der Syntax von Programmiersprachen, ist aber sprachenübergreifend verwendbar
- Er erlaubt es, sich auf die Logik des Algorithmus zu konzentrieren, ohne sich mit sprachspezifischen Details auseinandersetzen zu müssen

## Beispiel: Gleicher Algorithmus in verschiedenen Darstellungen

Betrachten wir einen einfachen Algorithmus, der das Maximum einer Liste von Zahlen findet.
Wir stellen ihn in drei verschiedenen Formen dar:

**Pseudocode:**
```
FUNCTION finde_maximum(liste):
    WENN liste leer:
        GIB Fehler zurück
    ENDE WENN
    
    maximum = erstes Element der liste
    
    FÜR jedes element IN liste:
        WENN element > maximum:
            maximum = element
        ENDE WENN
    ENDE FÜR
    
    GIB maximum zurück
ENDE FUNKTION
```

**Struktogramm:**

```{figure} ../../figs/struktogramm-example.png
---
width: 600px
name: fig-struktogramm-example
---
Struktogramm für den Algorithmus zur Bestimmung des Maximums einer Liste.
```

**Python-Code:**

```{code-cell} python3
def finde_maximum(liste):
    if not liste:
        raise ValueError("Liste ist leer")
    
    maximum = liste[0]
    
    for element in liste:
        if element > maximum:
            maximum = element
    
    return maximum

# Beispiel
zahlen = [3, 7, 2, 9, 1, 5]
print(f"Das Maximum von {zahlen} ist {finde_maximum(zahlen)}")
```

Sie haben nur 3 Wege gesehen wie man einen Algorithmus kommunizieren kann. 

```{admonition} Dokumentation in der Praxis
:name: remark-dokumentation-praxis
:class: remark

In der Praxis werden Sie vor allem auf Sequenzdiagramme und Paketdiagramme treffen.
Diese Diagrammtypen stellen häufig Softwarearchitekturen dar, die allein aus dem Quellcode nicht mehr ersichtlich sind.

Ein wichtiger Grundsatz der Dokumentation lautet: **Dokumentiert und visualisiert wird all das, was nicht direkt aus dem Quellcode hervorgeht.**

Ist ein Algorithmus einmal implementiert, benötigen Sie sein Struktogramm in der Regel nicht mehr in der Dokumentation — die Implementierung im Quellcode reicht aus (sofern der Algorithmus korrekt implementiert wurde).
Das bedeutet jedoch nicht, dass der Entwickler beim Entwurf des Algorithmus kein Struktogramm verwendet hat.
Struktogramme und Pseudocode sind wichtige Werkzeuge während der Entwicklung, auch wenn sie später nicht in der finalen Dokumentation erscheinen.
```

## Mini-Übung (mit Lösung)

```{exercise} Medium wählen und Algorithmus kurz ausdrücken
:label: ex-visualization-medium

Sie möchten einer Kommilitonin erklären, was diese Funktion macht, **ohne** Python-Syntax im Detail zu besprechen:

> „Gegeben ist eine Liste von Zahlen. Gib die größte Zahl zurück. Falls die Liste leer ist, gib einen Fehler aus.“

1. Welches Kommunikationsmedium wählen Sie (Pseudocode, Struktogramm oder Python-Code) – und warum?
2. Schreiben Sie den Algorithmus in 5–10 Zeilen **Pseudocode**.
```

```{solution} ex-visualization-medium
:class: dropdown

1. **Pseudocode** ist hier gut geeignet, weil er sprachenübergreifend ist und die Logik klar zeigt, ohne syntaktische Details.
2. Beispiel-Pseudocode:

   - Wenn die Liste leer ist: Fehler zurückgeben
   - maximum = erstes Element
   - Für jedes Element in der Liste:
     - Wenn Element > maximum: maximum = Element
   - maximum zurückgeben
```
