# Multiparadigmen

```{admonition} Behauptung
:class: remark
„Python ist objektorientiert.“
```

Diese Aussage liest man oft – und sie ist „halb richtig“. Python **ermöglicht** objektorientierte Programmierung sehr gut, ist aber gleichzeitig **multiparadigmatisch**.

**Was genau hat es damit auf sich?**

Ein Programmierparadigma kann man sich wie einen Programmierstil vorstellen: eine bestimmte Art, wie man eine Funktionalität in Programmcode niederschreibt und strukturiert. Paradigmen sind dabei weitgehend unabhängig von der konkreten Sprache – eine Sprache kann ein Paradigma stärker „nahelegen“, aber oft mehrere unterstützen.

Drei wichtige Paradigmen sind (vgl. {cite}`martin:2017clean`):

- Strukturierte/Prozedurale Programmierung
- Funktionale Programmierung
- Objektorientierte Programmierung

Für dieselbe Aufgabe gibt es daher oft mehrere „richtige“ Implementierungen – abhängig vom Stil, den man wählt. Und selbst innerhalb eines Stils gibt es meist mehrere Lösungen. Diese müssen Sie nicht alle lernen oder beherrschen, aber Sie sollten nicht überrascht sein, wenn Code manchmal ganz anders aussieht.

Beispiel: Quadrat einer Zahl berechnen 

```python
def quadrat_strukturiert(x: int) -> int:
    return x * x

quadrat_funktional = lambda x: x * x

class QuadratRechner:
    def __init__(self, x: int):
        self.x = x

    def berechne(self) -> int:
        return self.x * self.x

if __name__ == "__main__":
    print(quadrat_strukturiert(5))        # 25
    print(quadrat_funktional(5))          # 25
    print(QuadratRechner(5).berechne())   # 25
```

```{admonition} Wichtig
:class: important
:name: important-paradigm-choice
Wir werden in diesem Modul vor allem strukturiert/prozedural programmieren.
```
Wie Sie im Beispiel gesehen haben, erlaubt uns Python, dass wir sowohl prozedural, funktional als auch objekt-orientiert programmieren. 

```{admonition} Klarstellung
:class: note

- **Python ist sehr gut für objektorientierte Programmierung geeignet**, aber nicht darauf beschränkt.
- **Python ist multiparadigmatisch**: strukturiert, funktional und objektorientiert sind möglich – es unterstützt objektorientierte, funktionale und strukturierte Programmierung. Viele Bibliotheken und Konventionen sind jedoch objektorientiert geprägt.
- In der Praxis ist weniger wichtig, „welches Paradigma richtig ist“, sondern **welches Modell Ihr Problem am klarsten beschreibt**.
```