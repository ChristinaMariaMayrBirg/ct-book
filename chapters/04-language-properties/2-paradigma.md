# Programmierparadigmen

Es gibt verschiedene Stile, wie man einen Algorithmus implementieren kann. Diese Stile werden in der Fachsprache als **Programmierparadigmen** bezeichnet. Sie sind unabhängig von einer Programmiersprache!

Die drei wichtigsten Programmierparadigmen sind:

- **Strukturierte Programmierung**
- **Funktionale Programmierung**
- **Objektorientierte Programmierung**

## Beispiel: Quadrat einer Zahl berechnen

Wir berechnen das Quadrat einer Zahl in Python - einmal für jedes Paradigma:

### Strukturierte Programmierung

```python
def square_number(zahl):
    ergebnis = zahl * zahl
    return ergebnis

if __name__ == "__main__":
    x = 5
    quadrat_von_x = square_number(x)
    print(quadrat_von_x)  # Ausgabe: 25
```

### Funktionale Programmierung

```python
# Funktionale Programmierung mit Lambda
quadrat_funktional = lambda z: z * z

if __name__ == "__main__":
    quadrat_von_5 = quadrat_funktional(5)
    print(quadrat_von_5)  # Ausgabe: 25
```

### Objektorientierte Programmierung

**Variante 1: Mit Instanzmethode**

```python
# Objektorientierte Programmierung
class QuadratRechner:
    def __init__(self, zahl):
        self.zahl = zahl
    
    def berechne(self):
        return self.zahl * self.zahl

if __name__ == "__main__":
    rechner = QuadratRechner(5)
    ergebnis = rechner.berechne()
    print(ergebnis)  # Ausgabe: 25
```

**Variante 2: Mit Klassenmethode**

```python
# Objektorientierte Programmierung mit Klassenmethode
class QuadratRechner:
    @classmethod
    def berechne(cls, zahl):
        return zahl * zahl

if __name__ == "__main__":
    ergebnis = QuadratRechner.berechne(5)
    print(ergebnis)  # Ausgabe: 25
```

```{admonition} Wichtig
:class: important
:name: important-paradigm-choice
Wir haben jetzt 4 Wege gesehen, wie man in Python eine Funktionalität implementieren kann. Und es gibt viele weitere! Welcher Weg für Ihre Problemstellung am geeignesten ist, müssen Sie entscheiden. In diesem Kurs liegt der Fokus vor allem auf der strukturierten Programmierung.
```

```{admonition} Hinweis
:class: remark
:name: remark-python-paradigms
Python wird oft als objektorientierte Sprache bezeichnet. Das ist nicht ganz korrekt: Python ermöglicht objektorientierte Programmierung, aber auch funktionale und strukturierte Programmierung, wie wir im Beispiel gesehen haben. Python wurde so entwickelt, dass objektorientierte Strukturen besonders effizient ausgeführt werden können.
```

# Architectural and Design Patterns

Am obigen Beispiel haben wir gesehen, dass es viele Wege gibt, eine Funktionalität zu implementieren. Dort gab es nur eine Funktionalität (eine Zahl quadrieren), die nur einmal genutzt wurde.

## Das Problem bei größeren Softwareprojekten

In einer Software gibt es üblicherweise 1000 oder 100.000 Funktionalitäten, von denen vielleicht nur ein Bruchteil aufgerufen wird. Stellen Sie sich Word vor: Dort können Sie die Schriftgröße und die Farbe ändern. Sie können aber auch das Dokument drucken. Nicht immer wird der Nutzer alle Funktionalitäten nutzen. Damit er überhaupt einen Überblick behalten kann, sind die Funktionalitäten in unterschiedlichen Kacheln (Menüs) organisiert.

Ähnlich ist es mit Software: Damit sich Programmierer\*innen darin zurechtfinden, verwendet man bestimmte Strategien. Bestimmte Software-Funktionalitäten werden auf eine bestimmte Art und Weise an einem bestimmten Ort, also nach einem bestimmten **Muster**, in der Software abgelegt - man spricht daher auch von **Design Patterns**.

## Vorteile von Design Patterns

Das Nutzen von Design Patterns sorgt dafür:

- **Korrekte Verwendung:** Funktionalitäten werden nur dafür eingesetzt, wofür sie gedacht sind
- **Arbeitsteilung:** Die Entwicklung von Funktionalitäten kann aufgeteilt werden. Jeder übernimmt eine Funktionalität. Das Zusammenspiel ist über das Design Pattern festgelegt. Jeder weiß, wie er "mitmachen darf"
- **Stabilität:** Instabile Programme werden vermieden. Design Patterns sind die Umsetzung von Strategien, bei denen sich herausgestellt hat, dass die Software weniger häufig abstürzt und schneller erweitert werden kann

```{admonition} Profi-Tipp
:class: tip
:name: tip-design-patterns
Wenn Sie Software entwickeln wollen, die skalierbar ist, die erweitert werden kann, also nachhaltig ist: Lernen Sie Design Patterns und lernen Sie, wie die Design Patterns in Ihrer Programmiersprache umgesetzt werden!

Wissen über Software-Architektur und die richtige Anwendung von Design Patterns ist Grundlage des Sustainable Software Engineering.
```
