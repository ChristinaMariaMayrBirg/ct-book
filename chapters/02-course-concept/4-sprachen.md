# Programmiersprachen

Es existiert eine Vielzahl an Programmiersprachen. Es gibt nicht die beste Programmiersprache! 
Welche Programmiersprache Sie verwenden hängt immer von ihrem Problem ab! 
Ein guter Softwareentwickler kennt viele Programmiersprachen und entscheidet abhängig vom Problem welche dafür geeignet ist.





Was heißt es, eine Programmiersprache zu lernen?

Eine Programmiersprache zu lernen bedeutet, dass wir:

- den **Syntax** der Sprache ("die Grammatik") und deren **Semantik** ("die Bedeutung") verstehen
- deren **Konzepte** kennen und anwenden können


## Syntax

Die Syntax einer Programmiersprache beschreibt die Regeln, wie Code geschrieben werden muss. Ein Vergleich zwischen "Hello World" in C und Python zeigt die Unterschiede:

**Hello World in C:**
```c
#include <stdio.h>

int main(void) {
    printf("Hello World\n");
    return 0;
}
```

**Hello World in Python:**
```python
if __name__ == "__main__":
    print("Hello World")
```

Wir sehen, dass die selbe Logik in unterschiedlichen Sprachen unterschiedlich aussieht.

## Semantik

Die Semantik beschreibt die Bedeutung des Codes. Zwei Programme können syntaktisch unterschiedlich sein, aber bei bestimmten Eingaben das gleiche Ergebnis liefern. Dennoch können sie unterschiedliche Semantik haben:

**Programm 1 (mit if-Statement):**
```python
if __name__ == "__main__":
    x = 5
    if x == 5:
        print("Hello World")
```

**Programm 2 (ohne if-Statement):**
```python
if __name__ == "__main__":
    x = 5
    print("Hello World")
```

Beide Programme verhalten sich bei `x = 5` identisch - sie geben "Hello World" aus. Bei `x = 3` würde Programm 1 nichts ausgeben, Programm 2 würde weiterhin "Hello World" ausgeben. Die Programme haben also unterschiedliche Semantik, auch wenn sie bei bestimmten Werten das gleiche Verhalten zeigen.


Bestimmte "Textbausteine" entscheiden über das Verhalten des Codes. Die Semantik bestimmt, was der Code tatsächlich tut, nicht nur wie er aussieht.


```{admonition} Hinweis
:name: syntax-semantik
:class: remark
Syntax-Fehler werden von der IDE oder dem Interpreter sofort erkannt. Semantik-Fehler sind schwieriger zu finden: Der Code ist syntaktisch korrekt, tut aber nicht das, was beabsichtigt war. Die Unterscheidung zwischen Syntax (wie schreibe ich es?) und Semantik (was tut es?) ist fundamental für das Verständnis von Programmiersprachen.
```


## Konzepte

Programmiersprachen unterscheiden sich nicht nur in Syntax und Semantik, sondern auch in den **Konzepten**, die sie bereitstellen. Konzepte sind Lösungsansätze für wiederkehrende Probleme in der Programmierung.

**Beispiel: Speicherverwaltung**

In einigen Programmiersprachen (z.B. C, C++) müssen Programmierer\*innen explizit Speicherplatz reservieren und wieder freigeben. In anderen Sprachen (z.B. Python, Java) übernimmt dies die Sprache automatisch.

**Abwägung:**
- **Manuelle Speicherverwaltung:** Hohe Kontrolle über Ressourcen, aber komplexer und fehleranfälliger
- **Automatische Speicherverwaltung:** Einfacher zu erlernen und weniger fehleranfällig, aber weniger Kontrolle

**Entscheidungskriterium:** Je nach Anforderung (hohe Kontrolle vs. schneller Einstieg) wählt man eine Programmiersprache, die passende Konzepte bereitstellt.

Die Eigenschaften der Programmiersprache Python, einschließlich ihrer Konzepte, werden im Kapitel [Spracheigenschaften](chapters/04-language-properties/0-intro) detailliert behandelt.

```{admonition} Tipp
:class: tip
:name: tip-learning-order
**Lernreihenfolge:** Lernen Sie zunächst die Konzepte einer Programmiersprache kennen, bevor Sie Syntax und Semantik anwenden. 

In dieser Vorlesung finden Sie:
- **Konzepte** im Teil "Python verstehen" 
- **Programmiertechniken** (Anwendung von Syntax und Semantik zur Umsetzung von Logik) im Teil "Python anwenden"
```














