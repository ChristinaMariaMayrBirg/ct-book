
## Referenzen

Im vorherigen Hausbeispiel haben wir gesehen, dass Python Seiteneffekte zulässt. Dabei wurde ein Objekt von zwei unterschiedlichen Programmteilen verändert. Was wir noch nicht geklärt haben, ist, wie Python auf die Objekte zugreift. 

Stellen Sie sich vor, Sie möchten einem Freund ein Buch geben. Es gibt verschiedene Möglichkeiten:

1. Sie kopieren das gesamte Buch und geben die Kopie weiter. Wenn Ihr Freund in seiner Kopie etwas ändert (z.B. Seiten herausreißt), bleibt Ihr Original unverändert. Sie haben zwei völlig unabhängige Bücher.

2. Sie geben Ihrem Freund die Adresse, wo das Buch liegt. Ihr Freund geht dorthin und kann das Original-Buch direkt verändern. Alle Änderungen betreffen dasselbe Buch.

3. Sie geben Ihrem Freund die Adresse des Buches. Aber: Wenn das Buch in einem Safe liegt (unveränderbar), kann Ihr Freund es nicht ändern. Wenn das Buch auf einem Tisch liegt (veränderbar), kann er es direkt verändern. 

Der letze Fall, Fall 3, ist was in Python umgesetzt ist. Man nennt das einen **"object references"**-basiertes Übergabemechanismus. Das bedeutet:

- Wenn Sie eine Variable an eine Funktion übergeben, wird nicht das Objekt selbst kopiert, sondern nur eine Referenz (Adresse) auf das Objekt
- Bei veränderbaren Objekten (Listen, Dictionaries, etc.) bedeutet das: Alle Variablen, die auf dasselbe Objekt verweisen, sehen Änderungen an diesem Objekt


```{admonition} Profiwissen
:name: uebergabemechanismen
:class: tip
Neben dem Object References, das von Python genutzt wird, gibt es noch zwei weitere Arten von Übergabemechanismen in anderen Programmiersprachen:

- **Pass by Value (Wertübergabe)**: Eine Kopie des Wertes wird übergeben. Änderungen in der Funktion wirken sich nicht auf das Original aus. Beispiel: C bei primitiven Datentypen
- **Pass by Reference (Referenzübergabe)**: Die Adresse des Objekts wird übergeben. Änderungen wirken sich direkt auf das Original aus. Beispiel: C++ mit `&`-Parametern
```

Was bedeutet das konkret für die Programmierung?

Wenn Sie in Python eine Variable einer anderen zuweisen, wird nicht das Objekt kopiert, sondern beide Variablen zeigen auf dasselbe Objekt:

```python
a = [1, 2, 3]
b = a  # b zeigt auf dasselbe Objekt wie a
b.append(4)
print(a)  # Ausgabe: [1, 2, 3, 4] - a wurde auch verändert!
```
