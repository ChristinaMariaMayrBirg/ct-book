# Eingaben mit GUI-Frameworks

Endanwender nutzen in der Regel keine Texteingabe-Schnittstelle, sondern eine **grafische Benutzeroberfläche (GUI)**.
Grafische Benutzeroberflächen werden programmatisch erstellt.
Man schreibt also Quellcode, der beschreibt, wie ein Fenster aufgebaut ist.
Hierfür verwendet man in der Regel **GUI-Frameworks**, die fertige Strukturen wie z. B. Eingabefelder und Knöpfe zur Verfügung stellen.

**Wie funktioniert das?**
Sie sagen dem Framework: "Ich hätte gerne oben ein Bild, daneben ein Eingabefeld für eine E-Mail-Adresse und darunter ein Eingabefeld für eine Zahl."
Das Framework stellt Ihnen diese Komponenten bereit.
Sie programmieren nicht das Eingabefeld selbst,  
sondern nur dessen Verhalten. Die Eingabeverarbeitung übernimmt das Framework für Sie, siehe hierzu das Beispiel unten.

**Beispiel: Zahleneingabe mit GUI-Framework (PySide6)**

```python
from PySide6.QtWidgets import QApplication, QLineEdit
from PySide6.QtGui import QDoubleValidator
import sys

app = QApplication(sys.argv)

field = QLineEdit()
validator = QDoubleValidator(-20.0, 45.9, 1)
field.setValidator(validator)

field.setPlaceholderText("Wert zwischen -20.0 und 45.9")
field.show()

app.exec()
```
Wie Sie erkennen können, müssen Sie hierbei keine Typumwandlung und Validierung vornehmen. Sie können sich auf Ihr eigentliches Problem konzentrieren: z.B. die Zahl zu quadrieren (fachliche Aufgabe).


```{admonition} Hinweis: Low-Level vs. High-Level Programmierung
:name: tip-low-level-vs-high-level
:class: tip

Wenn wir alle Aspekte der Eingabeverarbeitung selbst programmieren, sprechen wir von **Low-Level Programming**. 
„Low-Level" bedeutet hier **nicht** hardwarenah, sondern:

> Wir kümmern uns um technische Details, obwohl sie nicht zur eigentlichen fachlichen Aufgabe gehören.

**Unsere eigentliche Aufgabe (High-Level)** ist zum Beispiel:
- eine eingelesene **Float-Zahl zu quadrieren**
- fachliche Logik korrekt umzusetzen

**Die folgenden Aufgaben gehören dagegen zur Low-Level-Programmierung:**
- Texteingaben interpretieren
- Datentypen umwandeln
- Wertebereiche prüfen
- Fehlerfälle abfangen
- Sonderfälle bei der Eingabe berücksichtigen

Für diese Aufgaben existieren in der Praxis **bewährte Lösungen** (Frameworks, Validatoren, ...). 
Sie selbst zu implementieren ist möglich, aber zeitaufwendig und vor allem **testintensiv**. 
```

